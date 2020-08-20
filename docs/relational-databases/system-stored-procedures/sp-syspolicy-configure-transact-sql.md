---
description: sp_syspolicy_configure (Transact-SQL)
title: sp_syspolicy_configure (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 820952e0829014efc3669759dabf5d1dfc208d91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473574"
---
# <a name="sp_syspolicy_configure-transact-sql"></a>sp_syspolicy_configure (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  設定以原則為基礎的管理設定，例如是否啟用以原則為基礎的管理。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 這是您想要設定的設定名稱。 *名稱* 是 **sysname**，是必要的，而且不可以是 Null 或空字串。  
  
 *名稱* 可以是下列任何一個值：  
  
-   'Enabled' - 判斷是否啟用以原則為基礎的管理。  
  
-   'HistoryRetentionInDays' - 指定原則評估記錄應保留的天數。 如果設定為 0，將不會自動移除記錄。  
  
-   'LogOnSuccess' - 指定以原則為基礎的管理是否會記錄成功的原則評估。  
  
`[ @value = ] value` 這是與指定的 *名稱*值相關聯的值。 *值* 為 **SQL_variant**，且為必要項。  
  
-   如果您為 [ *名稱*] 指定 [Enabled]，您可以使用下列其中一個值：  
  
    -   0 = 停用以原則為基礎的管理  
  
    -   1 = 啟用以原則為基礎的管理  
  
-   如果您為 [ *名稱*] 指定 ' HistoryRententionInDays '，請將天數指定為整數值。  
  
-   如果您為 *名稱*指定 ' LogOnSuccess '，您可以使用下列其中一個值：  
  
    -   0 = 只記錄失敗的原則評估。  
  
    -   1 = 成功和失敗的原則評估都會記錄。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_configure。  
  
 若要檢視這些設定的目前值，請查詢 msdb.dbo.syspolicy_configuration 系統檢視表。  
  
## <a name="permissions"></a>權限  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> [!IMPORTANT]  
>  可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體作業的原則執行。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會啟用以原則為基礎的管理。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 以下範例將原則記錄保留設為 14 天。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 下列範例會設定以原則為基礎的管理，以便將成功和失敗的原則評估都記錄下來。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
