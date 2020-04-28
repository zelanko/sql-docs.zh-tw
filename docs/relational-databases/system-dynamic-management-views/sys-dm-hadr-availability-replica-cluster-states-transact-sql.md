---
title: sys.databases dm_hadr_availability_replica_cluster_states （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_replica_cluster_states_TSQL
- dm_hadr_availability_replica_cluster_states
- sys.dm_hadr_availability_replica_cluster_states
- dm_hadr_availability_replica_cluster_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_states dynamic management view
ms.assetid: 2e0dd780-6a71-4f4b-b7f7-6e063bec71d6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3e2fccaed2b3c001fdcc8a0d7938f0a75a8f10d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246346"
---
# <a name="sysdm_hadr_availability_replica_cluster_states-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 Windows Server 容錯移轉叢集 (WSFC) 叢集中所有 Always On 可用性群組 (不論複本位置為何) 的每一個 Always On 可用性複本 (不論其聯結狀態為何)，各傳回一個資料列。  
  
##  <a name="connected_state"></a>  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|可用性複本的唯一識別碼。|  
|**replica_server_name**|**nvarchar(256)**|裝載此複本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼。|  
|**join_state**|**tinyint**|0 = 未聯結<br /><br /> 1 = 已聯結，獨立<br /><br /> 2 = 已聯結，容錯移轉叢集執行個體|  
|**join_state_desc**|**nvarchar(60)**|NOT_JOINED<br /><br /> JOINED_STANDALONE<br /><br /> JOINED_FAILOVER_CLUSTER_INSTANCE|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
