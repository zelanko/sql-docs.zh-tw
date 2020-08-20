---
description: DENY 伺服器主體權限 (Transact-SQL)
title: DENY 伺服器主體權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0b3dbb2766d1e42fd1812e9eba5d92c40b324a25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478909"
---
# <a name="deny-server-principal-permissions-transact-sql"></a>DENY 伺服器主體權限 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拒絕授與的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入權限。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *permission*  
 指定可以拒絕的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 LOGIN **::** *SQL_Server_login*  
 指定要拒絕其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 範圍限定詞 ( **::** ) 是必要項。  
  
 SERVER ROLE **::** *server_role*  
 指定要拒絕其權限的伺服器角色。 範圍限定詞 ( **::** ) 是必要項。  
  
 TO \<server_principal>  
 指定要授與其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或伺服器角色。  
  
 TO *SQL_Server_login*  
 指定要拒絕其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *SQL_Server_login_from_Windows_login*  
 指定從 Windows 登入建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_certificate*  
 指定對應至憑證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_AsymKey*  
 指定對應至非對稱金鑰的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *server_role*  
 指定伺服器角色的名稱。  
  
 CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來拒絕權限。  
  
## <a name="remarks"></a>備註  
 只有在目前資料庫是 master 的情況下，才能夠拒絕伺服器範圍的權限。  
  
 有關伺服器權限的資訊可在 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 目錄檢視中取得。 有關伺服器主體的資訊可在 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視中取得。  
  
 當您拒絕主體的權限 (而其已透過 GRANT OPTION 獲授與該權限) 時，若未指定 CASCADE，DENY 陳述式會失敗。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和伺服器角色是伺服器層級安全性實體。 下表所列的是可以拒絕之最特定和最有限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或伺服器角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|SQL Server 登入或伺服器角色權限|SQL Server 登入或伺服器角色權限所隱含|伺服器權限所隱含|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>權限  
 對於登入，需要登入的 CONTROL 權限或伺服器的 ALTER ANY LOGIN 權限。  
  
 對於伺服器角色，需要伺服器角色的 CONTROL 權限或伺服器的 ALTER ANY SERVER ROLE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. 拒絕登入的 IMPERSONATE 權限  
 下列範例會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入拒絕 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `WanidaBenshoof` 的 `IMPERSONATE` 權限，而這項登入是從 Windows 使用者 `AdvWorks\YoonM` 所建立。  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. 拒絕具有 CASCADE 的 VIEW DEFINITION 權限  
 下列範例會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `VIEW DEFINITION` 拒絕 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `EricKurjan` 的 `RMeyyappan` 權限。 `CASCADE` 選項指出也會對 `VIEW DEFINITION` 對其授與這個權限的主體，拒絕 `EricKurjan` 的 `RMeyyappan` 權限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. 拒絕伺服器角色的 VIEW DEFINITION 權限  
 下列範例會對 `VIEW DEFINITION` 伺服器角色拒絕 `Sales` 伺服器角色的 `Auditors` 權限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
