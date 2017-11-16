---
title: "效能計數器 (SSAS) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0e2d625f6c9060f32fb2a2dc676c84c673f55c8f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="performance-counters-ssas"></a>效能計數器 (SSAS)
  使用效能監視器可以透過效能計數器來監視 Microsoft SQL Server Analysis Services (SSAS) 執行個體的效能。  
  
 效能監視器是追蹤資源使用方式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Control (MMC) 嵌入式管理單元。 您可以啟動這個 MMC 嵌入式管理單元，方法是在命令提示字元中輸入 **PerfMon** ，或是從 [控制台] 按一下 **[系統管理工具]**然後按一下 **[效能監視器]**。 效能監視器可讓您使用預先定義的物件和計數器來追蹤伺服器和處理序效能與活動，並利用使用者定義的計數器來監視事件。 效能監視器會收集計數而非關於事件的資料，例如，記憶體使用量、使用中交易數目或 CPU 活動。 您也可在特定計數器上設定臨界值，以產生通知操作員的警示。  
  
 效能監視器可以監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的遠端與本機執行個體。 如需詳細資訊，請參閱 [使用效能監視器](http://technet.microsoft.com/library/cc749115.aspx)。  
  
 若要查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以使用之任何計數器的描述，請在效能監視器中開啟 **[新增計數器]** 對話方塊，並選取效能物件，然後按一下 **[顯示描述]**。 最重要的計數器有 CPU 使用量、記憶體使用量、磁碟 IO 速率。 建議您從這些重要的計數器開始，當您較為了解可透過監視提升哪些效能時，再移至更詳細的計數器。 如需有關要包含哪些計數器的詳細資訊，請參閱 [SQL Server 2008 R2 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 計數器已分組，因此您可以更輕鬆地找到相關計數器。  
  
## <a name="counters-by-groups"></a>依群組分組的計數器  
  
|群組|說明|  
|-----------|-----------------|  
|[Cache](#bkmk_Cache)|與 Analysis Services 彙總快取相關的統計資料。|  
|[連接](#bkmk_Connection)|與 Microsoft Analysis Services 連接相關的統計資料。|  
|[Data Mining Prediction](#bkmk_DataMiningPrediction)|與處理資料採礦模型相關的統計資料。|  
|[Data Mining Model Processing](#bkmk_DataMiningModelProcessing)|與根據資料採礦模型建立預測相關的統計資料。|  
|[鎖定](#bkmk_Locks)|與 Microsoft Analysis Services 內部伺服器鎖定相關的統計資料。|  
|[MDX](#bkmk_MDX)|與 Microsoft Analysis Services MDX 計算相關的統計資料。|  
|[記憶體](#bkmk_Memory)|與 Microsoft Analysis Services 內部伺服器記憶體相關的統計資料。|  
|[主動式快取](#bkmk_ProactiveCaching)|與 Microsoft Analysis Services 主動式快取相關的統計資料。|  
|[Processing Aggregations](#bkmk_ProcAggregations)|與處理 MOLAP 資料檔之彙總相關的統計資料。|  
|[Processing Indexes](#bkmk_ProcIndexes)|與處理 MOLAP 資料檔之索引相關的統計資料。|  
|[Processing](#bkmk_Processing)|與處理資料相關的統計資料。|  
|[Storage Engine Query](#bkmk_StorageEngineQuery)|與 Microsoft Analysis Services 儲存引擎查詢相關的統計資料。|  
|[Threads](#bkmk_Threads)|與 Microsoft Analysis Services 執行緒相關的統計資料。|  
  
###  <a name="bkmk_Cache"></a> Cache  
 與 Microsoft Analysis Services 彙總快取相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current KB|目前由彙總快取所使用的記憶體，以 KB 為單位。|  
|KB added/sec|記憶體加入快取的速率，KB/秒。|  
|Current entries|目前快取項目的數目。|  
|Inserts/sec|插入至快取的速率。  此速率是根據每個資料庫每個 Cube 的每個資料分割來追蹤。|  
|Evictions/sec|來自快取的收回速率。  這是根據每個資料庫每個 Cube 的每個資料分割。  收回通常是由背景清除器造成的。|  
|Total inserts|插入至快取的數目。  此速率是根據每個資料庫每個 Cube 的每個資料分割來追蹤。|  
|Total evictions|來自快取的收回數目。  收回是根據每個資料庫每個 Cube 的每個資料分割來追蹤。  收回通常是由背景清除器造成的。|  
|Direct hits/sec|快取直接叫用的速率。 快取叫用表示從現有的快取項目回應查詢。|  
|Misses/sec|快取遺漏的速率。|  
|Lookups/sec|快取查閱的速率。|  
|Total direct hits|快取直接點擊次數總計。  快取直接點擊表示從現有的快取項目回應查詢。|  
|Total misses|快取遺漏總計。|  
|查閱總計|查閱快取的總數。|  
|Direct hit ratio|取得計數器數值的期間，快取直接叫用與快取查閱之間的比率。|  
|Total filtered iterator cache hits|快取點擊總數，會傳回篩選結果上的索引 Iterator。|  
|Total filtered iterator cache misses|快取點擊總數，這類叫用因為無法在篩選的結果上建立索引 Iterator，所以必須用篩選的結果建立新的快取。|  
  
###  <a name="bkmk_Connection"></a> 連接  
 與 Microsoft Analysis Services 連接相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current connections|目前已建立的用戶端連接數目。|  
|Requests/sec|連接要求的速率。  這些是到達的要求。|  
|Total requests|連接要求的總計。  這些是到達的要求。|  
|Successes/sec|成功完成連接的速率。|  
|Total successes|連接成功的總計。|  
|Failures/sec|連接失敗的速率。|  
|Total failures|嘗試連接失敗的總計。|  
|Current user sessions|目前建立的使用者工作階段數目。|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a> Data Mining Model Processing  
 與 Microsoft Analysis Services 資料採礦模型處理相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Cases/sec|處理案例的速率。|  
|Current models processing|目前正在處理的模型數目。|  
  
###  <a name="bkmk_DataMiningPrediction"></a> Data Mining Prediction  
 與 Microsoft Analysis Services 資料採礦預測相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Concurrent DM queries|目前正在處理的資料採礦查詢數目。|  
|Predictions/sec|在資料採礦查詢中產生的預測數目。|  
|Rows/sec|在資料採礦預測查詢期間中處理的資料列數目。|  
|Queries/sec|已處理的資料採礦查詢數目。|  
|Total Queries|伺服器收到的資料採礦查詢總數。|  
|總計資料列|資料採礦查詢傳回的資料列總計。|  
|Total Predictions|伺服器收到的資料採礦預測查詢總數。|  
  
###  <a name="bkmk_Locks"></a> 鎖定  
 與 Microsoft Analysis Services 內部伺服器鎖定相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current latch waits|目前等候閂鎖的執行緒數目。  這些是無法立即被授與，而處於等候狀態的閂鎖要求。|  
|Latch waits/sec|無法立即被授與及必須等候授與的閂鎖要求速率。|  
|Current locks|目前已鎖定物件的數目。|  
|Current lock waits|目前正在等候鎖定的用戶端數目。|  
|Lock requests/sec|每秒鎖定要求的數目。|  
|Lock grants/sec|每秒鎖定授與的數目。|  
|Lock waits/sec|每秒鎖定等候的數目。  這些是無法立即被授與鎖定，而處於等候狀態的鎖定要求。|  
|Lock denials/sec|鎖定拒絕的速率。|  
|Unlock requests/sec|每秒解除鎖定要求的數目。|  
|Total deadlocks detected|偵測到的死結總數。|  
  
###  <a name="bkmk_MDX"></a> MDX  
 與 Microsoft Analysis Services MDX 計算相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Number of calculation covers|由 MDX 執行計畫所建立的評估節點總數，包括使用中和快取的。|  
|Current number of evaluation nodes|由使用中和快取的 MDX 執行計畫所建立的目前 (大約) 評估節點數目。|  
|Number of Storage Engine evaluation nodes|由 MDX 執行計畫所建立的儲存引擎評估節點總數。|  
|Number of cell-by-cell evaluation nodes|由 MDX 執行計畫所建立的逐資料格評估節點總數。|  
|Number of bulk-mode evaluation nodes|由 MDX 執行計畫所建立的大量模式評估節點總數。|  
|Number of evaluation nodes that covered a single cell|由只涵蓋一個資料格的 MDX 執行計畫所建立的評估節點總數。|  
|Number of evaluation nodes with calculations at the same granularity|由 MDX 執行計畫所建立的評估節點總數，這些執行計畫中的計算與評估節點的資料粒度相同。|  
|Current number of cached evaluation nodes|由 MDX 執行計畫所建立的目前 (大約) 快取評估節點數目。|  
|Number of cached Storage Engine evaluation nodes|由 MDX 執行計畫所建立的快取儲存引擎評估節點總數|  
|Number of cached bulk-mode evaluation nodes|由 MDX 執行計畫所建立的快取大量模式評估節點總數。|  
|Number of cached 'other' evaluation nodes|由 MDX 執行計畫所建立、既不是儲存引擎也不是大量模式的快取評估節點總數。|  
|Number of evictions of evaluation nodes|衝突所致的評估節點快取收回總數。|  
|Number of hash index hits in the cache of evaluation nodes|雜湊索引所滿足的評估節點快取點擊總數。|  
|Number of cell-by-cell hits in the cache of evaluation nodes|評估節點快取中的逐資料格叫用總數。|  
|Number of cell-by-cell misses in the cache of evaluation nodes|評估節點快取中的逐資料格遺漏總數。|  
|Number of subcube hits in the cache of evaluation nodes|評估節點快取中的 Subcube 叫用總數。|  
|Number of subcube misses in the cache of evaluation nodes|評估節點快取中的 Subcube 遺漏總數。|  
|Total Sonar subcubes|查詢最佳化工具產生的 Subcube 總數。|  
|Total cells calculated|導出的資料格屬性總數。|  
|Total recomputes|由於錯誤而重新計算的資料格總數。|  
|Total flat cache inserts|插入於一般計算快取中的資料格值總數。|  
|Total calculation cache registered|已經註冊的計算快取總數。|  
|Total NON EMPTY|NON EMPTY 演算法使用的總次數。|  
|Total NON EMPTY unoptimized|使用未最佳化的 NON EMPTY 演算法的總次數。|  
|Total NON EMPTY for calculated members|NON EMPTY 演算法對導出成員迴圈的總次數。|  
|Total Autoexist|自動存在執行的總次數。|  
|Total EXISTING|執行 EXISTING 集合運算的總次數。|  
  
###  <a name="bkmk_Memory"></a> 記憶體  
 與 Microsoft Analysis Services 內部伺服器記憶體相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Page Pool 64 Alloc KB|從系統借用的記憶體大小，以 KB 為單位。  此記憶體會提供給伺服器的其他部分使用。|  
|Page Pool 64 Lookaside KB|目前在 64KB 對應清單中的記憶體，以 KB 為單位  (備妥供使用的記憶體頁面)。|  
|Page Pool 8 Alloc KB|從 64KB 分頁集區借用的記憶體大小，以 KB 為單位。  此記憶體會提供給伺服器的其他部分使用。|  
|Page Pool 8 Lookaside KB|目前在 8KB 對應清單中的記憶體，以 KB 為單位  (備妥供使用的記憶體頁面)。|  
|Page Pool 1 Alloc KB|從 64KB 分頁集區借用的記憶體大小，以 KB 為單位。  此記憶體會提供給伺服器的其他部分使用。|  
|Page Pool 1 Lookaside KB|目前在 8KB 對應清單中的記憶體，以 KB 為單位  (備妥供使用的記憶體頁面)。|  
|Cleaner Current Price|記憶體目前的價格 ($/位元組/時間)，並正規化為 1000。|  
|Cleaner Balance/sec|平衡+壓縮作業的速率。|  
|Cleaner Memory shrunk KB/sec|壓縮的速率，以 KB/秒為單位。|  
|Cleaner Memory shrinkable KB|背景清除器將清除的記憶體數量，以 KB 為單位。|  
|Cleaner Memory nonshrinkable KB|背景清除器將不會清除的記憶體數量，以 KB 為單位。|  
|Cleaner Memory KB|背景清除器所知道的記憶體數量，以 KB 為單位  (可壓縮的清除器記憶體 + 不可壓縮的清除器記憶體)。|  
|Memory Usage KB|伺服器處理序用於計算清除器記憶體價格的記憶體使用量。  等於計數器 Process\PrivateBytes 加上記憶體對應的資料大小，忽略 xVelocity 記憶體中分析引擎 (VertiPaq) 在超出 xVelocity 引擎記憶體限制外對應或配置的任何記憶體。|  
|Memory Limit Low KB|來自組態檔的記憶體下限。|  
|Memory Limit High KB|來自組態檔的記憶體上限。|  
|AggCacheKB|目前配置給彙總快取的記憶體，以 KB 為單位。|  
|Quota KB|目前的記憶體配額，以 KB 為單位。  記憶體配額也就是指授與使用的記憶體，或是保留的記憶體。|  
|Quota Blocked|在釋放其他記憶體配額之前，目前已封鎖的配額要求數目。|  
|Filestore KB|目前配置給 Filestore 的記憶體 (檔案快取)，以 KB 為單位。|  
|Filestore Page Faults/sec|Filestore 頁面錯誤的速率。|  
|Filestore Reads/sec|Filestore 頁面讀取/秒。|  
|Filestore KB Reads/sec|Filestore KB 讀取/秒。|  
|Filestore Writes/sec|每秒寫入 Filestore 的頁面數。寫入為非同步。|  
|Filestore KB Write/sec|每秒寫入 Filestore 的 KB。寫入為非同步。|  
|Filestore IO Errors/sec|Filestore IO 錯誤率。|  
|Filestore IO Errors|Filestore IO 錯誤總計。|  
|Filestore Clock Pages Examined/sec|背景清除器基於收回的考量而檢查頁面的速率。|  
|Filestore Clock Pages HaveRef/sec|背景清除器檢查具有目前參考計數之頁面 (目前在使用中) 的速率。|  
|Filestore Clock Pages Valid/sec|背景清除器檢查可做為收回之有效候選頁面的速率。|  
|Filestore Memory Pinned KB|目前 Filestore 記憶體 Pin，以 KB 為單位。|  
|In-memory Dimension Property File KB|記憶體中維度屬性檔的目前大小，以 KB 為單位。|  
|In-memory Dimension Property File KB/sec|寫入記憶體中維度屬性檔的速率，以 KB 為單位。|  
|Potential In-memory Dimension Property File KB|記憶體中維度屬性檔的潛在大小，以 KB 為單位。|  
|Dimension Property Files|維度屬性檔的數目。|  
|In-memory Dimension Index (Hash) File KB|目前記憶體中的維度索引 (雜湊) 檔的大小，以 KB 為單位。|  
|In-memory Dimension Index (Hash) File KB/sec|寫入記憶體中維度索引 (雜湊) 檔的速率，以 KB 為單位。|  
|Potential In-memory Dimension Index (Hash) File KB|記憶體中維度索引 (雜湊) 檔的潛在大小，以 KB 為單位。|  
|Dimension Index (Hash) Files|維度索引 (雜湊) 檔的數目。|  
|In-memory Dimension String File KB|記憶體中維度字串檔的目前大小，以 KB 為單位。|  
|In-memory Dimension String File KB/sec|寫入記憶體中維度字串檔的速率，以 KB 為單位。|  
|Potential In-memory Dimension String File KB|記憶體中維度字串檔的潛在大小，以 KB 為單位。|  
|Dimension String Files|維度字串檔的數目。|  
|In-memory Map File KB|記憶體中對應檔的目前大小，以 KB 為單位。|  
|In-memory Map File KB/sec|寫入記憶體中對應檔的速率，以 KB 為單位。|  
|Potential In-memory Map File KB|記憶體中對應檔的潛在大小，以 KB 為單位。|  
|Map Files|對應檔的數目。|  
|In-memory Aggregation Map File KB|記憶體中彙總對應檔的目前大小，以 KB 為單位。|  
|In-memory Aggregation Map File KB/sec|寫入記憶體中彙總對應檔的速率，以 KB 為單位。|  
|Potential In-memory Aggregation Map File KB|可能在記憶體中的彙總對應檔的大小，以 KB 為單位。|  
|Aggregation Map Files|彙總對應檔的數目。|  
|In-memory Fact Data File KB|目前記憶體中的事實資料檔的大小，以 KB 為單位。|  
|In-memory Fact Data File KB/sec|寫入記憶體中事實資料檔的 KB 速率。|  
|Potential In-memory Fact Data File KB|可能在記憶體中的事實資料檔的大小，以 KB 為單位。|  
|Fact Data Files|事實資料檔的數目。|  
|In-memory Fact String File KB|目前記憶體中的事實字串檔的大小，以 KB 為單位。|  
|In-memory Fact String File KB/sec|寫入記憶體中事實字串檔的速率，以 KB 為單位。|  
|Potential In-memory Fact String File KB|可能在記憶體中的事實字串檔的大小，以 KB 為單位。|  
|Fact String Files|事實字串檔的數目。|  
|In-memory Fact Aggregation File KB|記憶體中事實彙總檔的目前大小，以 KB 為單位。|  
|In-memory Fact Aggregation File KB/sec|寫入記憶體中事實彙總檔的速率，以 KB 為單位。|  
|Potential In-memory Fact Aggregation File KB|可能在記憶體中的事實彙總檔的大小，以 KB 為單位。|  
|Fact Aggregation Files|事實彙總檔的數目。|  
|In-memory Other File KB|目前記憶體中的其他檔案的大小，以 KB 為單位。|  
|In-memory Other File KB/sec|寫入記憶體中其他檔案的速率，以 KB 為單位。|  
|Potential In-memory Other File KB|可能在記憶體中的其他檔案的大小，以 KB 為單位。|  
|Other Files|其他檔案的數目。|  
|VertiPaq Paged KB|用於記憶體中資料的分頁記憶體 (千位元組)。|  
|VertiPaq Nonpaged KB|記憶體中引擎所使用的工作集中鎖定的記憶體 (千位元組)。|  
|VertiPaq Memory-Mapped KB|用於記憶體中資料的可分頁記憶體 (千位元組)。|  
|Memory Limit Hard KB|組態檔中的固定記憶體限制。|  
|Memory Limit VertiPaq KB|來自組態檔的記憶體中限制。|  
  
###  <a name="bkmk_ProactiveCaching"></a> 主動式快取  
 與 Microsoft Analysis Services 主動式快取相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Notifications/sec|來自關聯式資料庫的通知速率。|  
|Processing Cancellations/sec|通知所引起的處理取消速率。|  
|Proactive Caching Begin/sec|主動式快取開始的速率。|  
|Proactive Caching Completion/sec|主動式快取完成的速率。|  
  
###  <a name="bkmk_ProcAggregations"></a> Processing Aggregations  
 與 Microsoft Analysis Services 處理 MOLAP 資料檔之彙總相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current partitions|目前正在處理的資料分割數目。|  
|Total partitions|已處理的資料分割總計 (成功或失敗)。|  
|Memory size rows|目前在記憶體中的彙總大小。  這是預估的計數。|  
|Memory size bytes|目前在記憶體中的彙總大小。  這是預估的計數。|  
|Rows merged/sec|資料列合併或插入至彙總的速率。|  
|Rows created/sec|建立彙總資料列的速率。|  
|Temp file rows written/sec|將資料列寫入至暫存檔的速率。  彙總超過記憶體限制時會寫入暫存檔。|  
|Temp file bytes written/sec|將位元組寫入至暫存檔的速率。  彙總超過記憶體限制時會寫入暫存檔。|  
  
###  <a name="bkmk_ProcIndexes"></a> Processing Indexes  
 與 Microsoft Analysis Services 處理 MOLAP 資料檔之索引相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current partitions|目前正在處理的資料分割數目。|  
|Total partitions|已處理的資料分割總計 (成功或失敗)。|  
|Rows/sec|使用從 MOLAP 檔案資料列建立索引的速率。|  
|總計資料列|來自 MOLAP 檔案、用來建立索引的資料列總計。|  
  
###  <a name="bkmk_Processing"></a> Processing  
 與 Microsoft Analysis Services 處理資料相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Rows read/sec|從所有關聯式資料庫讀取資料列的速率。|  
|Total rows read|從所有關聯式資料庫讀取的資料列計數。|  
|Rows converted/sec|處理期間資料列轉換的速率。|  
|Total rows converted|處理期間資料列轉換的計數。|  
|Rows written/sec|處理期間資料列寫入的速率。|  
|Total rows written|處理期間資料列寫入的計數。|  
  
###  <a name="bkmk_StorageEngineQuery"></a> Storage Engine Query  
 與 Microsoft Analysis Services 儲存引擎查詢相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Current measure group queries|目前正在進行的量值群組查詢數目。|  
|Measure group queries/sec|量值群組查詢的速率|  
|Total measure group queries|量值群組查詢總數。|  
|Current dimension queries|目前正在進行的維度查詢數目。|  
|Dimension queries/sec|維度查詢的速率。|  
|Total dimension queries.|維度查詢的總數。|  
|Queries answered/sec|回應查詢的速率。|  
|Total queries answered|已回應的查詢總數。|  
|Bytes sent/sec|回應查詢時，由伺服器傳送位元組至用戶端的速率。|  
|Total bytes sent|回應查詢時，由伺服器傳送至用戶端的位元組總計。|  
|Rows sent/sec|由伺服器傳送資料列至用戶端的速率。|  
|Total rows sent|由伺服器傳送至用戶端的資料列總計。|  
|Queries from cache direct/sec|直接從快取回應查詢的速率。|  
|Queries from cache filtered/sec|篩選現有快取項目來回應查詢的速率。|  
|Queries from file/sec|從檔案回應查詢的速率。|  
|Total queries from cache direct|直接從快取衍生的查詢總數。  請注意，這是依每個資料分割。|  
|Total queries from cache filtered|篩選現有快取項目來回應查詢的總計。|  
|Total queries from file|從檔案回應的查詢總數。|  
|Map reads/sec|正在使用對應檔的邏輯讀取作業數目。|  
|Map bytes/sec|從對應檔讀取的位元組。|  
|Data reads/sec|正在使用資料檔的邏輯讀取作業數目。|  
|Data bytes/sec|從資料檔讀取的位元組。|  
|Avg time/query|每個查詢的平均時間，以毫秒計。  回應時間是依據上一次的計數測量到回應查詢的時間。|  
|Network round trips/sec|網路往返的速率。  這包含所有的用戶端/伺服器通訊。|  
|Total network round trips|網路往返總計。  這包含所有的用戶端/伺服器通訊。|  
|Flat cache lookups/sec|一般快取查閱率。  這包括全域、工作階段和查詢範圍的一般快取。|  
|Flat cache hits/sec|一般快取點擊率。  這包括全域、工作階段和查詢範圍的一般快取。|  
|Calculation cache lookups/sec|計算快取查閱率。  這包括全域、工作階段和查詢範圍的計算快取。|  
|Calculation cache hits/sec|計算快取點擊率。  這包括全域、工作階段和查詢範圍的計算快取。|  
|Persisted cache lookups/sec|永續性快取查閱率。  永續性快取是用 MDX 指令碼 CACHE 陳述式建立的。|  
|Persisted cache hits/sec|永續性快取點擊率。  永續性快取是用 MDX 指令碼 CACHE 陳述式建立的。|  
|Dimension cache lookups/sec|維度快取查閱率。|  
|Dimension cache hits/sec|維度快取點擊率。|  
|Measure group cache lookups/sec|量值群組快取查閱率。|  
|Measure group cache hits/sec|量值群組快取點擊率。|  
|Aggregation lookups/sec|彙總查閱率。|  
|Aggregation hits/sec|彙總叫用率。|  
  
###  <a name="bkmk_Threads"></a> Threads  
 與 Microsoft Analysis Services 執行緒相關的統計資料。  
  
|計數器|說明|  
|-------------|-----------------|  
|Short parsing idle threads|簡短剖析執行緒集區中的閒置執行緒數目。|  
|Short parsing busy threads|簡短剖析執行緒集區中的忙碌執行緒數目。|  
|Short parsing job queue length|簡短剖析執行緒集區佇列中的作業數目。|  
|Short parsing job rate|透過簡短剖析執行緒集區的作業速率。|  
|Long parsing idle threads|完整剖析執行緒集區中的閒置執行緒數目。|  
|Long parsing busy threads|完整剖析執行緒集區中的忙碌執行緒數目。|  
|Long parsing job queue length|完整剖析執行緒集區佇列中的作業數目。|  
|Long parsing job rate|透過完整剖析執行緒集區的作業速率。|  
|Query pool idle threads|查詢執行緒集區中的閒置執行緒數目。|  
|Query pool busy threads|查詢執行緒集區中的忙碌執行緒數目。|  
|Query pool job queue length|查詢執行緒集區佇列中的作業數目。|  
|Query pool job rate|透過查詢執行緒集區的作業速率。|  
|Processing pool idle non-I/O threads|處理執行緒集區中專供非 I/O 作業使用的閒置執行緒數目。|  
|Processing pool busy non-I/O threads|處理執行緒集區中執行非 I/O 作業的執行緒數目。|  
|Processing pool job queue length|處理執行緒集區佇列中的非 I/O 作業數目。|  
|Processing pool job rate|透過處理執行緒集區的非 I/O 作業速率。|  
|Processing pool idle I/O job threads|處理執行緒集區中 I/O 作業的閒置執行緒數目。|  
|Processing pool busy I/O job threads|處理執行緒集區中執行 I/O 作業的執行緒數目。|  
|Processing pool I/O job queue length|處理執行緒集區佇列中的 I/O 作業數目。|  
|Processing pool I/O job completion rate|透過處理執行緒集區的 I/O 作業速率。|  
  
  

