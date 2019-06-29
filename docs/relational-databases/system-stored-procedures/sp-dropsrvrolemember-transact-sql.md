---
title: sp_dropsrvrolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 2624ed4800a247b0847adc5839346758aa50f140
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463568"
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

從固定伺服器角色移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 Windows 使用者或群組。

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)改。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>語法

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>引數

**[ @loginame = ]** '_login_'  
這是要從固定伺服器角色中移除的登入名稱。 *登入*已**sysname**，沒有預設值。 *登入*必須存在。  

**[ @rolename = ]** '_role_'  
這是伺服器角色的名稱。 *角色*已**sysname**，預設值是 NULL。 *角色*必須是下列值之一：  

-   sysadmin  
  
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
 只有 sp_dropsrvrolemember 可用來從固定的伺服器角色移除登入。 您可以使用 sp_droprolemember 來移除資料庫角色的成員。  
  
 無法從固定的伺服器角色中移除 sa 登入。  
  
 sp_dropsrvrolemember 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要 sysadmin 固定伺服器角色或這兩個 ALTER ANY LOGIN 權限的伺服器和從中成員正在卸除的角色的成員資格的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 `JackO` 固定伺服器角色移除登入 `sysadmin`。  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
