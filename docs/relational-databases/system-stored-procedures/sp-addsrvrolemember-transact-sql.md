---
description: sp_addsrvrolemember (Transact-SQL)
title: sp_addsrvrolemember (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec0b94d4423574729d4c92d869a73d04673edac8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536733"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  加入一個登入，做為固定伺服器角色的成員。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>引數  
 [ @loginame **=** ] **'**_login_**'**  
 這是加入至固定伺服器角色的登入名稱。 *login* 是 **sysname**，沒有預設值。 *登* 入可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 Windows 登入。 如果 Windows 登入尚未獲得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權，會自動授與其存取權。  
  
 [ @rolename **=** ] **'**_role_**'**  
 這是要加入登入的固定伺服器角色名稱。 *role* 是 **sysname**，預設值是 Null，而且必須是下列其中一個值：  
  
-   系統管理員 (sysadmin)  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 將登入加入至固定伺服器角色時，登入可取得與該角色相關聯的權限。  
  
 sa 登入和 public 的角色成員資格不能變更。  
  
 請使用 sp_addrolemember 在固定資料庫角色或使用者自訂角色中加入一個成員。  
  
 sp_addsrvrolemember 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要加入新成員之角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將 Windows 登入加入 `Corporate\HelenS` 至 `sysadmin` 固定伺服器角色。  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
