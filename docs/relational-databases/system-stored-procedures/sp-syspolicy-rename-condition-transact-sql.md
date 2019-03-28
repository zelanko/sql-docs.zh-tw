---
title: sp_syspolicy_rename_condition (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_condition
- sp_syspolicy_rename_condition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_condition
ms.assetid: d9f3f9b1-701b-4fce-9b42-c282656caf84
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0305e7bc2daa087483fce0472d32df0887271ba3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534600"
---
# <a name="spsyspolicyrenamecondition-transact-sql"></a>sp_syspolicy_rename_condition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在以原則為基礎的管理中重新命名現有的條件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_rename_condition { [ @name = ] 'name' | [ @condition_id = ] condition_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 是您想要重新命名之條件的名稱。 *名稱*已**sysname**，而且必須指定如果*condition_id&lt*是 NULL。  
  
`[ @condition_id = ] condition_id` 是您想要重新命名之條件的識別碼。 *condition_id&lt*已**int**，而且必須指定如果*名稱*是 NULL。  
  
`[ @new_name = ] 'new_name'` 這是條件的新名稱。 *new_name*已**sysname**，而且需要。 不得為 NULL 或空字串。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_rename_condition。  
  
 您必須針對指定的值*名稱*或是*condition_id&lt*。 兩者不得同時為 NULL。 若要取得這些值，請查詢 msdb.dbo.syspolicy_conditions 系統檢視表。  
  
## <a name="permissions"></a>Permissions  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> [!IMPORTANT]  
>  可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響作業的執行個體的原則執行[!INCLUDE[ssDE](../../includes/ssde-md.md)]。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會重新命名原來名稱為 'Change Tracking Enabled' 的條件。  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_condition @name = N'Change Tracking Enabled'  
, @new_name = N'Verify Change Tracking Enabled';  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
