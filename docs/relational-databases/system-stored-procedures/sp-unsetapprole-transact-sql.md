---
title: sp_unsetapprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 65fe8e1496fba4e622d63f1ce560aba4c1acfb83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022238"
---
# <a name="spunsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停用應用程式角色並還原至先前的安全性內容。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>引數  
 **@cookie**  
 指定在應用程式角色啟動時所建立的 Cookie。 Cookie 由[sp_setapprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)。 **varbinary(8000)** 。  
  
> [!NOTE]  
>  **sp_setapprole** 的 Cookie **OUTPUT** 參數目前記載成 **varbinary(8000)** ，這是正確的長度上限。 但目前的實作會傳回 **varbinary(50)** 。 應用程式應繼續保留**varbinary(8000)** ，讓應用程式能夠繼續正常運作的 cookie 傳回大小如有增加在未來的版本。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 和 1 (失敗)  
  
## <a name="remarks"></a>備註  
 應用程式角色啟動之後使用**sp_setapprole**，直到使用者從伺服器中斷連接或執行的角色會保持作用**sp_unsetapprole**。  
  
 如需應用程式角色的概觀，請參閱 <<c0> [ 應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**公開**及儲存應用程式角色啟動時的 cookie 的知識。  
  
## <a name="examples"></a>範例  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>利用 Cookie 啟動應用程式角色，然後還原為先前的內容  
 下列範例會啟動含有密碼 `Sales11` 的 `fdsd896#gfdbfdkjgh700mM` 應用程式角色，然後建立 Cookie。 範例會傳回目前的使用者名稱，並接著執行還原為原始的內容**sp_unsetapprole**。  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
