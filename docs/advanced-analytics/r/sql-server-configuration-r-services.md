---
title: "SQL Server 組態 (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b65eb600060a5d7e12d3095d145a23f5b8b3290b
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-configuration-for-use-with-r"></a>使用 R 與 SQL Server 組態

本文是說明兩個案例研究為基礎的 R 服務的效能最佳化的數列中的第二個。  本文章提供用來執行 SQL Server R Services 的電腦的硬體與網路設定的相關指引。 它也包含有關如何設定 SQL Server 執行個體、 資料庫或資料表用於方案中的相關資訊。 使用 SQL Server 中的 NUMA 模糊的硬體和資料庫最佳化的關係之間的線，因為第三個區段會討論詳細 CPU 分配和資源控管。

> [!TIP]
> 如果您不熟悉 SQL Server，我們強烈建議您也檢閱 SQL Server 效能微調指南：[監視和微調效能](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬體最佳化

伺服器電腦的最佳化，請務必確定您有執行外部指令碼資源。 資源有限時，您可能會看到這類的徵兆：

- 工作執行已延後或取消排列優先順序的其他資料庫作業
- 超過錯誤 「 配額 」 導致 R 指令碼終止而不需要完成
- 載入至 R 記憶體截斷，結果不完整的資料。

### <a name="memory"></a>記憶體

電腦上可用的記憶體數量會對進階分析演算法的效能產生很大的影響。 使用 SQL 計算內容時，記憶體不足可能會影響平行處理原則程度。 它也會影響可處理的區塊大小 (每次讀取作業的資料列)，以及可同時支援的工作階段數目。

強烈建議至少 32 GB。 如果您有多個 32 gb 的記憶體可用時，您可以設定要用於每個讀取作業中的多個資料列，以改善效能的 SQL 資料來源。

您也可以管理執行個體所使用的記憶體。 根據預設，SQL Server 會優先於外部指令碼處理程序，當配置記憶體時。 在預設安裝中的 R 服務，可用記憶體的 20%配置給。

通常這是不夠的資料科學工作，但您要在既未佔用的記憶體的 SQL server。 您應該試驗和微調資料庫引擎、 相關的服務和外部指令碼，了解最佳的設定不同的案例之間的記憶體配置。

繼續比對模型中，外部指令碼的用途是大量且沒有任何其他資料庫引擎服務執行中;因此，資源配置給外部指令碼已增加到 70%，此為指令碼效能的最佳組態。

### <a name="power-options"></a>電源選項

在 Windows 作業系統上**高效能**應使用電源選項。 使用不同的電源設定會導致效能降低或不一致時使用 SQL Server。

### <a name="disk-io"></a>磁碟 IO

定型和預測使用 R 服務的工作本質上是 IO 繫結，並儲存資料庫的磁碟速度而定。 可能有助於更快速的磁碟機，例如固態硬碟 (SSD)。

磁碟 IO 也會受到存取磁碟的其他應用程式所影響：例如，其他用戶端對資料庫的讀取作業。 磁碟 IO 效能也會受到使用中檔案系統上的設定所影響，例如，檔案系統所使用的區塊大小。

如果有多個磁碟機，因此，要求的 database engine 的 SQL Server 不同的磁碟上的資料庫無法到達相同的磁碟的存放區的要求儲存在資料庫中的資料。

執行 RevoScaleR 分析函數以在定型期間使用多個反覆項目時，磁碟 IO 也會大幅影響效能。 例如， `rxLogit`， `rxDTree`， `rxDForest`，和`rxBTrees`所有使用多個反覆項目。 SQL Server 資料來源時，這些演算法會使用已最佳化，以擷取資料的暫存檔案。 系統會在工作階段完成之後自動清除這些檔案。 具有讀取/寫入作業的高效能磁碟，可大幅改善整體的經過時間，這些演算法。

> [!NOTE]
> 舊版的 R 服務所需 8.3 檔案名稱支援 Windows 作業系統上。 Service Pack 1 之後，已提高此限制。 不過，您可以使用 fsutil.exe 來判斷磁碟機是否支援 8.3 檔案名稱，或如果沒有啟用支援。

### <a name="paging-file"></a>分頁檔

Windows 作業系統會使用分頁檔來管理損毀傾印，以及用來儲存虛擬記憶體分頁。 如果您注意到過度分頁，請考慮增加機器上的實體記憶體。 雖然有更多實體記憶體並不會消除分頁，但它確實可以降低分頁的需求。

分頁檔儲存所在的磁碟速度也會影響效能。 將分頁檔儲存於 SSD 上，或跨多個 SSD 使用多個分頁檔，均可改善效能。

如需調整分頁檔的大小資訊，請參閱[如何判斷適當的分頁檔大小為 64 位元版本的 Windows](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>在執行個體或資料庫層級的最佳化

最佳化 SQL Server 執行個體是要能夠有效率地執行外部指令碼的索引鍵。

> [!NOTE]
> 最佳的設定不同的大小和類型的資料，您將用於計分或定型模型的資料行數目。
> 
> 您可以檢閱結果的最後一個發行項中的特定最佳化：[效能微調-案例研究結果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 範例指令碼，請參閱個別[GitHub 儲存機制](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>資料表壓縮

IO 效能通常可以提升使用壓縮或單欄式資料存放區。 一般而言，資料會經常重複在數個資料行在資料表中，好讓壓縮資料時使用的資料行存放區會利用這些重複項目。

資料行存放區可能不是如果有多個資料表中，插入效率，但如果資料是靜態或只在不常變更，是不錯的選擇。 如果單欄式存放區不適用，則對資料列主要資料表啟用壓縮，可用來改善 IO。

如需詳細資訊，請參閱下列文件：

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>記憶體最佳化的資料表

Screen 鍵則記憶體已不再現代電腦的問題。 繼續改善硬體規格，它是相對較容易到達良好值的 RAM。 不過，在相同的時間，則會被比以往，更快速地產生資料，而且必須與低度延遲處理資料。

記憶體最佳化資料表會代表一種解決方案，，他們會利用進階處理巨量資料的問題的電腦上提供大量的記憶體。 記憶體最佳化資料表主要是位在記憶體中，使資料是從讀取和寫入記憶體。 持久性，資料表的第二個副本保留在磁碟上，資料只會從磁碟讀取資料庫復原期間。

如果您需要讀經常寫入資料表，記憶體最佳化資料表會協助高延展性和低度延遲。  在繼續比對案例中，使用的記憶體最佳化的資料表，我們從資料庫讀取所有的恢復功能，並將它們儲存在主要記憶體中，以符合新的工作機會。 這會大幅降低磁碟 IO。

使用程序從多個並行批次預測回寫到資料庫的記憶體最佳化資料表所達成進一步提高效能。 啟用低度延遲要使用的記憶體最佳化資料表的 SQL Server 上資料表的讀取和寫入。

在開發期間伺服器也順暢的體驗。 建立資料庫的同時建立持久性記憶體最佳化的資料表。 因此，開發使用相同的工作流程，不論資料儲存位置。

### <a name="processor"></a>處理器

SQL Server 可以執行平行工作所使用電腦; 上的可用核心數目可供使用，更多核心的較佳的效能。 繫結的 IO 作業可能無法協助增加核心數目，而受限於 CPU 的演算法權益從具有許多核心更快速的 Cpu。

因為伺服器通常由使用多個使用者同時，資料庫管理員必須決定，理想的支援尖峰工作負載計算所需的核心數目。

### <a name="resource-governance"></a>資源管理

在支援資源管理員的版本中，您可以指定特定工作負載會配置一定數量的 Cpu 使用資源集區。 您也可以管理配置給特定的工作負載的記憶體數量。

SQL Server 中的資源管理機制可讓您集中監視和控制 r 和 SQL Server 所使用的各種資源例如，您可能會配置資料庫引擎，以確保服務能隨時執行即便暫時性較重的工作負載之核心半可用的記憶體。

記憶體耗用量外部指令碼的預設值是限制為 20%的總記憶體可供 SQL Server 本身。 若要確保依賴 資料庫伺服器的所有工作都不會嚴重都影響長時間執行的 R 作業所預設會套用此限制。 不過，資料庫管理員可以變更這些限制。 在許多情況下，不適合用來支援嚴重的機器學習服務工作負載的 20%的限制。

支援的組態選項都**MAX_CPU_PERCENT**， **MAX_MEMORY_PERCENT**，和**MAX_PROCESSES**。 若要檢視目前的設定，請使用此陳述式：`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果伺服器主要用於 R 服務，可能很有幫助 MAX_CPU_PERCENT 增加至 40%或 60%。

-  如果多個 R 工作階段必須使用相同的伺服器在相同的時間，就應增加所有三項設定。

若要變更已配置的資源值，請使用 T-SQL 陳述式。

+ 這個陳述式會設定為 40%的記憶體使用量：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 這個陳述式會設定所有三個可設定的值：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果您變更記憶體、 CPU 或最大的處理序設定，並想要立即套用設定，執行此陳述式：`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>軟體 NUMA 硬體 NUMA 和 CPU 親和性

使用 SQL Server 時當成計算內容，您可以有時達到更佳的效能微調 NUMA 與處理器親和性的相關設定。 

系統與_硬體 NUMA_有多個系統匯流排，每一個服務一小組處理器。 每一個 CPU 可以存取以一致的方式與其他群組相關聯的記憶體。 每一個群組就稱為 NUMA 節點。 如果您有硬體 NUMA，它可設定為使用交錯記憶體，而非 NUMA。 在此情況下，Windows，因此 SQL Server 會不將它視為 NUMA。 

您可以執行下列查詢來尋找 SQL Server 可用的記憶體節點的數目：

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查詢傳回單一記憶體節點 （節點 0），您沒有硬體 NUMA，或硬體設定為交錯的 (非 NUMA)。 SQL Server 也會忽略硬體 NUMA 時有四個或更少的 Cpu，或如果至少一個節點只有一個 CPU。

如果您的電腦有多個處理器，但沒有硬體 NUMA，您也可以使用[NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)至 Cpu 細分為較小的群組。  在 SQL Server 2016 和 SQL Server 2017，啟動 SQL Server 服務時，自動會啟用 NUMA 功能。

啟用 NUMA 時，SQL Server 自動節點會為您管理;不過，若要最佳化特定工作負載，您可以停用_軟性親和性_，然後手動設定軟體 NUMA 節點的 CPU 相似性。 這可讓您更多控制的工作負載指派給哪一個節點，特別是當您使用的支援支援資源監管的 SQL Server 版本。 指定 CPU 相似性，並對齊資源集區使用的 Cpu 群組，可以減少延遲，並確保相關處理序執行於相同的 NUMA 節點內。

設定軟體 NUMA 和 CPU 親和性來支援 R 工作負載的整體程序如下所示：

1. 如果有的話，請啟用軟體 NUMA
2. 定義處理器相關性
3. 建立外部處理序，使用的資源集區[資源管理員](../r/resource-governance-for-r-services.md)
4. 指派[工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)至特定的同質群組

如需詳細資訊，包括程式碼範例，請參閱本教學課程： [SQL 最佳化的秘訣和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他資源：**

+ [SQL Server 中的軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何將軟體 NUMA 節點對應到 Cpu

+ [自動軟體式 NUMA： 只會執行更快的 （Bob 行政區）](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   說明歷程記錄以及實作詳細資料，以較新的多核心伺服器上的效能。

## <a name="task-specific-optimizations"></a>工作特定的最佳化

本節摘要說明和其他測試，來最佳化特定機器學習服務工作負載中這些案例研究、 採用的方法。 常見的工作負載包含模型定型、 擷取特徵和功能工程和計分的各種案例： 單一資料列、 小型的批次和大型批次。

### <a name="feature-engineering"></a>特徵工程

使用 R 的一個痛苦點是通常處理單一 CPU 上。 這是主要的效能瓶頸的許多工作，尤其是功能工程團隊。 在繼續比對方案中，建立 2500 的交叉乘積功能必須與原始 100 功能結合，單獨的功能工程工作。 如果所有項目已在單一的 CPU 上執行，此工作會花費很長的時間。

有多種方式可以改善效能的功能工程團隊。 您可以最佳化您的 R 程式碼，並保留模型建立程序內擷取特徵或將功能工程程序移至 SQL。

- 使用。您定義的函式，並將它做為引數傳遞[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)在定型期間。 如果模型支援平行處理，可以使用多個 Cpu 處理執行功能的工程工作。 資料科學團隊使用這個方法，觀察方面計分時間 16%的效能改進。 不過，這種方法都需要可支援平行化作業，可以使用的平行計畫來執行查詢的模型。

- 使用 R 與 SQL 計算內容。 在隔離的資源可供個別批次的執行與多處理器環境中，您可以藉由隔離用於每個批次中，從資料表擷取資料，並限制在相同的工作負載群組資料的 SQL 查詢來達成更高的效率。 用來隔離批次的方法包含資料分割，並使用 PowerShell 來平行執行個別的查詢。

- 臨機操作的平行執行： 在 SQL Server 計算內容，您可以依賴 SQL database engine 強制盡可能平行執行的而且如果該選項能夠更有效率。

- 使用 T-SQL 如何個別處理序中。 Precomputing 使用 SQL 的功能資料通常會更快。

### <a name="prediction-scoring-in-parallel"></a>預測 （計分），以平行方式

SQL server 的優點之一是它能夠處理大量的資料列，以平行方式。 不是這項優勢因此標示為 「 計分。 通常模型不需要存取所有資料進行評分，因此您可以分割輸入的資料，與每個處理一項工作的工作負載群組。

您也可以傳送輸入的資料為單一查詢，以及 SQL Server 接著會分析該查詢。 如果平行查詢計畫可以建立輸入資料，它會自動指派給節點的資料分割，並也平行方式執行必要的聯結和彙總。

如果您想要如何使用預存程序定義計分的詳細資訊，請參閱範例專案[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)尋找檔案 」 step5_score_for_matching.sql"。 範例指令碼也會追蹤查詢的開始和結束時間，以及寫入至 SQL 主控台的時間，讓您可以評估效能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用資源群組的並行計分

若要向上擴充計分的問題，很好的作法是採用 map-reduce 方法包含數百萬個項目會分成多個批次。 然後，會同時執行多個計分工作。 這個架構中，在批次是在不同的 CPU 集上處理，而且結果會收集並寫回至資料庫。

這正是此案例中使用繼續比對。不過，SQL Server 中的資源管理機制是不可或缺的實作此方法。 藉由建立外部指令碼工作的工作負載群組，您可以路由傳送到不同的處理器群組計分工作 R，並達成更快速的輸送量。

資源管理機制也可協助配置分割 （CPU 和記憶體），以減少工作負載競爭的伺服器上的可用資源。 您可以設定的分類函數來區別不同類型的 R 工作： 例如，您可能會決定，計分呼叫從應用程式一律優先處理，雖然訓練工作有低優先順序。 此資源隔離可能可以改善執行時間，並提供更可預測的效能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 並行計分

如果您決定自行分割資料，您可以使用 PowerShell 指令碼執行多個並行的計分工作。 若要這樣做，請使用 Invoke-sqlcmd 指令程式，並起始平行的計分工作。

在繼續比對案例中，並行處理的設計，如下所示如下：

- 20 處理器分成五個 Cpu 的四個群組。 每個群組的 Cpu 位於相同的 NUMA 節點。

- 並行批次的最大數目已設為八個。

- 每個工作負載群組必須處理兩個計分工作。 一項工作已完成讀取資料和計分啟動，因為其他工作才能開始從資料庫讀取資料。

若要查看此案例中的 PowerShell 指令碼，開啟 在檔案 experiment.ps1 [Github 專案](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)。

### <a name="storing-models-for-prediction"></a>儲存模型來進行預測

當定型和評估完成和您選取最佳的模型時，我們建議將模型儲存至資料庫，讓它可用於預測。 從預測資料庫載入預先計算的模型很有效率，因為 SQL Server 機器學習使用特殊的序列化演算法，來儲存及載入模型，R 和資料庫之間移動時。

> [!TIP]
> 在 SQL Server 2017，您可以使用預測函數執行計分即使 R 未安裝在伺服器上。 支援有限的模型類型，從 RevoScaleR 封裝。

不過，根據您使用的演算法，某些模型可能相當大，尤其是在大型資料集上定型。 例如，例如演算法**lm**或**glm**產生大量的摘要資料，以及規則。 因為上一個模型，可以儲存在 varbinary 資料行的大小有限制，我們建議您在實際執行的資料庫中儲存模型之前消除不必要的成品從模型。

## <a name="articles-in-this-series"></a>在這一系列的文章

[效能調整的 R-簡介](../r/sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](../r/sql-server-configuration-r-services.md)

[效能調整的 R-R 程式碼和資料最佳化](../r/r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](../r/performance-case-study-r-services.md)
