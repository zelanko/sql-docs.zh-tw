---
description: sp_grantlogin (Transact-SQL)
title: sp_grantlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantlogin_TSQL
- sp_grantlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantlogin
ms.assetid: 0c873d99-c3bf-4eb1-948b-a46cb235ccd4
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: ddca7a999c1095bc1f6da91e62bd675c736dd96b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447062"
---
# <a name="sp_grantlogin-transact-sql"></a>sp_grantlogin (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_grantlogin [@loginame=] 'login'  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login'` 這是 Windows 使用者或群組的名稱。 Windows 使用者或群組必須以*網域*使用者格式的 windows 功能變數名稱限定 \\ * *，例如， **London\Joeb**。 *login* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_grantlogin** 會呼叫建立登入，以支援其他選項。 如需建立 SQL Server 登入的詳細資訊，請參閱 [CREATE LOGIN &#40;transact-sql&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **sp_grantlogin** 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `CREATE LOGIN` 來建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 使用者的登入 `Corporate\BobJ.` 。這是慣用的方法。  
  
```sql
CREATE LOGIN [Corporate\BobJ] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
