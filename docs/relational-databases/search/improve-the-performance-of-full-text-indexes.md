---
title: 改善全文檢索索引的效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], full-text search
- full-text queries [SQL Server], performance
- crawls [full-text search]
- full-text indexes [SQL Server], performance
- full-text search [SQL Server], performance
- batches [SQL Server], full-text search
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8d948862b4bf39d7970aae4a0b174feb6dc21639
ms.sourcegitcommit: 0510e1eb5bcb994125cbc8b60f8a38ff0d2e2781
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2019
ms.locfileid: "57736793"
---
# <a name="improve-the-performance-of-full-text-indexes"></a>改善全文檢索索引的效能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
本主題描述全文檢索索引和查詢效能降低的一些常見原因。 它也會提供一些建議，以減少這些問題的發生並改善效能。
  
##  <a name="causes"></a> Common causes of performance issues
### <a name="hardware-resource-issues"></a>硬體資源問題
全文檢索索引與全文檢索查詢的效能受到硬體資源的影響，例如記憶體、磁碟速度、CPU 速度與電腦架構。  

全文檢索索引效能降低的主要原因即為硬體資源的限制。  
  
-   **CPU**。 如果篩選背景程式主機處理序 (fdhost.exe) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序 (sqlservr.exe) 的 CPU 使用率接近 100%，表示 CPU 就是瓶頸。  
  
-   **記憶體**。 如果實體記憶體不足，記憶體就可能是瓶頸。  

-   **磁碟**。 如果平均磁碟等候佇列長度超過磁碟讀寫頭數目的兩倍，表示磁碟有瓶頸。 主要的解決方式是建立和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案和記錄分開的全文檢索目錄。 請將記錄、資料庫檔案和全文檢索目錄放在不同的磁碟上。 安裝較快速的磁碟以及使用 RAID 也有助於改善索引效能。  
  
    > [!NOTE]  
    >  從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，全文檢索引擎就可以使用 AWE 記憶體，因為全文檢索引擎屬於 sqlservr.exe 程序的一部分。  

### <a name="full-text-batching-issues"></a>全文檢索批次問題
 如果系統沒有任何硬體瓶頸，全文檢索搜尋的索引效能大多取決於下列條件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立全文檢索批次所花的時間。  
  
-   篩選背景程式可以取用這些批次的速度。  

### <a name="full-text-index-population-issues"></a>全文檢索索引母體擴展問題
-   **母體擴展的類型**. 與完整母體擴展不同，累加、手動和自動變更追蹤母體擴展並非設計來最大化硬體資源以達到更快的速度。 因此，本主題中的微調建議可能無法在全文檢索索引使用累加、手動或自動變更追蹤母體擴展時增強其效能。  
  
-   **主要合併**. 完成母體擴展後會觸發最後的合併程序，將索引片段合併成一個主要的全文檢索索引。 如此可提升查詢的效能，因為只需要查詢一個主索引而不需查詢數個索引片段，而且可使用較佳的計分系統來排定關聯順序。 不過，主要合併過程可能需要密集的磁碟 I/O，因為合併索引片段時必須讀寫大量的資料，但是不會阻止傳入的查詢。  
  
    主要合併大量資料可能會建立長時間執行的交易，並在檢查點期間延遲截斷交易記錄。 在此情況下，交易記錄可能會在完整復原模式下明顯成長。 最佳作法是確認您的異動記錄包含足夠的空間，可供長時間執行的異動使用，然後在使用完整復原模式的資料庫中，辨識大型全文檢索索引。 如需詳細資訊，請參閱 [管理交易記錄檔的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)。  
  
##  <a name="tuning"></a> 微調全文檢索索引的效能  
若要將全文檢索索引的效能發揮至極限，請實作下列最佳作法：  
  
-   請將 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) '**max full-text crawl range**' 設為系統上的 CPU 數目，以使用所有處理器或核心來發揮最大效能。 此組態選項的相關資訊，請參閱 [全文檢索搜耙最大範圍伺服器組態選項](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)。  
  
-   請確定基底資料表具有叢集索引。 對叢集索引的第一個資料行使用整數資料類型。 避免在叢集索引的第一個資料行使用 GUID。 叢集索引的多重範圍母體擴展可能會產生最高的母體擴展速度。 我們建議當做全文檢索索引鍵的資料行應該是整數資料類型。  
  
-   請使用 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 陳述式來更新基底資料表的統計資料。 更重要的是，請更新叢集索引上的統計資料或完整母體擴展的全文檢索索引鍵。 這有助於多重範圍母體擴展在資料表上產生良好的資料分割。  
  
-   在大型的多重 CPU 電腦上執行完整母體擴展之前，建議您設定 [最大伺服器記憶體] 值來暫時限制緩衝集區的大小，以便保留足夠的記憶體供 fdhost.exe 處理序和作業系統使用。 如需詳細資訊，請參閱本主題稍後的＜估計篩選背景程式主機處理序 (fdhost.exe) 的記憶體需求＞一節。

-   如果您使用根據時間戳記資料行的累加母體擴展，請在 [時間戳記] 資料行上建置次要索引以改善累加母體擴展的效能。  
  
##  <a name="full"></a> 為完整母體擴展的效能進行疑難排解  
### <a name="review-the-full-text-crawl-logs"></a>檢閱全文檢索編目記錄檔
 若要協助診斷效能問題，請查看全文檢索編目記錄檔。
 
搜耙發生錯誤時，「全文檢索搜尋」搜耙記錄功能會建立並維護搜耙記錄檔，此記錄檔是一個純文字檔。 每個搜耙記錄檔都對應至特定的全文檢索目錄。 所指定執行個體 (在此範例中為預設執行個體) 的編目記錄檔預設位於 `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG` 資料夾中。
 
搜耙記錄檔會遵循下列命名結構：  
  
`SQLFT<DatabaseID\><FullTextCatalogID\>.LOG[<n\>]`
  
以下是編目記錄檔名稱的變動部分。
-   \<**DatabaseID**> - 資料庫的識別碼。 <**dbid**> 是開頭為零的五位數數字。  
-   <**FullTextCatalogID**> - 全文檢索目錄識別碼。 \<**catid**> 是開頭為零的五位數數字。  
-   <**n**> - 是一個整數，指示相同全文檢索目錄的編目記錄檔數目。  
  
 例如，`SQLFT0000500008.2` 是指資料庫識別碼 = 5 而且全文檢索目錄識別碼 = 8 之資料庫的編目記錄檔。 位於檔案名稱結尾的 2 表示此資料庫/目錄組有兩個搜耙記錄檔。  

### <a name="check-physical-memory-usage"></a>檢查實體記憶體使用量  
 在全文檢索母體擴展期間，fdhost.exe 或 sqlservr.exe 可能會造成記憶體不足或用完記憶體。
-   如果全文檢索搜耙記錄檔顯示 fdhost.exe 經常重新啟動或者傳回錯誤碼 8007008，就表示其中一個處理序用完記憶體。
-   如果 fdhost.exe 正在產生傾印 (尤其是在大型的多重 CPU 電腦上)，它可能會用完記憶體。  
-   若要取得全文檢索編目所使用之記憶體緩衝區的資訊，請參閱 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)。  
  
 記憶體過低或記憶體不足問題的可能原因如下︰  
  
-   **記憶體不足**。 如果完整母體擴展期間可用的實體記憶體數量為零，表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 緩衝集區可能耗用系統上的大部分實體記憶體。  
  
     sqlservr.exe 處理序嘗試擷取緩衝集區的所有可用記憶體，最多至已設定的最大伺服器記憶體。 如果 [最大伺服器記憶體] 配置太大，fdhost.exe 處理序可能會發生記憶體不足以及無法配置共用記憶體的狀況。  
  
     您可以透過適當設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 緩衝集區的 [最大伺服器記憶體] 來解決此問題。 如需詳細資訊，請參閱本主題稍後的＜估計篩選背景程式主機處理序 (fdhost.exe) 的記憶體需求＞一節。 減少全文檢索索引所使用的批次大小可能也會有所幫助。  

-   **記憶體競爭**。 在多重 CPU 電腦上進行全文檢索母體擴展期間，fdhost.exe 或 sqlservr.exe 之間可能會發生競爭緩衝集區記憶體的情況。 所產生的共用記憶體不足會導致批次重試、記憶體壓力以及 fdhost.exe 處理序的傾印。  

-   **分頁問題**。 分頁檔大小不足 (例如，在具有成長受限之小型分頁檔的系統上) 可能也會導致 fdhost.exe 或 sqlservr.exe 用完記憶體。 如果搜耙記錄檔並未指出任何記憶體相關的失敗，可能是由於過度分頁而導致效能降低。  
  
### <a name="estimate-the-memory-requirements-of-the-filter-daemon-host-process-fdhostexe"></a>估計篩選背景程式主機處理序 (fdhost.exe) 的記憶體需求  
 fdhost.exe 處理序進行母體擴展所需的記憶體數量主要取決於它所使用的全文檢索搜耙範圍數目、內部共用記憶體 (ISM) 的大小，以及 ISM 執行個體的數目上限。  
  
 您可以使用下列公式來概略估計篩選背景程式主機所耗用的記憶體數量 (以位元組為單位)：  
  
`number_of_crawl_ranges * ism_size * max_outstanding_isms * 2`  
  
 上述公式中變數的預設值如下所示：  
  
|**變數**|**預設值**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|CPU 的數目|  
|*ism_size*|1 MB (適用於 x86 電腦)<br /><br /> 4 MB、8 MB 或 16MB (適用於 x64 電腦，端視實體記憶體總數而定)|  
|*max_outstanding_isms*|25 (適用於 x86 電腦)<br /><br /> 5 (適用於 x64 電腦)|  
  
 下表將列出有關如何估計 fdhost.exe 記憶體需求的指導方針。 此表中的公式會使用下列值：  
  
-   *F*，這是 fdhost.exe 所需記憶體的估計 (以 MB 為單位)。  
  
-   *T*，這是系統上可用的實體記憶體總計 (以 MB 為單位)。  
  
-   *M*，這是最佳 [最大伺服器記憶體] 設定。  
  
如需下列公式的基本資訊，請參閱資料表後面的附註。  
  
|平台|以 MB 為單位估計 fdhost.exe 記憶體需求-*F*^1|計算最大伺服器記憶體的公式-*M*^2|  
|--------------|-----------------------------------------------------------|-----------------------------------------------------|  
|x86|*F* = *編目範圍數目* * 50|*M* =minimum(*T*, 2000) - F - 500|  
|x64|*F* = *編目範圍數目* * 10 * 8|*M* = *T* - *F* - 500|  

**公式的附註**
1.  如果有多個完整母體擴展正在進行中，請個別計算每個母體擴展的 fdhost.exe 記憶體需求，例如 *F1*、*F2* 等。 然後將 *M* 計算為 _T_**-** sigma **(**_F_i **)**。  
2.  500 MB 是系統中其他處理序所需記憶體的估計值。 如果系統正在進行其他工作，請據此增加這個值。  
3.  。*ism_size* 在 x64 平台假設為 8 MB。  
  
 #### <a name="example-estimate-the-memory-requirements-of-fdhostexe"></a>範例估計 fdhost.exe 的記憶體需求  
  
 這個範例適用於具有 8GM RAM 和 4 個雙核心處理器的 64 位元電腦。 第一個計算會估計 fdhost.exe 所需的記憶體-*F*。 搜耙範圍的數目是 `8`。  
  
 `F = 8*10*8=640`  
  
 下一個計算會取得**最大伺服器記憶體**-*M* 的最佳值。 此系統上可用的實體記憶體總計-*T* (以 MB 為單位) 為 `8192`。  
  
 `M = 8192-640-500=7052`  
  
 #### <a name="example-setting-max-server-memory"></a>範例設定最大伺服器記憶體  
  
 此範例使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 和 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，將 [最大伺服器記憶體] 設為上述範例中計算的 *M* 值，即 `7052`：  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
如需設定伺服器記憶體選項的詳細資訊，請參閱[伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
### <a name="check-cpu-usage"></a>檢查 CPU 使用量  
當平均 CPU 耗用率大約低於 30% 時，完整母體擴展的效能並非最佳化。 以下是影響 CPU 耗用率的一些因素。  
  
-   分頁等候時間很高  
  
     若要了解分頁等候時間是否很高，請執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     下表將說明在此重要的等候類型。  
  
    |等候類型|Description|可能的解決方案|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH (_EX 或 _UP)|這可能表示 IO 瓶頸，而在此情況下，您通常也會看見很高的平均磁碟佇列長度。|將全文檢索索引移至不同磁碟上的不同檔案群組可能有助於減少 IO 瓶頸。|  
    |PAGELATCH_EX (或 _UP)|這可能表示嘗試寫入相同資料庫檔案的執行緒之間存在大量競爭的情況。|將檔案加入至全文檢索索引所在的檔案群組可能有助於減少這類競爭的情況。|  
  
     如需詳細資訊，請參閱 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。  
  
-   掃描基底資料表的效率不足  
  
     完整母體擴展會掃描基底資料表來產生批次。 在下列狀況中，這種資料表掃描作業可能會沒有效率：  
  
    -   如果基底資料表中正在進行全文檢索索引之資料列外資料行的百分比很高，掃描基底資料表來產生批次的作業可能就是瓶頸。 在此情況下，使用 **varchar (max)** 或 **nvarchar (max)** 移動較小的 in-row 資料會有幫助。  
  
    -   如果基底資料表嚴重片段化，掃描可能就沒有效率。 如需計算資料列外資料和索引片段的相關資訊，請參閱 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 和 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)。  
  
         若要減少片段，您可以重新組織或重建叢集索引。 如需詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
##  <a name="filters"></a> 為緩慢編製文件索引進行疑難排解

> [!NOTE]
> 本節描述只會影響客戶的問題，而客戶會編製內嵌其他文件類型之文件 (例如 Microsoft Word 文件) 的索引。

擴展全文檢索索引時，全文檢索引擎會使用兩種篩選：多執行緒篩選和單一執行緒篩選。
-   某些文件 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文件) 是使用多執行緒篩選進行篩選。
-   其他文件 (例如 Adobe Acrobat Portable Document Format (PDF) 文件) 則是使用單一執行緒篩選進行篩選。  
  
 基於安全性理由，篩選是由篩選背景程式主機處理序載入。 伺服器執行個體會針對所有多執行緒篩選使用多執行緒處理序，而針對所有單一執行緒篩選使用單一執行緒處理序。 當使用多執行緒篩選的文件包含使用單一執行緒篩選的內嵌文件時，全文檢索引擎就會針對內嵌文件啟動單一執行緒處理序。 例如，如果遇到包含 PDF 文件的 Word 文件，全文檢索引擎就會針對 Word 內容啟動多執行緒處理序，而針對 PDF 內容啟動單一執行緒處理序。 不過，單一執行緒篩選在此環境下可能無法正常運作，而且可能會使篩選處理序不穩定。 在經常會有這類內嵌的特定情況下，不穩定可能會導致處理序損毀。 發生這個狀況時，全文檢索引擎就會將任何失敗的文件 (例如，包含內嵌 PDF 內容的 Word 文件) 重新路由傳送至單一執行緒篩選處理序。 如果經常發生重新路由傳送的狀況，則會導致全文檢索索引處理序的效能降低。  
  
若要解決這個問題，請將容器文件 (在此範例中是 Word 文件) 的篩選標示成單一執行緒篩選。 若要將篩選標示成單一執行緒篩選，請將篩選的 **ThreadingModel** 登錄值設為 **Apartment Threaded**。 如需有關單一執行緒 Apartment 的詳細資訊，請參閱 [Understanding and Using COM Threading Models](https://go.microsoft.com/fwlink/?LinkId=209159)(了解與使用 COM 執行緒模型) 技術白皮書。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [全文檢索搜耙最大範圍伺服器組態選項](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)   
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)   
 [疑難排解全文檢索索引](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
  
