---
title: sp_syspolicy_update_policy_category & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_TSQL
- sp_syspolicy_update_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category
ms.assetid: 6b6413c2-7a3b-4eff-91d9-5db2011869d6
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 815e19a5a36f23173af9f674fd26cbfafb8f9287
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835746"
---
# <a name="spsyspolicyupdatepolicycategory-transact-sql"></a>sp_syspolicy_update_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新原則類別目錄是否設定為可託管資料庫訂閱。 如果可託管訂閱，原則類別目錄會套用到所有資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_update_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@name=** ] **'***name***'**  
 這是原則類別目錄的名稱。 *名稱*已**sysname**，而且必須指定如果*policy_category_id&lt*是 NULL。  
  
 [ **@policy_category_id=** ] *policy_category_id*  
 這是原則類別目錄的識別碼。 *policy_category_id&lt*已**int**，而且必須指定如果*名稱*是 NULL。  
  
 [  **@mandate_database_subscriptions=** ] *mandate_database_subscriptions*  
 判斷是否針對原則類別目錄託管資料庫訂閱。 *mandate_database_subscriptions*已**元**值，預設值是 NULL。 您可以使用下列其中一個值：  
  
-   0 = 未託管  
  
-   1 = 已託管  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_update_policy_category。  
  
 您必須針對指定的值*名稱*若是*policy_category_id&lt*。 兩者不得同時為 NULL。 若要取得這些值，請查詢 msdb.dbo.syspolicy_policy_categories 系統檢視表。  
  
## <a name="permissions"></a>Permissions  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> [!IMPORTANT]  
>  可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體作業的原則執行。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會更新 'Finance' 類別目錄來託管資料庫訂閱。  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category @name = N'Finance'  
, @mandate_database_subscriptions = 1;  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [sp_syspolicy_rename_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)  
  
  
