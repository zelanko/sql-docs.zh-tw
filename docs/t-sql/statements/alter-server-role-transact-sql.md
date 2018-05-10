---
title: ALTER SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ef22affdaed66594def90051a18d512aca0d1a80
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

變更伺服器角色的成員資格或變更使用者定義伺服器角色的名稱。 固定伺服器角色不能重新命名。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>引數  
*server_role_name*  
這是要變更的伺服器角色名稱。  
  
ADD MEMBER *server_principal*  
將指定的伺服器主體加入至伺服器角色。 *server_principal* 可以是登入或使用者定義的伺服器角色。 *server_principal* 不能是固定伺服器角色、資料庫角色或系統管理員。  
  
DROP MEMBER *server_principal*  
從伺服器角色移除指定的伺服器主體。 *server_principal* 可以是登入或使用者定義的伺服器角色。 *server_principal* 不能是固定伺服器角色、資料庫角色或系統管理員。  
  
WITH NAME **=***new_server_role_name*  
指定使用者定義伺服器角色的新名稱。 此名稱不能已存在於伺服器中。  
  
## <a name="remarks"></a>Remarks  
變更使用者定義伺服器角色的名稱不會變更角色的識別碼、擁有者或權限。  
  
為變更角色成員資格，`ALTER SERVER ROLE` 會取代 sp_addsrvrolemember 和 sp_dropsrvrolemember。 這些預存程序都已被取代。  
  
您可以查詢 `sys.server_role_members` 和 `sys.server_principals` 目錄檢視來檢視伺服器角色。  
  
若要變更使用者定義伺服器角色的擁有者，請使用 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
需要伺服器的 `ALTER ANY SERVER ROLE` 權限，才能變更使用者定義伺服器角色的名稱。  
  
**固定伺服器角色**  
  
若要將成員加入至固定伺服器角色，您必須是該固定伺服器角色的成員，或是 `sysadmin` 固定伺服器角色的成員。  
  
> [!NOTE]  
>  `CONTROL SERVER` 和 `ALTER ANY SERVER ROLE` 權限並不足以執行固定伺服器角色的 `ALTER SERVER ROLE`，`ALTER` 權限亦無法授與固定伺服器角色。  
  
**使用者定義的伺服器角色**  
  
若要將成員新增至使用者定義的伺服器角色，您必須是 `sysadmin` 固定伺服器角色的成員，或擁有 `CONTROL SERVER` 或 `ALTER ANY SERVER ROLE` 權限。 或者，您必須有該角色的 `ALTER` 權限。  
  
> [!NOTE]  
>  不同於固定伺服器角色，使用者定義伺服器角色的成員本來就沒有將成員加入至該相同角色的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-name-of-a-server-role"></a>A. 變更伺服器角色的名稱  
下列範例會建立一個名為 `Product` 的伺服器角色，然後將伺服器角色名稱變更為 `Production`。  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. 將網域帳戶加入至伺服器角色  
下列範例會將網域帳戶 `adventure-works\roberto0` 新增至使用者定義的伺服器角色 `Production` 。  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. 將 SQL Server 登入加入至伺服器角色  
下列範例會將 `Ted` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入新增至 `diskadmin` 固定伺服器角色中。  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. 從伺服器角色移除網域帳戶  
下列範例會從使用者定義的伺服器角色 `Production` 移除網域帳戶 `adventure-works\roberto0`。  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. 從伺服器角色移除 SQL Server 登入  
下列範例會從 `diskadmin` 固定伺服器角色移除 `Ted` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. 將加入登入至使用者定義伺服器角色的權限授與登入  
下列範例允許 `Ted` 將其他登入加入至使用者定義的伺服器角色 `Production`。  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. 若要檢視角色成員資格  
若要檢視角色成員資格，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [伺服器角色 (成員)] 頁面，或執行下列查詢：  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. 基本語法  
下列範例會將 `Anna` 的 Windows 登入新增至 `LargeRC` 固定伺服器角色中。  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. 從資源類別移除登入。  
下列範例會卸除 Anna 在 `LargeRC` 伺服器角色中的成員資格。  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>另請參閱  
[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
