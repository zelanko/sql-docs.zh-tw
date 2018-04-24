---
title: CREATE TABLE (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: f54fc1df1d31914c8ceb29d1788b8d092579612c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

將新的 SQL 圖形資料表建立為 `NODE` 或 `EDGE` 資料表。 
  
> [!NOTE]   
>  針對標準 Transact-SQL 陳述式，請參閱 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>引數  
本文件僅列出屬於 SQL 圖形的引數。 如需支援之引數的完整清單和描述，請參閱 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 資料表據以建立之資料庫的名稱。 *database_name* 必須指定現有資料庫的名稱。 如果未指定，*database_name* 便預設為目前的資料庫。 目前連接的登入必須與 *database_name* 指定的資料庫中現有使用者識別碼有關聯，且這個使用者識別碼必須具有 CREATE TABLE 權限。  
  
 *schema_name*    
 這是新的資料表所屬的結構描述名稱。  
  
 *table_name*    
 節點或邊緣資料表的名稱。 資料表名稱必須遵照[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 *table_name* 最多可有 128 個字元，但本機暫存資料表名稱 (名稱前附加一個數字符號 (#)) 除外，其不可超過 116 個字元。  
  
 NODE   
 建立節點資料表。

 EDGE  
 建立邊緣資料表。  
  
## <a name="remarks"></a>Remarks  
不支援建立暫存資料表作為節點或邊緣資料表。  

不支援建立節點或邊緣資料表作為時態表。

針對節點或邊緣資料表，不支援 Stretch Database。

節點或邊緣資料表不可為外部資料表 (圖形資料表沒有 polybase 支援)。 
  
 
## <a name="examples"></a>範例  
  
### <a name="a-create-a-node-table"></a>A. 建立 `NODE` 資料表
 下列範例示範如何建立 `NODE` 資料表

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. 建立 `EDGE` 資料表
下列範例示範如何建立 `EDGE` 資料表

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)

