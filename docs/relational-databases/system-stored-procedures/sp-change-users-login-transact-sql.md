---
title: "sp_change_users_login (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/13/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 207272f7644ab39055b7c6bb330faf6053353601
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangeuserslogin-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將現有的資料庫使用者對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER USER](../../t-sql/statements/alter-user-transact-sql.md)改為。  
  
  
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
 [ @Action=] '*動作*'  
 描述此程序所要執行的動作。 *動作*是**varchar （10)**。 *動作*可以有下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**Auto_Fix**|將目前資料庫中 sys.database_principals 系統目錄檢視的使用者項目連結到相同名稱的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 如果沒有相同名稱的登入，則會建立一個。 檢查的結果**Auto_Fix**陳述式來確認，事實上進行正確的連結。 請避免使用**Auto_Fix**在安全性敏感的情況下。<br /><br /> 當您使用**Auto_Fix**，您必須指定*使用者*和*密碼*如果登入不存在，否則您必須指定*使用者*但*密碼*會被忽略。 *登入*必須是 NULL。 *使用者*必須是目前資料庫中的有效使用者。 不能有其他使用者對應至登入。|  
|**報表**|列出目前資料庫中未連結至任何登入的使用者和對應的安全性識別碼 (SID)。 *使用者*，*登入*，和*密碼*必須是 NULL 或未指定。<br /><br /> 若要取代查詢中使用的系統資料表 [報表] 選項，比較中的項目**sys.server_prinicpals**中項目的**sys.database_principals**。|  
|**Update_One**|連結指定*使用者*在目前資料庫的現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*登入*。 *使用者*和*登入*必須指定。 *密碼*必須是 NULL 或未指定。|  
  
 [ @UserNamePattern=] '*使用者*'  
 這是目前資料庫中的使用者名稱。 *使用者*是**sysname**，預設值是 NULL。  
  
 [ @LoginName=] '*登入*'  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。 *登入*是**sysname**，預設值是 NULL。  
  
 [ @Password=] '*密碼*'  
 指派給新的密碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定所建立的登入**Auto_Fix**。 如果符合的登入已經存在，對應的使用者和登入和*密碼*會被忽略。 如果符合的登入不存在，則 sp_change_users_login 會建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入並指派*密碼*當做新登入的密碼。 *密碼*是**sysname**，而且不可以是 NULL。  
  
> **重要！！** 一律使用[強式密碼 ！](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|資料庫使用者名稱。|  
|UserSID|**varbinary(85)**|使用者的安全性識別碼。|  
  
## <a name="remarks"></a>備註  
 請使用 sp_change_users_login 將目前資料庫中的資料庫使用者與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入連結。 如果使用者的登入變更，可利用 sp_change_users_login 將使用者連結至新的登入，此舉並不會遺失使用者權限。 新*登入*不可以是 sa，而*使用者*不可為 dbo、 gues 或 INFORMATION_SCHEMA 使用者。  
  
 sp_change_users_login 不能用來將資料庫使用者對應至 Windows 層級的主體、憑證或非對稱金鑰。  
  
 sp_change_users_login 不能搭配從 Windows 主體建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入使用，或是搭配 CREATE USER WITHOUT LOGIN 建立的使用者使用。  
  
 sp_change_users_login 無法在使用者定義的交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 固定資料庫角色中的成員資格。 只有 sysadmin 固定的伺服器角色的成員可以指定**Auto_Fix**選項。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
