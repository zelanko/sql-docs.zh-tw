---
title: "sp_approlepassword (TRANSACT-SQL) |Microsoft 文件"
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
- sp_approlepassword
- sp_approlepassword_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_approlepassword
ms.assetid: 7967dc0b-bee2-4c63-b8e9-1c3ce2f5db2a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6456a0fa5330b2c6ef921dec959f9cc9fb6f07b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spapprolepassword-transact-sql"></a>sp_approlepassword (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更目前資料庫中應用程式角色的密碼。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER APPLICATION ROLE](../../t-sql/statements/alter-application-role-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_approlepassword [ @rolename= ] 'role' , [ @newpwd = ] 'password'   
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是應用程式角色的名稱。 *角色*是**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫。  
  
 [  **@newpwd =** ] **'***密碼***'**  
 這是應用程式角色的新密碼。 *密碼*是**sysname**，沒有預設值。 *密碼*不能是 NULL。  
  
> [!IMPORTANT]  
>  請勿使用 NULL 密碼。 請使用增強式密碼。 如需詳細資訊，請參閱 [Strong Passwords](../../relational-databases/security/strong-passwords.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_approlepassword**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將 `PayrollAppRole` 應用程式角色的密碼設為 `B3r12-36`。  
  
```  
EXEC sp_approlepassword 'PayrollAppRole', '''B3r12-36';  
```  
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_addapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_setapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
