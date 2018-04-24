---
title: INSERT (SQL Graph) | Microsoft Docs
description: SQL Graph 節點或邊緣資料表的 INSERT 語法。
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: d7d93bfc1ffa3e926bc8e9dcdea46183a0801155
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="insert-sql-graph"></a>INSERT (SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  將一或多個資料列新增至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `node` 或 `edge` 資料表。 

> [!NOTE]   
>  如需標準 Transact-SQL 陳述式，請參閱 [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>插入節點資料表語法 
插入節點資料表的語法與一般資料表相同。 

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
 本文件僅描述與 SQL Graph 有關的參數。 如需 INSERT 陳述式支援之引數的完整清單和描述，請參閱 [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 這是一個選擇性關鍵字，您可以在 `INSERT` 和目標資料表之間使用它。  
  
 *search_condition_with_match*   
 `MATCH` 子句在插入節點或邊緣資料表時，可以用於子查詢。 針對 `MATCH` 陳述式語法，請參閱 [GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 提供給 `MATCH` 子句的搜尋模式，作為圖表述詞的一部分。

 *edge_table_column_list*   
 插入至邊緣時，使用者必須提供 `$from_id` 和 `$to_id` 的值。 如果未提供值或 NULL 插入這些資料行，則會傳回錯誤。 
  

## <a name="remarks"></a>Remarks  
插入至節點是與插入至任何關聯式資料表相同。 $node_id 資料行的值會自動產生。

插入至邊緣資料表時，使用者必須提供 `$from_id` 和 `$to_id` 的值。   

節點資料表的大量插入仍然與關聯式資料表相同。

在大量插入邊緣資料表之前，必須先匯入節點資料表。 然後可以從節點資料表的 `$node_id` 資料行擷取 `$from_id` 和 `$to_id` 的值，然後插入為邊緣。 

  
### <a name="permissions"></a>Permissions  
 需要目標資料表的 INSERT 權限。  
  
 INSERT 權限預設會授與 **sysadmin** 固定伺服器角色、**db_owner** 和 **db_datawriter** 固定資料庫角色的成員，以及資料表擁有者。 **sysadmin**、**db_owner** 和 **db_securityadmin** 角色的成員，以及資料表擁有者，可以將權限轉讓給其他使用者。  
  
 若要搭配使用 OPENROWSET 函式與 BULK 選項來執行 INSERT，您必須是 **sysadmin** 固定伺服器角色或 **bulkadmin** 固定伺服器角色的成員。  
  

## <a name="examples"></a>範例  
  
#### <a name="a--insert-into-node-table"></a>A.  插入至節點資料表  
 下列範例會建立 Person 節點資料表並且插入 2 個資料列。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  插入至邊緣資料表  
 下列範例會建立一個朋友邊緣資料表並將插入一個邊緣。

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>另請參閱  
 [INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [圖形處理與 SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  


