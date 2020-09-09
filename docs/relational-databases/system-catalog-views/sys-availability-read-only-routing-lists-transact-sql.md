---
description: sys.availability_read_only_routing_lists (Transact-SQL)
title: sys. availability_read_only_routing_lists (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_read_only_routing_lists_TSQL
- availability_read_only_routing_lists
- sys.availability_read_only_routing_lists
- sys.availability_read_only_routing_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- sys.availability_read_only_routing_lists dynamic management view
ms.assetid: 0686bc5a-c206-41ef-b40a-79a8259d51d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 88d9f7757489e929f9e7981600f66a34ef79e920
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537471"
---
# <a name="sysavailability_read_only_routing_lists-transact-sql"></a>sys.availability_read_only_routing_lists (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對 WSFC 容錯移轉叢集中 AlwaysOn 可用性群組內每個可用性複本的唯讀路由清單，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|擁有路由清單之可用性複本的唯一識別碼。|  
|**routing_priority**|**int**|路由的優先順序 (1 是第一、2 是第二，依此類推)。|  
|**read_only_replica_id**|**uniqueidentifier**|將路由唯讀工作負載之目標可用性複本的唯一識別碼。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 &#40;Transact-sql&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
