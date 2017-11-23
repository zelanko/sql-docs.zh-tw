---
title: "授與結構描述權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- GRANT statement, schemas
- granting permissions [SQL Server], schemas
ms.assetid: b2aa1fc8-e7af-45d2-9f80-737543c8aa95
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 35e4775e421102931c0864dee97be0a862901416
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="grant-schema-permissions-transact-sql"></a>GRANT 結構描述權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  授與結構描述的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT permission  [ ,...n ] ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定可以授與的結構描述權限。 如需權限清單，請參閱這個主題稍後的＜備註＞一節。  
  
 ON SCHEMA **::**結構描述*b*  
 指定正在授與權限的結構描述。 範圍限定詞**::**需要。  
  
 *database_principal*  
 指定要對其授與權限的主體。 它有下列幾種：  
  
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
 指定主體，執行這項查詢的主體就是從這個主體衍生權限來授與權限。 它有下列幾種：  
  
-   資料庫使用者  
-   資料庫角色  
-   應用程式角色  
-   對應至 Windows 登入的資料庫使用者  
-   對應至 Windows 群組的資料庫使用者  
-   對應至憑證的資料庫使用者  
-   對應至非對稱金鑰的資料庫使用者  
-   未對應至伺服器主體的資料庫使用者  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  在某些情況下，ALTER 與 REFERENCE 權限的結合可允許被授與者檢視資料或執行未經授權的函數。 例如：擁有資料表的 ALTER 權限和函數的 REFERENCE 權限之使用者，可以透過函數來建立計算資料行並執行它。 在此情況下，使用者也必須擁有計算資料行的 SELECT 權限。  
  
 結構描述是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下面所列的是可以授與之最特定且最有限的結構描述權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|結構描述權限|結構描述權限所隱含|資料庫權限所隱含|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|DELETE|CONTROL|DELETE|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|執行 CREATE 陳述式之前，請先執行|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
> [!CAUTION]  
>  在結構描述上具有 ALTER 權限的使用者可以使用擁有權鏈結來存取其他結構描述中的安全性實體，包括使用者已被明確拒絕存取的安全性實體。 這是因為當所參考物件的擁有主體同時也擁有參考這些物件的物件時，擁有權鏈結就會略過參考物件上的權限檢查。 在結構描述上具有 ALTER 權限的使用者可以建立由結構描述擁有者所擁有的程序、同義字和檢視。 這些物件還可以在結構描述擁有者所擁有的其他結構描述中存取資訊 (透過擁有權鏈結)。 如果結構描述的擁有者同時也擁有其他結構描述，則在可能情況下，您應該盡量避免授與該結構描述的 ALTER 權限。  
  
 例如，這個問題可能會在下列狀況下發生。 下列狀況假設稱為 U1 的使用者在 S1 結構描述上具有 ALTER 權限。 U1 使用者在存取結構描述 S2 中稱為 T1 的資料表物件時遭拒。 S1 結構描述和 S2 結構描述是由同一個擁有者所擁有。  
  
 U1 使用者在資料庫上具有 CREATE PROCEDURE 權限，在 S1 結構描述上則具有 EXECUTE 權限。 因此，U1 使用者可以建立預存程序，然後在預存程序中存取遭拒的物件 T1。  
  
 U1 使用者在資料庫上具有 CREATE SYNONYM 權限，在 S1 結構描述上則具有 SELECT 權限。 因此，U1 使用者可以針對遭拒的物件 T1 在 S1 結構描述中建立同義字，然後使用該同義字存取遭拒的物件 T1。  
  
 U1 使用者在資料庫上具有 CREATE VIEW 權限，在 S1 結構描述上則具有 SELECT 權限。 因此，U1 使用者可以在 S1 結構描述中建立檢視從遭拒的物件 T1 查詢資料，然後使用該檢視存取遭拒的物件 T1。  
  
 如需詳細資訊，請參閱 Microsoft 知識庫文件編號 914847。  
  
## <a name="permissions"></a>Permissions  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用這些額外的需求。  
  
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
  
### <a name="a-granting-insert-permission-on-schema-humanresources-to-guest"></a>A. 將結構描述 HumanResources 的 INSERT 權限授與 Guest  
  
```  
GRANT INSERT ON SCHEMA :: HumanResources TO guest;  
```  
  
### <a name="b-granting-select-permission-on-schema-person-to-database-user-wiljo"></a>B. 將結構描述 Person 的 SELECT 權限授與資料庫使用者 WilJo  
  
```  
GRANT SELECT ON SCHEMA :: Person TO WilJo WITH GRANT OPTION;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [拒絕結構描述權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)   
 [REVOKE 結構描述權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [建立應用程式角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
