---
title: DENY 資料庫主體權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- denying permissions [SQL Server], database roles
- denying permissions [SQL Server], database users
- permissions [SQL Server], database roles
- DENY statement, database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- database permissions [SQL Server], denying
- DENY statement, application roles
- DENY statement, database users
- denying permissions [SQL Server], application roles
- application roles [SQL Server], permissions
ms.assetid: e2429a5d-e9be-4c05-be20-414d1038a63a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d781778f46617a8961506fb022854835717ea0bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114886"
---
# <a name="deny-database-principal-permissions-transact-sql"></a>DENY 資料庫主體權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中拒絕授與資料庫使用者、資料庫角色或應用程式角色的權限。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DENY permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
      [ CASCADE ]  
      [ AS <database_principal> ]  
  
<database_principal> ::=  
    Database_user   
  | Database_role   
  | Application_role   
  | Database_user_mapped_to_Windows_User   
  | Database_user_mapped_to_Windows_Group   
  | Database_user_mapped_to_certificate   
  | Database_user_mapped_to_asymmetric_key   
  | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>引數  
 *permission*  
 指定可拒絕的資料庫主體權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 USER ::*database_user*  
 指定拒絕其權限之使用者的類別和名稱。 範圍限定詞 ( **::** ) 是必要項。  
  
 ROLE ::*database_role*  
 指定拒絕其權限之角色的類別和名稱。 範圍限定詞 ( **::** ) 是必要項。  
  
 APPLICATION ROLE ::*application_role*  
 **適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定拒絕其權限之應用程式角色的類別和名稱。 範圍限定詞 ( **::** ) 是必要項。  
  
 CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
 AS \<database_principal>  
 指定主體，執行這項查詢的主體會從這個主體衍生其權限來撤銷權限。  
  
 *Database_user*  
 指定資料庫使用者。  
  
 *Database_role*  
 指定資料庫角色。  
  
 *Application_role*  
 **適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定應用程式角色。  
  
 *Database_user_mapped_to_Windows_User*  
 指定對應至 Windows 使用者的資料庫使用者。  
  
 *Database_user_mapped_to_Windows_Group*  
 指定對應至 Windows 群組的資料庫使用者。  
  
 *Database_user_mapped_to_certificate*  
  指定對應至憑證的資料庫使用者。  
  
 *Database_user_mapped_to_asymmetric_key*  
  指定對應至非對稱金鑰的資料庫使用者。  
  
 *Database_user_with_no_login*  
 指定不含對應伺服器層級主體的資料庫使用者。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="database-user-permissions"></a>資料庫使用者權限  
 資料庫使用者是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以拒絕之最特定且最有限的資料庫使用者權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|資料庫使用者權限|資料庫使用者權限所隱含|資料庫權限所隱含|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>資料庫角色權限  
 資料庫角色是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以拒絕之最特定且最有限的資料庫角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|資料庫角色權限|資料庫角色權限所隱含|資料庫權限所隱含|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>應用程式角色權限  
 應用程式角色是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以拒絕之最特定且最有限的應用程式角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|應用程式角色權限|應用程式角色權限所隱含|資料庫權限所隱含|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>權限  
 需要指定主體的 CONTROL 權限，或需要隱含 CONTROL 權限的更高權限。  
  
 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員) 可以拒絕資料庫中任何安全性實體的任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-denying-control-permission-on-a-user-to-another-user"></a>A. 對其他使用者拒絕使用者的 CONTROL 權限  
 下列範例會對使用者 `CONTROL` 拒絕 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 使用者 `Wanida` 的 `RolandX` 權限。  
  
```  
USE AdventureWorks2012;  
DENY CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-denying-view-definition-permission-on-a-role-to-a-user-to-which-it-was-granted-with-grant-option"></a>B. 對被授與 GRANT OPTION 的使用者，拒絕角色的 VIEW DEFINITION 權限  
 下列範例會對資料庫使用者 `VIEW DEFINITION` 拒絕 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 角色 `SammamishParking` 的 `JinghaoLiu` 權限。 有指定 `CASCADE` 選項，因為使用者 `JinghaoLiu` 被授與 VIEW DEFINITION 權限 WITH GRANT OPTION。  
  
```  
USE AdventureWorks2012;  
DENY VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-denying-impersonate-permission-on-a-user-to-an-application-role"></a>C. 對應用程式角色拒絕使用者的 IMPERSONATE 權限  
 下列範例會對 `IMPERSONATE` 應用程式角色 `HamithaL`，拒絕使用者 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 的 `AccountsPayable17` 權限。  
  
**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
```  
USE AdventureWorks2012;  
DENY IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>另請參閱  
 [GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [REVOKE 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
