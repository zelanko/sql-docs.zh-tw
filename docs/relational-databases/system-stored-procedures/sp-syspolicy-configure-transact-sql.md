---
title: "sp_syspolicy_configure (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40f59b534e794eec407cbfd96f4982bb219864dd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spsyspolicyconfigure-transact-sql"></a>sp_syspolicy_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定以原則為基礎的管理設定，例如是否啟用以原則為基礎的管理。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>引數  
 [  **@name =** ] **'***名稱***'**  
 這是您想要設定的設定名稱。 *名稱*是**sysname**是必要的且不可為 NULL 或空字串。  
  
 *名稱*可以是下列值之一：  
  
-   'Enabled' - 判斷是否啟用以原則為基礎的管理。  
  
-   'HistoryRetentionInDays' - 指定原則評估記錄應保留的天數。 如果設定為 0，將不會自動移除記錄。  
  
-   'LogOnSuccess' - 指定以原則為基礎的管理是否會記錄成功的原則評估。  
  
 [  **@value =** ]*值*  
 指定的值相關聯的值*名稱*。 *值*是**sql_variant**，而且需要。  
  
-   如果您指定 'Enabled'*名稱*，您可以使用下列值之一：  
  
    -   0 = 停用以原則為基礎的管理  
  
    -   1 = 啟用以原則為基礎的管理  
  
-   如果您指定 'HistoryRententionInDays'*名稱*，成為整數值中指定的天數。  
  
-   如果您指定 'LogOnSuccess'*名稱*，您可以使用下列值之一：  
  
    -   0 = 只記錄失敗的原則評估。  
  
    -   1 = 成功和失敗的原則評估都會記錄。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_configure。  
  
 若要檢視這些設定的目前值，請查詢 msdb.dbo.syspolicy_configuration 系統檢視表。  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>請參閱＜  
 [以原則為基礎的管理預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
