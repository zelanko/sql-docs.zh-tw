---
title: SQL Server 組態 (R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dda5d84aca714530bbc2bef79344db889e113d4f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714997"
---
# <a name="sql-server-configuration-for-use-with-r"></a>用於 R 的 SQL Server 設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列中的第二篇, 描述以兩個個案研究為基礎的 R 服務效能優化。  本文提供用來執行 SQL Server R Services 之電腦的硬體和網路設定的相關指導方針。 其中也包含有關設定方案中所使用之 SQL Server 實例、資料庫或資料表之方式的資訊。 由於在 SQL Server 中使用 NUMA 會模糊硬體與資料庫優化之間的程式程式碼, 因此第三節會詳細討論 CPU affinitization 和資源管理。

> [!TIP]
> 如果您不熟悉 SQL Server, 強烈建議您同時參閱 SQL Server 效能微調指南:[效能的監視和微調](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬體優化

伺服器電腦的優化非常重要, 可確保您擁有執行外部腳本的資源。 當資源受到限制時, 您可能會看到像這樣的徵兆:

- 已延後或取消作業執行, 以優先處理其他資料庫操作
- 錯誤「超出配額」導致 R 腳本終止而未完成
- 載入至 R 記憶體的資料因未完成的結果而被截斷

### <a name="memory"></a>記憶體

電腦上可用的記憶體數量會對進階分析演算法的效能產生很大的影響。 使用 SQL 計算內容時, 記憶體不足可能會影響平行處理原則的程度。 它也會影響可處理的區塊大小 (每次讀取作業的資料列)，以及可同時支援的工作階段數目。

強烈建議至少 32 GB。 如果您有超過 32 GB 的可用空間, 可以將 SQL 資料來源設定為在每個讀取作業中使用更多資料列來改善效能。

您也可以管理實例所使用的記憶體。 根據預設, 在配置記憶體時, SQL Server 的優先順序高於外部腳本進程。 在 R 服務的預設安裝中, 只有 20% 的可用記憶體會配置給 R。

這通常不足以進行資料科學工作, 但您不會想要使 SQL server 的記憶體。 您應該在資料庫引擎、相關服務和外部腳本之間進行實驗和微調記憶體配置, 並瞭解最佳設定會因大小寫而有所不同。

對於繼續比對模型, 外部腳本使用很繁重, 而且沒有其他資料庫引擎服務正在執行;因此, 配置給外部腳本的資源已增加至 70%, 這是腳本效能的最佳設定。

### <a name="power-options"></a>電源選項

在 Windows 作業系統上, 應該使用 [**高效能**] 電源選項。 使用不同的電源設定, 會導致在使用 SQL Server 時效能降低或不一致。

### <a name="disk-io"></a>磁碟 IO

使用 R Services 的定型和預測作業本質上是 IO 系結, 並取決於資料庫儲存所在的磁片速度。 較快的磁片磁碟機 (例如固態硬碟 (SSD)) 可能會有説明。

磁碟 IO 也會受到存取磁碟的其他應用程式所影響：例如，其他用戶端對資料庫的讀取作業。 磁碟 IO 效能也會受到使用中檔案系統上的設定所影響，例如，檔案系統所使用的區塊大小。

如果有多個磁片磁碟機, 請將資料庫儲存在與 SQL Server 不同的磁片磁碟機上, 如此一來, database engine 的要求就不會到達與資料庫中儲存之資料的要求相同的磁片。

執行 RevoScaleR 分析函數以在定型期間使用多個反覆項目時，磁碟 IO 也會大幅影響效能。 `rxLogit`例如, `rxDTree` 、、`rxBTrees`和全都使用多個反復專案。 `rxDForest` 當 SQL Server 資料來源時, 這些演算法會使用已優化來捕捉資料的暫存檔案。 系統會在工作階段完成之後自動清除這些檔案。 具有高效能磁片來進行讀取/寫入作業, 可以大幅改善這些演算法的整體耗用時間。

> [!NOTE]
> 舊版 R Services 需要 Windows 作業系統上的8.3 檔案名支援。 此限制已在 Service Pack 1 之後提升。 不過, 您可以使用 fsutil 來判斷磁片磁碟機是否支援8.3 檔案名, 或如果沒有, 則啟用支援。

### <a name="paging-file"></a>分頁檔

Windows 作業系統會使用分頁檔來管理損毀傾印，以及用來儲存虛擬記憶體分頁。 如果您注意到過度分頁，請考慮增加機器上的實體記憶體。 雖然有更多實體記憶體並不會消除分頁，但它確實可以降低分頁的需求。

分頁檔儲存所在的磁碟速度也會影響效能。 將分頁檔儲存於 SSD 上，或跨多個 SSD 使用多個分頁檔，均可改善效能。

如需調整頁面檔案大小的詳細資訊, 請參閱[如何判斷64位版本 Windows 的適當頁面檔案大小](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>實例或資料庫層級的優化

SQL Server 實例的優化是有效率地執行外部腳本的關鍵。

> [!NOTE]
> 最佳設定會根據您的資料大小和類型、用來評分或定型模型的資料行數目而有所不同。
> 
> 您可以在最後一篇文章中查看特定優化的結果:[效能微調-案例研究結果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 如需範例腳本, 請參閱個別的[GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>資料表壓縮

您通常可以使用壓縮或單欄式資料存放區來改善 IO 效能。 一般來說, 資料通常會在資料表內的數個數據行中重複, 因此使用資料行存放區時, 會在壓縮資料時利用這些重複的功能。

如果資料表中有多個插入, 則資料行存放區可能不會有效率, 但如果資料是靜態的, 或只是不常變更, 則是不錯的選擇。 如果單欄式存放區不適用，則對資料列主要資料表啟用壓縮，可用來改善 IO。

如需詳細資訊，請參閱下列文件：

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>記憶體最佳化的資料表

現今, 對於新式電腦而言, 記憶體已不再是問題。 隨著硬體規格的持續改進, 以適當的值取得 RAM 相當容易。 不過, 在此同時, 資料的產生速度比以往更快, 而且必須以低延遲處理資料。

記憶體優化資料表代表一個解決方案, 因為它們會利用 advanced 電腦中可用的大型記憶體來解決 big data 的問題。 記憶體優化資料表主要位於記憶體中, 以便從記憶體讀取和寫入資料。 針對持久性, 資料表的第二份複本會保留在磁片上, 而且只會在資料庫復原期間從磁片讀取資料。

如果您需要經常讀取和寫入資料表, 記憶體優化的資料表可以提供高擴充性和低延遲的協助。  在繼續比對案例中, 使用記憶體優化資料表時, 可讓我們從資料庫讀取所有繼續功能, 並將它們儲存在主儲存體中, 以符合新的作業開頭。 這會大幅減少磁片 IO。

在從多個並行批次將預測寫入資料庫的程式中使用記憶體優化的資料表, 即可達到額外的效能提升。 在 SQL Server 上使用記憶體優化資料表會在資料表的讀取和寫入上啟用低延遲。

在開發期間也可以順暢地體驗。 持久的記憶體優化資料表是在建立資料庫時建立的。 因此, 不論儲存資料的位置為何, 開發都會使用相同的工作流程。

### <a name="processor"></a>處理器

SQL Server 可以使用機器上的可用核心, 以平行方式執行工作。可用的核心越多, 效能就愈好。 雖然增加核心數目可能無法協助進行 IO 系結作業, 但 CPU 系結演算法卻受益于具有許多核心的更快 Cpu。

因為伺服器通常由多個使用者同時使用, 所以資料庫管理員必須判斷支援尖峰工作負載計算所需的理想核心數目。

### <a name="resource-governance"></a>資源管理

在支援 Resource Governor 的版本中, 您可以使用資源集區來指定特定工作負載會配置一些 Cpu。 您也可以管理配置給特定工作負載的記憶體數量。

SQL Server 中的資源管理可讓您集中監視和控制 SQL Server 和 R 所使用的各種資源。例如, 您可能會為資料庫引擎配置一半的可用記憶體, 以確保核心服務一定可以在暫時性的較繁重工作負載的情況下執行。

外部腳本的記憶體耗用量預設值限制為 SQL Server 本身可用總記憶體的 20%。 預設會套用此限制, 以確保依賴資料庫伺服器的所有工作都不會受到長時間執行 R 作業的嚴重影響。 不過，資料庫管理員可以變更這些限制。 在許多情況下, 20% 的限制並不足以支援嚴重的機器學習工作負載。

支援的設定選項為**MAX_CPU_PERCENT**、 **MAX_MEMORY_PERCENT**和**MAX_PROCESSES**。 若要查看目前的設定, 請使用下列語句:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果伺服器主要用於 R 服務, 將 MAX_CPU_PERCENT 增加至 40% 或 60% 可能會很有説明。

-  如果有許多 R 會話必須同時使用相同的伺服器, 則應該增加這三項設定。

若要變更已配置的資源值, 請使用 T-sql 語句。

+ 此語句會將記憶體使用量設定為 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此語句會設定三個可設定的值:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果您變更 [記憶體]、[CPU] 或 [最大處理常式] 設定, 然後想要立即套用這些設定, 請執行下列語句:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>軟體 NUMA、硬體 NUMA 和 CPU 親和性

使用 SQL Server 做為計算內容時, 您有時可以藉由調整與 NUMA 和處理器親和性相關的設定, 來達到較佳的效能。 

具有_硬體 NUMA_的系統有一個以上的系統匯流排, 每個都提供一組小型的處理器。 每個 CPU 都能以一致的方式存取與其他群組相關聯的記憶體。 每一個群組就稱為 NUMA 節點。 如果您有硬體 NUMA，它可設定為使用交錯記憶體，而非 NUMA。 在此情況下, Windows 和因此 SQL Server 無法將它辨識為 NUMA。 

您可以執行下列查詢, 找出可用來 SQL Server 的記憶體節點數目:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查詢傳回單一記憶體節點 (節點 0), 可能是您沒有硬體 NUMA, 或是硬體已設定為交錯 (非 NUMA)。 SQL Server 也會在有四個或更少的 Cpu, 或至少一個節點只有一個 CPU 時, 忽略硬體 NUMA。

如果您的電腦有多個處理器, 但沒有硬體 NUMA, 您也可以使用[軟體 numa](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)將 cpu 細分成較小的群組。  在 SQL Server 2016 和 SQL Server 2017 中, 啟動 SQL Server 服務時, 會自動啟用軟體 NUMA 功能。

啟用軟體 NUMA 時, SQL Server 會自動為您管理節點;不過, 若要針對特定工作負載優化, 您可以停用_軟相似性_, 並手動設定軟 NUMA 節點的 CPU 親和性。 這可讓您更充分掌控指派給哪些節點的工作負載, 特別是當您使用支援資源管理的 SQL Server 版本時。 藉由指定 CPU 親和性並將資源集區與 Cpu 群組對齊, 您可以減少延遲, 並確保在相同的 NUMA 節點內執行相關的進程。

設定軟體 NUMA 和 CPU 親和性以支援 R 工作負載的整體程式如下所示:

1. 啟用軟體 NUMA (如果有的話)
2. 定義處理器親和性
3. 使用[Resource Governor](../r/resource-governance-for-r-services.md)建立外部進程的資源集區
4. 將[工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)指派給特定的同質群組

如需詳細資訊, 包括範例程式碼, 請參閱此教學課程:[SQL 優化秘訣和訣竅 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他資源:**

+ [SQL Server 中的軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何將軟體 NUMA 節點對應至 Cpu

## <a name="task-specific-optimizations"></a>工作特定的優化

本節將摘要說明這些案例研究中所採用的方法, 以及用於優化特定機器學習工作負載的其他測試。 常見的工作負載包括模型定型、功能的提取和特徵工程, 以及用於計分的各種案例: 單一資料列、小型批次和大型批次。

### <a name="feature-engineering"></a>特徵工程

R 的一個難題是, 它通常是在單一 CPU 上處理。 這是許多工的主要效能瓶頸, 特別是功能工程。 在繼續比對解決方案中, 「功能工程」工作單獨建立了2500的跨產品功能, 必須與原始的100功能結合。 如果所有專案都是在單一 CPU 上完成, 這項工作會花很長的時間。

有多種方式可以改善功能工程的效能。 您可以將 R 程式碼優化, 並在模型化程式中保留功能解壓縮, 或將功能工程設計程式移至 SQL。

- 使用 R。您在定型期間定義函式, 然後將它當做引數傳遞給[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) 。 如果模型支援平行處理, 則可以使用多個 Cpu 來處理功能工程工作。 使用這種方法, 資料科學小組在計分時間方面觀察到 16% 的效能改進。 不過, 此方法需要支援平行處理的模型, 以及可使用平行計畫來執行的查詢。

- 使用 R 搭配 SQL 計算內容。 在有隔離的資源可執行個別批次的多處理器環境中, 您可以隔離用於每個批次的 SQL 查詢, 以從資料表中提取資料並限制相同工作負載群組上的資料, 以達到更高的效率。 用來隔離批次的方法包括分割, 以及使用 PowerShell 以平行方式執行個別的查詢。

- 特定平行執行:在 SQL Server 計算內容中, 您可以依賴 SQL database 引擎來強制平行執行, 如果有找到更有效率的選項。

- 在個別的特徵化進程中使用 T-sql。 使用 SQL Precomputing 功能資料通常會更快。

### <a name="prediction-scoring-in-parallel"></a>平行預測 (計分)

SQL Server 的優點之一, 就是能夠平行處理大量的資料列。 這項優點就是在計分中標示為。 一般而言, 此模型不需要存取所有資料進行計分, 因此您可以分割輸入資料, 每個工作負載群組處理一項工作。

您也可以將輸入資料當做單一查詢來傳送, 然後 SQL Server 分析查詢。 如果可以針對輸入資料建立平行查詢計劃, 它會自動分割指派給節點的資料, 並同時執行必要的聯結和匯總。

如果您對如何定義預存程式以用於計分的細節感興趣, 請參閱[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)上的範例專案, 並尋找 "step5_score_for_matching" 檔案。 範例腳本也會追蹤查詢開始和結束時間, 並將時間寫入 SQL 主控台, 讓您可以評估效能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用資源群組進行並行評分

若要相應增加評分問題, 最佳做法是採用地圖縮減方法, 其中數百萬個專案會分割成多個批次。 然後, 會同時執行多個評分作業。 在此架構中, 批次會在不同的 CPU 集合上進行處理, 並收集結果並將其寫回資料庫。

這是在繼續比對案例中使用的方法;不過, SQL Server 中的資源管理是執行此方法的必要項。 藉由設定外部腳本作業的工作負載群組, 您可以將 R 評分作業路由至不同的處理器群組, 以達到更快的輸送量。

資源控管也可以協助配置將伺服器上的可用資源 (CPU 和記憶體) 分割, 以將工作負載競爭降至最低。 您可以設定分類函數來區別不同類型的 R 作業: 例如, 您可能會決定從應用程式呼叫的評分一律優先, 而重新定型作業的優先順序低。 此資源隔離可能會改善執行時間, 並提供更可預測的效能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 進行並行評分

如果您決定自行分割資料, 您可以使用 PowerShell 腳本來執行多個並行計分工作。 若要這麼做, 請使用 Invoke-SqlCmd Cmdlet, 並以平行方式起始評分工作。

在繼續比對案例中, 並行處理的設計如下:

- 20個處理器分成四個群組, 每個都有五個 Cpu。 每個 Cpu 群組都位於相同的 NUMA 節點上。

- 同時批次的最大數目已設定為8。

- 每個工作負載群組都必須處理兩個評分作業。 一旦一項工作完成讀取資料並開始評分, 另一個工作就可以開始從資料庫讀取資料。

若要查看此案例的 PowerShell 腳本, 請在[Github 專案](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)中開啟檔案實驗。

### <a name="storing-models-for-prediction"></a>儲存用於預測的模型

當定型和評估完成, 而且您已選取最佳模型時, 建議您將模型儲存在資料庫中, 讓它可用於預測。 從資料庫載入預先計算的模型以進行預測很有效率, 因為 SQL Server 機器學習服務會使用特殊的序列化演算法來儲存和載入模型 (在 R 和資料庫之間移動時)。

> [!TIP]
> 在 SQL Server 2017 中, 您可以使用 PREDICT 函數來執行計分, 即使伺服器上未安裝 R 也一樣。 RevoScaleR 套件支援有限的模型類型。

不過, 視您使用的演算法而定, 某些模型可能相當大, 尤其是在大型資料集上定型時。 例如, **lm**或**glm**之類的演算法會產生許多摘要資料以及規則。 因為可以儲存在 Varbinary 資料行中的模型大小有所限制, 所以我們建議您先從模型中排除不必要的成品, 然後再將模型儲存到資料庫中以供生產環境使用。

## <a name="articles-in-this-series"></a>本系列文章

[R 效能微調-簡介](../r/sql-server-r-services-performance-tuning.md)

[R SQL Server 設定的效能微調](../r/sql-server-configuration-r-services.md)

[R-R 程式碼和資料優化的效能微調](../r/r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](../r/performance-case-study-r-services.md)
