---
description: CREATE TABLE (SQL Graph)
title: CREATE TABLE (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc39fbcb191810f7e357167f15c4d0ca084711d8
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688667"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (SQL Graph)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

將新的 SQL 圖形資料表建立為 `NODE` 或 `EDGE` 資料表。 
  
> [!NOTE]   
>  針對標準 Transact-SQL 陳述式，請參閱 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } 
       | <computed_column_definition>
       | <column_set_definition>
       | [ <table_constraint> ] [ ,... n ]
       | [ <table_index> ] }
          [ ,...n ]
    )   
    AS [ NODE | EDGE ]
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
[ ; ] 

< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
```  
  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
本文件僅列出屬於 SQL 圖形的引數。 如需支援之引數的完整清單和描述，請參閱 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 資料表據以建立之資料庫的名稱。 *database_name* 必須指定現有資料庫的名稱。 如果未指定，*database_name* 會預設為目前的資料庫。 目前連接的登入必須與 *database_name* 指定的資料庫中現有使用者識別碼有關聯，且這個使用者識別碼必須具有 CREATE TABLE 權限。  
  
 *schema_name*    
 這是新的資料表所屬的結構描述名稱。  
  
 *table_name*      
 節點或邊緣資料表的名稱。 資料表名稱必須遵照[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 *table_name* 最多可有 128 個字元，但本機暫存資料表名稱 (名稱前附加一個數字符號 (#)) 除外，其不可超過 116 個字元。  
  
 NODE   
 建立節點資料表。

 EDGE  
 建立邊緣資料表。  
 
 *table_constraint*   
 指定 PRIMARY KEY、UNIQUE、FOREIGN KEY、CONNECTION 條件約束、CHECK 條件約束的屬性，或新增至資料表的 DEFAULT 定義屬性
 
 ON { partition_scheme | filegroup | "default" }    
 指定儲存資料表的分割區配置或檔案群組。 如果指定了 partition_scheme，資料表便是一份分割區資料表，其分割區儲存在 partition_scheme 指定的一組檔案群組中 (其具有一或多個檔案群組)。 如果指定了 filegroup，資料表會儲存在具名檔案群組中。 檔案群組必須在資料庫內。 如果指定了 default，或完全未指定 ON，資料表就會儲存在預設檔案群組中。 CREATE TABLE 所指定的資料表儲存機制無法進行後續的改變。

 ON {partition_scheme | filegroup | "default"}    
 PRIMARY KEY 或 UNIQUE 條件約束中也可指定此項目。 這些條件約束會建立索引。 如果指定了 filegroup，索引會儲存在具名檔案群組中。 如果指定了 default，或完全未指定 ON，索引就會儲存在與資料表相同的檔案群組中。 如果 PRIMARY KEY 或 UNIQUE 條件約束建立叢集索引，資料表的資料頁面會儲存在索引的相同檔案群組中。 如果指定了 CLUSTERED 或常數建立了叢集索引，且所指定 partition_scheme 與資料表定義的 partition_scheme 或 filegroup 不同 (反之亦然)，則只會遵守條件約束定義，其他一概予以忽略。
  
## <a name="remarks"></a>備註  
不支援建立暫存資料表作為節點或邊緣資料表。  

不支援建立節點或邊緣資料表作為時態表。

針對節點或邊緣資料表，不支援 Stretch Database。

節點或邊緣資料表不可為外部資料表 (圖形資料表沒有 PolyBase 支援)。 

非資料分割之圖形節點/邊緣資料表無法更改為資料分割的圖形節點/邊緣資料表。 
  
 
## <a name="examples"></a>範例  
  
### <a name="a-create-a-node-table"></a>A. 建立 `NODE` 資料表
 下列範例示範如何建立 `NODE` 資料表

```sql
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. 建立 `EDGE` 資料表
下列範例示範如何建立 `EDGE` 資料表

```sql
 CREATE TABLE friends (
    id INTEGER PRIMARY KEY,
    start_date DATe
 ) AS EDGE;
```

```sql
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;
```


## <a name="see-also"></a>另請參閱 
 [ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)

