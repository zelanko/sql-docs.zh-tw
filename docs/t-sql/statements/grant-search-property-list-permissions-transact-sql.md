---
title: "GRANT 搜尋屬性清單權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], permissions
- search property lists [SQL Server], permissions
- granting permissions [SQL Server], search property lists
- GRANT statement, search property list permissions
ms.assetid: bb2d2550-9c0e-4a88-b50c-12e481d4d3ae
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5af3884c41ad4f240ed53215b0d0e807cacf64a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="grant-search-property-list-permissions-transact-sql"></a>GRANT 搜尋屬性清單權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  授與搜尋屬性清單的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GRANT permission [ ,...n ] ON   
    SEARCH PROPERTY LIST :: search_property_list_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 這是權限的名稱。 安全性實體權限的有效對應描述於本主題後面的「備註」一節中。  
  
 搜尋屬性清單**::***search_property_list_name*  
 指定要授與其權限的搜尋屬性清單。 範圍限定詞**::**需要。  
  
 **若要檢視現有的搜尋屬性清單**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 *database_principal*  
 指定要對其授與權限的主體。 主體可以是下列其中一項：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
 GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS *granting_principal*  
 指定主體，執行這項查詢的主體就是從這個主體衍生權限來授與權限。 主體可以是下列其中一項：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
## <a name="remarks"></a>備註  
  
## <a name="search-property-list-permissions"></a>SEARCH PROPERTY LIST 權限  
 搜尋屬性清單是一個由資料庫所自主資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以授與之最特定且最有限的搜尋屬性清單權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|搜尋屬性清單權限|搜尋屬性清單權限所隱含|資料庫權限所隱含|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用下列額外的需求。  
  
|AS *granting_principal*|其他必要的權限|  
|------------------------------|------------------------------------|  
|資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 登入的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 群組的資料庫使用者|Windows 群組中的成員資格、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至憑證的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至非對稱金鑰的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|未對應至任何伺服器主體的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|資料庫角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|應用程式角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
  
 物件擁有者可以授與他們所擁有之物件的權限。 具有安全性實體之 CONTROL 權限的主體可以授與該安全性實體的權限。  
  
 CONTROL SERVER 權限的被授與者 (例如系統管理員 (sysadmin) 固定伺服器角色的成員)，可以授與伺服器中任何安全性實體的任何權限。 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以授予資料庫中任何安全性實體的任何權限。 結構描述之 CONTROL 權限的被授與者，可以授與結構描述中任何物件的任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="granting-permissions-to-a-search-property-list"></a>授與搜尋屬性清單的權限  
 下列範例會將搜尋屬性清單 `Mary` 的 `VIEW DEFINITION` 權限授與 `DocumentTablePropertyList`。  
  
```  
GRANT VIEW DEFINITION  
    ON SEARCH PROPERTY LIST :: DocumentTablePropertyList  
    TO Mary ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [建立應用程式角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [建立搜尋屬性清單 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [拒絕搜尋屬性清單權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [撤銷搜尋屬性清單權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.registered_search_property_lists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
