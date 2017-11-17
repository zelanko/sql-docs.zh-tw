---
title: "改變資料庫稽核規格 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06d58a9ecce3175e021e7db484aeadbe41f3b372
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能改變資料庫稽核規格物件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
  
```  
  
## <a name="arguments"></a>引數  
 *audit_specification_name*  
 稽核規格的名稱。  
  
 *audit_name*  
 套用此規格的稽核名稱。  
  
 *audit_action_specification*  
 一個或多個資料庫層級可稽核的動作名稱。 如需稽核動作群組的清單，請參閱[SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 一個或多個資料庫層級可稽核的動作群組名稱。 如需稽核動作群組的清單，請參閱[SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *類別*  
 安全性實體上的類別名稱 (適用的話)。  
  
 *安全性實體*  
 資料庫中套用稽核動作或稽核動作群組的資料表、檢視表或其他安全性實體物件。 如需相關資訊，請參閱 [Securables](../../relational-databases/security/securables.md)。  
  
 *資料行*  
 安全性實體上的資料行名稱 (適用的話)。  
  
 *主體*  
 套用稽核動作或稽核動作群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主體名稱。 如需詳細資訊，請參閱[主體 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 與**(**狀態 **=**  {ON |關閉} **)**  
 啟用或停用從這個稽核規格收集而來之記錄的稽核。 稽核規格狀態變更必須在使用者交易外部完成，而且當轉換從 ON 到 OFF 時，相同的陳述式中可能不會有其他變更。  
  
## <a name="remarks"></a>備註  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 您必須將稽核規格的狀態設為 OFF 選項，才可以變更資料庫稽核規格。 如果在設定 STATE=OFF 以外的任何選項時啟用稽核，而且執行 ALTER DATABASE AUDIT SPECIFICATION，您將會收到錯誤訊息。 如需詳細資訊，請參閱 [tempdb Database](../../relational-databases/databases/tempdb-database.md)。  
  
## <a name="permissions"></a>Permissions  
 具有 ALTER ANY DATABASE AUDIT 權限的使用者可以改變資料庫稽核規格，並將其繫結至任何稽核。  
  
 建立資料庫稽核規格之後，就可以檢視由具有 CONTROL SERVER 或 ALTER ANY DATABASE AUDIT 權限、 系統管理員帳戶或具有對稽核之明確存取主體的主體中。  
  
## <a name="examples"></a>範例  
 下列範例會改變稱為 `HIPPA_Audit_DB_Specification` 的資料庫稽核規格，它會稽核 `SELECT` 使用者針對稱為 `dbo` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稽核所建立的 `HIPPA_Audit` 陳述式。  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 如需有關如何建立稽核的完整範例，請參閱[SQL Server Audit &#40; Database engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立伺服器稽核 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [建立伺服器稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [建立資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  

