---
title: SQL Server 的 Access Methods 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ab394b7eed0a284b8ed74e5333b01f27283469ca
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67987360"
---
# <a name="sql-server-access-methods-object"></a>SQL Server 的 Access Methods 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **的** Access Methods [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件會提供計數器，可監視資料庫內的邏輯資料如何存取。 您可以使用 **Buffer Manager** 計數器來監視實體存取磁碟內的資料庫頁面。 監視用來存取資料庫內儲存之資料的方法，可協助您判定增加或修改索引、新增或移動分割、新增檔案或檔案群組、重組索引或重新撰寫查詢，能否改善查詢效能。 **Access Methods** 計數器也可用來監視資料庫內的資料、索引和可用空間，藉以指出每個伺服器執行個體的資料量和片段。 索引片段過多會影響到效能。  
  
 如需有關資料量、片段與使用量的詳細資訊，請使用下列動態管理檢視：  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 如需有關檔案之 **tempdb** 內耗用的空間量，請使用下列動態管理檢視：  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Access Methods** 計數器。  
  
|SQL Server 的 Access Methods 計數器|描述|  
|----------------------------------------|-----------------|  
|**AU cleanup batches/sec**|可將延遲的已卸除配置單位清除的背景工作，每秒內可順利完成的批次數。|  
|**AU cleanups/sec**|可將延遲的已卸除配置單位清除的背景工作，每秒內順利卸除的配置單位數。 每次卸除配置單位都需要多個批次。|  
|**By-reference Lob Create Count**|By-reference 所傳送的大型物件 (lob) 值計數。 特定大量作業中會使用 By-reference Lob，避免以值傳送它們而產生的成本。|  
|**By-reference Lob Use Count**|已使用的 By-reference Lob 值的計數。 特定大量作業中會使用 By-reference Lob，避免以值傳送它們而產生的成本。|  
|**Count Lob Readahead**|發出 Readahead 的 Lob 頁數。|  
|**Count Pull In Row**|從 off-row 提取到 in-row 的值計數。|  
|**Count Push Off Row**|從 in-row 發送到 off-row 的值計數。|  
|**Deferred Dropped Aus**|可將延遲的已卸除配置單位清除的背景工作，等待卸除的配置單位數。|  
|**Deferred Dropped rowsets**|可將延遲的已卸除資料列集清除的背景工作，等待卸除的已中止線上索引建置作業所建立的資料列集數目。|  
|**Dropped rowset cleanups/sec**|可將延遲的已卸除資料列集清除的背景工作，順利卸除的已中止線上索引建置作業所建立的資料列集數目。|  
|**Dropped rowsets skipped/sec**|可將延遲的已卸除資料列集清除的背景工作，要略過的已中止線上索引建置作業所建立的資料列集數目。|  
|**Extent Deallocations/sec**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的所有資料庫，每秒取消配置的範圍數目。|  
|**Extents Allocated/sec**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的所有資料庫，每秒配置的範圍數目。|  
|**Failed AU cleanup batches/sec**|可將延遲的已卸除配置單位清除的背景工作，每秒內失敗且必須重試的批次數。 可能是由於缺少記憶體或磁碟空間、硬體失敗以及其他原因，才造成失敗。|  
|**Failed leaf page cookie**|分葉頁面上有所變更後，無法在索引搜尋期間使用分葉頁面 Cookie 的次數。 Cookie 用於加速索引搜尋。|  
|**Failed tree page cookie**|那些樹狀頁面的父系頁面上有所變更後，無法在索引搜尋期間使用樹狀頁面 Cookie 的次數。 Cookie 用於加速索引搜尋。|  
|**Forwarded Records/sec**|每秒透過轉寄的記錄指標擷取的記錄數。|  
|**FreeSpace Page Fetches/sec**|可用空間掃描每秒提取的頁面數 這些掃描搜尋會尋找頁面內已經配置給配置單位的可用空間，以滿足插入或修改記錄片斷的要求。|  
|**FreeSpace Scans/sec**|每秒初始化的掃描數目，以搜尋頁面內已經配置給配置單位的可用空間，以插入或修改記錄片斷。 每次掃描可能會找到多個的頁面。|  
|**Full Scans/sec**|每秒的未限制完整掃描數。 這些可為基底資料表或完整索引掃描。|  
|**Index Searches/sec**|每秒的索引搜尋數。 這些可用來啟動範圍掃描、重新定位範圍掃描、重新驗證掃描點、提取單一索引記錄和向下搜尋索引以尋找可插入新資料列之處。|  
|**InSysXact waits/sec**|讀取器因 InSysXact 位元已設定而必須等候頁面的次數。|  
|**LobHandle Create Count**|建立的暫存 Lob 計數。|  
|**LobHandle Destroy Count**|終結的暫存 Lob 計數。|  
|**LobSS Provider Create Count**|建立的 LOB 儲存體服務提供者 (LobSSP) 計數。 針對每個 LobSSP 建立一個工作資料表。|  
|**LobSS Provider Destroy Count**|終結的 LobSSP 計數。|  
|**LobSS Provider Truncation Count**|截斷的 LobSSP 計數。|  
|**Mixed page allocations/sec**|每秒自混合範圍所配置的分頁數。 這些可以用來儲存 IAM 頁面，以及已配置給配置單位的前八個頁面。|  
|**頁面壓縮嘗試次數/秒**|為頁面層級壓縮評估的頁數。 包括由於可以大量省下頁面所以未壓縮的頁面。 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的所有物件。 如需特定物件的資訊，請參閱 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)執行個體的所有資料庫，每秒取消配置的範圍數目。|  
|**Page Deallocations/sec**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的所有資料庫，每秒取消配置的頁面數目。 這些包括來自混合範圍與統一範圍的頁面。|  
|**Page Splits/sec**|每秒由於索引頁面溢位造成的頁面分隔數。|  
|**Pages Allocated/sec**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的所有資料庫，每秒配置的頁面數目。 這些包括來自混合範圍與統一範圍的頁面配置。|  
|**壓縮的頁面/秒**|使用 PAGE 壓縮所壓縮的資料頁數。 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的所有物件。 如需特定物件的資訊，請參閱 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)執行個體的所有資料庫，每秒取消配置的範圍數目。|  
|**Probe Scans/sec**|每秒的探查掃描數目，用以在索引或基底資料表中直接尋找至多一個合格的資料列。|  
|**Range Scans/sec**|每秒透過索引的合格範圍掃描數。|  
|**Scan Point Revalidations/sec**|每秒掃描點必須重新驗證以繼續掃描的次數。|  
|**Skipped Ghosted Records/sec**|掃描期間中每秒所跳過的代理資料記錄。|  
|**Table Lock Escalations/sec**|資料表上鎖定擴大至 TABLE 或 HoBT 資料粒度的次數。|  
|**Used leaf page cookie**|由於分葉頁面上沒有變更，所以在索引搜尋期間可順利使用分葉頁面 Cookie 的次數。 Cookie 用於加速索引搜尋。|  
|**Used tree page cookie**|由於樹狀頁面的父系頁面上沒有變更，所以在索引搜尋期間可順利使用樹狀頁面 Cookie 的次數。 Cookie 用於加速索引搜尋。|  
|**Workfiles Created/sec**|每秒建立的工作檔數。 例如，工作檔案可用來儲存雜湊聯結與雜湊彙總的暫存結果。|  
|**Worktables Created/sec**|每秒建立的工作資料表數。 例如，工作資料表可用來儲存查詢多工緩衝處理、lob 變數、XML 變數與資料指標的暫存結果。|  
|**Worktables From Cache Base**|僅供內部使用。|  
|**Worktables From Cache Ratio**|已建立的工作資料表百分比，尚未配置工作資料表的兩個初始頁面，但可從工作表快取立即取得。 卸除工作資料表後，可能會維持配置兩個頁面，而且它們會回到工作資料表快取。 這樣可以增加效能)。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
