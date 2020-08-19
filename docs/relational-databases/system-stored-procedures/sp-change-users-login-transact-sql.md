---
description: sp_change_users_login (Transact-SQL)
title: sp_change_users_login (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c82241030646e2ef20c978cb1905cf836f9a589b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447397"
---
# <a name="sp_change_users_login-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將現有的資料庫使用者對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 
  
 > [!IMPORTANT]
 > [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) 。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @Action =] '*action*'  
 描述此程序所要執行的動作。 *動作* 是 **Varchar (10) **。 *動作* 可以具有下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**Auto_Fix**|將目前資料庫中 sys.database_principals 系統目錄檢視的使用者項目連結到相同名稱的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 如果沒有相同名稱的登入，則會建立一個。 檢查 **Auto_Fix** 語句的結果，以確認確實已進行正確的連結。 避免在安全性敏感的情況下使用 **Auto_Fix** 。<br /><br /> 當您使用 **Auto_Fix**時，如果登入不存在，您必須指定 [ *使用者* ] 和 [ *密碼* ]，否則您必須指定 [ *使用者* ]，否則會忽略 *密碼* 。 *登* 入必須是 Null。 *使用者* 必須是目前資料庫中的有效使用者。 不能有其他使用者對應至登入。|  
|**Report**|列出目前資料庫中未連結至任何登入的使用者和對應的安全性識別碼 (SID)。 *使用者*、 *登*入和 *密碼* 必須是 Null 或未指定。<br /><br /> 若要使用系統資料表來取代報表選項與查詢，請將 **sys. server_prinicpals** 中的專案與 **sys. database_principals**中的專案進行比較。|  
|**Update_One**|將目前資料庫中指定的 *使用者* 連結至現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *登*入。 必須指定*使用者*和*登*入。 *密碼* 必須是 Null 或未指定。|  
  
 [ @UserNamePattern =] '*使用者*'  
 這是目前資料庫中的使用者名稱。 *使用者* 是 **sysname**，預設值是 Null。  
  
 [ @LoginName =] '*login*'  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。 *login* 是預設值為 NULL 的 **sysname**。  
  
 [ @Password =] '*password*'  
 這是指派給藉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 由指定 **Auto_Fix**所建立之新登入的密碼。 如果符合的登入已存在，則會對應使用者和登入，並忽略 *密碼* 。 如果符合的登入不存在，sp_change_users_login 會建立新的登入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並將 *密碼* 指派為新登入的密碼。 *密碼* 是 **sysname**，不能是 Null。  
  
> **重要！！** 請一律使用 [強式密碼！](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|資料庫使用者名稱。|  
|UserSID|**Varbinary (85) **|使用者的安全性識別碼。|  
  
## <a name="remarks"></a>備註  
 請使用 sp_change_users_login 將目前資料庫中的資料庫使用者與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入連結。 如果使用者的登入變更，可利用 sp_change_users_login 將使用者連結至新的登入，此舉並不會遺失使用者權限。 新的 *登* 入不能是 sa，且 *使用者* 不能是 dbo、guest 或 INFORMATION_SCHEMA 使用者。  
  
 sp_change_users_login 不能用來將資料庫使用者對應至 Windows 層級的主體、憑證或非對稱金鑰。  
  
 sp_change_users_login 不能搭配從 Windows 主體建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入使用，或是搭配 CREATE USER WITHOUT LOGIN 建立的使用者使用。  
  
 sp_change_users_login 無法在使用者定義的交易內執行。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格。 只有系統管理員（sysadmin）固定伺服器角色的成員，才能夠指定 **Auto_Fix** 選項。  
  
## <a name="examples"></a>範例  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 顯示目前使用者與登入對應的報表  
 下列範例會產生目前資料庫中的使用者及其安全性識別碼 (SID) 的報表。  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. 將資料庫使用者對應至新的 SQL Server 登入  
 下列範例中，資料庫使用者會與新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入建立關聯。 第一次對應至其他登入的資料庫使用者 `MB-Sales`，會重新對應至登入 `MaryB`。  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. 自動將使用者對應至登入，視需要建立新的登入  
 下列範例會顯示如何使用 `Auto_Fix` 將現有使用者對應至相同名稱的登入，或者如果登入 `Mary` 不存在的話，就會建立密碼為 `B3r12-3x$098f6` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Mary`。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
