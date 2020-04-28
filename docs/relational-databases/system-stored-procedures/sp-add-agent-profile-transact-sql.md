---
title: sp_add_agent_profile （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 24a900409ae5979c13bdbff0d67d9d2670059208
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770848"
---
# <a name="sp_add_agent_profile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  建立複寫代理程式的新設定檔。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id`這是與新插入之設定檔相關聯的識別碼。 *profile_id*是**int** ，而且是選擇性的輸出參數。 如果指定的話，這個值會設為新設定檔識別碼。  
  
`[ @profile_name = ] 'profile_name'`這是設定檔的名稱。 *profile_name*是**sysname**，沒有預設值。  
  
`[ @agent_type = ] 'agent_type'`這是複寫代理程式的類型。 *agent_type*為**int**，沒有預設值，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式|  
|**2**|記錄讀取器代理程式|  
|**3**|散發代理程式|  
|**4**|合併代理程式|  
|**9**|佇列讀取器代理程式|  
  
`[ @profile_type = ] profile_type`這是設定檔的類型。*profile_type*是**int**，預設值是**1**。  
  
 **0**表示系統設定檔。 **1**表示自訂設定檔。 您只能使用這個預存程式來建立自訂設定檔;因此，唯一有效的值為**1**。 只[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會建立系統設定檔。  
  
`[ @description = ] 'description'`這是設定檔的描述。 *描述*是**Nvarchar （3000）**，沒有預設值。  
  
`[ @default = ] default`指出設定檔是否為*agent_type * ** 的預設值。 *預設值*是**bit**，預設值是**0**。 **1**表示要加入的設定檔會成為*agent_type*所指定之代理程式的新預設設定檔。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_add_agent_profile**用於快照式複寫、異動複寫和合併式複寫中。  
  
 自訂代理程式設定檔會隨著預設代理程式參數值而一併加入。 使用[sp_change_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)來變更這些預設值，或[sp_add_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)新增其他參數。  
  
 執行**sp_add_agent_profile**時，會在[MSagent_profiles &#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)資料表中加入新自訂設定檔的資料列，並將此設定檔的相關聯預設參數加入至[MSagent_parameters &#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)資料表。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_add_agent_profile**。  
  
## <a name="see-also"></a>另請參閱  
 [使用複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
