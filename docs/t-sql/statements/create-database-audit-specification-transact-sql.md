---
title: CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE DATABASE AUDIT
- DATABASE_AUDIT_SPECIFICATION_TSQL
- DATABASE AUDIT SPECIFICATION
- CREATE_DATABASE_AUDIT_SPECIFICATION_TSQL
- CREATE_DATABASE_AUDIT_TSQL
- CREATE DATABASE AUDIT SPECIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- database audit specification
- CREATE DATABASE AUDIT SPECIFICATION statement
ms.assetid: 0544da48-0ca3-4a01-ba4c-940e23dc315b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2612f61d9a64d8b7d7cf156a1bd03d32d29dc1c9
ms.sourcegitcommit: 8cc38f14ec72f6f420479dc1b15eba64b1a58041
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/08/2018
ms.locfileid: "51289878"
---
# <a name="create-database-audit-specification-transact-sql"></a>CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能建立資料庫稽核規格物件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    FOR SERVER AUDIT audit_name   
        [ { ADD ( { <audit_action_specification> | audit_action_group_name } )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      action [ ,...n ]ON [ class :: ] securable BY principal [ ,...n ]  
}  
```  
  
## <a name="arguments"></a>引數  
 *audit_specification_name*  
 這是稽核規格的名稱。  
  
 *audit_name*  
 這是套用此規格的稽核名稱。  
  
 *audit_action_specification*  
 這是主體針對安全性實體所進行之動作的規格，而這些動作應該記錄在稽核中。  
  
 *action*  
 這是一或多個資料庫層級可稽核的動作名稱。 如需稽核動作的清單，請參閱 [SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 這是一或多個資料庫層級可稽核的動作群組名稱。 如需稽核動作群組的清單，請參閱 [SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *class*  
 這是安全性實體上的類別名稱 (適用的話)。  
  
 *securable*  
 這是資料庫中套用稽核動作或稽核動作群組的資料表、檢視表或其他安全性實體物件。 如需相關資訊，請參閱 [Securables](../../relational-databases/security/securables.md)。  
  
 *principal*  
 這是套用稽核動作或稽核動作群組的資料庫主體名稱。 若要稽核所有資料庫主體，請使用資料庫主體 `public`。 如需詳細資訊，請參閱[主體 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 WITH ( STATE = { ON | OFF } )  
 啟用或停用從這個稽核規格收集而來之記錄的稽核。  
  
## <a name="remarks"></a>Remarks  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 當建立資料庫稽核規格之後，它就會處於停用狀態。  
  
## <a name="permissions"></a>[權限]  
 具有 `ALTER ANY DATABASE AUDIT` 權限的使用者可以建立資料庫稽核規格，並將其繫結至任何稽核。  
  
 建立資料庫稽核規格之後，具有 `CONTROL SERVER`、`ALTER ANY DATABASE AUDIT` 權限的主體或 `sysadmin` 帳戶就可以檢視此規格。  
  
## <a name="examples"></a>範例

### <a name="a-audit-select-and-insert-on-a-table-for-any-database-principal"></a>A. 針對任何資料庫主體，稽核資料表的 SELECT 和 INSERT 
 下列範例會針對 `AdventureWorks2012` 資料庫中的 `HumanResources.EmployeePayHistory` 資料表，建立稱為 `Payrole_Security_Audit` 的伺服器稽核，然後建立可由任何使用者 (`public`) 稽核 `SELECT` 和 `INSERT` 陳述式的資料庫稽核規格，其稱為 `Payrole_Security_Audit`。  
  
```  
USE master ;  
GO  
-- Create the server audit.  
CREATE SERVER AUDIT Payrole_Security_Audit  
    TO FILE ( FILEPATH =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;  
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT Payrole_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
FOR SERVER AUDIT Payrole_Security_Audit  
ADD (SELECT , INSERT  
     ON HumanResources.EmployeePayHistory BY dbo )  
WITH (STATE = ON) ;  
GO  
``` 

### <a name="b-audit-any-dml-insert-update-or-delete-on-all-objects-in-the-sales-schema-for-a-specific-database-role"></a>B. 針對特定的資料庫角色，稽核 _sales_ 結構描述中「所有」物件的任何 DML (INSERT、UPDATE 或 DELETE)  
 下列範例會針對 `AdventureWorks2012` 資料庫中的 `Sales` 資料表，建立稱為 `DataModification_Security_Audit` 的伺服器稽核，然後建立由具新資料庫角色 `SalesUK` 使用者稽核 `INSERT`、`UPDATE` 和 `DELETE` 陳述式的資料庫稽核規格，其稱為 `Audit_Data_Modification_On_All_Sales_Tables`。  
  
```  
USE master ;  
GO  
-- Create the server audit.
-- Change the path to a path that the SQLServer Service has access to. 
CREATE SERVER AUDIT DataModification_Security_Audit  
    TO FILE ( FILEPATH = 
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ; 
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT DataModification_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
CREATE ROLE SalesUK
GO
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Data_Modification_On_All_Sales_Tables  
FOR SERVER AUDIT DataModification_Security_Audit  
ADD ( INSERT, UPDATE, DELETE  
     ON Schema::Sales BY SalesUK )  
WITH (STATE = ON) ;    
GO  
```  


## <a name="see-also"></a>另請參閱  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [建立伺服器稽核與伺服器稽核規格](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
