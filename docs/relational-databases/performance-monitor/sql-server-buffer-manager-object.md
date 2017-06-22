---
title: "SQL Server 的 Buffer Manager 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29b1764e30fe28153f6f86731f5b6fc520dc9027
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-buffer-manager-object"></a>SQL Server 的 Buffer Manager 物件
  **Buffer Manager** 物件提供了可監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用情形的計數器：  
  
-   要儲存資料頁的記憶體。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 讀取和寫入資料庫頁面時，監視實體 I/O 的計數器。  
  
-   緩衝集區延伸模組，透過使用快速靜態儲存區 (例如固態硬碟 (SSD)) 來擴充緩衝快取。  
  
 監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的記憶體與計數器有助於判斷：  
  
-   是否因實體記憶體不足而產生瓶頸。 是否無法將經常存取的資料儲存在快取中，使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須從磁碟中擷取資料。   
  
-   是否可藉由增加更多記憶體，或讓資料快取或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部結構可使用更多記憶體，而改善查詢效能。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 須自磁碟中讀取資料的頻率。 和其他的作業相比 (例如記憶體存取)，實體 I/O 消耗的時間更多。 將實體 I/O 最小化可改善查詢的效能。  
  
## <a name="buffer-manager-performance-objects"></a>Buffer Manager 效能物件  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Manager** 效能物件。  
  
|SQL Server Buffer Manager 計數器|說明|  
|----------------------------------------|-----------------|  
|**Background writer pages/sec**|為了強制執行復原間隔設定而排清的頁數。| 
|**Buffer cache hit ratio**|表示不需讀取磁碟即可在緩衝區快取中找到之頁面的百分比。 此比率是過去數千個分頁存取中，快取叫用總數除以快取查閱所得的結果。 時間一久，比率的變動會越來越小。 從快取讀取遠比從磁碟讀取節省成本，因此您會希望此比率越高越好。 通常，您可以藉由增加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用的記憶體數量或是使用緩衝集區擴充功能，來提高緩衝區快取叫用比率。|  
|**Buffer cache hit ratio base**|僅供內部使用。|
|**Checkpoint pages/sec**|表示每秒經由檢查點或其他導致所有變更分頁排清至磁碟的作業所轉存至磁碟的分頁數。|  
|**Database pages**|表示具有資料庫內容之緩衝集區的頁面數。|  
|**延伸模組配置的頁面**|緩衝集區延伸模組檔案中非可用的快取頁面總數。|  
|**延伸模組可用頁面**|緩衝集區延伸模組檔案中可用的快取頁面總數。|  
|**使用中的延伸模組百分比**|緩衝區管理員頁面所佔用之緩衝集區延伸模組分頁檔的百分比。|  
|**延伸模組未完成的 IO 計數器**|緩衝集區擴充檔的 I/O 佇列長度。|  
|**每秒的延伸模組頁面收回數目**|每秒從緩衝集區延伸模組檔案收回的頁數。|  
|**每秒的延伸模組頁面讀取數**|每秒從緩衝集區延伸模組檔案讀取的頁數。|  
|**延伸模組頁面未參考的時間**|表示頁面將停留在這個沒有參考之緩衝集區延伸模組中的平均秒數。|  
|**每秒的延伸模組頁面寫入數**|每秒寫入緩衝集區延伸模組檔案的頁數。|  
|**Free list stalls/sec**|表示每秒鐘必須等待可用頁面的要求數。|  
|**Integral Controller Slope**|緩衝集區的整體控制器上次使用的斜率，乘以 -100 億。| 
|**Lazy writes/sec**|表示每秒鐘由緩衝區管理員的延遲寫入器所寫入的緩衝區數目。 「延遲寫入器」是一種系統處理序，可排清整批已變更且過時的緩衝區 (這種緩衝區包含必須重新寫入磁碟以便讓緩衝區可重複用於其他頁面的變更)，使其可供使用者處理序使用。 使用延遲寫入器，即不需經常執行檢查點來建立可用的緩衝區。|  
|**Page life expectancy**|表示頁面停留在這個沒有參考之緩衝集區中的秒數。|  
|**Page lookups/sec**|表示每秒鐘在緩衝集區中尋找頁面的要求數。|  
|**Page reads/sec**|表示每秒鐘發出的實體資料庫頁面讀取數。 這項統計資料可顯示所有資料庫的實體頁面讀取總數。 由於實體 I/O 成本很高，因此您可以藉由使用較大的資料快取、智慧型索引、和較有效的查詢，或藉由變更資料庫設計，盡可能降低成本。|  
|**Page writes/sec**|表示每秒鐘發出的實體資料庫頁面寫入數。|  
|**Readahead pages/sec**|表示每秒鐘預期會使用而讀取的頁數。|  
|**Readahead time/sec**|發出 readahead 花費的時間 (微秒)。|
|**Target pages**|緩衝集區的理想分頁數。|

  
## <a name="see-also"></a>另請參閱  
 [SQL Server:Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)   
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server 的 Plan Cache 物件](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [緩衝集區擴充](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
