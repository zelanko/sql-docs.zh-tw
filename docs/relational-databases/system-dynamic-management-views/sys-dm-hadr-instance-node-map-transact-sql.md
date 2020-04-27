---
title: sys.databases dm_hadr_instance_node_map （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: edd2ea7a215f01c25539753dff4bd170cf9d422f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900413"
---
# <a name="sysdm_hadr_instance_node_map-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對裝載已聯結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至其 Always On 可用性群組之可用性複本的每個實例，傳回裝載伺服器實例的 Windows Server 容錯移轉叢集（WSFC）節點名稱。 這個動態管理檢視有下列用途：  
  
-   這個動態管理檢視適用於偵測有多個可用性複本裝載於同一個 WSFC 節點的可用性群組，如果可用性群組不正確地設定，在 FCI 容錯移轉後可能會發生此不支援的組態狀況。 如需詳細資訊，請參閱[容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)。  
  
-   當多個 SQL Server 執行個體裝載於同一個 WSFC 節點時，資源 DLL 會使用此動態管理檢視來判斷要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|可用性群組的唯一識別碼，做為 WSFC 中的資源。|  
|**instance_name**|**nvarchar(256)**|名稱-*伺服器*/*實例*-裝載可用性群組之複本的伺服器實例。|  
|**node_name**|**nvarchar(256)**|WSFC 節點的名稱。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On 可用性群組目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;監視可用性群組](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
