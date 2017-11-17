---
title: "建立資料庫稽核規格 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0148505f91cdf572205f34b3854a3c093f5352d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
 *動作*  
 這是一或多個資料庫層級可稽核的動作名稱。 如需稽核動作的清單，請參閱[SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 這是一或多個資料庫層級可稽核的動作群組名稱。 如需稽核動作群組的清單，請參閱[SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *類別*  
 這是安全性實體上的類別名稱 (適用的話)。  
  
 *安全性實體*  
 這是資料庫中套用稽核動作或稽核動作群組的資料表、檢視表或其他安全性實體物件。 如需相關資訊，請參閱 [Securables](../../relational-databases/security/securables.md)。  
  
 *主體*  
 是要套用稽核動作或稽核動作群組的主體資料庫的名稱。 如需詳細資訊，請參閱[主體 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 WITH ( STATE = { ON | OFF } )  
 啟用或停用從這個稽核規格收集而來之記錄的稽核。  
  
## <a name="remarks"></a>備註  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 當建立資料庫稽核規格之後，它就會處於停用狀態。  
  
## <a name="permissions"></a>Permissions  
 具有使用者`ALTER ANY DATABASE AUDIT`權限可以建立資料庫稽核規格，並將其繫結至任何稽核。  
  
 建立資料庫稽核規格之後，就可以檢視的主體與`CONTROL SERVER`，`ALTER ANY DATABASE AUDIT`權限，或`sysadmin`帳戶。  
  
## <a name="examples"></a>範例  
 下列範例會針對 `Payrole_Security_Audit` 資料庫中的 `Payrole_Security_Audit` 資料表，建立稱為 `SELECT` 的伺服器稽核，然後建立可由 `INSERT` 使用者稽核 `dbo` 和 `HumanResources.EmployeePayHistory` 陳述式的資料庫稽核規格，其名稱為 `AdventureWorks2012`。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [建立伺服器稽核 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [建立伺服器稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [建立資料庫稽核規格 (TRANSACT-SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [卸除資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [建立伺服器稽核與伺服器稽核規格](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

