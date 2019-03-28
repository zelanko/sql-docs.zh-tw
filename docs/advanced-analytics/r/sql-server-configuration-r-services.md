---
title: SQL Server 組態 （R 服務）-SQL Server Machine Learning 服務
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f5dd6ee267b7bac933e40f90282d1bf74aa57b62
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511845"
---
# <a name="sql-server-configuration-for-use-with-r"></a>搭配 R 的 SQL Server 組態
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章會說明兩個案例研究為基礎的 R 服務的效能最佳化的數列中的第二個。  本文提供指引來執行 SQL Server R Services 的電腦硬體和網路設定。 它也包含有關如何設定 SQL Server 執行個體、 資料庫或資料表用於方案中的相關資訊。 使用 SQL Server 中的 NUMA 模糊了硬體和資料庫最佳化之間的線，因為第三個區段將討論詳細 CPU 分配和資源控管。

> [!TIP]
> 如果您不熟悉 SQL Server，我們強烈建議您也檢閱 SQL Server 效能微調指南：[效能監視與微調](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬體最佳化

伺服器電腦的最佳化很重要，確定您有資源可執行外部指令碼。 資源有限時，您可能會看到這類的徵狀：

- 工作執行已延後或取消排定其他資料庫作業的優先順序
- 錯誤 「 配額已超過 」 而造成 R 指令碼終止而不需要完成
- 資料載入至 R 記憶體截斷，不完整的結果

### <a name="memory"></a>記憶體

電腦上可用的記憶體數量會對進階分析演算法的效能產生很大的影響。 使用 SQL 計算內容時，記憶體不足可能會影響平行處理原則程度。 它也會影響可處理的區塊大小 (每次讀取作業的資料列)，以及可同時支援的工作階段數目。

強烈建議至少 32 GB。 如果您有多個 32 gb 的可用空間，您可以設定 SQL 資料來源中每個讀取作業使用多個資料列，以改善效能。

您也可以管理執行個體所使用的記憶體。 根據預設，SQL Server 會優先於外部指令碼處理程序，在配置記憶體時。 在 R Services 的預設安裝中，只有 20%的可用記憶體配置給。

通常這不是足夠的資料科學工作，但您要在不佔用 SQL server 的記憶體。 您應該試驗，微調資料庫引擎、 相關的服務和外部的指令碼，並了解最佳的組態設定會依案例的之間的記憶體配置。

繼續比對模型中，外部指令碼的用途是大量，而且已沒有其他資料庫引擎服務執行;因此，配置給外部指令碼資源已增加到 70%，這是指令碼效能的最佳組態。

### <a name="power-options"></a>電源選項

在 Windows 作業系統上**高效能**應該使用電源選項。 使用不同的電源設定導致降低或不一致的效能，當您使用 SQL Server。

### <a name="disk-io"></a>磁碟 IO

定型和預測使用 R Services 的工作本質上是 IO 繫結，並相依於資料庫儲存在磁碟的速度。 可能有助於更快速的磁碟機，例如固態硬碟 (SSD)。

磁碟 IO 也會受到存取磁碟的其他應用程式所影響：例如，其他用戶端對資料庫的讀取作業。 磁碟 IO 效能也會受到使用中檔案系統上的設定所影響，例如，檔案系統所使用的區塊大小。

如果有多個磁碟機，因此，要求的 database engine 的 SQL Server 不同的磁碟上的資料庫未達到相同的磁碟的存放區會要求儲存在資料庫中的資料。

執行 RevoScaleR 分析函數以在定型期間使用多個反覆項目時，磁碟 IO 也會大幅影響效能。 例如， `rxLogit`， `rxDTree`， `rxDForest`，和`rxBTrees`所有使用多個反覆項目。 SQL Server 資料來源時，這些演算法會使用已最佳化來擷取資料的暫存檔案。 系統會在工作階段完成之後自動清除這些檔案。 具有讀取/寫入作業的高效能磁碟，可大幅改善這些演算法經過的總時間。

> [!NOTE]
> 舊版的 R Services 所需在 Windows 作業系統上的 8.3 檔案名稱支援。 Service Pack 1 之後，已提高此限制。 不過，您可以使用 fsutil.exe 來判斷磁碟機是否支援 8.3 檔案名稱，或如果未啟用支援。

### <a name="paging-file"></a>分頁檔

Windows 作業系統會使用分頁檔來管理損毀傾印，以及用來儲存虛擬記憶體分頁。 如果您注意到過度分頁，請考慮增加機器上的實體記憶體。 雖然有更多實體記憶體並不會消除分頁，但它確實可以降低分頁的需求。

分頁檔儲存所在的磁碟速度也會影響效能。 將分頁檔儲存於 SSD 上，或跨多個 SSD 使用多個分頁檔，均可改善效能。

如需調整分頁檔的資訊，請參閱[如何判斷適當的分頁檔大小為 64 位元版本的 Windows](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>在執行個體或資料庫層級的最佳化

最佳化 SQL Server 執行個體是最有效率的執行外部指令碼的索引鍵。

> [!NOTE]
> 最佳的設定是根據大小和您的資料類型，您要用於計分或定型模型的資料行數目而有所不同。
> 
> 您可以檢閱結果的最後一篇文章中的特定最佳化：[效能微調-案例研究結果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 如需範例指令碼，請參閱個別[GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>資料表壓縮

使用壓縮或單欄式資料存放區，通常可以改善 IO 效能。 一般而言，只有在數個資料行在資料表中，讓使用資料行存放區壓縮的資料時，會充分利用這些重複項目，通常有重複的資料。

資料行存放區可能不是那麼有效率，如果有多個插入至資料表，但如果資料是靜態或不常變更，是不錯的選擇。 如果單欄式存放區不適用，則對資料列主要資料表啟用壓縮，可用來改善 IO。

如需詳細資訊，請參閱下列文件：

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>記憶體最佳化的資料表

時至今日，記憶體不會再是現代電腦的問題。 因為硬體規格，持續改進，就非常簡單的良好值取得 RAM。 不過，在此同時，資料會比以往，更快速地產生，而且必須處理具有低延遲的資料。

記憶體最佳化資料表會代表一種解決方案，，他們便會利用大量的記憶體可用來處理巨量資料的問題的進階電腦中。 記憶體最佳化資料表主要是位在記憶體中，使資料是從讀取和寫入記憶體。 如需持久性，第二份資料表會維護磁碟上，以及資料只會從磁碟讀取資料庫復原期間。

如果您需要讀取和寫入至資料表的常見問題，記憶體最佳化資料表可協助高延展性和低延遲。  在繼續比對的情況下，使用經記憶體最佳化的資料表，讓我們從資料庫讀取所有的恢復功能，並將它們儲存在主要記憶體中，以符合新的工作機會。 這會大幅降低磁碟 IO。

進一步提高效能，已使用記憶體最佳化的資料表，從多個並行的批次預測回寫到資料庫的過程中來達成。 使用記憶體最佳化的資料表，SQL Server 上啟用低延遲資料表讀取和寫入。

體驗也是無縫開發過程中。 建立資料庫的同時建立持久性記憶體最佳化的資料表。 因此，開發會使用相同的工作流程，不論資料儲存的位置。

### <a name="processor"></a>處理器

SQL Server 可以執行平行工作所使用電腦; 上的可用核心數目可供使用，更多核心的較佳的效能。 繫結的 IO 作業可能無法協助增加的核心數目，而 CPU 繫結演算法權益中更快的 Cpu，含有許多核心。

因為伺服器通常由多位使用者同時使用，資料庫管理員必須判斷支援尖峰工作負載計算所需的核心的理想數目。

### <a name="resource-governance"></a>資源控管

在支援資源管理員的版本中，您可以使用資源集區指定某些工作負載會配置 Cpu 的部分數目。 您也可以管理配置給特定的工作負載的記憶體數量。

SQL Server 中的資源管理可讓您集中監視和控制 r 和 SQL Server 所使用的各種資源例如，您可能會配置一半可用的記憶體，針對資料庫引擎，以確保服務可以永遠執行，儘管暫時性更繁重的工作負載的核心。

外部指令碼的記憶體耗用量的預設值僅限於適用於 SQL Server 本身的記憶體總計的 20%。 根據預設，以確保，依賴資料庫伺服器的所有工作不會嚴重都影響長時間執行的 R 作業會套用此限制。 不過，資料庫管理員可以變更這些限制。 在許多情況下，20%限制並不足以支援嚴重的機器學習服務工作負載。

支援的組態選項都**MAX_CPU_PERCENT**， **MAX_MEMORY_PERCENT**，並**MAX_PROCESSES**。 若要檢視目前的設定，請使用此陳述式： `SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果伺服器主要用於 R Services，可能很有幫助 MAX_CPU_PERCENT 增加至 40%或 60%。

-  如果多個 R 工作階段必須同時使用相同的伺服器，就應增加所有三個設定。

若要變更已配置的資源值，請使用 T-SQL 陳述式。

+ 此陳述式會設定為 40%的記憶體使用量： `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此陳述式會設定所有三個可設定的值： `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果您變更記憶體、 CPU 或處理程序上限設定，並接著要立即套用設定時，執行此陳述式： `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>軟體 NUMA，硬體 NUMA、 CPU 親和性

時使用 SQL Server 作為計算內容，您有時可以微調 NUMA 和處理器親和性的相關設定來達到更佳的效能。 

系統_硬體 NUMA_有多個系統匯流排，每一種較少的處理器。 每一個 CPU 可以存取相同的方式與其他群組相關聯的記憶體。 每一個群組就稱為 NUMA 節點。 如果您有硬體 NUMA，它可設定為使用交錯記憶體，而非 NUMA。 在此情況下，Windows，因此 SQL Server 會不將它視為 NUMA。 

您可以執行下列查詢，以找出記憶體供 SQL Server 的節點數目：

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查詢傳回單一記憶體節點 （節點 0），您沒有硬體 NUMA，或硬體設定為交錯的 (非 NUMA)。 SQL Server 也會忽略硬體 NUMA 時有四個或更少的 Cpu，或如果至少一個節點只有一個 CPU。

如果您的電腦有多個處理器，但沒有硬體 NUMA，您也可以使用[軟體式 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) ，將 Cpu 細分成較小的群組。  在 SQL Server 2016 和 SQL Server 2017 中，啟動 SQL Server 服務時，自動會啟用軟體式 NUMA 功能。

SQL Server 啟用 NUMA 時，會自動管理您; 節點不過，若要最佳化特定工作負載，您可以停用_軟性親和性_並手動設定軟體 NUMA 節點的 CPU 相似性。 這可讓您更多的控制哪些工作負載指派給哪一個節點中，特別是當您使用的 SQL Server 支援資源控管版本。 藉由指定 CPU 相似性，並配合使用的 Cpu 群組的資源集區，您可以減少延遲，並確保相關處理程序會在相同的 NUMA 節點內執行。

設定軟體式 NUMA 和 CPU 親和性，以支援 R 工作負載的整體程序如下所示：

1. 如果有的話，請啟用軟體 NUMA
2. 定義處理器相關性
3. 建立資源集區使用的外部處理序[Resource Governor](../r/resource-governance-for-r-services.md)
4. 指派[工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)至特定的同質群組

如需詳細資訊，包括範例程式碼，請參閱本教學課程：[SQL 最佳化祕訣和訣竅 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他資源：**

+ [SQL Server 中的軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何將軟體 NUMA 節點對應到 Cpu

+ [自動軟體式 NUMA:它只會執行更快 (Bob Ward)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   描述歷程記錄以及實作詳細資料，在較新的多核心伺服器上的效能。

## <a name="task-specific-optimizations"></a>工作特定的最佳化

本節摘要說明這些案例研究、 中和在其他測試中，最佳化特定機器學習服務工作負載採用的方法。 常見的工作負載包含模型訓練、 擷取特徵和功能工程，以及用於評分的各種案例： 單一資料列、 小型的批次和大型批次。

### <a name="feature-engineering"></a>特徵工程

使用 R 的一個痛苦點是通常處理單一 CPU 上。 這是主要的效能瓶頸的許多工作，尤其是特徵工程設計。 在繼續比對方案中，單獨的功能工程工作會建立 2,500 必須與原始的 100 功能結合的交叉乘積功能。 此工作會需要大量的時間，如果所有項目已完成上一個 CPU。

有多種方式可以改善效能的特徵工程設計。 您可以最佳化您的 R 程式碼，並保留模型化程序內的功能擷取或將功能工程程序移至 SQL。

- 使用。您定義函式，然後將它傳遞做為引數[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)在定型期間。 如果模型支援平行處理，可以使用多個 Cpu 處理工程工作。 使用這個方法，資料科學小組所觀察到方面評分時間 16%的效能改進。 不過，此方法需要可支援平行處理和查詢，您可以使用平行計畫執行的模型。

- 使用 R 與 SQL 計算內容。 在隔離的資源可供個別批次執行多處理器環境中，您可以藉由隔離每個批次，用來從資料表擷取資料及限制在相同的工作負載群組的資料的 SQL 查詢來達到更高的效率。 用來找出的批次的方法包括資料分割，並使用 PowerShell 來平行執行個別查詢。

- 臨機操作的平行執行：在 SQL Server 計算內容中，您可以依賴 SQL database engine，以強制執行，盡可能平行執行，且該選項若找到能夠更有效率。

- 使用 T-SQL 在不同的特徵化程序。 Precomputing 使用 SQL 的功能資料通常會更快。

### <a name="prediction-scoring-in-parallel"></a>預測 （計分），以平行方式

SQL server 的好處之一是能夠處理大量的平行的資料列。 尤是這項優勢因此標示為 「 評分。 通常模型不需要存取所有資料進行評分，因此您可以分割輸入的資料，與每個處理一項工作的工作負載群組。

您也可以為單一查詢，來傳送輸入的資料和 SQL Server 接著會分析該查詢。 如果平行查詢計畫可以建立輸入資料，它會自動指派給節點的資料分割，並執行以平行方式也的必要的聯結和彙總。

如果您想要如何定義使用預存程序計分的詳細資訊，請參閱範例專案[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)並尋找 「 step5_score_for_matching.sql"的檔案。 範例指令碼也會追蹤查詢的開始和結束時間以及寫入至 SQL 主控台的時間，讓您可以評估效能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用資源群組的並行評分

若要相應增加評分的問題時，理想的作法是採用 map-reduce 方法數以百萬計的項目會分成多個批次。 然後，會同時執行多個評分的工作。 在此架構中，批次都是不同的 CPU 設定上處理，且結果會收集並寫回至資料庫。

這是此案例中使用繼續比對; 方法不過，SQL Server 中的資源控管是不可或缺的實作此方法。 藉由設定外部指令碼工作的工作負載群組，您可以路由傳送至不同的處理器群組評分作業的 R，並達到更快速的輸送量。

資源控管也可協助配置分割 （CPU 和記憶體），以減少工作負載競爭的伺服器上的可用資源。 您可以設定分類函數來區別不同類型的 R 工作： 例如，您可能會決定，評分呼叫從應用程式一律會優先採用，雖然重新訓練作業有低優先順序服務。 此資源隔離可能可以改善執行時間，並提供更可預測的效能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 的並行評分

如果您決定自行分割的資料，您可以使用 PowerShell 指令碼執行多個並行的計分工作。 若要這樣做，請使用 Invoke-sqlcmd cmdlet，並起始評分的工作，以平行方式。

在繼續比對案例中，並行處理的設計，如下所示：

- 20 處理器分成五個 Cpu 的四個群組。 每個 Cpu 群組位於相同的 NUMA 節點。

- 並行批次的最大數目已設為八個。

- 每個工作負載群組必須處理兩個評分的工作。 一項工作已完成讀取資料和評分的會啟動，因為另一個工作就可以開始從資料庫讀取資料。

若要查看此案例中的 PowerShell 指令碼，開啟 在檔案 experiment.ps1 [Github 專案](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)。

### <a name="storing-models-for-prediction"></a>儲存模型來進行預測

當訓練和評估完成而您選取最佳的模型時，我們建議在資料庫中儲存模型，使其可供預測。 從預測資料庫載入預先計算的模型很有效率，因為 SQL Server 機器學習服務會使用特殊的序列化演算法，來儲存和載入 R 和資料庫之間移動時的模型。

> [!TIP]
> 在 SQL Server 2017 中，您可以使用 PREDICT 函式來執行計分，即使未在伺服器上安裝 R。 支援有限的模型型別，RevoScaleR 套件中。

不過，根據您所使用的演算法，某些模型可能相當大，尤其是在大型資料集上定型。 比方說，這類的演算法**lm**或是**glm**產生大量的摘要資料，以及規則。 因為一個模型，可以儲存在 varbinary 資料行的大小限制，所以我們建議您消除不必要的構件，從模型，然後再將模型儲存在生產環境資料庫中。

## <a name="articles-in-this-series"></a>在這一系列的文章

[效能微調的 R-簡介](../r/sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](../r/sql-server-configuration-r-services.md)

[R-R 效能微調程式碼和資料最佳化](../r/r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](../r/performance-case-study-r-services.md)
