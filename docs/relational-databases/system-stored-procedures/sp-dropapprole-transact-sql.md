---
title: "sp_dropapprole (TRANSACT-SQL) |Microsoft 文件"
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
- sp_dropapprole_TSQL
- sp_dropapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropapprole
ms.assetid: ea1aefe6-8f7d-46e9-a3cb-7b037b393e73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51581dbebaeb9e1ad39b4cc2792d9b628324d3e1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spdropapprole-transact-sql"></a>sp_dropapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除應用程式角色。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[DROP APPLICATION ROLE](../../t-sql/statements/drop-application-role-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropapprole [@rolename = ] 'role'  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是要移除的應用程式角色。 *角色*是**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫。  
  
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
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_changeobjectowner &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md)   
 [sp_setapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
