---
title: sp_changeobjectowner (TRANSACT-SQL) |Microsoft Docs
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
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e3150cce9a4ddb4fce2dd1e7bfc6196858f63ec6
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032421"
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更目前資料庫中的物件擁有者。  
  
> [!IMPORTANT]  
>  這個預存程序只能搭配中可用的物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)或是[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)改。 **sp_changeobjectowner**變更結構描述和擁有者。 為了保留與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性，當目前擁有者和新擁有者同時擁有與資料庫使用者同名的結構描述時，這個預存程序只會變更物件擁有者。  
  
> [!IMPORTANT]  
>  新的權限需求已經加入這個預存程序中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>引數  
 [  **@objname =** ] **'***物件***'**  
 這是目前資料庫中現有資料表、檢視表、使用者定義函數或預存程序的名稱。 *物件*已**nvarchar(776)**，沒有預設值。 *物件*可以在表單中的現有物件的擁有者限定*existing_owner ***。*** 物件*如果結構描述和其擁有者具有相同的名稱。  
  
 [  **@newowner=**] **' * * * 擁有者* **'**  
 這是即將成為物件新擁有者的安全性帳戶名稱。 *擁有者*已**sysname**，沒有預設值。 *擁有者*必須是有效的資料庫使用者、 伺服器角色、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入或具有目前資料庫存取權的 Windows 群組。 如果新擁有者是一個 Windows 使用者或是沒有對應資料庫層級主體的 Windows 群組，就會建立一個資料庫使用者。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_changeobjectowner**從物件移除所有現有權限。 您必須重新套用任何您想要保留在執行後的權限**sp_changeobjectowner**。 因此，我們建議您先編寫現有權限，才能執行**sp_changeobjectowner**。 待物件擁有權變更之後，您就可以利用指令碼，重新套用權限了。 在執行之前，您必須先修改權限指令碼中的物件擁有者。  
  
 若要變更安全性實體的擁有者，請使用 ALTER AUTHORIZATION。 若要變更結構描述，請使用 ALTER SCHEMA。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定資料庫角色或成員資格，在這兩**db_ddladmin**固定的資料庫角色並**db_securityadmin**固定資料庫角色並控制物件的權限。  
  
## <a name="examples"></a>範例  
 下列範例會變更的擁有者`authors`資料表`Corporate\GeorgeW`。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
