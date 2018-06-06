---
title: sp_syspolicy_add_policy_category_subscription (TRANSACT-SQL) |Microsoft 文件
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
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c3e5f4079a75fca4112da1185a941b3a77e6b85
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicyaddpolicycategorysubscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將原則類別目錄訂閱新增到指定的資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@target_type=** ] **'***target_type***'**  
 這是類別目錄訂閱的目標類型。 *target_type*是**sysname**是必要的且必須設定為 'DATABASE'。  
  
 [ **@target_object=** ] **'***target_object***'**  
 會將訂閱類別目錄資料庫的名稱。 *target_object*是**sysname**，而且需要。  
  
 [ **@policy_category=** ] **'***policy_category***'**  
 是要訂閱的原則類別目錄的名稱。 *policy_category*是**sysname**，而且需要。  
  
 若要取得的值*policy_category*，查詢 msdb.dbo.syspolicy_policy_categories 系統檢視表。  
  
 [ **@policy_category_subscription_id=** ] *policy_category_subscription_id*  
 這是類別目錄訂閱的識別碼。 *policy_category_subscription_id*是**int**，而且會當做 OUTPUT 傳回。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_add_policy_category_subscription。  
  
 如果您指定不存在的原則類別目錄，就會建立新的原則類別目錄，而且當您執行此預存程序時，所有資料庫都會託管此訂閱。 如果您之後針對新的類別目錄清除託管的訂閱，只會針對您指定為 *target_object* 的資料庫來套用此訂閱。 如需如何變更授權之訂閱設定的詳細資訊，請參閱 [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 此預存程序會在目前預存程序擁有者的內容中執行。  
  
## <a name="examples"></a>範例  
 下列範例會設定指定的資料庫來訂閱名為 'Table Naming Policies' 的原則類別目錄。  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [原則式管理預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
