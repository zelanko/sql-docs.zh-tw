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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250583"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的**Memory Node**物件會提供計數器，可監視 NUMA 節點上的伺服器記憶體使用量。  
  
## <a name="memory-node-counters"></a>Memory Node 計數器  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** 計數器。  
  
|SQL Server Memory Manager 計數器|描述|  
|----------------------------------------|-----------------|  
|**資料庫節點記憶體（KB）**|指定伺服器目前用於此節點之資料庫頁面的記憶體數量。|  
|**可用節點記憶體（KB）**|指定伺服器未用於此節點的記憶體數量。|  
|**外部節點記憶體（KB）**|指定此節點上非 NUMA 本機記憶體的數量。|  
|**遭竊的記憶體節點（KB）**|指定伺服器用於此節點之資料庫頁面以外目的的記憶體數量。|  
|**目標節點記憶體**|指定此節點的理想記憶體數量。|  
|**節點記憶體總計**|表示伺服器已在此節點上認可的記憶體總數。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server 的 Buffer Manager 物件](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
