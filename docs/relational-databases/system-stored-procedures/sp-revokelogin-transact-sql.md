---
title: sp_revokelogin (TRANSACT-SQL) |Microsoft Docs
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
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a7a6d791b8e8115a2b62b99d526962f59a995871
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036163"
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除登入項目，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 使用者或群組使用 CREATE LOGIN、 建立**sp_grantlogin**，或**sp_denylogin**。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame=**] **'***登入***'**  
 這是 Windows 使用者或群組的名稱。 *登入*已**sysname**，沒有預設值。 *登入*可以是任何現有的 Windows 使用者名稱或群組形式*電腦名稱*\\*使用者或網域*\\*使用者*。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_revokelogin**停用使用所指定的帳戶連線*登入*參數。 但是在撤銷其個別存取權之後，透過 Windows 群組成員資格獲得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體存取權的 Windows 使用者仍然可以用群組方式進行連接。 同樣地，如果*登入*參數指定 Windows 群組的名稱，該群組成員的個別授與存取權的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]仍然可以連接。  
  
 比方說，如果 Windows 使用者**ADVWORKS\john**是 Windows 群組的成員**ADVWORKS\Admins**，並**sp_revokelogin**撤銷的存取權`ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 使用者**ADVWORKS\john**仍然可以連接，如果**ADVWORKS\Admins**已授與存取權的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 同樣地，如果 Windows 群組**ADVWORKS\Admins**撤銷存取權，但**ADVWORKS\john**授與存取權， **ADVWORKS\john**仍然可以連接。  
  
 使用**sp_denylogin**明確防止使用者連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不論其 Windows 群組成員資格。  
  
 **sp_revokelogin**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
 下列範例會移除 Windows 使用者的登入項目`Corporate\MollyA`。  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 或  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
