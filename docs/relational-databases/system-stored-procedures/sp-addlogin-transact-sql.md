---
title: "sp_addlogin (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- sp_addlogin
- sp_addlogin_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: be1975ed58567b53ad10af9cd9d40d7640bd1621
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一項新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，讓使用者利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)改為。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @loginame=] '*登入*'  
 這是登入的名稱。 *登入*是**sysname**，沒有預設值。  
  
 [ @passwd=] '*密碼*'  
 這是登入密碼。 *密碼*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*資料庫*'  
 這是登入的預設資料庫 (在登入之後，登入第一次連接的資料庫)。 *資料庫*是**sysname**，預設值是**主要**。  
  
 [ @deflanguage=] '*語言*'  
 這是登入的預設語言。 *語言*是**sysname**，預設值是 NULL。 如果*語言*未指定，預設值*語言*，新登入設定為伺服器的目前預設語言。  
  
 [ @sid=] '*sid*'  
 這是安全性識別碼 (SID)。 *sid*是**varbinary （16)**，預設值是 NULL。 如果*sid*是 NULL，系統會產生新的登入的 SID。 使用儘管**varbinary**資料類型 NULL 以外的值必須剛好為 16 個位元組的長度，且必須尚未存在。 指定*sid*非常有用，例如，當您要編寫指令碼或移動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從一部伺服器的登入另一個且您想要有相同的 SID 不同伺服器上的登入。  
  
 [ @encryptopt=] '*encryption_option*'  
 指定以明碼方式傳遞密碼，或以純文字密碼的雜湊來傳遞密碼。 請注意，這裡並不進行任何加密。 這項討論用到 "encrypt" 一字，是為了與舊版相容。 如果傳入純文字密碼，就會雜湊這個密碼。 這項雜湊會儲存起來。 *encryption_option*是**varchar （20)**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|NULL|傳遞純文字密碼。 這是預設值。|  
|**skip_encryption**|密碼已雜湊。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該直接儲存這個值，不需要重新雜湊。|  
|**skip_encryption_old**|提供的密碼是由舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所雜湊的。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該直接儲存這個值，不需要重新雜湊。 這個選項專用來升級。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入可以包含 1 到 128 個字元，其中包括字母、符號和數字。 登入不能包含反斜線 (\\); 可以是保留的登入名稱，例如 sa 或 public，或已經存在; 或為 NULL 或空字串 (`''`)。  
  
 如果提供了預設資料庫的名稱，您可以直接連接到指定的資料庫，不需要執行 USE 陳述式。 不過，您無法使用的預設資料庫之前您都可以存取該資料庫的資料庫擁有者 (使用[sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)或[sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) 或[sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 SID 號碼是在伺服器中用來唯一識別登入的 GUID。  
  
 變更伺服器的預設語言並不會變更現有登入的預設語言。 若要變更伺服器的預設語言，請使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 使用**skip_encryption**來抑制密碼雜湊會很有用，如果密碼已雜湊時登入加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果密碼已雜湊舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用**skip_encryption_old**。  
  
 sp_addlogin 無法在使用者自訂交易內執行。  
  
 下表顯示搭配 sp_addlogin 使用的數個預存程序。  
  
|預存程序|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|加入 Windows 使用者或群組。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|變更使用者的密碼。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|變更使用者的預設資料庫。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|變更使用者的預設語言。|  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-sql-server-login"></a>A. 建立 SQL Server 登入  
 下列範例會建立 `Victoria` 使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，密碼是 `B1r12-36`，不指定預設資料庫。  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 建立有預設資料庫的 SQL Server 登入  
 下列範例會建立 `Albert` 使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，密碼是 `B5432-3M6`，預設資料庫是 `corporate`。  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 建立有不同預設語言的 SQL Server 登入  
 下列範例會建立 `TzTodorov` 使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，密碼是 `709hLKH7chjfwv`，預設資料庫是 `AdventureWorks2012`，預設語言是 `Bulgarian`。  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 建立有特定 SID 的 SQL Server 登入  
 下列範例會建立 `Michael` 使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，密碼是 `B548bmM%f6`，預設資料庫是 `AdventureWorks2012`，預設語言是 `us_english`，SID 是 `0x0123456789ABCDEF0123456789ABCDEF`。  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
