---
title: "sys.dm_hadr_availability_group_states (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
caps.latest.revision: "43"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b48d1d3291a1cdcbfcaa84b71c323e1ea410afc8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadravailabilitygroupstates-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，每個 Alwayson 可用性群組擁有可用性複本上的本機執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 每個資料列會顯示定義給定之可用性群組健全狀況的狀態。  
  
> [!NOTE]  
>  若要取得的完整清單，請查詢[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目錄檢視。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼。|  
|**primary_replica**|**varchar （128)**|裝載目前主要複本的伺服器執行個體名稱。<br /><br /> NULL = 不是主要複本，或是無法與 WSFC 容錯移轉叢集通訊。|  
|**primary_recovery_health**|**tinyint**|表示主要複本的復原健全狀況，可為下列其中一個值：<br /><br /> 0 = 進行中<br /><br /> 1 = 線上<br /><br /> NULL<br /><br /> 在次要複本上**primary_recovery_health**資料行是 NULL。|  
|**primary_recovery_health_desc**|**nvarchar （60)**|描述**primary_replica_health**，下列其中一個的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|指出次要複本，其中的復原健全狀況：<br /><br /> 0 = 進行中<br /><br /> 1 = 線上<br /><br /> NULL<br /><br /> 在主要複本**secondary_recovery_health**資料行是 NULL。|  
|**secondary_recovery_health_desc**|**nvarchar （60)**|描述**secondary_recovery_health**，下列其中一個的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|反映的彙總**synchronization_health**可用性群組中的所有可用性複本。 以下是可能的值和其說明。<br /><br /> 0： 非狀況良好。 可用性複本沒有狀況良好**synchronization_health** (2 = HEALTHY)。<br /><br /> 1： 部分狀況良好。 部分 (而不是所有) 可用性複本的同步處理狀況良好。<br /><br /> 2： 狀況良好。 每一個可用性複本的同步處理狀況良好。<br /><br /> 複本同步處理健全狀況的相關資訊，請參閱**synchronization_health**中的資料行[sys.dm_hadr_availability_replica_states &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar （60)**|描述**synchronization_health**，下列其中一個的：<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 可用性群組動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
