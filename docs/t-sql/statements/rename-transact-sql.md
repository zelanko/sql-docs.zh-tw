---
description: RENAME (Transact-SQL)
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 97cabcda2e5b680e9fe2d5d6a4f0ce2130e19a27
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91226878"
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

重新命名 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中使用者建立的資料表。 重新命名 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中使用者建立的資料表、使用者所建立資料表或資料庫中的資料行。

> [!NOTE]
> 若要重新命名 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 中的資料庫，請使用 [ALTER DATABASE ([!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)])](alter-database-transact-sql.md?view=aps-pdw-2016-au7&preserve-view=true)。 若要重新命名 Azure SQL Database 中的資料庫，請使用 [ALTER DATABASE (Azure SQL Database)](alter-database-transact-sql.md?view=azuresqldb-mi-current&preserve-view=true) 陳述式。 若要重新命名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫，請使用預存程序 [sp_renamedb](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md)。

## <a name="syntax"></a>語法

```syntaxsql
-- Syntax for Azure Synapse Analytics

-- Rename a table.
RENAME OBJECT [::] [ [ database_name . [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name
[;]

```

```syntaxsql
-- Syntax for Analytics Platform System

-- Rename a table
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name
[;]

-- Rename a database
RENAME DATABASE [::] database_name TO new_database_name
[;]

-- Rename a column 
RENAME OBJECT [::] [ [ database_name . [schema_name ] ] . ] | [schema_name . ] ] table_name COLUMN column_name TO new_column_name [;]
```

## <a name="arguments"></a>引數

RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*
**適用於：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

變更使用者定義之資料表的名稱。 指定要重新命名為一部分、 兩部分或三部分名稱的資料表。 將新的資料表 *new_table_name* 指定為一部分名稱。

RENAME DATABASE [::] [ *database_name* TO *new_database_name*
**適用於：** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

將使用者定義的資料庫名稱從 *database_name* 變更為 *new_database_name*。 您無法將資料庫重新命名為任一以下 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 保留的資料庫名稱：

- master
- model
- msdb
- tempdb
- pdwtempdb1
- pdwtempdb2
- DWConfiguration
- DWDiagnostics
- DWQueue


RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* COLUMN *column_name* TO *new_column_name*
**APPLIES TO:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

變更資料表中的資料行名稱。 

## <a name="permissions"></a>權限

若要執行此命令，您需要此權限：

- 資料表的 **ALTER** 權限

## <a name="limitations-and-restrictions"></a>限制事項

### <a name="cannot-rename-an-external-table-indexes-or-views"></a>無法重新命名外部資料表、 索引或檢視表

您無法重新命名外部資料表、索引或檢視表。 在無法重新命名的情況下，您可以卸除外部資料表、 索引或檢視表，然後使用不同的名稱來重建它。

### <a name="cannot-rename-a-table-in-use"></a>無法重新命名使用中的資料表

正在使用資料表或資料庫時，您無法將其重新命名。 需要資料表的獨佔鎖定，才能重新命名。 如果資料表正在使用中，您可能需要找出是哪些工作階段正在使用該資料表，然後予以終止。 若要終止工作階段，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段終止後，任何未認可的工作都將回復。 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 中的工作階段前面會加上 'SID'。 叫用 KILL 命令時，請包含 'SID' 與此工作階段編號。 此範例會檢視作用中或閒置的工作階段清單，然後會終止工作階段 'SID1234'。

### <a name="rename-column-restrictions"></a>重新命名資料行的限制

您無法重新命名用於資料表散發的資料行。 您也無法重新命名外部資料表或暫存資料表中的任何資料行。 

### <a name="views-are-not-updated"></a>不會更新檢視表

重新命名資料庫時，所有使用舊資料庫名稱的檢視都會都變成無效。 此行為適用於資料庫內部和外部的檢視表。 例如，如果重新命名 Sales 資料庫，則包含 `SELECT * FROM Sales.dbo.table1` 的檢視表將變成無效。 若要解決此問題，您可以避免在檢視表中使用三部分的名稱，或是更新檢視表來參考新的資料庫名稱。

重新命名資料表時，無法更新檢視表來參考新的資料表名稱。 無論是資料庫內部或外部檢視表，只要參考舊資料表名稱，都將變成無效。 若要解決此問題，您可以更新每一個檢視表來參考新的資料表名稱。

重新命名資料行時，無法更新檢視來參考新的資料行名稱。 在執行變更檢視前，檢視會持續顯示舊的資料行名稱。 在某些情況下，需要卸除並重新建立的檢視，可能會變成無效。

## <a name="locking"></a>鎖定

重新命名資料表時，會取得 DATABASE 物件上的共用鎖定、SCHEMA 物件上的共用鎖定、以及資料表上的獨佔鎖定。

## <a name="examples"></a>範例

### <a name="a-rename-a-database"></a>A. 重新命名資料庫

僅 **適用於：** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

此範例會將使用者定義的資料庫從 AdWorks 重新命名為 AdWorks2。

```sql
-- Rename the user defined database AdWorks
RENAME DATABASE AdWorks to AdWorks2;

```

 重新命名資料表時，會更新與該資料表相關聯的所有物件與屬性以參考新的資料表名稱。 例如，會更新資料表定義、 索引、 條件約束與權限。 不會更新檢視表。

### <a name="b-rename-a-table"></a>B. 重新命名資料表

**適用於：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

此範例會將 Customer 資料表重新命名為 Customer 1。

```sql
-- Rename the customer table
RENAME OBJECT Customer TO Customer1;

RENAME OBJECT mydb.dbo.Customer TO Customer1;
```

重新命名資料表時，會更新與該資料表相關聯的所有物件與屬性以參考新的資料表名稱。 例如，會更新資料表定義、 索引、 條件約束與權限。 不會更新檢視表。

### <a name="c-move-a-table-to-a-different-schema"></a>C. 將資料表移到不同的結構描述

**適用於：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

如果您想要將物件移至不同的結構描述，請使用 [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)。 例如，下列陳述式會將資料表項目從產品結構描述移至 dbo 結構描述。

```sql
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;
```

### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. 重新命名資料表前，先終止工作階段

**適用於：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

您無法在資料表使用中時將其重新命名。 重新命名資料表時，需要取得資料表的獨佔鎖定。 如果資料表正在使用中，您可能需要找出是哪些工作階段正在使用該資料表，然後予以終止。 若要終止工作階段，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段終止後，任何未認可的工作都將回復。 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 中的工作階段前面會加上 'SID'。 叫用 KILL 命令時，應該包含 'SID' 與工作階段編號。 此範例會檢視作用中或閒置的工作階段清單，然後會終止工作階段 'SID1234'。

```sql
-- View a list of the current sessions
SELECT session_id, login_name, status
FROM sys.dm_pdw_exec_sessions
WHERE status='Active' OR status='Idle';

-- Terminate a session using the session_id.
KILL 'SID1234';
```

### <a name="e-rename-a-column"></a>E. 重新命名資料行 

**適用於：** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

此範例會將 Customer 資料表的 FName 資料行重新命名為 FirstName。

```sql
-- Rename the Fname column of the customer table
RENAME OBJECT::Customer COLUMN FName TO FirstName;

RENAME OBJECT mydb.dbo.Customer COLUMN FName TO FirstName;
```
