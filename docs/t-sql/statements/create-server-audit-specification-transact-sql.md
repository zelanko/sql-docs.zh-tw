---
title: "建立伺服器稽核規格 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- CREATE_SERVER_AUDIT_SPECIFICATION_TSQL
- CREATE SERVER AUDIT SPECIFICATION
dev_langs: TSQL
helpviewer_keywords: CREATE SERVER AUDIT SPECIFICATION statement
ms.assetid: db77fa77-fedb-40ac-83e6-06343063e518
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06457f549575de83fc93c53d204a79061f4f4254
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-server-audit-specification-transact-sql"></a>CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能建立伺服器稽核規格物件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE SERVER AUDIT SPECIFICATION audit_specification_name  
FOR SERVER AUDIT audit_name  
{  
    { ADD ( { audit_action_group_name } )   
    } [, ...n]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *audit_specification_name*  
 伺服器稽核規格的名稱。  
  
 *audit_name*  
 套用此規格的稽核名稱。  
  
 *audit_action_group_name*  
 伺服器層級之可稽核動作的群組名稱。 如需稽核動作群組的清單，請參閱[SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 與**(**狀態 **=**  {ON |關閉} **)**  
 啟用或停用從這個稽核規格收集而來之記錄的稽核。  
  
## <a name="remarks"></a>備註  
 在您為它建立伺服器稽核規格之前，必須有稽核存在。 當建立伺服器稽核規格之後，它就會處於停用狀態。  
  
## <a name="permissions"></a>Permissions  
 具有 ALTER ANY SERVER AUDIT 權限的使用者可以建立伺服器稽核規格，並將其繫結至任何稽核。  
  
 一旦建立伺服器稽核規格之後，就可以使用具有 CONTROL SERVER 或 ALTER ANY SERVER AUDIT 權限的主體、系統管理員 (sysadmin) 帳戶或具有此稽核之明確存取權的主體來加以檢視。  
  
## <a name="examples"></a>範例  
 下列範例會建立稱為 `HIPPA_Audit_Specification` 的伺服器稽核規格，它會針對稱為 `HIPPA_Audit` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稽核來稽核失敗的登入。  
  
```  
CREATE SERVER AUDIT SPECIFICATION HIPPA_Audit_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (FAILED_LOGIN_GROUP);  
GO  
```  
  
 如需有關如何建立稽核的完整範例，請參閱[SQL Server Audit &#40; Database engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [建立伺服器稽核 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [建立資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  
