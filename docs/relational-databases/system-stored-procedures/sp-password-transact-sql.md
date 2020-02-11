---
title: sp_password （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c02b9327dbff75e3c0816bb3eec19e3cb3135d50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008915"
---
# <a name="sp_password-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  加入或變更[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入的密碼。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @old = ] 'old_password'`這是舊密碼。 *old_password*是**sysname**，預設值是 Null。  
  
`[ @new = ] 'new_password'`這是新的密碼。 *new_password*是**sysname**，沒有預設值。 如果未使用具名引數，則必須指定*old_password* 。  
  
> [!IMPORTANT]  
>  請勿使用 NULL 密碼。 請使用增強式密碼。 如需詳細資訊，請參閱 [增強式密碼](../../relational-databases/security/strong-passwords.md)。  
  
`[ @loginame = ] 'login'`這是受到密碼變更影響的登入名稱。 *login*是**sysname**，預設值是 Null。 *登*入必須已經存在，而且只能由**sysadmin**或**securityadmin**固定伺服器角色的成員來指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_password**會呼叫 ALTER LOGIN。 這個陳述式支援其他選項。 如需變更密碼的詳細資訊，請參閱[ALTER LOGIN &#40;transact-sql&#41;](../../t-sql/statements/alter-login-transact-sql.md)。  
  
 **sp_password**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
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
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [建立登入 &#40;Transact-sql&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
