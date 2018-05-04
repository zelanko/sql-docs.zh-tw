---
title: sp_password (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7aadc50a6a57a7880fa8aed9ad498d713090c009
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sppassword-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  加入或變更的密碼[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@old=** ] **'***old_password***'**  
 這是舊密碼。 *old_password*是**sysname**，預設值是 NULL。  
  
 [  **@new=** ] **'***new_password***'**  
 這是新密碼。 *new_password*是**sysname**，沒有預設值。 *old_password*必須指定是否沒有使用具名的參數。  
  
> [!IMPORTANT]  
>  請勿使用 NULL 密碼。 請使用增強式密碼。 如需詳細資訊，請參閱 [Strong Passwords](../../relational-databases/security/strong-passwords.md)。  
  
 [  **@loginame=** ] **'***登入***'**  
 這是受到密碼變更影響的登入名稱。 *login* 是預設值為 NULL 的 **sysname**。 *登入*必須存在，而且可以指定的成員只能由**sysadmin**或**securityadmin**固定伺服器角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_password**呼叫 ALTER LOGIN。 這個陳述式支援其他選項。 如需變更密碼資訊，請參閱[ALTER LOGIN &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)。  
  
 **sp_password**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 權限。 若要在不提供舊密碼的情況下重設密碼，或是被變更的登入具有 CONTROL SERVER 權限，則也需要 CONTROL SERVER 權限。  
  
 主體可以變更本身的密碼。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. 在不知道舊密碼的情況下變更登入密碼  
 下列範例會顯示如何使用 `ALTER LOGIN` 將登入 `Victoria` 的密碼變更為 `B3r1000d#2-36`。 這是慣用的方法。 執行這個命令的使用者必須具有 CONTROL SERVER 權限。  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. 變更密碼  
 下列範例會顯示如何使用 `ALTER LOGIN` 將登入 `Victoria` 的密碼從 `B3r1000d#2-36` 變更為 `V1cteAmanti55imE`。 這是慣用的方法。 使用者 `Victoria` 不需要其他權限就可以執行這個命令。 其他使用者需要 ALTER ANY LOGIN 權限。  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
