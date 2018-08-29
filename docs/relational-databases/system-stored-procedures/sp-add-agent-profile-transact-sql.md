---
title: sp_add_agent_profile & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b4d69bc8803bf7c5b6b5b2d0e674c7513d5d9fae
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036644"
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@profile_id=** ] *profile_id*  
 這是與新插入之設定檔相關聯的識別碼。 *profile_id*已**int**是選擇性的 OUTPUT 參數。 如果指定的話，這個值會設為新設定檔識別碼。  
  
 [  **@profile_name=** ] **'***profile_name***'**  
 這是設定檔的名稱。 *profile_name*已**sysname**，沒有預設值。  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 這是複寫代理程式的類型。 *agent_type*已**int**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式|  
|**2**|記錄讀取器代理程式|  
|**3**|散發代理程式|  
|**4**|[合併代理程式]|  
|**9**|佇列讀取器代理程式|  
  
 [  **@profile_type=** ] *profile_type*  
 為設定檔的類型。*profile_type*是**int**，預設值是**1**。  
  
 **0**表示系統設定檔。 **1**表示自訂設定檔。 使用此預存程序，就可以建立自訂的設定檔因此，唯一有效的值是**1**。 只有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會建立系統設定檔。  
  
 [  **@description=** ] **'***描述***'**  
 這是設定檔的描述。 *描述*已**nvarchar(3000)**，沒有預設值。  
  
 [  **@default=** ]*預設*  
 指出設定檔是否為預設*agent_type * *。* *預設值*已**位元**，預設值是**0**。 **1**表示所加入的設定檔將成為所指定的代理程式的新預設設定檔*agent_type*。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_add_agent_profile**用於快照式複寫、 異動複寫和合併式複寫。  
  
 自訂代理程式設定檔會隨著預設代理程式參數值而一併加入。 使用[sp_change_agent_parameter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)來變更這些預設值或[sp_add_agent_parameter &#40;-&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)來新增額外的參數。  
  
 當**sp_add_agent_profile**是執行，資料列會加入新的自訂設定檔中[MSagent_profiles &#40;-&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)資料表和相關聯的預設參數，這個設定檔新增至[m &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)資料表。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_agent_profile**。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
