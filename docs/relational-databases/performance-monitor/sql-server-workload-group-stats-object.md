---
title: "SQL Server 的 Workload Group Stats 物件 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 12/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 668f0f7cf7b38fb18144e58cccbc7e4902a39f75
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-workload-group-stats-object"></a>SQL Server, Workload Group Stats 物件
  SQLServer:Workload Group Stats 物件包含效能計數器，可報告資源管理員工作負載群組統計資料的相關資訊。  
  
 每個作用中工作負載群組都會建立 SQLServer:Workload Group Stats 效能物件的執行個體，而且此執行個體的名稱與資源管理員工作負載群組名稱相同。 下表描述這個執行個體支援的計數器。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Active parallel threads**|目前平行執行緒使用量的計數。|  
|**Active requests**|目前正在這個工作負載群組中執行的要求數目。 這個計數應該等於群組識別碼所篩選之 sys.dm_exec_requests 中的資料列計數。|  
|**Blocked requests**|目前在工作負載群組中封鎖的要求數目。 這個值可用來判斷工作負載特性。|  
|**CPU delayed %**|指定的效能物件執行個體中，所有要求之系統 CPU 延遲佔使用時間總計的百分比。| 
|**CPU delayed % base**|僅供內部使用。| 
|**CPU effective %**|指定的效能物件執行個體中，所有要求之系統 CPU 使用量佔使用時間總計的百分比。| 
|**CPU effective % base**|僅供內部使用。| 
|**CPU usage %**|這個工作負載群組中所有要求的 CPU 頻寬使用量 (相對於電腦所測得並正規化為系統上的所有 CPU)。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序可用的 CPU 數量變更時，這個值將會變更。 但是，它不會正規化為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序收到的內容。| 
|**CPU usage % base**|僅供內部使用。| 
|**CPU 違反的 %**|CPU 保留與有效排程百分比之間的差異。|  
|**Max request CPU time (ms)**|目前正在這個工作負載群組中執行之要求所使用的最大 CPU 時間 (以毫秒為單位)。|  
|**Max request memory grant (KB)**|查詢之記憶體授權的最大值 (以 KB 為單位)。|  
|**Query optimizations/sec**|在這個工作負載群組中每秒發生的查詢最佳化數目。 這個值可用來判斷工作負載特性。|  
|**Queued requests**|目前正在等候收取的佇列要求數目。 如果到達 GROUP_MAX_REQUESTS 限制之後調整流速，則這個計數可以是非零。|  
|**Reduced memory grants/sec**|每秒小於理想記憶體授權數量的查詢數目。|  
|**Requests completed/sec**|在這個工作負載群組中完成的要求數目。 這個數目是累計的。|  
|**Suboptimal plans/sec**|在這個工作負載群組中每秒產生的次佳計畫數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Resource Pool Stats 物件](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
  
  

