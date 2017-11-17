---
title: "GRANT 類型權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
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
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e29ede5580418d1cbcb55d5a877196c3cabab92
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="grant-type-permissions-transact-sql"></a>GRANT 類型權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  授與類型的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
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
 *權限*  
 指定可以授與的類型權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 型別上**::** [ *schema_name***。** ] *type_name*  
 指定要授與其權限的類型。 範圍限定詞 (**::**) 是必要。 如果*schema_name*未指定，會使用預設的結構描述。 如果*schema_name*指定時，結構描述範圍限定詞 (**。**) 是必要。  
  
 若要\<database_principal > 指定的正在授與權限的主體。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS \<database_principal > 指定要從中執行此查詢的主體衍生權限來授與權限的主體。  
  
 *Database_user*  
 指定資料庫使用者。  
  
 *Database_role*  
 指定資料庫角色。  
  
 *Application_role*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 指定應用程式角色。  
  
 *Database_user_mapped_to_Windows_User*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定對應至 Windows 使用者的資料庫使用者。  
  
 *Database_user_mapped_to_Windows_Group*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定對應至 Windows 群組的資料庫使用者。  
  
 *Database_user_mapped_to_certificate*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定對應至憑證的資料庫使用者。  
  
 *Database_user_mapped_to_asymmetric_key*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定對應至非對稱金鑰的資料庫使用者。  
  
 *Database_user_with_no_login*  
 指定不含對應伺服器層級主體的資料庫使用者。  
  
## <a name="remarks"></a>備註  
 類型是一個由結構描述所包含的結構描述層級安全性實體，在權限階層中，此結構描述為該安全性實體的父系。  
  
> [!IMPORTANT]  
>  **授與**， **DENY**和**撤銷**權限不會套用到系統類型。 使用者定義類型可以被授與權限。 如需使用者定義類型的詳細資訊，請參閱[使用 SQL Server 中的使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)。  
  
 下表所列的是可以授與之最特定和最有限的類型權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|類型權限|類型權限所隱含|結構描述權限所隱含|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|執行 CREATE 陳述式之前，請先執行|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用下列其他需求。  
  
|AS|其他必要的權限|  
|--------|------------------------------------|  
|資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至 Windows 登入的資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至 Windows 群組的資料庫使用者|在 Windows 群組中的成員資格的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至憑證的資料庫使用者|中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|對應至非對稱金鑰的資料庫使用者|中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|未對應至任何伺服器主體的資料庫使用者|中的成員資格使用者的 IMPERSONATE 權限**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|資料庫角色|ALTER 權限的角色中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
|應用程式角色|ALTER 權限的角色中的成員資格**db_securityadmin**固定的資料庫角色、 成員資格**db_owner**固定資料庫角色或中的成員資格**sysadmin**固定的伺服器角色。|  
  
## <a name="examples"></a>範例  
 下列範例會將使用者定義類型 `VIEW DEFINITION` 的 `GRANT OPTION` 權限及 `PhoneNumber` 授與使用者 `KhalidR`。 `PhoneNumber` 位於結構描述 `Telemarketing`。  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DENY 類型權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [REVOKE 類型權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


