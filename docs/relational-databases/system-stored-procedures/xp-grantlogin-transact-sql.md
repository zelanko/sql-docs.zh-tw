---
description: xp_grantlogin (Transact-SQL)
title: xp_grantlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 185532cdcade18b6902fe1c3e8d1c8ab3eb568b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419262"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權授與 Windows 群組或使用者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login'` 這是要加入之 Windows 使用者或群組的名稱。 Windows 使用者或群組必須以*網域*使用者格式的 windows 功能變數名稱加以限定 \\ * *。 *login* 是 **sysname**，沒有預設值。  
  
`[ @logintype = ] 'logintype'` 這是授與存取權之登入的安全性層級。 *logintype* 是 **Varchar (5) **，預設值是 Null。 只有系統 **管理員** 可以指定。 如果指定了 **admin** ， *登* 入就會被授與存取權， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並加入成為 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **xp_grantlogin** 現在是系統預存程式，而不是擴充預存程式。 **xp_grantlogin** 呼叫 **sp_grantlogin** 和 **sp_addsrvrolemember**。  
  
## <a name="permissions"></a>權限  
 需要 **securityadmin** 固定伺服器角色中的成員資格。 變更 *logintype*時，需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的一般擴充預存程式 ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
