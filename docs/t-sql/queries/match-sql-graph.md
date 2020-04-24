---
title: MATCH (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
- Shortest Path, shortest_path
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3bc420d4e086e8256590fd206790f5fa41689e0a
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635515"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  指定圖表的搜尋條件。 MATCH 只能在 SELECT 陳述式的 WHERE 子句中與圖表節點和邊緣資料表搭配使用。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
  {  
      <simple_match_pattern> 
    | <arbitrary_length_match_pattern>  
    | <arbitrary_length_match_last_node_predicate> 
  }

<simple_match_pattern>::=
  {
      LAST_NODE(<node_alias>) | <node_alias>   { 
          { <-( <edge_alias> )- } 
        | { -( <edge_alias> )-> }
        <node_alias> | LAST(<node_alias>)
        } 
  }
  [ { AND } { ( <simple_match_pattern> ) } ]
  [ ,...n ]

<node_alias> ::=
  node_table_name | node_table_alias 

<edge_alias> ::=
  edge_table_name | edge_table_alias


<arbitrary_length_match_pattern>  ::=
  { 
    SHORTEST_PATH( 
      <arbitrary_length_pattern> 
      [ { AND } { <arbitrary_length_pattern> } ] 
      [ ,…n] 
    )
  } 

<arbitrary_length_match_last_node_predicate> ::=
  {  LAST_NODE( <node_alias> ) = LAST_NODE( <node_alias> ) }


<arbitrary_length_pattern> ::=
    {  LAST_NODE( <node_alias> )   | <node_alias>
     ( <edge_first_al_pattern> [<edge_first_al_pattern>…,n] )
     <al_pattern_quantifier> 
  }
    |  ( {<node_first_al_pattern> [<node_first_al_pattern> …,n] )
        <al_pattern_quantifier> 
        LAST_NODE( <node_alias> ) | <node_alias> 
 }
    
<edge_first_al_pattern> ::=
  { (  
        { -( <edge_alias> )->   } 
      | { <-( <edge_alias> )- } 
      <node_alias>
      ) 
  } 

<node_first_al_pattern> ::=
  { ( 
      <node_alias> 
        { <-( <edge_alias> )- } 
      | { -( <edge_alias> )-> }
      ) 
  } 


<al_pattern_quantifier> ::=
  {
        +
      | { 1 , n }
  }

n -  positive integer only.
 
```

## <a name="arguments"></a>引數  
*graph_search_pattern*  
指定要在圖表中搜尋的模式或周遊的路徑。 此模式會使用 ASCII 作品語法來周遊圖表中的路徑。 此模式會朝著所提供的箭頭方向，透過邊緣從一個節點移至另一個節點。 邊緣名稱或別名會以括弧括住。 節點名稱或別名會顯示在箭頭的兩端。 箭頭在模式中可以朝任一方向。

*node_alias*  
在 FROM 子句中提供的節點資料表名稱或別名。

*edge_alias*  
在 FROM 子句中提供的邊緣資料表名稱或別名。

*SHORTEST_PATH*   
最短路徑函式會用來尋找圖表中兩個指定節點間的最短路徑，或是圖表中指定節點跟所有其它節點之間的最短路徑。 它會接受任意長度的模式作為輸入，並在圖表中重複搜尋該輸入。 

*arbitrary_length_match_pattern*  
指定要在到達所需節點前重複周遊的節點和邊緣，還是在到達模式中所指定的反覆運算次數上限前持續進行。 

*al_pattern_quantifier*   
任意長度的模式，接受規則運算式樣式的模式數量詞，來指定重複指定搜尋模式的次數。 支援的搜尋模式數量詞包括：   
* **+** ：重複模式 1 或多次。 在找到最短路徑後立即終止。    
* **{1,n}** ：重複模式 1 至 'n' 次。 在找到最短路徑後立即終止。     

## <a name="remarks"></a>備註  
MATCH 內的節點名稱可以重複。  換句話說，在同一個查詢中，可以對某個節點周遊任意的次數。  
邊緣節點名稱在 MATCH 內不可重複。  
邊緣可以指向任一方向，但方向必須明確。  
在 MATCH 模式中不支援 OR 和 NOT 運算子。 在 WHERE 子句中使用 AND 可將 MATCH 與其他運算式結合。 不過，不支援使用 OR 或 NOT 將它與其他運算式結合。 

## <a name="examples"></a>範例  
### <a name="a--find-a-friend"></a>A.  尋找朋友 
 下列範例會建立 Person 節點資料表和 friend 邊緣資料表、插入一些資料，然後使用 MATCH 來尋找 Alice (圖表中的一個人) 的朋友。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';

 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  尋找朋友的朋友
 下列範例會嘗試尋找 Alice 朋友的朋友。 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  其他 `MATCH` 模式
 以下是可在 MATCH 內指定模式的一些其他方法。

 ```
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>另請參閱  
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)  
