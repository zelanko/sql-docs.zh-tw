---
title: GRANT 資料庫主體權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- permissions [SQL Server], database roles
- granting permissions [SQL Server], database users
- granting permissions [SQL Server], application roles
- granting permissions [SQL Server], database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- GRANT statement, users
- GRANT statement, roles
- application roles [SQL Server], permissions
ms.assetid: 012588a2-cbe1-48f0-a731-b4a2b83203d5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac987ef327b021665ae797aa3f14aad6446fcc4d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807716"
---
# <a name="grant-database-principal-permissions-transact-sql"></a>GRANT 資料庫主體權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫使用者、資料庫角色或應用程式角色的權限。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
       [ WITH GRANT OPTION ]  
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
 指定可授予的資料庫主體權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 USER ::*database_user*  
 指定授與其權限之使用者的類別和名稱。 需要範圍限定詞 (::)。  
  
 ROLE ::*database_role*  
 指定獲得權限授與之角色的類別和名稱。 需要範圍限定詞 (::)。  
  
 APPLICATION ROLE ::*application_role*  
   
 指定授與其權限之應用程式角色的類別和名稱。 需要範圍限定詞 (::)。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS \<database_principal>  
 指定主體，執行這項查詢的主體就是從這個主體衍生權限來授與權限。  
  
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
 您可以在 [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 目錄檢視中，看到有關資料庫主體的資訊。 您可以在 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 目錄檢視中，看到有關資料庫層級權限的資訊。  
  
## <a name="database-user-permissions"></a>資料庫使用者權限  
 資料庫使用者是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列為可授與資料庫使用者之最特別和最有限的權限，以及利用隱含方式包含前述權限的較通用權限。  
  
|資料庫使用者權限|資料庫使用者權限所隱含|資料庫權限所隱含|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>資料庫角色權限  
 資料庫角色是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以授與之最特定和最有限的資料庫角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|資料庫角色權限|資料庫角色權限所隱含|資料庫權限所隱含|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>應用程式角色權限  
 應用程式角色是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下面所列的是可以授與之最特定和最有限的應用程式角色權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|應用程式角色權限|應用程式角色權限所隱含|資料庫權限所隱含|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>[權限]  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用下列其他需求。  
  
|AS *granting_principal*|其他必要的權限|  
|------------------------------|------------------------------------|  
|資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 使用者的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 群組的資料庫使用者|Windows 群組中的成員資格、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至憑證的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至非對稱金鑰的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或 sysadmin 固定伺服器角色中的成員資格。|  
|未對應至任何伺服器主體的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|資料庫角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或 sysadmin 固定伺服器角色中的成員資格。|  
|應用程式角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
  
 具有安全性實體之 CONTROL 權限的主體可以授與該安全性實體的權限。  
  
 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以授予資料庫中任何安全性實體的任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-control-permission-on-a-user-to-another-user"></a>A. 將一個使用者的 CONTROL 權限授與另一個使用者  
 下列範例會將 `CONTROL` 使用者 `AdventureWorks2012` 的 `Wanida` 權限授與使用者 `RolandX`。  
  
```  
GRANT CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-granting-view-definition-permission-on-a-role-to-a-user-with-grant-option"></a>B. 將角色的 VIEW DEFINITION 權限授與具有 GRANT OPTION 的使用者  
 下列範例將 `VIEW DEFINITION` 角色 `AdventureWorks2012` 的 `SammamishParking` 權限連同 `GRANT OPTION` 授與資料庫使用者 `JinghaoLiu`。  
  
```  
GRANT VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-impersonate-permission-on-a-user-to-an-application-role"></a>C. 將使用者的 IMPERSONATE 權限授與應用程式角色  
 下列範例對 `IMPERSONATE` 應用程式角色 `HamithaL` 授與使用者 `AdventureWorks2012` 的 `AccountsPayable17` 權限。  
  
**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
```  
GRANT IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>另請參閱  
 [DENY 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [REVOKE 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
