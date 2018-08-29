---
title: sp_defaultlanguage (TRANSACT-SQL) |Microsoft Docs
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
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a920323efff6126a2afb5c2c88dde4fe69501103
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036081"
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的預設語言。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@loginame =** ] **'***login***'**  
 這是登入名稱。 *登入*已**sysname**，沒有預設值。 *登入*可以是現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 使用者或群組。  
  
 [  **@language =** ] **'***語言***'**  
 這是登入的預設語言。 *語言*已**sysname**，預設值是 NULL。 *語言*必須是有效的語言，在伺服器上。 如果*語言*未指定，則*語言*設定為伺服器的預設語言; 預設語言由定義**sp_configure**組態變數**預設語言**。 變更伺服器的預設語言，並不會變更現有登入的預設語言。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_defaultlanguage**呼叫 ALTER LOGIN，它支援其他選項。 如需變更其他登入的預設值的詳細資訊，請參閱 < [ALTER LOGIN &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)。  
  
 請使用 SET LANGUAGE 陳述式來變更目前工作階段的語言。 使用 @@LANGUAGE函式來顯示目前的語言設定。  
  
 如果登入的預設語言已從伺服器卸除，該登入便會取得伺服器的預設語言。 **sp_defaultlanguage**無法在使用者自訂交易內執行。  
  
 在伺服器上安裝的語言的相關資訊會顯示在**sys.syslanguages**目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
 下列範例會利用 `ALTER LOGIN`，將登入 `Fathima` 的預設語言改成「阿拉伯文」。 這是慣用的方法。  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.syslanguages &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
