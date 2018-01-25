---
title: CREATE TABLE (SQL Graph) | Microsoft Docs
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: 
caps.latest.revision: "1"
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe8ace1b8f8c55c14d4807514fcb1436f6966fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-sql-graph"></a>建立資料表 （SQL 圖形）
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

建立新的 SQL 圖形資料表，可能是`NODE`或`EDGE`資料表。 
  
> [!NOTE]   
>  對於標準的 TRANSACT-SQL 陳述式，請參閱[CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)。
  
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
本文件列出只屬於 SQL 圖形的引數。 如需完整清單和支援的引數的描述，請參閱[CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 資料表據以建立之資料庫的名稱。 *database_name*必須指定現有資料庫的名稱。 如果未指定， *database_name*預設為目前的資料庫。 目前連接的登入必須與所指定的資料庫中的現有使用者識別碼相關聯*database_name*，而且該使用者識別碼必須具有 CREATE TABLE 權限。  
  
 *schema_name*    
 這是新的資料表所屬的結構描述名稱。  
  
 *table_name*    
 是節點或邊緣資料表的名稱。 資料表名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 *table_name*最多可有 128 個字元，除了本機暫存資料表名稱 (名稱加上一個數字符號 （#）)，不能超過 116 個字元。  
  
 節點   
 建立節點的資料表。

 邊緣  
 建立邊緣資料表。  
  
## <a name="remarks"></a>備註  
不支援建立暫存資料表做為節點或邊緣資料表。  

不支援建立節點或邊緣資料表為時態表。

Stretch database 不支援的節點或邊緣資料表。

節點或邊緣資料表不可為外部資料表 （圖表資料表沒有 polybase 支援）。 
  
 
## <a name="examples"></a>範例  
  
### <a name="a-create-a-node-table"></a>A. 建立`NODE`資料表
 下列範例示範如何建立`NODE`資料表

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. 建立`EDGE`資料表
下列範例顯示如何建立`EDGE`資料表

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
 [處理與 SQL Server 2017 圖形](../../relational-databases/graphs/sql-graph-overview.md)

