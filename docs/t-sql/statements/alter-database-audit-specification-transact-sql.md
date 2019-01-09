---
title: ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 622e6be1e798569de5184333144ff53e3e7d80a6
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2019
ms.locfileid: "53979584"
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
 一個或多個資料庫層級可稽核的動作名稱。 如需稽核動作群組的清單，請參閱 [SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 一個或多個資料庫層級可稽核的動作群組名稱。 如需稽核動作群組的清單，請參閱 [SQL Server Audit 動作群組和動作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *class*  
 安全性實體上的類別名稱 (適用的話)。  
  
 *securable*  
 資料庫中套用稽核動作或稽核動作群組的資料表、檢視表或其他安全性實體物件。 如需相關資訊，請參閱 [Securables](../../relational-databases/security/securables.md)。  
  
 *column*  
 安全性實體上的資料行名稱 (適用的話)。  
  
 *principal*  
 套用稽核動作或稽核動作群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主體名稱。 如需詳細資訊，請參閱[主體 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 WITH **(** STATE **=** { ON | OFF } **)**  
 啟用或停用從這個稽核規格收集而來之記錄的稽核。 稽核規格狀態變更必須在使用者交易外部完成，而且當轉換從 ON 到 OFF 時，相同的陳述式中可能不會有其他變更。  
  
## <a name="remarks"></a>Remarks  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 您必須將稽核規格的狀態設定為 OFF 選項，才可以變更資料庫稽核規格。 如果在設定 STATE=OFF 以外的任何選項時啟用稽核，而且執行 ALTER DATABASE AUDIT SPECIFICATION，您將會收到錯誤訊息。 如需詳細資訊，請參閱 [tempdb Database](../../relational-databases/databases/tempdb-database.md)。  
  
## <a name="permissions"></a>[權限]  
 具有 ALTER ANY DATABASE AUDIT 權限的使用者可以改變資料庫稽核規格，並將其繫結至任何稽核。  
  
 建立資料庫稽核規格之後，具有 CONTROL SERVER 或 ALTER ANY DATABASE AUDIT 權限的主體、系統管理員帳戶或具有稽核明確存取權的主體就可以檢視此規格。  
  
## <a name="examples"></a>範例  
 下列範例會改變稱為 `HIPAA_Audit_DB_Specification` 的資料庫稽核規格，它會稽核 `SELECT` 使用者針對稱為 `dbo` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稽核所建立的 `HIPAA_Audit` 陳述式。  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPAA_Audit_DB_Specification  
FOR SERVER AUDIT HIPAA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 如需如何建立稽核的完整範例，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md) (SQL Server 稽核 &#40;資料庫引擎&#41)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  
