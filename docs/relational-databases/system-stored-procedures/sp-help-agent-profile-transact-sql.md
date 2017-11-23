---
title: "sp_help_agent_profile (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords: sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2459e35032b90dda8056e5cf3a31d99698b36ffa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpagentprofile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示指定代理程式的設定檔。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@agent_type=**] *agent_type*  
 這是代理程式的類型。 *agent_type*是**int**，預設值是**0**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式|  
|**2**|記錄讀取器代理程式|  
|**3**|散發代理程式|  
|**4**|合併代理程式|  
|**9**|佇列讀取器代理程式|  
  
 [  **@profile_id=**] *profile_id*  
 這是要顯示的設定檔識別碼。 *profile_id*是**int**，預設值是**-1**，它會傳回中的所有設定檔**MSagent_profiles**資料表。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|設定檔的識別碼。|  
|**profile_name**|**sysname**|對代理程式類型而言是唯一的。|  
|**agent_type**|**int**|**1** = 快照集代理程式<br /><br /> **2** = 記錄讀取器代理程式<br /><br /> **3** = 散發代理程式<br /><br /> **4** = 合併代理程式<br /><br /> **9** = 佇列讀取器代理程式|  
|**型別**|**int**|**0** = 系統<br /><br /> **1** = 自訂|  
|**描述**|**varchar(3000)**|設定檔的描述。|  
|**def_profile**|**bit**|指定這個設定檔是否為這個代理程式類型的預設值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_agent_profile**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**replmonitor**固定的資料庫角色可以執行**sp_help_agent_profile**。  
  
## <a name="see-also"></a>請參閱＜  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
