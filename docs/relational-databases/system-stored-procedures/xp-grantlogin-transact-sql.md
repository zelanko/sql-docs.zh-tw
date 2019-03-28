---
title: xp_grantlogin (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c6a6e31b4dc36e0f280dfb03d8eadf09a7d4ff7c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534860"
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權授與 Windows 群組或使用者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login'` 是要新增的 Windows 使用者或群組的名稱。 Windows 使用者或群組必須在表單中的 Windows 網域名稱限定*網域*\\*使用者*。 *登入*已**sysname**，沒有預設值。  
  
`[ @logintype = ] 'logintype'` 登入的安全性層級正在授與存取權。 *logintype*已**varchar(5)**，預設值是 NULL。 只有**admin**可以指定。 如果**系統管理員**指定，則*登入*授與存取權[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並新增成員的身分**sysadmin**固定的伺服器角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **xp_grantlogin**現在系統預存程序，而不是擴充預存程序。 **xp_grantlogin**呼叫**sp_grantlogin**並**sp_addsrvrolemember**。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**securityadmin**固定的伺服器角色。 變更時*logintype*，需要的成員資格**sysadmin**固定的伺服器角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
