---
title: sp_help_agent_profile & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 737c65e0b8e2e089eed21225dfaa9d127a0fc349
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781506"
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
 這是代理程式的類型。 *agent_type*已**int**，預設值是**0**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式|  
|**2**|記錄讀取器代理程式|  
|**3**|散發代理程式|  
|**4**|[合併代理程式]|  
|**9**|佇列讀取器代理程式|  
  
 [  **@profile_id=**] *profile_id*  
 這是要顯示的設定檔識別碼。 *profile_id*已**int**，預設值是 **-1**，它會傳回中的所有設定檔**MSagent_profiles**資料表。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|設定檔的識別碼。|  
|**profile_name**|**sysname**|對代理程式類型而言是唯一的。|  
|**agent_type**|**int**|**1** = 快照集代理程式<br /><br /> **2** = 記錄讀取器代理程式<br /><br /> **3** = 散發代理程式<br /><br /> **4** = 合併代理程式<br /><br /> **9** = 佇列讀取器代理程式|  
|**型別**|**int**|**0** = 系統<br /><br /> **1** = 自訂|  
|**description**|**varchar(3000)**|設定檔的描述。|  
|**def_profile**|**bit**|指定這個設定檔是否為這個代理程式類型的預設值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_agent_profile**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**replmonitor**固定的資料庫角色可以執行**sp_help_agent_profile**。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
