---
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/20/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3c08b4d991717d877ca33cd2d136d0dbf0d30483
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  重新命名 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中使用者建立的資料表。 重新命名 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中使用者建立的資料表或資料庫。  
  
> [!NOTE]  
>  若要重新命名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫，請使用預存程序 [sp_renamedb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md)。 若要重新命名 Azure SQL Database 中的資料庫，請使用 [ALTER DATABASE (Azure SQL Database)](/statements/alter-database-azure-sql-database.md) 陳述式。 
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [ :: ]  [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 RENAME OBJECT [::]   
          [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*  
 **適用於：**  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 變更使用者定義之資料表的名稱。 指定要重新命名為一部分、 兩部分或三部分名稱的資料表。    將新的資料表 *new_table_name* 指定為一部分名稱。  
  
 RENAME DATABASE [::]   
          [ *database_name* TO *new_database_name*  
 **適用於：**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 將使用者定義的資料庫名稱從 *database_name* 變更為 *new_database_name*。  您無法將資料庫重新命名為以下任何這些[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]保留的資料庫名稱：  
  
-   master  
  
-   model  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Permissions  
 若要執行此命令，您需要此權限：  
  
-   資料表的 **ALTER** 權限  
   
  
## <a name="limitations-and-restrictions"></a>限制事項  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>無法重新命名外部資料表、 索引或檢視表
您無法重新命名外部資料表、 索引或檢視表。 在無法重新命名的情況下，您可以卸除外部資料表、 索引或檢視表，然後使用不同的名稱來重建它。

### <a name="cannot-rename-a-table-in-use"></a>無法重新命名使用中的資料表  
 資料表或資料庫正在使用中時，您無法重新命名。 需要資料表的獨佔鎖定，才能重新命名。 如果資料表正在使用中，您可能需要找出是哪些工作階段正在使用該資料表，然後予以終止。 若要終止工作階段，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段終止後，任何未認可的工作都將回復。 SQL 資料倉儲中的工作階段名稱前面都會加上 'SID'。 叫用 KILL 命令時，您應該包含此識別碼與工作階段編號。 此範例會檢視作用中或閒置的工作階段清單，然後會終止工作階段 'SID1234'。  
  
### <a name="views-are-not-updated"></a>不會更新檢視表  
 重新命名資料庫時，所有使用舊資料庫名稱的檢視都會都變成無效。 這適用於資料庫內部和外部的檢視表。 例如，如果重新命名 Sales 資料庫，則包含 `SELECT * FROM Sales.dbo.table1` 的檢視表將變成無效。 若要解決此問題，您可以避免在檢視表中使用三部分名稱，或者更新檢視表來參考新的資料庫名稱。  
  
 重新命名資料表時，無法更新檢視表來參考新的資料表名稱。 無論是資料庫內部或外部檢視表，只要參考舊資料表名稱，都將變成無效。 若要解決此問題，您可以更新每一檢視表來參考新的資料表名稱。  
  
## <a name="locking"></a>鎖定  
 重新命名資料表時，會取得 DATABASE 物件上的共用鎖定、SCHEMA 物件上的共用鎖定、以及資料表上的獨佔鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-rename-a-database"></a>A. 重新命名資料庫  
 **適用於：**僅 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 此範例會將使用者定義的資料庫從 AdWorks 重新命名為 AdWorks2。  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 重新命名資料表時，會更新與該資料表相關聯的所有物件與屬性以參考新的資料表名稱。 例如，會更新資料表定義、 索引、 條件約束與權限。 不會更新檢視表。  
  
### <a name="b-rename-a-table"></a>B. 重新命名資料表  
 **適用於：**  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 此範例會將 Customer 資料表重新命名為 Customer 1。  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 重新命名資料表時，會更新與該資料表相關聯的所有物件與屬性以參考新的資料表名稱。 例如，會更新資料表定義、 索引、 條件約束與權限。 不會更新檢視表。  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. 將資料表移到不同的結構描述  
 **適用於：**  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 如果您想要將物件移至不同的結構描述，請使用 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)。 例如，這樣會將資料表項目從 product 結構描述移至 dbo 結構描述。  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. 重新命名資料表前，先終止工作階段  
 **適用於：**  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 請務必記得，如果資料表正在使用中，便無法重新命名。 重新命名資料表時，需要取得資料表的獨佔鎖定。 如果資料表正在使用中，您可能需要找出是哪些工作階段正在使用該資料表，然後予以終止。 若要終止工作階段，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段終止後，任何未認可的工作都將回復。 SQL 資料倉儲中的工作階段名稱前面都會加上 'SID'。 叫用 KILL 命令時，您應該包含此識別碼與工作階段編號。 此範例會檢視作用中或閒置的工作階段清單，然後會終止工作階段 'SID1234'。  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
