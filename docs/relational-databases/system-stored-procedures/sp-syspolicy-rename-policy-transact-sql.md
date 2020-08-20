---
description: sp_syspolicy_rename_policy (Transact-SQL)
title: sp_syspolicy_rename_policy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_TSQL
- sp_syspolicy_rename_policy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_policy
ms.assetid: ce2b07f5-23b1-4f49-8e7b-c18cf3f3d45b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 782128b1d41f94c63f4e9de22e618378c4ec6e6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481008"
---
# <a name="sp_syspolicy_rename_policy-transact-sql"></a>sp_syspolicy_rename_policy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在以原則為基礎的管理中重新命名現有的原則。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_rename_policy { [ @name = ] 'name' | [ @policy_id = ] policy_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 這是您想要重新命名的原則名稱。 *名稱* 是 **sysname**，而且如果 *policy_id* 為 Null，則必須指定。  
  
`[ @policy_id = ] policy_id` 這是您要重新命名之原則的識別碼。 *policy_id* 為 **int**，而且如果 *name* 為 Null，則必須指定。  
  
`[ @new_name = ] 'new_name'` 這是原則的新名稱。 *new_name* 為 **sysname**，而且是必要的。 不得為 NULL 或空字串。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_rename_policy。  
  
 您必須指定 *name* 或 *policy_id*的值。 兩者不得同時為 NULL。 若要取得這些值，請查詢 msdb.dbo.syspolicy_policies 系統檢視表。  
  
## <a name="permissions"></a>權限  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> [!IMPORTANT]  
>  可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體作業的原則執行。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會將名為 'Test Policy 1' 的原則重新命名為 'Test Policy 2'。  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy @name = N'Test Policy 1'  
, @new_name = N'Test Policy 2';  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
