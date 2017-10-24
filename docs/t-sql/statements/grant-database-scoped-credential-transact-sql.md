---
title: "授與資料庫範圍認證 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8fff82fbd6c81fea9cd9a7a95cabf35b0b8ecb7f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>授與資料庫範圍認證的權限 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

  授與權限的資料庫範圍認證。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定的權限可授與在資料庫範圍認證。 如下所列。  
  
 在資料庫範圍認證**::***credential_name*  
 指定授權的資料庫範圍的認證。 需要範圍限定詞 "::"。  
  
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
 資料庫範圍認證是包含資料庫層級安全性實體權限階層中其父系的資料庫。 最特定且最有限的權限可授與資料庫範圍認證是下面所列，列出利用隱含方式包含它們的較通用權限。  
  
|資料庫範圍認證的權限|資料庫範圍認證的權限所隱含|資料庫權限所隱含|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用這些額外的需求。  
  
|AS *granting_principal*|其他必要的權限|  
|------------------------------|------------------------------------|  
|資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至 Windows 登入的資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至 Windows 群組的資料庫使用者|在 Windows 群組中的成員資格的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至憑證的資料庫使用者|中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至非對稱金鑰的資料庫使用者|中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|未對應至任何伺服器主體的資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|資料庫角色|ALTER 權限的角色中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|應用程式角色|ALTER 權限的角色中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
  
 物件擁有者可以授與他們所擁有之物件的權限。 具有安全性實體之 CONTROL 權限的主體可以授與該安全性實體的權限。  
  
 被授與者的 CONTROL SERVER 權限，例如的成員**sysadmin**固定的伺服器角色可授與任何權限的任何伺服器安全性實體。 被授與者的 CONTROL 權限的資料庫，例如的成員**db_owner**固定的資料庫角色可授與任何權限的任何安全性實體，在資料庫中。 結構描述之 CONTROL 權限的被授與者，可以授與結構描述中任何物件的任何權限。  
  
## <a name="see-also"></a>另請參閱  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE 資料庫範圍認證 (TRANSACT-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [拒絕資料庫範圍認證 (TRANSACT-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

