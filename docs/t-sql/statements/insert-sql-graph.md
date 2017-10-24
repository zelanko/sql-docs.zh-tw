---
title: "插入 （SQL 圖形） |Microsoft 文件"
description: "插入 SQL 圖形節點或邊緣資料表的語法。"
ms.date: 05/12/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e694d89efef130d2abcd5cd6424e2be576ef09de
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---

# <a name="insert-sql-graph"></a>插入 （SQL 圖形）
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]  

  將一個或多個資料列`node`或`edge`資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 

> [!NOTE]   
>  對於標準的 TRANSACT-SQL 陳述式，請參閱[插入資料表 (TRANSACT-SQL)](../../t-sql/statements/insert-transact-sql.md)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>插入節點 Table 語法 
插入節點的資料表的語法是與一般資料表相同。 

```  
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>引數  
 本文件說明屬於 SQL 圖形的引數。 如需完整清單和 INSERT 陳述式中支援的引數的描述，請參閱[插入資料表 (TRANSACT-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 這是一個可以之間使用的選擇性關鍵字`INSERT`和目標資料表。  
  
 *search_condition_with_match*   
 `MATCH`子句可以用於子查詢，同時插入節點或邊緣資料表。 如`MATCH`陳述式語法，請參閱[圖形相符項目 (TRANSACT-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 搜尋模式提供給`MATCH`子句做為圖形述詞的一部分。

 *edge_table_column_list*   
 使用者必須提供值`$from_id`和`$to_id`時插入邊緣。 如果未提供值或 Null 插入這些資料行，則會傳回錯誤。 
  

## <a name="remarks"></a>備註  
將插入的節點是與插入任何關聯式資料表相同。 $Node_id 欄位的值會自動產生。

同時插入邊緣資料表，使用者必須提供值`$from_id`和`$to_id`資料行。   

大量插入節點資料表是維持相同的關聯式資料表。

邊緣資料表中插入大量前, 必須匯入節點資料表。 值`$from_id`和`$to_id`可以擷取自`$node_id`節點資料表的資料行插入為邊緣。 

  
### <a name="permissions"></a>Permissions  
 需要目標資料表的 INSERT 權限。  
  
 INSERT 成員的權限預設**sysadmin**固定伺服器角色、 **db_owner**和**db_datawriter**固定資料庫角色，以及資料表擁有者。 成員**sysadmin**， **db_owner**，而**db_securityadmin**角色，以及資料表擁有者可以將權限移轉給其他使用者。  
  
 若要執行 INSERT 搭配 OPENROWSET 函數 BULK 選項，您必須隸屬**sysadmin**固定的伺服器角色或**bulkadmin**固定的伺服器角色。  
  

## <a name="examples"></a>範例  
  
#### <a name="a--insert-into-node-table"></a>A.  插入節點資料表  
 下列範例會建立 Person 節點資料表，並將 2 個資料列插入至該資料表。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  邊緣資料表中插入  
 下列範例會建立 friend 邊緣資料表，並插入資料表中的邊緣。

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>另請參閱  
 [插入資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [處理與 SQL Server 2017 圖形](../../relational-databases/graphs/sql-graph-overview.md)  



