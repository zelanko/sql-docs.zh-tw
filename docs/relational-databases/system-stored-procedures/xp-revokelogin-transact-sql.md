---
title: "xp_revokelogin (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- xp_revokelogin
- xp_revokelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_revokelogin
ms.assetid: b3fa7678-dba4-4537-be94-5ae63ca11f81
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60ea17a6ce82608a63f29a18b4f49ecaadf3339b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="xprevokelogin-transact-sql"></a>xp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤銷 Windows 群組或使用者對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_revokelogin {[@loginame=] 'login'}  
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame =** ] **'***登入***'**  
 這是要從中撤銷存取權之 Windows 使用者或群組的名稱。 *登入*必須包含網域名稱，例如**[ADVWKS\sylvester1]**。 *登入*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 請改用 DROP LOGIN。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="see-also"></a>請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
