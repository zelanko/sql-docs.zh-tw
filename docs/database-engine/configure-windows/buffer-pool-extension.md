---
title: 緩衝集區延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 909ab7d2-2b29-46f5-aea1-280a5f8fedb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f732c4038940ef2ed5ee511e399f3bcf2efae54f
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606888"
---
# <a name="buffer-pool-extension"></a>緩衝集區擴充
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中導入緩衝集區擴充，可將非動態隨機存取記憶體 (也就是固態硬碟) 擴充完全整合到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 緩衝集區，如此能大幅提升 I/O 輸送量。 並非每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都有提供緩衝集區擴充。 如需詳細資訊，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
## <a name="benefits-of-the-buffer-pool-extension"></a>緩衝集區擴充的優點  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的主要用途是為了儲存和擷取資料，因此大量磁碟 I/O 是 Database Engine 的核心特性。 因為磁碟 I/O 作業會秏用許多資源，而且相對上需要較長的時間才能完成，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 非常著重提高 I/O 的效率。 緩衝集區可做為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的主要記憶體配置來源。 緩衝區管理是達成這種效率的重要元件。 緩衝區管理元件包含兩種機制：可存取和更新資料庫頁面的緩衝區管理員，以及可減少資料庫檔案 I/O 的緩衝集區快取。  
  
 資料與索引頁面都會從磁碟讀入緩衝集區，而修改的頁面 (也稱為中途分頁) 則會重新寫入磁碟。 伺服器和資料庫檢查點的記憶體壓力會導致緩衝區快取中使用頻繁 (使用中) 的中途分頁從快取收回並寫入機械磁碟，然後再重新讀入快取中。 這些 I/O 作業通常是很小的隨機讀取和寫入 (4 到 16 KB 的資料順序)。 小型隨機 I/O 模式會產生頻繁的搜尋、競爭機械磁碟臂、增加 I/O 延遲，並降低系統的彙總 I/O 輸送量。  
  
 解決這些 I/O 瓶頸的一般方法是加入更多 DRAM，或者加入高效能的 SAS 主軸。 雖然這些選項很有用，但是有很大的缺點：DRAM 比資料存放磁碟更為昂貴，而且增加主軸會增加硬體採購的資本支出，而且也會因為增加用電量和元件故障機率而增加營運成本。  
  
 緩衝集區擴充功能可透過非動態儲存 (通常是 SSD) 延伸緩衝集區快取。 因為有了這個延伸模組，緩衝集區可以容納更大的資料庫工作集，強制將 RAM 與 SSD 之間的 I/O 分頁。 這樣可有效地將機械磁碟中的小型隨機 I/O 卸載到 SSD。 由於 SSD 的延遲較低而且隨機 I/O 效能更好，所以緩衝集區擴充會大幅提高 I/O 輸送量。  
  
 下列清單描述緩衝集區擴充功能的優點。  
  
-   增加隨機 I/O 輸送量  
  
-   減少 I/O 延遲  
  
-   增加交易輸送量  
  
-   透過更大的混合式緩衝集區來提升讀取效能  
  
-   可以充分利用現有和將來的低成本記憶體磁碟的快取架構  
  
### <a name="concepts"></a>概念  
 下列詞彙適用於緩衝集區擴充功能。  
  
 固態硬碟 (SSD)  
 固態硬碟會以持續方式將資料儲存在記憶體 (RAM) 中。 如需詳細資訊，請參閱 [這個定義](https://en.wikipedia.org/wiki/Solid-state_drive)。  
  
 緩衝區  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，緩衝區是 8 KB 的記憶體頁面，大小與資料或索引頁面相同。 因此，緩衝區快取也分成 8 KB 的頁面。 頁面會保留在緩衝區快取中，直到緩衝區管理員需要緩衝區來讀取更多資料為止。 只有資料修改後，才會重新寫入磁碟。 這些記憶體中已修改的頁面稱為中途分頁。 如果頁面相當於它在磁碟上的資料庫映像，就表示它不是中途頁面。 在重新寫入磁碟之前，可以多次修改緩衝區快取中的資料。  
  
 緩衝集區  
 也稱為緩衝區快取。 緩衝集區是所有資料庫的快取資料頁面所共用的全域資源。 緩衝集區快取大小的上限和下限是在啟動期間決定，或者當使用 sp_configure 來動態重新設定 SQL Server 的執行個體時所決定。 此大小會決定執行中的執行個體內隨時可在緩衝集區內快取的最大頁數。  
  
 如果在電腦上執行的其他應用程式製造繁重的記憶體壓力，緩衝集區擴充能認可的最大記憶體將會受到限制。  
  
 檢查點  
 檢查點會建立一個已知的恰當起點， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以從這個點開始套用發生非預期的關機或當機之後，於復原期間包含在交易記錄中的變更。 檢查點會將中途分頁和交易記錄資訊從記憶體寫入磁碟，也會記錄有關交易記錄的資訊。 如需詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)。  
  
## <a name="buffer-pool-extension-details"></a>緩衝集區擴充詳細資料  
 SSD 儲存體是當做記憶體子系統的延伸模組來使用，而非磁碟儲存體的子系統。 也就是說，緩衝集區擴充檔案允許緩衝集區管理員使用 DRAM 和 NAND 快閃記憶體，在 SSD 支援的非揮發性隨機存取記憶體中維護較大的 lukewarm 頁面緩衝集區。 這樣會建立多層級快取階層，其中的層級 1 (L1) 為 DRAM，而層級 (L2) 為 SSD 上的緩衝集區擴充檔案。 只有乾淨的頁面會寫入 L2 快取中，如此有助於維護資料安全。 緩衝區管理員會處理 L1 與 L2 快取之間非中途頁面的移動。  
  
 下圖提供緩衝集區相較於其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的高階架構概觀。  
  
 ![SSD 緩衝集區延伸模組架構](../../database-engine/configure-windows/media/ssdbufferpoolextensionarchitecture.gif "SSD 緩衝集區延伸模組架構")  
  
 啟用時，緩衝集區擴充會指定 SSD 上緩衝集區快取檔案的大小和檔案路徑。 這個檔案是 SSD 上連續的儲存範圍，而且會在啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的期間以靜態方式設定。 只有當緩衝集區擴充功能停用時，才能執行檔案組態參數的更改。 當停用緩衝集區擴充時，所有相關的組態設定都會從登錄中移除。 當 SQL Server 執行個體關機後，便會刪除緩衝集區擴充檔案。  
  
## <a name="best-practices"></a>最佳作法  
 我們建議您依照以下的最佳作法進行。  
  
-   建議您在初次啟用緩衝集區延伸模組後重新啟動 SQL Server 執行個體，讓效能達到最高效益。  
  
-   緩衝集區擴充大小最大可達 max_server_memory 之值的 32 倍。  建議的實體記憶體大小 (max_server_memory) 與緩衝集區擴充大小比率為 1:16 或更低。 1:4 到 1:8 的範圍內的較低比率可能會比較理想。 如需設定 max_server_memory 選項的資訊，請參閱 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
-   在生產環境中實作之前，請徹底測試緩衝集區擴充。 一旦實際執行之後，請避免對檔案進行組態變更或關閉此功能。 這些活動可能對伺服器效能造成負面影響，因為功能停用時，緩衝集區的大小會大幅減少。 停用時，直到 SQL Server 執行個體重新啟動為止，才會開始回收用於支援功能的記憶體。 不過，如果重新啟用功能，則會重複使用記憶體而不需重新啟動執行個體。  
  
## <a name="return-information-about-the-buffer-pool-extension"></a>傳回有關緩衝集區擴充的資訊  
 您可以使用下列動態管理檢視顯示緩衝集區擴充的組態，並傳回有關擴充中資料頁的資訊。  
  
-   [sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
-   [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
 SQL Server 中的緩衝區管理員物件有提供效能計數器，以便追蹤緩衝集區擴充檔案中的資料頁面。 如需詳細資訊，請參閱＜ [緩衝集區擴充效能計數器](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)＞。  
  
 下列是可以使用的 Xevent。  
  
|XEvent|Description|參數|  
|------------|-----------------|----------------|  
|sqlserver.buffer_pool_extension_pages_written|會在從緩衝集區收回一個頁面或一組頁面，並將頁面寫入緩衝集區擴充檔時引發。|*number_page*<br /><br /> *first_page_id*<br /><br /> *first_page_offset*<br /><br /> *initiator_numa_node_id*|  
|sqlserver.buffer_pool_extension_pages_read|會在從緩衝集區擴充檔案將頁面讀到緩衝集區時引發。|*number_page*<br /><br /> *first_page_id*<br /><br /> *first_page_offset*<br /><br /> *initiator_numa_node_id*|  
|sqlserver.buffer_pool_extension_pages_evicted|會在從緩衝集區擴充檔收回頁面時引發。|*number_page*<br /><br /> *first_page_id*<br /><br /> *first_page_offset*<br /><br /> *initiator_numa_node_id*|  
|sqlserver.buffer_pool_eviction_thresholds_recalculated|會在計算收回臨界值時引發。|*warm_threshold*<br /><br /> *cold_threshold*<br /><br /> *pages_bypassed_eviction*<br /><br /> *eviction_bypass_reason*<br /><br /> *eviction_bypass_reason_description*|  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**工作描述**|**主題**|  
|啟用及設定緩衝集區擴充|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)|  
|修改緩衝集區擴充組態|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)|  
|檢視緩衝集區擴充組態|[sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)|  
|監視緩衝集區擴充|[sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)<br /><br /> [效能計數器](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|  
  
  
