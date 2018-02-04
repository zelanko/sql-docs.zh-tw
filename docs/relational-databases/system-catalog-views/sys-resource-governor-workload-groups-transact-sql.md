---
title: "sys.resource_governor_workload_groups (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2bc9e45c38c8dbe50d9bd7c5d6a8c79203c4fed
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中儲存的工作負載群組組態。 每個工作負載群組都可以訂閱一個資源集區，而且只能訂閱一個資源集區。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|工作負載群組的唯一識別碼。 不可為 Null。|  
|name|**sysname**|工作負載群組的名稱。 不可為 Null。|  
|importance|**sysname**|**注意：**重要性僅適用於相同的資源集區中的工作負載群組。<br /><br /> 要求在此工作負載群組中的相對重要性。 重要性為下列其中之一，「 中 」 的預設值： 低、 中度高。<br /><br /> 不可為 Null。|  
|request_max_memory_grant_percent|**int**|針對單一要求授與的最大記憶體 (以百分比為單位)。 預設值為 25。 不可為 Null。<br /><br /> **注意：**如果此設定高於 50%，大型查詢將會執行一次。 因此，查詢執行時，發生記憶體不足之錯誤的風險比較大。|  
|request_max_cpu_time_sec|**int**|單一要求的最大 CPU 使用限制 (以秒為單位)。 預設值為 0 時，不會指定任何限制。 不可為 Null。<br /><br /> **注意：**如需詳細資訊，請參閱[CPU Threshold Exceeded Event Class<](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。|  
|request_memory_grant_timeout_sec|**int**|單一要求的記憶體授權逾時 (以秒為單位)。 預設值為 0 時，會根據查詢成本使用內部計算。 不可為 Null。|  
|max_dop|**int**|工作負載群組之平行處理原則的最大程度。 預設值為 0 時，使用全域設定。 不可為 Null。<br /><br /> **節點：**這項設定會覆寫查詢選項**maxdop**。|  
|group_max_requests|**int**|並行要求的最大數目。 預設值為 0 時，不會指定任何限制。 不可為 Null。|  
|pool_id|**int**|這個工作負載群組所使用之資源集區的識別碼。|  
|external_pool_id|**int**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 此工作負載群組所使用的外部資源集區的識別碼。|  
  
## <a name="remarks"></a>備註  
 目錄檢視會顯示儲存的中繼資料。 若要查看記憶體中組態，請使用對應的動態管理檢視， [sys.dm_resource_governor_workload_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 如果資源管理員組態已經變更，但是尚未套用 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式，儲存的組態與記憶體中組態可能會不同。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW ANY DEFINITION 權限檢視內容；需要 CONTROL SERVER 權限變更內容。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [資源管理員目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
