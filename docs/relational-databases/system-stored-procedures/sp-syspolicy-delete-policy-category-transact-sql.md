---
title: sp_syspolicy_delete_policy_category (TRANSACT-SQL) |Microsoft Docs
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
- sp_syspolicy_delete_policy_category_TSQL
- sp_syspolicy_delete_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_category
ms.assetid: e09d0d50-94d5-48fd-b284-445ddea6dfcd
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7b4c8fb9dcac2487dec7f6ece96556cc5705ea13
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032855"
---
# <a name="spsyspolicydeletepolicycategory-transact-sql"></a>sp_syspolicy_delete_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在原則式管理中刪除原則類別目錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_delete_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
```  
  
## <a name="arguments"></a>引數  
 [ **@name=** ] **'***name***'**  
 這是原則類別目錄的名稱。 *名稱*已**sysname**，而且必須指定如果*policy_category_id&lt*是 NULL。  
  
 [ **@policy_category_id=** ] *policy_category_id*  
 這是原則類別目錄的識別碼。 *policy_category_id&lt*已**int**，而且必須指定如果*名稱*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_delete_policy_category。  
  
 您必須指定的值*名稱*若是*policy_category_id&lt*。 兩者不得同時為 NULL。 若要取得這些值，請查詢 msdb.dbo.syspolicy_policy_categories 系統檢視表。  
  
 若要刪除原則類別目錄，此類別目錄不得由任何原則所參考。  
  
## <a name="permissions"></a>Permissions  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> [!IMPORTANT]  
>  可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體作業的原則執行。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會刪除名稱為 'Finance' 的原則類別目錄。  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_category @name = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)  
  
  
