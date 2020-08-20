---
description: sp_addlogin (Transact-SQL)
title: sp_addlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 585461904b68f26d3ea71e255b24e9ed6d38786a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474553"
---
# <a name="sp_addlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  建立一項新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，讓使用者利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
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
 [ @loginame =] '*login*'  
 這是登入的名稱。 *login* 是 **sysname**，沒有預設值。  
  
 [ @passwd =] '*password*'  
 這是登入密碼。 *password* 是 **sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb =] '*資料庫*'  
 這是登入的預設資料庫 (在登入之後，登入第一次連接的資料庫)。 *資料庫* 是 **sysname**，預設值是 **master**。  
  
 [ @deflanguage =] '*language*'  
 這是登入的預設語言。 *language* 是 **sysname**，預設值是 Null。 如果未指定 *language* ，新登入的預設 *語言* 會設為伺服器的目前預設語言。  
  
 [ @sid =] '*sid*'  
 這是安全性識別碼 (SID)。 *sid* 是 **Varbinary (16) **，預設值是 Null。 如果 *sid* 為 Null，系統會產生新登入的 sid。 儘管使用 **Varbinary** 資料類型，Null 以外的值的長度必須剛好為16個位元組，且不能已經存在。 例如*sid* ，當您撰寫腳本或將登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從某個伺服器移至另一部伺服器，而且您想要讓登入在不同的伺服器上具有相同的 sid 時，指定 sid 會很有用。  
  
 [ @encryptopt =] '*encryption_option*'  
 指定以明碼方式傳遞密碼，或以純文字密碼的雜湊來傳遞密碼。 請注意，這裡並不進行任何加密。 這項討論用到 "encrypt" 一字，是為了與舊版相容。 如果傳入純文字密碼，就會雜湊這個密碼。 這項雜湊會儲存起來。 *encryption_option* 是 **Varchar (20) **，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|NULL|傳遞純文字密碼。 這是預設值。|  
|**skip_encryption**|密碼已雜湊。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該直接儲存這個值，不需要重新雜湊。|  
|**skip_encryption_old**|提供的密碼是由舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所雜湊的。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該直接儲存這個值，不需要重新雜湊。 這個選項專用來升級。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入可以包含 1 到 128 個字元，其中包括字母、符號和數字。 登入不能包含反斜線 (\\) ; 必須是保留的登入名稱（例如 sa 或 public）或已存在; 或者為 Null 或 () 的空字串 `''` 。  
  
 如果提供了預設資料庫的名稱，您可以直接連接到指定的資料庫，不需要執行 USE 陳述式。 不過，在您使用 [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) 或 [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) 或 [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)取得資料庫擁有者 (存取該資料庫之前，您無法使用預設資料庫。  
  
 SID 號碼是在伺服器中用來唯一識別登入的 GUID。  
  
 變更伺服器的預設語言並不會變更現有登入的預設語言。 若要變更伺服器的預設語言，請使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 如果在將登入加入至時，密碼已雜湊，則使用 **skip_encryption** 隱藏密碼雜湊會很有用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果已使用舊版來雜湊密碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請使用 **skip_encryption_old**。  
  
 sp_addlogin 無法在使用者自訂交易內執行。  
  
 下表顯示搭配 sp_addlogin 使用的數個預存程序。  
  
|預存程序|描述|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|加入 Windows 使用者或群組。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|變更使用者的密碼。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|變更使用者的預設資料庫。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|變更使用者的預設語言。|  
  
## <a name="permissions"></a>權限  
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
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
