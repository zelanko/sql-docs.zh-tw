---
title: GRANT 伺服器主體權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- impersonate [SQL Server], granting
- granting permissions [SQL Server], logins
- permissions [SQL Server], impersonate
- permissions [SQL Server], logins
- GRANT statement, impersonation
- GRANT statement, logins
- logins [SQL Server], granting access
- granting permissions [SQL Server], impersonation
ms.assetid: 4cbed281-5e1e-4d8b-b410-4c18a6cd0205
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 19cccc7c8199e3cdfc425cf8269c363549ad69de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781406"
---
# <a name="grant-server-principal-permissions-transact-sql"></a>GRANT 伺服器主體權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GRANT permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>引數  
 *permission*  
 指定可以授與的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 LOGIN **::** *SQL_Server_login*  
 指定要授與其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 範圍限定詞 (**::**) 是必要項。  
  
 SERVER ROLE **::** *server_role*  
 指定授與其權限之使用者定義伺服器角色。 範圍限定詞 (**::**) 是必要項。  
  
 TO \<server_principal> 指定要對其授與權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或伺服器角色。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *SQL_Server_login_from_Windows_login*  
 指定從 Windows 登入建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_certificate*  
 指定對應至憑證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_AsymKey*  
 指定對應至非對稱金鑰的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *server_role*  
 指定使用者定義伺服器角色的名稱。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來授與權限。  
  
## <a name="remarks"></a>Remarks  
 只有在目前資料庫是 master 的情況下，才能夠授與伺服器範圍的權限。  
  
 您可以在 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 目錄檢視中，看到有關伺服器權限的資訊。 您可以在 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視中，看到有關伺服器主體的資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和伺服器角色是伺服器層級安全性實體。 下表所列的是可以授與之最特定和最有限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或伺服器角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|SQL Server 登入或伺服器角色權限|SQL Server 登入或伺服器角色權限所隱含|伺服器權限所隱含|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>[權限]  
 對於登入，需要登入的 CONTROL 權限或伺服器的 ALTER ANY LOGIN 權限。  
  
 對於伺服器角色，需要伺服器角色的 CONTROL 權限或伺服器的 ALTER ANY SERVER ROLE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-impersonate-permission-on-a-login"></a>A. 授與登入的 IMPERSONATE 權限  
 下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `WanidaBenshoof` 的 `IMPERSONATE` 權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，而該項登入是透過 Windows 使用者 `AdvWorks\YoonM` 所建立。  
  
```  
USE master;  
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-granting-view-definition-permission-with-grant-option"></a>B. 授與具有 GRANT OPTION 的 VIEW DEFINITION 權限  
 下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `VIEW DEFINITION` 的 `EricKurjan` 授與具有 `RMeyyappan` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `GRANT OPTION`。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    WITH GRANT OPTION;  
GO   
```  
  
### <a name="c-granting-view-definition-permission-on-a-server-role"></a>C. 授與伺服器角色的 VIEW DEFINITION 權限  
 下列範例會將 `VIEW DEFINITION` 伺服器角色的 `Sales` 權限授與 `Auditors` 伺服器角色。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

