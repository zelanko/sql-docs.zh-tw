---
title: sp_help_agent_default （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57b3016f0f5ee9f58e41ce6993af69c33aa3b742
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827749"
---
# <a name="sp_help_agent_default-transact-sql"></a>sp_help_agent_default (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  擷取作為參數來傳遞的代理程式類型之預設組態的識別碼。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] _profile_idOUTPUT`這是代理程式類型的預設設定識別碼。 *profile_id*是**int**，沒有預設值。*profile_id*也是輸出參數，並會傳回代理程式類型的預設設定識別碼。  
  
`[ @agent_type = ] 'agent_type'`這是代理程式的類型。 *agent_type*為**int**，沒有預設值，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|快照集代理程式。|  
|**2**|記錄讀取器代理程式。|  
|**3**|散發代理程式。|  
|**4**|合併代理程式。|  
|**9**|佇列讀取器代理程式|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_agent_default**用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**replmonitor**固定資料庫角色的成員，才能夠執行**sp_help_agent_default**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
