---
title: sys.dm_hadr_availability_replica_cluster_nodes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_cluster_nodes
- sys.dm_hadr_availability_replica_cluster_nodes_TSQL
- dm_hadr_availability_replica_cluster_nodes_TSQL
- sys.dm_hadr_availability_replica_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_nodes dynamic management view
ms.assetid: dbd7e416-badd-4332-a45c-438aa0145a99
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 15dc02b29e4d51c1fa8845195828a644fdf69edd
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmhadravailabilityreplicaclusternodes-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 Windows Server 容錯移轉叢集 (WSFC) 叢集中 AlwaysOn 可用性群組的每一個可用性複本 (不論聯結狀態為何)，各傳回一個資料列。  

 ##  <a name="connected_state"></a>  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**group_name**|**nvarchar(256)**|可用性群組的名稱。|  
|**replica_server_name**|**nvarchar(256)**|裝載此複本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|**node_name**|**nvarchar(256)**|叢集節點的名稱。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [監視可用性群組 & #40;TRANSACT-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
