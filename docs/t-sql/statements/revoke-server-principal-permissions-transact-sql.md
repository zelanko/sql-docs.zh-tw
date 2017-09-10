---
title: "REVOKE 伺服器主體權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, impersonation
- permissions [SQL Server], impersonation
- permissions [SQL Server], logins
- impersonate [SQL Server], revoking
- logins [SQL Server], revoking
- REVOKE statement, logins
ms.assetid: 75409024-f150-4326-af16-9d60e900df18
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13dca8052ad8bc74491136c941677606ccecbe3c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-server-principal-permissions-transact-sql"></a>REVOKE 伺服器主體權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤銷授與或拒絕的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey     
    | server_role  
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定可以撤銷的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 登入**::** *SQL_Server_login*  
 指定要撤銷其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 範圍限定詞 (**::**) 是必要。  
  
 伺服器角色**::** *server_role*  
 指定要撤銷其權限的伺服器角色。 範圍限定詞 (**::**) 是必要。  
  
 {從 |為} \<server_principal > 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在撤銷權限的登入或伺服器角色。  
  
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
  
 GRANT OPTION  
 指出會撤銷對其他主體授與指定權限的權限。 不會撤銷權限本身。  
  
> [!IMPORTANT]  
>  如果主體有不含 GRANT 選項的指定權限，則會撤銷權限本身。  
  
 CASCADE  
 指出目前正在撤銷的權限，而這個權限也會被這個主體所授與或拒絕的其他主體所撤銷。  
  
> [!CAUTION]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來撤銷權限。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和伺服器角色是伺服器層級安全性實體。 下表所列的是可以撤銷之最特定和最有限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或伺服器角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|SQL Server 登入或伺服器角色權限|SQL Server 登入或伺服器角色權限所隱含|伺服器權限所隱含|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissions  
 對於登入，需要登入的 CONTROL 權限或伺服器的 ALTER ANY LOGIN 權限。  
  
 對於伺服器角色，需要伺服器角色的 CONTROL 權限或伺服器的 ALTER ANY SERVER ROLE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-revoking-impersonate-permission-on-a-login"></a>A. 撤銷登入的 IMPERSONATE 權限  
 下列範例會撤銷`IMPERSONATE`權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入`WanidaBenshoof`從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所建立的 Windows 使用者的登入`AdvWorks\YoonM`。  
  
```  
USE master;  
REVOKE IMPERSONATE ON LOGIN::WanidaBenshoof FROM [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-with-cascade"></a>B. 撤銷具有 CASCADE 的 VIEW DEFINITION 權限  
 下列範例會撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `VIEW DEFINITION` 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `EricKurjan` 的 `RMeyyappan` 權限。 `CASCADE` 選項指出 `VIEW DEFINITION` 的 `EricKurjan` 權限也會被 `RMeyyappan` 所授與權限的主體所撤銷。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON LOGIN::EricKurjan FROM RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-revoking-view-definition-permission-on-a-server-role"></a>C. 撤銷伺服器角色的 VIEW DEFINITION 權限  
 下列範例會對 `VIEW DEFINITION` 伺服器角色撤銷 `Sales` 伺服器角色的 `Auditors` 權限。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [DENY 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  


