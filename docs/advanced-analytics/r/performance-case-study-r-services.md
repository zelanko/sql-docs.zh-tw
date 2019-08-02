---
title: SQL Server R Services 的效能-結果和資源
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aa56a9367271df2172236b133d85b5771089b1ac
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715038"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services 的效能: 結果和資源
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列中的第四個和最後一個, 描述 R 服務的效能優化。 本文摘要說明兩個測試各種優化方法之個案研究的方法、結果和結論。

這兩個案例研究有不同的目標:

+ 第一次使用 R Services 開發小組的案例研究, 以測量特定優化技巧的影響
+ 第二個案例研究 (由資料科學家小組實驗) 會使用多種方法來判斷特定大量評分案例的最佳優化。

本主題列出第一個案例研究的詳細結果。 針對第二個案例研究, 摘要說明整體結果。 本主題的結尾是所有腳本和範例資料的連結, 以及原始作者所使用的資源。

## <a name="performance-case-study-airline-dataset"></a>效能案例研究:航空公司資料集

SQL Server R Services 開發小組的這種案例研究已測試各種優化的效果。 建立單一 rxLogit 模型, 並對航空公司資料集執行評分。 優化會在定型和評分程式期間套用, 以評估個別的影響。

- GitHubSQL Server 優化研究的[範例資料和腳本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>測試方法

1. 航空公司資料集包含單一資料表的1千萬個列。 它已下載並大量載入 SQL Server。
2. 已製作資料表的六份複本。
3. 已將各種修改套用到資料表的複本, 以測試 SQL Server 的功能, 例如頁面壓縮、資料列壓縮、索引、單欄式資料存放區等。
4. 效能是在套用每個優化之前和之後測量。

| 資料表名稱| 描述|
|------|------|
| *airline* | 使用 `rxDataStep` 從原始 xdf 檔案轉換的資料|                          |
| *airlineWithIntCol*   | 轉換成整數而不是字串的 *DayOfWeek*。 會一併新增 *rowNum* 資料行。|
| *airlineWithIndex*    | 與 *airlineWithIntCol* 資料表的資料相同，但是具有使用 *rowNum* 資料行的單一叢集索引。|
| *airlineWithPageComp* | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用頁面壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineWithRowComp*  | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用資料列壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineColumnar*     | 具有單一叢集索引的單欄式存放區。 此資料表中會填入來自已清除之 csv 檔案的資料。|

每項測試都是由下列步驟組成:

1. 在每次測試之前都引發了 R 記憶體回收。
2. 羅吉斯回歸模型是根據資料表資料所建立。 每個測試的 *rowsPerRead* 的值是設定為 500000。
3. 分數是使用定型的模型產生的
4. 每項測試都執行六次。 第一次執行的時間 (「冷執行」) 已卸載。 若要允許偶爾的極端值, 剩餘五次執行的時間**上限**也會一併卸載。 系統取剩餘四次執行的平均值，來計算每個測試的平均經過執行時間。
5. 測試是使用*reportProgress*參數來執行, 其值為 3 (= 報告時間和進度)。 每個輸出檔都包含關於 IO、轉換時間和計算時間所花費之時間的資訊。 這些時間對於進行疑難排解和診斷相當有用。
6. 主控台輸出也會導向至輸出目錄中的檔案。
7. 測試腳本會處理這些檔案中的時間, 以計算執行的平均時間。

例如, 下列結果是來自單一測試的時間。 主要的相關時間為「總讀取時間」(IO 時間) 和「轉換時間」(在設定處理序以進行計算方面的負擔)。

**取樣時間**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

我們建議您下載並修改測試腳本, 以協助您針對 R Services 或 RevoScaleR 函數的問題進行疑難排解。

### <a name="test-results-all"></a>測試結果 (全部)

本節會比較每個測試的前後結果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>具有壓縮和單欄式資料表存放區的資料大小

第一項測試會比較使用壓縮和單欄式資料表來減少資料的大小。

| 資料表名稱            | 資料列     | 已保留   | Data       | index_size | 未使用  | 節省 % (已保留) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/a        | 368 KB  | 93%                 |

**結論**

藉由套用資料行存放區索引, 然後再進行頁面壓縮, 即可達到最大的資料大小縮減。

#### <a name="effects-of-compression"></a>壓縮的效果

這項測試會比較資料列壓縮、頁面壓縮和無壓縮的優點。 已使用從三個`rxLinMod`不同資料表的資料來定型模型。 針對所有資料表都使用了相同的公式和查詢。

| 資料表名稱            | 測試名稱       | numTasks | 平均時間 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-平行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-平行 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-平行  | 4        | 5.2375       |

**結論**

壓縮本身似乎不會提供協助。 在此範例中, 用來處理壓縮的 CPU 增加會補償 IO 時間降低的情況。

不過，當透過將 *numTasks* 設定為 4 來平行執行測試時，平均時間就會減少。

針對較大的資料集，壓縮的效果可能較為明顯。 壓縮取決於資料集和值，因此可能需要透過實驗，才能判斷壓縮對您資料集的影響。

### <a name="effect-of-windows-power-plan-options"></a>Windows 電源計劃選項的效果

在此實驗中，`rxLinMod` 是與 *airlineWithIntCol* 資料表搭配使用。 Windows 電源計劃已設定為 [**平衡**] 或 [**高效**能]。 所有測試的 *numTasks* 都是設定為 1。 測試執行了六次, 並在這兩個電源選項下執行兩次, 以調查結果的變化性。

**高效**能電源選項:

| 測試名稱 | 執行 \# | 經過時間 | 平均時間 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.57 秒 |              |
|           | 2      | 3.45 秒 |              |
|           | 3      | 3.45 秒 |              |
|           | 4      | 3.55 秒 |              |
|           | 5      | 3.55 秒 |              |
|           | 6      | 3.45 秒 |              |
|           |        |              | 3.475        |
|           | 1      | 3.45 秒 |              |
|           | 2      | 3.53 秒 |              |
|           | 3      | 3.63 秒 |              |
|           | 4      | 3.49 秒 |              |
|           | 5      | 3.54 秒 |              |
|           | 6      | 3.47 秒 |              |
|           |        |              | 3.5075       |

「平衡」電源選項：

| 測試名稱 | 執行 \# | 經過時間 | 平均時間 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.89 秒 |              |
|           | 2      | 4.15 秒 |              |
|           | 3      | 3.77 秒 |              |
|           | 4      | 5 秒    |              |
|           | 5      | 3.92 秒 |              |
|           | 6      | 3.8 秒  |              |
|           |        |              | 3.91         |
|           | 1      | 3.82 秒 |              |
|           | 2      | 3.84 秒 |              |
|           | 3      | 3.86 秒 |              |
|           | 4      | 4.07 秒 |              |
|           | 5      | 4.86 秒 |              |
|           | 6      | 3.75 秒 |              |
|           |        |              | 3.88         |

**結論**

使用 Windows**高效**能電源計劃時, 執行時間會更一致且更快。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整數和字串

這項測試已評估修改 R 程式碼的影響, 以避免字串因數的常見問題。 具體而言, 模型已使用`rxLinMod`兩個數據表來定型: 第一個中的因素會儲存為字串; 在第二個數據表中, 因素會儲存為整數。

+ 針對*航班*資料表, [DayOfWeek] 資料行包含字串。 _ColInfo_參數是用來指定因數層級 (星期一、星期二、...)

+  對於*airlineWithIndex*資料表, [DayOfWeek] 是一個整數。 未指定_colInfo_參數。

+ 在這兩個案例中，使用了相同的公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 資料表名稱          | 測試名稱   | 平均時間 |
|---------------------|-------------|--------------|
| *航空公司*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**結論**

使用整數而非字串做為因素時, 有一個明顯的好處。

### <a name="avoiding-transformation-functions"></a>避免轉換函數

在此測試中, 模型已使用`rxLinMod`定型, 但程式碼在兩個回合之間已變更:

+ 第一次執行時, 會將轉換函式套用為模型建立的一部分。 
+ 在第二次執行時, 會預先計算並提供功能值, 因此不需要任何轉換函數。

| 測試名稱             | 平均時間 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**結論**

定型時間較短, 但**不**使用轉換函數。 換句話說, 使用在資料表中預先計算並保存的資料行時, 模型的定型速度較快。

如果有更多的轉換, 且資料集較大 (\> 100M), 則節省的成本應該會更高。

### <a name="using-columnar-store"></a>使用單欄式存放區

這項測試已評估使用單欄式資料存放區和索引的效能優勢。 相同的模型已使用`rxLinMod`定型, 而且沒有任何資料轉換。

+ 在第一次執行時, 資料表使用的是標準資料列存放區。
+ 第二次執行時, 會使用資料行存放區。

| 資料表名稱         | 測試名稱 | 平均時間 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**結論**

單欄式存放區的效能優於標準資料列存放區。 較大的資料集 (\> 100 M) 可能會有顯著的效能差異。

### <a name="effect-of-using-the-cube-parameter"></a>使用 cube 參數的效果

這項測試的目的是要判斷 RevoScaleR 中使用預先計算**cube**參數的選項是否可以改善效能。 模型是使用來`rxLinMod`定型, 使用下列公式:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在資料表中, *DayOfWeek*因數會儲存為字串。

| 測試名稱     | Cube 參數 | numTasks | 平均時間 | 單一資料列預測 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**結論**

使用 cube 參數引數可清楚改善效能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>變更 rxDTree 模型之 maxDepth 的效果

在此實驗中, `rxDTree`演算法是用來在*airlineColumnar*資料表上建立模型。 此測試的 *numTasks* 是設定為 4。 *MaxDepth*有數個不同的值, 用來示範改變樹狀結構深度會如何影響執行時間。

| 測試名稱       | maxDepth | 平均時間 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**結論**

當樹狀結構的深度增加時, 節點總數會以指數方式增加。 建立模型所經過的時間也會大幅增加。

### <a name="prediction-on-a-stored-model"></a>預存模型的預測

這項測試的目的是要判斷當定型模型儲存至 SQL Server 資料表而不是當做目前執行程式碼的一部分產生時, 評分的效能影響。 針對計分, 會從資料庫載入預存模型, 並使用記憶體中的單一資料列資料框架 (本機計算內容) 來建立預測。

測試結果會顯示儲存模型的時間, 以及載入模型和預測所花費的時間。

| 資料表名稱 | 測試名稱 | 平均時間 (用於訓練模型) | 儲存/載入模型的時間|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09 (包括用於預測的時間) |

**結論**

從資料表載入定型的模型, 顯然是執行預測的更快速方式。 我們建議您避免在相同的腳本中建立模型並執行評分。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究:繼續比對工作的優化

繼續比對模型是由 Microsoft 資料科學家 Ke Huang 所開發, 可在 SQL Server 中測試 R 程式碼的效能, 並藉此協助資料科學家建立可調整的企業級解決方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 封裝都是用來在涉及大型資料集的複雜 R 方案中定型預測模型。 所有測試中的 SQL 查詢和 R 程式碼都相同。 測試是在已安裝 SQL Server 的單一 Azure VM 上執行。 然後, 作者會比較計分時間與和, 而不會 SQL Server 所提供的下列優化:

- 記憶體內部資料表
- ssNoVersion
- [資源管理員]

為了評估 R 腳本執行的軟體 NUMA 效果, 資料科學小組在具有20個實體核心的 Azure 虛擬機器上測試了解決方案。 在這些實體核心上, 會自動建立四個軟體 NUMA 節點, 讓每個節點都包含五個核心。

CPU affinitization 是在繼續比對案例中強制執行, 以評估對 R 作業的影響。 已建立四個**SQL 資源**集區和四個**外部資源**集區, 並指定 CPU 親和性, 以確保每個節點都使用同一組 cpu。

每個資源集區都已指派給不同的工作負載群組, 以優化硬體使用率。 原因是軟體 NUMA 和 CPU 親和性無法分割實體 NUMA 節點中的實體記憶體;因此, 根據定義, 所有以相同實體 NUMA 節點為基礎的軟 NUMA 節點, 都必須在相同的 OS 記憶體區塊中使用記憶體。 換句話說, 沒有記憶體對處理器的親和性。

下列進程是用來建立此設定:

1. 將預設配置的記憶體數量減少為 SQL Server。

2. 建立四個新的集區, 以平行方式執行 R 作業。

3. 建立四個工作負載群組, 讓每個工作負載群組與資源集區相關聯。

4. 使用新的工作負載群組和指派重新開機 Resource Governor。

5. 建立使用者定義的分類函數 (UDF), 以在不同的工作負載群組上指派不同的作業。

6. 更新 Resource Governor 設定, 以針對適當的工作負載群組使用函數。

### <a name="results"></a>結果

在繼續比對研究中具有最佳效能的設定如下所示:

-   四個內部資源集區 (適用于 SQL Server)

-   四個外部資源集區 (適用于外部腳本作業)

-   每個資源集區都與特定的工作負載群組相關聯

-   每個資源集區都會指派給不同的 Cpu

-   最大內部記憶體使用量 (適用于 SQL Server) = 30%

-   R 會話使用的最大記憶體 = 70%

對於繼續比對模型, 外部腳本使用很繁重, 而且沒有其他資料庫引擎服務正在執行。 因此, 配置給外部腳本的資源已增加至 70%, 這證明了最佳的腳本效能設定。

這項設定是藉由試驗不同的值來到達。 如果您使用不同的硬體或不同的解決方案, 最佳設定可能會不同。 請一律試驗以尋找適合您案例的最佳設定!

在優化解決方案中, 1100000 個數據列 (含100功能) 在20核心電腦的8.5 秒內進行評分。 優化在計分時間方面大幅提升了效能。

結果也會建議**功能數目**對評分時間有顯著的影響。 當預測模型中使用更多的功能時, 改善效果更明顯。

我們建議您閱讀這篇 blog 文章和隨附的教學課程, 以取得詳細的討論。

-   [SQL Server 中機器學習服務的優化秘訣和訣竅](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

許多使用者都注意到, 第一次載入 R (或 Python) 執行時間時, 會有短暫的暫停。 基於這個理由, 如這些測試中所述, 第一次執行的時間通常會測量, 但稍後會被捨棄。 後續的快取可能會導致第一個和第二次執行之間有顯著的效能差異。 在 SQL Server 和外部執行時間之間移動資料時, 也會有一些額外負荷, 特別是當資料是透過網路傳遞, 而不是直接從 SQL Server 載入時。

基於上述所有原因, 沒有單一解決方案可減輕此初始載入時間, 因為效能影響會因工作而有很大的差異。 例如, 針對批次中的單一資料列評分執行快取;因此, 後續評分作業的速度會更快, 而且不會重載模型或 R 執行時間。 您也可以使用[原生評分](../sql-native-scoring.md)來避免完全載入 R 執行時間。

若要定型大型模型, 或以大型批次評分, 相較于避免資料移動或串流處理和平行處理的增益, 額外負荷可能會比較少。 如需其他效能指引, 請參閱這篇文章:

+ [使用 R 偵測每秒1000000筆交易的詐騙](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>資源

以下是在開發這些測試時所使用的資訊、工具和腳本的連結。

+ 效能測試腳本和資料的連結:[SQL Server 優化研究的範例資料和腳本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 描述繼續比對解決方案的文章:[SQL Server R Services 的優化秘訣和訣竅](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 用於繼續比對解決方案的 SQL 優化中的腳本:[GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>瞭解 Windows server 管理

+ [如何判斷適用於 64 位元版本 Windows 的適當分頁檔大小](https://support.microsoft.com/kb/2860880)

+ [瞭解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支援 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>瞭解 SQL Server 優化

+ [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [記憶體優化資料表簡介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [示範：記憶體內部 OLTP 的效能改善](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [停用資料表或索引的壓縮](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>瞭解如何管理 SQL Server

+ [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [資源管理員](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor 簡介](https://technet.microsoft.com/library/bb895232.aspx)

+ [的資源管理](resource-governance-for-r-services.md)

+ [如何建立 R 的資源集區](how-to-create-a-resource-pool-for-r.md)

+ [設定 Resource Governor 的範例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 儲存體負載產生器/效能測試工具 (英文)](https://github.com/microsoft/diskspd)

+ [FSUtil 公用程式參考 (英文)](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>本系列的其他文章

[R 效能微調-簡介](sql-server-r-services-performance-tuning.md)

[R SQL Server 設定的效能微調](sql-server-configuration-r-services.md)

[R-R 程式碼和資料優化的效能微調](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
