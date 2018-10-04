---
title: syspolicy_policy_categories (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: afe9eacb2f5e42dc945505d54e420877a8f4cbca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646496"
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，針對每一個以原則為基礎的管理原則類別目錄各顯示一個資料列。 原則類別目錄可協助您組織原則，當您有多個原則。 下表描述 syspolicy_policy_groups 檢視表中的資料行。  
 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|原則類別目錄的識別碼。|  
|NAME|**sysname**|原則類別目錄的名稱。|  
|mandate_database_subscriptions|**bit**|指出原則類別目錄是否會套用到執行個體內的所有資料庫而不需要明確訂閱 (1)，或是原則類別目錄是否必須使用明確訂閱 (0) 套用到資料庫。|  
  
## <a name="remarks"></a>備註  
 顯示以原則為基礎的管理原則群組清單。  
  
## <a name="permissions"></a>Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
