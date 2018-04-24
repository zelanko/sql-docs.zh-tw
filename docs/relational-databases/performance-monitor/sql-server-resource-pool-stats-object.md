---
title: SQL Server 的 Resource Pool Stats 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24853ad0bfcd473c7f67492f187292118b639f55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server, Resource Pool Stats 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQLServer:Resource Pool Stats 物件包含效能計數器，可報告資源管理員資源集區統計資料的相關資訊。  
  
 每個作用中資源集區都會建立 SQLServer:Resource Pool Stats 效能物件的執行個體，而且此執行個體的名稱與資源管理員資源集區名稱相同。 下表描述這個執行個體支援的計數器。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Active memory grant amount (KB)**|目前授與記憶體的總數量 (以 KB 為單位)。 您也可以在 [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)中取得這項資訊。| 
|**Active memory grants count**|目前的記憶體授權總計數。 您也可以在 [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)中取得這項資訊。|  
|**平均磁碟讀取 IO (毫秒)**|從磁碟讀取作業的平均時間 (毫秒)。|  
|**Disk Read IO (ms) Base**|僅供內部使用。|
|**平均磁碟寫入 IO (毫秒)**|寫入磁碟作業的平均時間 (毫秒)。|  
|**Avg Disk Write IO (ms) Base**|僅供內部使用。|
|**Cache memory target (KB)**|快取的目前記憶體 Broker 目標 (以 KB 為單位)。|  
|**Compile memory target (KB)**|查詢編譯的目前記憶體 Broker 目標 (以 KB 為單位)。|  
|**CPU control effect %**|資源管理員對資源集區的影響。 計算成 (CPU 使用量 %) / (沒有資源管理員的 CPU 使用量 %)。|  
|**CPU delayed %**|指定的效能物件執行個體中，所有要求之系統 CPU 延遲佔使用時間總計的百分比。|
|**CPU delayed % base**|僅供內部使用。|
|**CPU effective %**|指定的效能物件執行個體中，所有要求之系統 CPU 使用量佔使用時間總計的百分比。|
|**CPU effective % base**|僅供內部使用。|
|**CPU usage %**|屬於此集區之所有工作負載群組中所有要求的 CPU 頻寬使用量。 這個值是相對於電腦所測得並正規化為系統上的所有 CPU。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序可用的 CPU 數量變更時，這個值將會變更。 但是，它不會正規化為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序收到的內容。|  
|**CPU usage % base**|僅供內部使用。|
|**CPU usage target %**|資源集區之 CPU 使用量 % 的目標值 (以資源集區組態設定和系統負載為基礎)。|  
|**CPU violated %**|CPU 保留與有效排程百分比之間的差異。|
|**磁碟讀取位元組/秒**|上一秒從磁碟讀取的位元組數。|  
|**節流的磁碟讀取 IO/秒**|上一秒讀取的節流作業數。|  
|**磁碟讀取 IO/秒**|上一秒從磁碟讀取的作業數目。| 
|**磁碟寫入位元組/秒**|上一秒寫入至磁碟的位元組數。|  
|**節流的磁碟寫入 IO/秒**|上一秒寫入的節流作業數。| 
|**磁碟寫入 IO/秒**|上一秒寫入至磁碟的作業數目。|
|**Max memory (KB)**|根據資源集區設定和伺服器狀態，資源集區可擁有的最大記憶體數量 (以 KB 為單位)。| 
|**Memory grant timeouts/sec**|每秒逾時的記憶體授權數目。|
|**Memory grants/sec**|在這個資源集區中每秒發生的記憶體授權數目。| 
|**Pending memory grant count**|在佇列中暫止之記憶體授權的要求數目。 您也可以在 [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)中取得這項資訊。|
|**Query exec memory target (KB)**|查詢執行記憶體授權的目前記憶體 Broker 目標 (以 KB 為單位)。 您也可以在 [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)中取得這項資訊。|  
|**Target memory (KB)**|根據資源集區設定和伺服器狀態，資源集區正嘗試取得的目標記憶體數量 (以 KB 為單位)。|   
|**Used memory (KB)**|資源集區所使用的記憶體數量 (以 KB 為單位)。|  

  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Workload Group Stats 物件](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
  
  
