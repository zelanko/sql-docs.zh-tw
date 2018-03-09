---
title: "xp_grantlogin (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb35af7a2de8fae7d227ea146d2578a73e5c6c28
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權授與 Windows 群組或使用者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame =** ] **'***登入***'**  
 這是您要加入的 Windows 使用者或群組名稱。 Windows 使用者或群組必須在表單中的 Windows 網域名稱限定*網域*\\*使用者*。 *登入*是**sysname**，沒有預設值。  
  
 [  **@logintype =** ] **'***logintype***'**  
 這是要被授與存取權之登入的安全性層級。 *logintype*是**varchar(5)**，預設值是 NULL。 只有**admin**可以指定。 如果**admin**指定，則*登入*授與存取權[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並加入成員的身分**sysadmin**固定的伺服器角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **xp_grantlogin**現在系統預存程序，而不是擴充預存程序。 **xp_grantlogin**呼叫**sp_grantlogin**和**sp_addsrvrolemember**。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**securityadmin**固定的伺服器角色。 變更時*logintype*，需要的成員資格**sysadmin**固定的伺服器角色。  
  
## <a name="see-also"></a>請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
