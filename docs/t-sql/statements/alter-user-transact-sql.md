---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 522ff2df33067792979e785b60417c9783d5e46a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62648804"
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  重新命名資料庫使用者或變更其預設結構描述。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```

> [!IMPORTANT]
> SQL Database 受控執行個體的 Azure AD 登入處於**公開預覽**狀態。 套用至使用 Azure AD 登入的使用者時，Azure SQL Database 受控執行個體只支援下列選項：`DEFAULT_SCHEMA = { schemaName | NULL }` 和 `DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }`

```
-- Syntax for Azure SQL Database  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,... n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *userName*  
 指定在這個資料庫內用來識別使用者的名稱。  
  
 LOGIN **=** _loginName_  
 變更使用者的安全性識別碼 (SID) 使其符合登入的 SID，以便將使用者重新對應到另一個登入。  
  
 如果 ALTER USER 陳述式是 SQL 批次中的唯一陳述式，Windows Azure SQL Database 會支援 WITH LOGIN 子句。 如果 ALTER USER 陳述式不是 SQL 批次中的唯一陳述式或是在動態 SQL 中執行，則不支援 WITH LOGIN 子句。  
  
 NAME **=** _newUserName_  
 指定新的名稱給這位使用者。 *newUserName* 不可已存在目前資料庫中。  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 指定當伺服器解析這位使用者的物件名稱時，將搜尋的第一個結構描述。 當預設結構描述設為 NULL 時，會從 Windows 群組移除預設結構描述。   NULL 選項不可用於 Windows 使用者。  
  
 PASSWORD **=** '*password*'  
 **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定正在變更之使用者的密碼。 密碼會區分大小寫。  
  
> [!NOTE]  
>  只有包含的使用者能夠使用此選項。 請參閱[自主資料庫](../../relational-databases/databases/contained-databases.md)和 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md) 以取得詳細資訊。  
  
 OLD_PASSWORD **=** _'oldpassword'_  
 **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 目前的使用者密碼，將由 '*password*' 取代。 密碼會區分大小寫。 密碼區分大小寫。除非您有 **ALTER ANY USER** 權限，否則需要 *OLD_PASSWORD* 才能變更密碼。 需要 *OLD_PASSWORD* 可防止具有 **IMPERSONATION** 權限的使用者變更密碼。  
  
> [!NOTE]  
>  只有包含的使用者能夠使用此選項。  
  
 DEFAULT_LANGUAGE **=** _{ NONE | \<lcid> | \<語言名稱> | \<語言別名> }_  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要指派給使用者的預設語言。 如果這個選項設為 NONE，預設語言將設為資料庫的目前預設語言。 如果稍後變更了資料庫的預設語言，使用者的預設語言會保持不變。 *DEFAULT_LANGUAGE* 可以是本機識別碼 (lcid)、語言名稱或語言別名。  
  
> [!NOTE]  
>  這個選項只能指定在自主資料庫中，而且只適用於包含的使用者。  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ] ]  
 **適用對象**：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 在大量複製作業時隱藏伺服器上的密碼編譯中繼資料檢查。 這會讓使用者得以在資料表或資料庫間大量複製加密資料，而無須解密資料。 預設值為 OFF。  
  
> [!WARNING]  
>  不當使用這個選項會導致資料損毀。 如需詳細資訊，請參閱[移轉透過 Always Encrypted 保護的機密資料](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
## <a name="remarks"></a>Remarks  
 預設結構描述是伺服器在解析這個資料庫使用者之物件名稱時，所搜尋到的第一個結構描述。 除非另有指定，否則預設結構描述是此資料庫使用者建立之物件的擁有者。  
  
 如果使用者有預設結構描述，則使用預設結構描述。 如果使用者沒有預設結構描述，但使用者是有預設結構描述之群組的成員，則使用群組的預設結構描述。 如果使用者沒有預設結構描述，而且是有一個以上之群組的成員，使用者的預設結構描述將會是具有最低 principle_id 且明確設定預設結構描述之 Windows 群組的結構描述。 如果無法判斷使用者的預設結構描述，即會使用 **dbo** 結構描述。  
  
 DEFAULT_SCHEMA 可設為目前不存在於資料庫中的結構描述。 因此，您可以在建立該結構描述之前，先將 DEFAULT_SCHEMA 指派給使用者。  
  
 DEFAULT_SCHEMA 不能指定給對應至憑證或非對稱金鑰的使用者。  
  
> [!IMPORTANT]  
>  如果使用者是 **sysadmin** 固定伺服器角色的成員，則會忽略 DEFAULT_SCHEMA 的值。 **sysadmin** 固定伺服器角色的所有成員都有預設的 `dbo` 結構描述。  
  
 當新使用者名稱的 SID 符合資料庫所記錄的 SID 時，您可以變更對應至 Windows 登入或群組的使用者名稱。 這項檢查可防止資料庫中詐騙的 Windows 登入。  
  
 WITH LOGIN 子句可讓使用者重新對應到另一個登入。 沒有登入的使用者、對應至憑證的使用者或是對應至非對稱金鑰的使用者，都無法使用這個子句來重新對應。 只有 SQL 使用者和 Windows 使用者 (或群組) 才能重新對應。 WITH LOGIN 子句無法用來變更使用者的類型，例如將 Windows 帳戶變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 如果下列條件成立，使用者的名稱將會自動重新命名為登入名稱。  
  
-   使用者是 Windows 使用者。  
  
-   名稱是 Windows 名稱 (包含反斜線)。  
  
-   沒有指定任何新的名稱。  
  
-   目前的名稱不同於登入名稱。  
  
 否則，除非呼叫端額外叫用 NAME 子句，否則使用者將不會重新命名。  
  
對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入、憑證或非對稱金鑰的使用者名稱不可包含反斜線字元 (\\)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Security  
  
> [!NOTE]  
>  具有 **ALTER ANY USER** 權限的使用者可以變更任何使用者的預設結構描述。 結構描述變更過的使用者可能會在不知情的情況下，從錯誤的資料表選取資料或從錯誤的結構描述執行程式碼。  
  
### <a name="permissions"></a>權限  
 若要變更使用者的名稱，需要具有 **ALTER ANY USER** 權限。  
  
 若要變更使用者的目標登入，則需要資料庫的 **CONTROL** 權限。  
  
 若要變更擁有資料庫 **CONTROL** 權限之使用者的使用者名稱，則需要資料庫的 **CONTROL** 權限。  
  
 若要變更預設結構描述或語言，需要使用者的 **ALTER** 權限。 使用者能夠變更他們自己的預設結構描述或語言。  
  
## <a name="examples"></a>範例  

所有的範例會在使用者資料庫中執行。  

### <a name="a-changing-the-name-of-a-database-user"></a>A. 變更資料庫使用者的名稱  
 下列範例會將資料庫使用者名稱 `Mary5` 變更為 `Mary51`。  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. 變更使用者的預設結構描述  
 下列範例會將使用者 `Mary51` 的預設結構描述變更為 `Purchasing`。  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. 一次變更數個選項  
 下列範例會在一個陳述式中變更自主資料庫使用者的數個選項。  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [自主資料庫](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  


