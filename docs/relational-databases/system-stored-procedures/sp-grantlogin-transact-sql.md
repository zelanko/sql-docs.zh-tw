---
title: "sp_grantlogin (TRANSACT-SQL) |Microsoft 文件"
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
- sp_grantlogin_TSQL
- sp_grantlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantlogin
ms.assetid: 0c873d99-c3bf-4eb1-948b-a46cb235ccd4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a28ab1b1611a2beff1bdc3c9707baa25a9cbaa89
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spgrantlogin-transact-sql"></a>sp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_grantlogin [@loginame=] 'login'  
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame =** ] **'***登入***'**  
 這是 Windows 使用者或群組的名稱。 Windows 使用者或群組必須在表單中的 Windows 網域名稱限定*網域*\\*使用者*; 例如， **London\Joeb**。 *登入*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_grantlogin**呼叫支援其他選項的 CREATE LOGIN。 如需建立 SQL Server 登入資訊，請參閱[CREATE LOGIN &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **sp_grantlogin**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用`CREATE LOGIN`建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 使用者的登入`Corporate\BobJ.`這是慣用的方法。  
  
```  
CREATE LOGIN [Corporate\BobJ] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
