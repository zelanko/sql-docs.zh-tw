---
title: "sys.dm_hadr_name_id_map (TRANSACT-SQL) |Microsoft 文件"
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
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 320d4856d0358612d462ef14c5559346624fe619
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadrnameidmap-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Alwayson 可用性群組的對應，會顯示目前的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已經聯結至三個唯一識別碼： 可用性群組識別碼、 WSFC 資源識別碼和 WSFC 群組識別碼。 此對應的目的是要處理重新命名 WSFC 資源/群組的案例。  
   
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|可用性群組的名稱。 這是使用者指定的名稱，它在 Windows Server 容錯移轉叢集 (WSFC) 叢集內必須是唯一的。|  
|**ag_id**|**uniqueidentifier**|可用性群組的唯一識別碼 (GUID)。|  
|**ag_resource_id**|**nvarchar(256)**|在 WSFC 叢集中做為資源之可用性群組的唯一識別碼。|  
|**ag_group_id**|**nvarchar(256)**|可用性群組的唯一 WSFC 群組識別碼。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [AlwaysOn 可用性群組動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
