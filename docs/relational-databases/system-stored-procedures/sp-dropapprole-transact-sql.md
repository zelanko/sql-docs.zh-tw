---
title: sp_dropapprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropapprole_TSQL
- sp_dropapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropapprole
ms.assetid: ea1aefe6-8f7d-46e9-a3cb-7b037b393e73
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 56752702ef62ad4afae65bf2a935757e72c189d8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047203"
---
# <a name="spdropapprole-transact-sql"></a>sp_dropapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除應用程式角色。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP APPLICATION ROLE](../../t-sql/statements/drop-application-role-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropapprole [@rolename = ] 'role'  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是要移除的應用程式角色。 *角色*已**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_dropapprole**只可用來移除應用程式角色。 如果角色擁有任何安全性實體，則無法卸除該角色。 在卸除擁有安全性實體的應用程式角色之前，必須先傳送或卸除安全性實體的擁有權。  
  
 **sp_dropapprole**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除 `SalesApp` 應用程式角色。  
  
```  
EXEC sp_dropapprole 'SalesApp';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addapprole &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_changeobjectowner &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md)   
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
