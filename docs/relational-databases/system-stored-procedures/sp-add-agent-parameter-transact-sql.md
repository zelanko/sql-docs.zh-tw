---
title: sp_add_agent_parameter (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- sp_add_agent_parameter_TSQL
- sp_add_agent_parameter
helpviewer_keywords:
- sp_add_agent_parameter
ms.assetid: 055f4765-0574-47c3-bf7d-6ef6e9bd8b34
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: efcfb48b6c39bc65c3e281baea01d8f4fe3fd1ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddagentparameter-transact-sql"></a>sp_add_agent_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的參數及其值加入代理程式設定檔中。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_agent_parameter [ @profile_id = ] profile_id  
        , [ @parameter_name = ] 'parameter_name'   
        , [ @parameter_value = ] 'parameter_value'   
```  
  
## <a name="arguments"></a>引數  
 [  **@profile_id=** ] *profile_id*  
 已從設定檔識別碼**MSagent_profiles**資料表中**msdb**資料庫。 *profile_id*是**int**，沒有預設值。  
  
 若要找出哪一個代理程式中輸入下列命令*profile_id*表示，尋找*profile_id*中[MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)資料表，並記下*agent_type*欄位值。 其值如下：  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式|  
|**2**|記錄讀取器代理程式|  
|**3**|散發代理程式|  
|**4**|合併代理程式|  
|**9**|佇列讀取器代理程式|  
  
 [  **@parameter_name=** ] **'***parameter_name***'**  
 這是參數的名稱。 *parameter_name*是**sysname**，沒有預設值。 已定義系統設定檔中的參數清單，請參閱[Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)。 如需每個代理程式完整的有效參數清單，請參閱下列主題：  
  
-   [複寫快照集代理程式](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [複寫佇列讀取器代理程式](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 [  **@parameter_value=**] **'***parameter_value***'**  
 這是指派給參數的值。 *parameter_value*是**nvarchar （255)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_add_agent_parameter**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_agent_parameter**。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
