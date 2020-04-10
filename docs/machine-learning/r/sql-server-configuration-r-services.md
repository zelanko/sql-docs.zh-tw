---
title: 與 R 搭配使用的設定
description: 本文會針對用來執行 SQL Server R Services 的電腦，提供關於其硬體和網路的設定指導方針。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cedc5c08f44da357da70f63b47676383f6f53675
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117341"
---
# <a name="sql-server-configuration-for-use-with-r"></a>與 R 搭配使用的 SQL Server 設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列文章中的第二篇，會根據兩個案例研究來描述 R Services 的效能最佳化。  本文會針對用來執行 SQL Server R Services 的電腦，提供關於其硬體和網路的設定指導方針。 文中也有相關資訊可讓您了解如何設定解決方案中所使用的 SQL Server 執行個體、資料庫或資料表。 由於在 SQL Server 中使用 NUMA 會讓硬體與資料庫最佳化之間的界線變得模糊，因此第三節會詳細討論 CPU 親和與資源治理。

> [!TIP]
> 如果您不熟悉 SQL Server，強烈建議您另外檢閱 SQL Server 效能微調指南：[監視和微調效能](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬體最佳化

對於要確保您會擁有可執行外部指令碼的資源來說，伺服器電腦的最佳化顯得非常重要。 當資源受到限制時，您可能會看到如下徵兆：

- 作業的執行延後或取消，以優先處理其他資料庫操作
- 出現「超出配額」錯誤導致 R 指令碼未完成就終止
- 載入至 R 記憶體的資料遭到截斷，以獲得不完整的結果

### <a name="memory"></a>記憶體

電腦上可用的記憶體數量會對進階分析演算法的效能產生很大的影響。 使用 SQL 計算內容時，記憶體不足可能會影響平行處理原則的程度。 它也會影響可處理的區塊大小 (每次讀取作業的資料列)，以及可同時支援的工作階段數目。

強烈建議至少 32 GB。 如果您的可用記憶體超過 32 GB，則可設定 SQL 資料來源，在每個讀取作業中讀取更多資料列以改善效能。

您也可以管理執行個體所使用的記憶體。 根據預設，系統在配置記憶體時，SQL Server 的優先順序會高於外部指令碼的處理序。 在 R Services 的預設安裝中，只有 20% 的可用記憶體會配置給 R。

一般來說，這樣的配置並不足以進行資料科學工作，但您也不會想要讓 SQL 伺服器缺乏記憶體。 您應該實驗並微調資料庫引擎、相關服務和外部指令碼三者之間的記憶體配置，並了解最佳設定會因案例而異。

在履歷表比對模型方面，其會大量使用外部指令碼，而且不會執行其他任何資料庫引擎服務；因此，配置給外部指令碼的資源已增加至 70%，這是最能發揮指令碼效能的設定。

### <a name="power-options"></a>電源選項

在 Windows 作業系統上，應使用 [高效能]  電源選項。 使用 SQL Server 時，所用的不同電源設定會導致下滑或不一致的效能。

### <a name="disk-io"></a>磁碟 IO

使用 R Services 的定型和預測作業原本就會與 IO 繫結，並且會仰賴資料庫儲存所在的磁碟速度。 更快速的磁碟機 (例如固態硬碟 (SSD)) 可能會有幫助。

磁碟 IO 也會受到存取磁碟的其他應用程式所影響：例如，其他用戶端對資料庫的讀取作業。 磁碟 IO 效能也會受到使用中檔案系統上的設定所影響，例如，檔案系統所使用的區塊大小。

如果有多個可用磁碟機，請將資料庫儲存在與 SQL Server 不同的磁碟機上，如此一來，對資料庫引擎的要求就不會到達對資料庫中所儲存資料的要求相同的磁碟。

執行 RevoScaleR 分析函數以在定型期間使用多個反覆項目時，磁碟 IO 也會大幅影響效能。 例如，`rxLogit`、`rxDTree`、`rxDForest` 和 `rxBTrees` 全都會使用多個反覆項目。 當資料來源是 SQL Server 時，這些演算法會使用已最佳化來擷取資料的暫存檔。 系統會在工作階段完成之後自動清除這些檔案。 具有適用於讀取/寫入作業的高效能磁碟，可大幅改善這些演算法已耗用的總時間。

> [!NOTE]
> 在 Windows 作業系統上，早期的 R Services 版本需要 8.3 檔案名稱支援。 在 Service Pack 1 之後，此限制已有所提升。 不過，您可以使用 fsutil.exe來判斷磁碟機是否支援 8.3 檔案名稱，如果沒有，則啟用支援。

### <a name="paging-file"></a>分頁檔

Windows 作業系統會使用分頁檔來管理損毀傾印，以及用來儲存虛擬記憶體分頁。 如果您注意到過度分頁，請考慮增加機器上的實體記憶體。 雖然有更多實體記憶體並不會消除分頁，但它確實可以降低分頁的需求。

分頁檔儲存所在的磁碟速度也會影響效能。 將分頁檔儲存於 SSD 上，或跨多個 SSD 使用多個分頁檔，均可改善效能。

如需如何調整分頁檔大小的相關資訊，請參閱[如何判斷適用於 64 位元版本 Windows 的適當分頁檔大小](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>執行個體或資料庫層級的最佳化

SQL Server 執行個體的最佳化是外部指令碼能否有效率執行的關鍵。

> [!NOTE]
> 根據資料的大小和類型、用來評分或定型模型的資料行數目，最佳設定會有所不同。
> 
> 您可以在最後一篇文章中檢閱特定最佳化的結果：[效能調整 - 案例研究結果](../../machine-learning/r/performance-case-study-r-services.md)
> 
> 如需指令碼範例，請參閱個別的 [GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>資料表壓縮

使用壓縮或資料行資料存放區，通常可以改善 IO 效能。 一般而言，資料通常會在資料表內的數個資料行中重複，因此，在壓縮資料時使用資料行存放區即可充分利用這些重複項目。

如果有很多插入至資料表的資料，資料行存放區可能就不是那麼有效率，但如果資料是靜態或不常變更，這會是個不錯的選擇。 如果單欄式存放區不適用，則對資料列主要資料表啟用壓縮，可用來改善 IO。

如需詳細資訊，請參閱下列文件：

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>記憶體最佳化的資料表

對於現今的新式電腦而言，記憶體已不再是問題。 隨著硬體規格的持續改進，要以好價格取得 RAM 變得相對容易。 不過，在此同時，資料的產生速度也比以往更快，而且資料在處理時也不能有過高的延遲。

經記憶體最佳化的資料表代表著一個解決方案，因為這樣的資料表會利用進階電腦中可用的大量記憶體來處理巨量資料的問題。 經記憶體最佳化的資料表主要位於記憶體中，以便在記憶體中讀取和寫入資料。 為了確保持久性，磁碟上會保有該資料表的第二個複本，而且只有在復原資料庫期間從會從磁碟讀取資料。

如果您需要經常讀取和寫入資料表，經記憶體最佳化的資料表有助於提供高延展性和低延遲。  在履歷表比對案例中，使用經記憶體最佳化的資料表讓我們得以從資料庫讀取所有履歷表特徵，並將這些特點儲存在主記憶體中，以便與新的職缺進行比對。 這可大幅減少磁碟 IO。

在透過多個並行批次將預測回寫到資料庫的過程中，使用經記憶體最佳化的資料表讓我們實現額外的效能提升成果。 在 SQL Server 上使用經記憶體最佳化的資料表，讓讀取和寫入實現了低延遲。

在開發期間，這項體驗也毫無窒礙。 在建立資料庫時，就已建立了持久的經記憶體最佳化的資料表。 因此，不論資料儲存在哪裡，開發小組所使用的工作流程都會一樣。

### <a name="processor"></a>處理器

SQL Server 可藉由使用機器上的可用核心，以平行方式執行工作；可用的核心越多，效能就越好。 雖然增加核心數目對於 IO 繫結作業可能沒有助益，但 CPU 繫結演算法將可因含有許多核心的更快速 CPU 而受益。

由於通常會有多位使用者同時使用伺服器，因此，資料庫管理員必須判斷支援尖峰工作負載計算所需的理想核心數目。

### <a name="resource-governance"></a>資源管理

在支援 Resource Governor 的版本中，您可以使用資源集區來指定要對特定工作負載配置一定數量的 CPU。 您也可以管理要配置給特定工作負載的記憶體數量。

SQL Server 中的資源治理可讓您集中監視和控制 SQL Server 與 R 所用的各種資源。例如，您可以為資料庫引擎配置一半的可用記憶體，以確保核心服務會永遠運作，而不受暫時加重的工作負載所影響。

外部指令碼的記憶體耗用量預設值，會限制在 SQL Server 本身可用記憶體總量的 20%。 系統會預設套用此限制，以確保仰賴資料庫伺服器的所有工作，不會因為長時間執行的 R 作業而受到嚴重影響。 不過，資料庫管理員可以變更這些限制。 在許多情況下，20% 的限制並不足以支援大量的機器學習工作負載。

所支援的設定選項包括 **MAX_CPU_PERCENT**、**MAX_MEMORY_PERCENT** 和 **MAX_PROCESSES**。 若要檢視目前的設定，請使用這個陳述式：`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果伺服器主要是用於執行 R Services，則將 MAX_CPU_PERCENT 增加至 40%或 60% 可能有幫助。

-  如果有許多 R 工作階段必須在同一時間使用相同的伺服器，則應該將這三項設定全部加大。

若要變更已配置的資源值，請使用 T-SQL 陳述式。

+ 此陳述式會將記憶體使用量設定為 40%：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此陳述式會一起設定這三個可設定的值：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果您變更記憶體、CPU 或最大處理序設定，然後想要立即套用這些設定，請執行這個陳述式：`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>軟體 NUMA、硬體 NUMA 和 CPU 親和性

使用 SQL Server 來作為計算內容時，您有時可以藉由調整與 NUMA 和處理器親和性相關的設定，來達到更好的效能。 

具有「硬體 NUMA」  的系統會有不止一個系統匯流排，每一個匯流排會服務一小組處理器。 每個 CPU 都可存取與使用相同方法設計之其他群組相關聯的記憶體。 每一個群組就稱為 NUMA 節點。 如果您有硬體 NUMA，它可設定為使用交錯記憶體，而非 NUMA。 在此情況下，Windows 及 SQL Server 將不會將它視為 NUMA。 

您可以執行下列查詢，來尋找 SQL Server 可用的記憶體節點數：

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查詢傳回單一記憶體節點 (節點 0)，表示您沒有硬體 NUMA，或硬體設定為交錯 (非 NUMA)。 SQL Server 也會在有四個以下的 CPU 時，或在至少一個節點只有一個 CPU 時，忽略硬體 NUMA。

如果您的電腦有多個處理器，但沒有硬體 NUMA，您也可以使用[軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)，將 CPU 細分成較小的群組。  在 SQL Server 2016 和 SQL Server 2017 中，啟動 SQL Server 服務時就會自動啟用軟體 NUMA 功能。

當軟體 NUMA 啟用時，SQL Server 會自動為您管理節點；不過，若要針對特定工作負載來最佳化，您可以停用「軟親和性」  並手動設定軟體 NUMA 節點的 CPU 親和性。 這會讓您更能掌控要將哪些工作負載指派給哪些節點，特別是如果您要使用的 SQL Server 版本可支援資源治理的話。 藉由指定 CPU 親和性並讓資源集區與 CPU 群組相符，您就可以減少延遲，並確保能在相同的 NUMA 節點內執行相關的處理序。

若要設定軟體 NUMA 和 CPU 親和性以支援 R 工作負載，其整體流程如下：

1. 啟用軟體 NUMA (如果可以使用的話)
2. 定義處理器親和性
3. 使用 [Resource Governor](../administration/resource-governor.md) 建立用於外部處理序的資源集區
4. 將[工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)指派給特定同質群組

如需詳細資訊 (包括程式碼範例)，請參閱此教學課程：[SQL 最佳化秘訣和訣竅 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他資源：**

+ [SQL Server 中的軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何將軟體 NUMA 節點對應到 CPU

## <a name="task-specific-optimizations"></a>工作專屬最佳化

本節將摘要說明這些案例研究以及其他測試中為了將特定機器學習工作負載最佳化所採用的方法。 常見的工作負載包括模型定型、特徵擷取和特徵工程，以及各種評分案例：單一資料列、小型批次和大型批次。

### <a name="feature-engineering"></a>特徵設計

R 有一個令人頭痛的問題，那就是其通常是在單一 CPU 上進行處理。 對於許多工作 (特別是特徵工程) 來說，這一點是主要的效能瓶頸。 在履歷表比對解決方案中，單單特徵工程工作就建立了 2,500 個必須與原本的 100 個特徵結合的乘積特徵。 如果所有程序都在單一 CPU 上進行，這項工作會花很長的時間。

有多種方式可以改善特徵工程的效能。 您可以將 R 程式碼最佳化並讓特徵擷取在模型化程序中進行，也可以將特徵工程程序移到 SQL 來進行。

- 使用 R。您可以定義函式，然後在定型期間將函式作為引數傳遞至 [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)。 如果模型支援平行處理，則可以使用多個 CPU 來處理特徵工程工作。 透過這種方法，資料科學小組發現，評分時間方面的效能提升了 16%。 不過，此方法需要有支援平行處理的模型，以及可使用平行計劃來執行的查詢。

- 搭配使用 R 與 SQL 計算內容。 在有隔離的資源可執行不同批次的多處理器環境中，您可以藉由隔離每個批次所用的 SQL 查詢，從資料表中擷取資料並將資料限制在相同的工作負載群組上，從而提升效率。 用來隔離批次的方法包括分割，以及使用 PowerShell 來平行執行個別查詢。

- 特定平行執行：在 SQL Server 計算內容中，您可以仰賴 SQL 資料庫引擎來強制進行平行執行，但前提是該選項要可行且更有效率。

- 在不同的特徵化程序中使用 T-SQL。 一般來說，使用 SQL 預先計算特徵資料通常會比較快。

### <a name="prediction-scoring-in-parallel"></a>平行預測 (評分)

SQL Server 的優點之一，就是能夠平行處理大量的資料列。 沒有任何工作會比評分更能看出這項優點。 一般而言，此模型不需要存取所有資料就能評分，因此您可以分割輸入資料，讓每個工作負載群組處理形成一個工作。

您也可以將輸入資料當作單一查詢來傳送，然後由 SQL Server 分析查詢。 如果可以為輸入資料建立平行查詢計劃，該計劃就會自動分割指派給節點的資料，並以平行方式執行所需的聯結和彙總。

如果您想要詳細了解如何定義用於評分的預存程序，請參閱 [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) 上的專案範例，並尋找 "step5_score_for_matching.sql" 檔案。 指令碼範例也會追蹤查詢的開始和結束時間，並將時間寫入到 SQL 主控台，以便您評估效能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用資源群組進行並行評分

若要擴大評分問題，最佳做法是採用 map-reduce 方法，讓數百萬個項目分割成多個批次。 然後，再並行執行多個評分作業。 在此架構中，批次會在不同的 CPU 集合上進行處理，然後再收集結果並寫回到資料庫。

這是履歷表比對案例中所用的方法；不過，若要實作此方法，SQL Server 中就不能缺少資源治理功能。 藉由為外部指令碼作業設定工作負載群組，您可以將 R 評分作業路由傳送至不同的處理器群組，以實現更快的輸送量。

資源治理也有助於配置分割伺服器上的可用資源 (CPU 和記憶體)，以將工作負載競爭情形降至最低。 您可以設定分類函式來區別不同類型的 R 作業：例如，您可以決定從應用程式呼叫的評分一律優先處理，而讓重新定型作業晚一點再處理。 此資源隔離動作有可能改善執行時間，並且會提供更可預測的效能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 進行並行評分

如果您決定自行分割資料，則可以使用 PowerShell 指令碼來執行多個並行評分工作。 若要這麼做，請使用 Invoke-SqlCmd Cmdlet，並以平行方式起始評分工作。

在履歷表比對案例中，並行處理的設計如下：

- 20 個處理器分成四個群組，每個群組有五個 CPU。 每個 CPU 群組都位於相同的 NUMA 節點上。

- 並行批次的最大數目設定為 8 個。

- 每個工作負載群組都必須處理兩個評分工作。 一旦有工作完成資料讀取並開始評分，另一個工作就可以開始從資料庫讀取資料。

若要查看此案例的 PowerShell 指令碼，請開啟 [Github 專案](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)中的 experiment.ps1 檔案。

### <a name="storing-models-for-prediction"></a>儲存用於預測的模型

當定型和評估作業完成，而且您已選取最佳模型時，建議您將該模型儲存在資料庫中，以便用於預測。 從資料庫載入預先計算的模型以進行預測會很有效率，因為 SQL Server 機器學習會在系統於 R 和資料庫之間移動時，使用特殊的序列化演算法來儲存和載入模型。

> [!TIP]
> 在 SQL Server 2017 中，即使 R 未安裝在伺服器上，您還是可以使用 PREDICT 函式來執行評分工作。 RevoScaleR 套件所支援的模型類型有限。

不過，視您使用的演算法而定，某些模型可能會很大，尤其是在大型資料集上定型時。 例如，**lm** 或 **glm** 之類的演算法會產生大量摘要資料以及規則。 因為可以儲存在 varbinary 資料行中的模型大小會受到限制，因此建議您先從模型中去除不必要的成品，然後再將模型儲存到生產環境的資料庫中。

## <a name="articles-in-this-series"></a>此系列中的文章

[R 的效能調整 - 簡介](../r/sql-server-r-services-performance-tuning.md)

[R 的效能調整 - SQL Server 設定](../r/sql-server-configuration-r-services.md)

[R 的效能調整 - R 程式碼和資料最佳化](../r/r-and-data-optimization-r-services.md)

[效能調整 - 案例研究結果](../r/performance-case-study-r-services.md)
