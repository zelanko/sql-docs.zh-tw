---
title: "重新命名 (TRANSACT-SQL) |Microsoft 文件"
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
# <a name="rename-transact-sql"></a>重新命名 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  重新命名的使用者建立的資料表中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 使用者建立的資料表或資料庫中的重新命名[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
> [!NOTE]  
>  若要重新命名資料庫，以在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用預存程序[sp_renamedb &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md). 若要重新命名 Azure SQL Database 中的資料庫，請使用 [ALTER DATABASE (Azure SQL Database)](/statements/alter-database-azure-sql-database.md) 陳述式。 
  
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
 重新命名物件 [::]   
          [[*database_name* 。 [ *schema_name* ]。 ] |[ *schema_name* 。 ] ]*table_name* TO *new_table_name*  
 **適用於：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 變更使用者定義資料表的名稱。 指定要重新命名與一段、 兩個或三部分名稱的資料表。    指定新的資料表*new_table_name*做為其中一個部分名稱。  
  
 重新命名資料庫 [::]   
          [ *database_name* TO *new_database_name*  
 **適用於：**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 變更使用者定義的資料庫名稱*database_name*至*new_database_name*。  您無法將資料庫重新命名為任何一項都[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]保留的資料庫名稱：  
  
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
 若要執行此命令中，您需要此權限：  
  
-   **ALTER**資料表的權限  
   
  
## <a name="limitations-and-restrictions"></a>限制事項  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>無法重新命名的外部資料表、 索引或檢視
您無法重新命名的外部資料表、 索引或檢視。 而不要重新命名，您可以卸除的外部資料表、 索引或檢視，並再重新建立具有新名稱。

### <a name="cannot-rename-a-table-in-use"></a>無法重新命名使用中的資料表  
 您無法重新命名資料表或資料庫，使用中時。 重新命名資料表，需要資料表的獨佔鎖定。 如果資料表是使用中，您可能需要終止工作階段所使用的資料表。 若要結束工作階段中，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段已終止任何未認可的工作將會回復。 SQL 資料倉儲中的工作階段都會加上 'SID'。 您必須叫用 KILL 命令時包含這和工作階段數目。 此範例檢視作用中或閒置工作階段的清單，然後會終止工作階段 'SID1234'。  
  
### <a name="views-are-not-updated"></a>不會更新檢視  
 在重新命名資料庫，使用先前的資料庫名稱的所有檢視都會都變成無效。 這適用於內部和外部資料庫的檢視。 例如，如果重新命名 Sales 資料庫檢視包含`SELECT * FROM Sales.dbo.table1`將變成無效。 若要解決此問題，您可以避免在檢視中，使用三部分名稱，或更新的檢視，來參考新的資料庫名稱。  
  
 在重新命名資料表，檢視無法更新為參考新的資料表名稱。 每個檢視的內部或外部參考先前資料表名稱的資料庫將變成無效。 若要解決此問題，您可以更新每個檢視，來參考新的資料表名稱。  
  
## <a name="locking"></a>鎖定  
 重新命名資料表會在資料庫物件上的共用的鎖定、 結構描述物件的共用的鎖定和資料表的獨佔鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-rename-a-database"></a>A. 重新命名資料庫  
 **適用於：** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]只  
  
 此範例中重新命名使用者定義資料庫 AdWorks AdWorks2。  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 在重新命名資料表，所有物件和資料表相關聯的屬性都更新為參考新的資料表名稱。 例如，資料表定義、 索引、 條件約束，並更新權限。 不會更新檢視。  
  
### <a name="b-rename-a-table"></a>B. 重新命名資料表  
 **適用於：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 此範例中重新命名 Customer1 Customer 資料表。  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 在重新命名資料表，所有物件和資料表相關聯的屬性都更新為參考新的資料表名稱。 例如，資料表定義、 索引、 條件約束，並更新權限。 不會更新檢視。  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. 將資料表移到不同的結構描述  
 **適用於：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 如果您的意圖是將物件移至不同的結構描述，使用[ALTER SCHEMA &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md). 比方說，這將資料表項目從產品結構描述 dbo 結構描述。  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. 終止工作階段，才能重新命名資料表  
 **適用於：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 請務必記得，您無法重新命名資料表使用中時。 重新命名的資料表需要資料表的獨佔鎖定。 如果資料表是使用中，您可能需要立即終止工作階段使用的資料表。 若要結束工作階段中，您可以使用 KILL 命令。 請小心使用 KILL，因為當工作階段已終止任何未認可的工作將會回復。 SQL 資料倉儲中的工作階段都會加上 'SID'。 您必須叫用 KILL 命令時包含這和工作階段數目。 此範例檢視作用中或閒置工作階段的清單，然後會終止工作階段 'SID1234'。  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
