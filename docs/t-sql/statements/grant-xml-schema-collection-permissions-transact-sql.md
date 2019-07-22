---
title: GRANT XML 結構描述集合權限 (Transact-SQL) | Microsoft Docs
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
- GRANT statement, XML schema collections
- XML schema collections [SQL Server], permissions
- granting permissions [SQL Server], XML schema collections
- schema collections [SQL Server], permissions
ms.assetid: 57e24465-cd43-45cf-bb52-eea0b49867f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dbd2c35b360d3b3e1e9f6dabe7d011c20795bc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071187"
---
# <a name="grant-xml-schema-collection-permissions-transact-sql"></a>GRANT XML 結構描述集合權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與 XML 結構描述集合的權限。   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GRANT permission  [ ,...n ] ON   
    XML SCHEMA COLLECTION :: [ schema_name . ]  
    XML_schema_collection_name  
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
 指定可以授與的 XML 結構描述集合權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ON XML SCHEMA COLLECTION :: [ *schema_name*. ] *XML_schema_collection_name*  
 指定要授與其權限的 XML 結構描述集合。 需要範圍限定詞 (::)。 如果未指定 *schema_name*，則會使用預設結構描述。 如果指定 *schema_name*，則需要結構描述範圍限定詞 (.)。  
  
 \<database_principal> 指定要對其授與權限的主體。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS \<database_principal> 指定主體，以讓執行這項查詢的主體可從該主體衍生授與權限的權力。  
  
 *Database_user*  
 指定資料庫使用者。  
  
 *Database_role*  
 指定資料庫角色。  
  
 *Application_role*  
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
 您可以在 [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) 目錄檢視中，看到有關 XML 結構描述集合的資訊。  
  
 XML 結構描述集合是一個由結構描述所包含的結構描述層級安全性實體，在權限階層中，此結構描述為該安全性實體的父系。 下表所列的是可以授與之最特定且最有限的 XML 結構描述集合權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|XML 結構描述集合權限|XML 結構描述集合所隱含|結構描述權限所隱含|  
|--------------------------------------|-------------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|執行 CREATE 陳述式之前，請先執行|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>權限  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用下列其他需求。  
  
|AS|其他必要的權限|  
|--------|------------------------------------|  
|資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 登入的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 群組的資料庫使用者|Windows 群組中的成員資格、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至憑證的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至非對稱金鑰的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|未對應至任何伺服器主體的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|資料庫角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|應用程式角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
  
## <a name="examples"></a>範例  
 下列範例會將 XML 結構描述集合 `EXECUTE` 的 `Invoices4` 權限授與使用者 `Wanida`。 XML 結構描述集合 `Invoices4` 在 `Sales` 資料庫中 `AdventureWorks2012` 結構描述內。  
  
 ```
 USE AdventureWorks2012;  
 GRANT EXECUTE ON XML SCHEMA COLLECTION::Sales.Invoices4 TO Wanida;  
 GO
 ```  
  
## <a name="see-also"></a>另請參閱  
 [DENY XML 結構描述集合權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)   
 [REVOKE XML 結構描述集合權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)   
 [sys.xml_schema_collections &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)   
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

