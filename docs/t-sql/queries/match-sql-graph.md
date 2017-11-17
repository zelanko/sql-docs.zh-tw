---
title: "比對 （SQL 圖形） |Microsoft 文件"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db211fa0988f2dbe6a72291f898d670d44d3f215
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="match-transact-sql"></a>比對 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  指定的搜尋條件圖形。 比對只可以搭配 SELECT 陳述式 WHERE 子句的一部分圖形節點和邊緣資料表。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
    {<node_alias> { 
                     { <-( <edge_alias> )- } 
                   | { -( <edge_alias> )-> }
                 <node_alias> 
                 } 
     }
     [ { AND } { ( <graph_search_pattern> ) } ]
     [ ,...n ]
  
<node_alias> ::=
    node_table_name | node_alias 

<edge_alias> ::=
    edge_table_name | edge_alias
```

## <a name="arguments"></a>引數  
*graph_search_pattern*  
指定要搜尋或路徑周遊圖表中的模式。 此模式會使用 ASCII 封面語法來周遊圖形中的路徑。 模式會從一個節點之間透過邊緣，提供箭頭的方向。 Parantheses 內提供邊緣名稱或別名。 節點名稱或別名會出現在兩端的箭頭。 在模式中的任一方向可以進入箭號。

*node_alias*  
名稱或別名的 FROM 子句中提供的節點資料表。

*edge_alias*  
名稱或別名的邊緣資料表的 FROM 子句中提供。


## <a name="remarks"></a>備註  
可以重複相符項目內的節點名稱。  換句話說，節點可以是周遊任意數目的相同查詢中的次數。  
邊緣名稱不能重複相符項目內。  
邊緣可以指向任一方向，但是它必須有明確的方向。  
或和比對模式中不支援 NOT 運算子。 使用其他運算式與 WHERE 子句中，可以結合相符項目。 不過，結合使用其他運算式 OR 或不支援。 

## <a name="examples"></a>範例  
### <a name="a--find-a-friend"></a>A.  尋找朋友 
 下列範例會建立人員節點資料表和朋友邊緣資料表、 將某些資料，然後使用 尋找 Alice，圖形中的人員的 friend 相符項目。

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
 下列範例會嘗試尋找 Alice 的 friend 的 friend。 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  多個`MATCH`模式
 以下是一些可以內符合指定模式中的多個方法。

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
 [建立資料表 &#40;SQL 圖形 &#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [插入 （SQL 圖形）](../../t-sql/statements/insert-sql-graph.md)]  
 [處理與 SQL Server 2017 圖形](../../relational-databases/graphs/sql-graph-overview.md)  

