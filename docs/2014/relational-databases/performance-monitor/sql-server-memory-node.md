---
title: SQL Server 的 Memory Node | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a2296fdb68e640ce8ebfc8dd9cdb351666b337
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250583"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
  Microsoft **中的** Memory Node [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件會提供計數器，可監視 NUMA 節點的伺服器記憶體使用狀況。  
  
## <a name="memory-node-counters"></a>Memory Node 計數器  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** 計數器。  
  
|SQL Server Memory Manager 計數器|描述|  
|----------------------------------------|-----------------|  
|**Database Node Memory (KB)**|指定伺服器目前用於此節點之資料庫頁面的記憶體數量。|  
|**Free Node Memory (KB)**|指定伺服器未用於此節點的記憶體數量。|  
|**Foreign Node Memory (KB)**|指定此節點上非 NUMA 本機記憶體的數量。|  
|**Stolen Memory Node (KB)**|指定伺服器用於此節點之資料庫頁面以外目的的記憶體數量。|  
|**Target Node Memory**|指定此節點的理想記憶體數量。|  
|**Total Node Memory**|表示伺服器已在此節點上認可的記憶體總數。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server 的 Buffer Manager 物件](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
