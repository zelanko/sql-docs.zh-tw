---
description: sp_unsetapprole (Transact-SQL)
title: sp_unsetapprole (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 03535e2aa88b0387f0d475531576034135ad142b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492883"
---
# <a name="sp_unsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  停用應用程式角色並還原至先前的安全性內容。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>引數  
 **\@餅乾**  
 指定在應用程式角色啟動時所建立的 Cookie。 Cookie 是由 [sp_setapprole &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)所建立。 **Varbinary (8000) **。  
  
> [!NOTE]  
>  **sp_setapprole** 的 Cookie **OUTPUT** 參數目前記載成 **varbinary(8000)** ，這是正確的長度上限。 但目前的實作會傳回 **varbinary(50)** 。 應用程式應繼續保留 **Varbinary (8000) ** ，以便在未來版本中的 cookie 傳回大小增加時，讓應用程式繼續正常運作。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 和 1 (失敗)  
  
## <a name="remarks"></a>備註  
 使用 **sp_setapprole**啟動應用程式角色之後，角色會保持作用中，直到使用者中斷與伺服器的連線或執行 **sp_unsetapprole**為止。  
  
 如需應用程式角色的總覽，請參閱 [應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
## <a name="permissions"></a>權限  
 需要 **公開** 的成員資格，以及啟用應用程式角色時所儲存之 cookie 的知識。  
  
## <a name="examples"></a>範例  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>利用 Cookie 啟動應用程式角色，然後還原為先前的內容  
 下列範例會啟動含有密碼 `Sales11` 的 `fdsd896#gfdbfdkjgh700mM` 應用程式角色，然後建立 Cookie。 此範例會傳回目前使用者的名稱，然後藉由執行 **sp_unsetapprole**來還原為原始內容。  
  
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
 [sp_setapprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性預存程式 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
