---
title: SQL Server R Services-「 結果 」 和 「 資源 」-SQL Server Machine Learning 服務的效能
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 392a6da09827355e6bc9a901b0e4580e5eb72bf5
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645550"
---
# <a name="performance-for-r-services-results-and-resources"></a>R services 的效能： 結果和資源
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是第四個，並說明 R services 效能最佳化的最後一個數列中。 本文摘要說明的方法、 發現和測試各種最佳化方法的兩個案例研究的結論。

兩個案例研究有不同的目標：

+ 第一個案例研究中，R Services 開發小組所要搜尋來測量特定的最佳化技術的影響
+ 第二個案例研究中，資料科學家小組，透過實驗使用多種方法以判斷最佳的最佳化，為特定的高容量評分的案例。

本主題列出第一個案例研究的詳細的結果。 針對第二個案例研究，摘要說明整體的結果。 在本主題結尾處是連結至所有指令碼和範例資料，以及原始作者所使用的資源。

## <a name="performance-case-study-airline-dataset"></a>效能案例研究：航班資料集

此案例研究，由 SQL Server R Services 開發小組測試各種最佳化的效果。 建立單一 rxLogit 模型和計分方式航線資料集上執行。 在訓練和評分來評估個別影響的程序期間套用最佳化。

- Github:[範例資料和指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)如 SQL Server 最佳化研究

### <a name="test-methods"></a>測試方法

1. 航班資料集包含 10 億個資料列的單一資料表。 它下載並大量載入到 SQL Server。
2. 已進行的六份資料表。
3. 各種修改已套用至資料表 （若要測試 SQL Server 功能，例如頁面壓縮，資料列壓縮，編製索引、 單欄式資料存放區等） 的複本。
4. 已套用每個最佳化之前和之後，就被測量效能。

| 資料表名稱| 描述|
|------|------|
| *airline* | 使用 `rxDataStep` 從原始 xdf 檔案轉換的資料|                          |
| *airlineWithIntCol*   | 轉換成整數而不是字串的 *DayOfWeek*。 會一併新增 *rowNum* 資料行。|
| *airlineWithIndex*    | 與 *airlineWithIntCol* 資料表的資料相同，但是具有使用 *rowNum* 資料行的單一叢集索引。|
| *airlineWithPageComp* | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用頁面壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineWithRowComp*  | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用資料列壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineColumnar*     | 具有單一叢集索引的單欄式存放區。 此資料表中會填入來自已清除之 csv 檔案的資料。|

每項測試是由下列步驟所組成：

1. 在每次測試之前都引發了 R 記憶體回收。
2. 羅吉斯迴歸模型是根據資料表資料所建立。 每個測試的 *rowsPerRead* 的值是設定為 500000。
3. 使用定型的模型產生分數
4. 每個測試都執行六次。 第一次執行 （冷執行） 的時間已卸除。 若要偶爾的極端值，允許**最大**剩餘五次執行之間的時間也捨棄不用。 系統取剩餘四次執行的平均值，來計算每個測試的平均經過執行時間。
5. 使用已執行測試*reportProgress*參數的值是 3 （= 報表執行時間和進度）。 每個輸出檔案包含有關在 IO、 轉換階段及運算階段所花費的時間資訊。 這些時間對於進行疑難排解和診斷相當有用。
6. 主控台輸出也被導向到輸出目錄中的檔案。
7. 測試指令碼處理這些檔案，以透過執行計算的平均時間的時間。

例如，下列的結果會是從單一測試的時間。 主要的相關時間為「總讀取時間」(IO 時間) 和「轉換時間」(在設定處理序以進行計算方面的負擔)。

**範例時間**

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

我們建議您下載並修改測試指令碼，可協助您疑難排解問題和 R Services，或使用 RevoScaleR 函式。

### <a name="test-results-all"></a>測試結果 （全部）

本節將比較針對每個測試之前和之後的結果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>使用壓縮和單欄式資料表存放區的資料大小

第一項測試會比較使用壓縮和單欄式資料表，以減少資料的大小。

| 資料表名稱            | 資料列     | 已保留   | 資料       | index_size | 未使用  | 節省 % (已保留) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/a        | 368 KB  | 93%                 |

**結論**

資料大小的最大減少已所套用的資料行存放區索引，後面接著頁面壓縮而達成的。

#### <a name="effects-of-compression"></a>壓縮的效果

這項測試會比較資料列壓縮、 頁面壓縮和未壓縮的優點。 使用定型模型`rxLinMod`三個不同資料表的資料。 針對所有資料表都使用了相同的公式和查詢。

| 資料表名稱            | 測試名稱       | numTasks | 平均時間 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-平行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - parallel  | 4        | 5.2375       |

**結論**

僅使用壓縮似乎並沒有幫助。 在此範例中，增加的 CPU 處理壓縮會減少 IO 時間的補償。

不過，當透過將 *numTasks* 設定為 4 來平行執行測試時，平均時間就會減少。

針對較大的資料集，壓縮的效果可能較為明顯。 壓縮取決於資料集和值，因此可能需要透過實驗，才能判斷壓縮對您資料集的影響。

### <a name="effect-of-windows-power-plan-options"></a>Windows 電源計劃選項的效果

在此實驗中，`rxLinMod` 是與 *airlineWithIntCol* 資料表搭配使用。 Windows 電源計劃設定為**平衡**或是**高效能**。 所有測試的 *numTasks* 都是設定為 1。 測試都執行六次，並執行兩次這兩種電源選項下調查結果的變化性。

**高效能**電源選項：

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

執行時間會更一致且更快使用 Windows 時**高效能**電源計劃。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整數和字串比較

這項測試會評估修改 R 程式碼，以避免常見的問題，具有字串因數的影響。 具體來說，使用定型模型`rxLinMod`使用兩個資料表： 在第一個因素都會儲存為字串，在第二個資料表中，因素會儲存為整數。

+ 針對*airline*資料表中，[DayOfWeek] 資料行包含字串。 _ColInfo_參數用來指定因數層級 （星期一、 星期二、...）

+  針對*airlineWithIndex*資料表，[DayOfWeek] 是一個整數。 _ColInfo_未指定參數。

+ 在這兩個案例中，使用了相同的公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 資料表名稱          | 測試名稱   | 平均時間 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**結論**

使用的因素的整數，而不是字串時，沒有明顯的好處。

### <a name="avoiding-transformation-functions"></a>避免轉換函式

在此測試中，已訓練模型使用`rxLinMod`，但兩個回合已變更的程式碼：

+ 在初次執行時，轉換函式套用做為模型建立的一部分。 
+ 如果您在第二個執行中，功能值已預先計算和可用的因此沒有任何轉換函式所需。

| 測試名稱             | 平均時間 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**結論**

定型時間已縮短時**不**使用轉換函數。 換句話說，此模型定型速度時使用已預先計算並保存在資料表的資料行。

省下的預期會更高，如果沒有更多轉換且資料集是較大 (\> 100m)。

### <a name="using-columnar-store"></a>使用單欄式存放區

這項測試來評估使用單欄式資料存放區和索引的效能優勢。 相同的模型定型使用`rxLinMod`和任何資料轉換。

+ 在初次執行時，資料表會使用標準的資料列存放區。
+ 如果您在第二個執行中，使用資料行存放區。

| 資料表名稱         | 測試名稱 | 平均時間 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**結論**

效能是透過比標準的資料列存放區使用的單欄式存放區更趨完美。 在較大的資料集上的預期效能有顯著差異 (\> 100m)。

### <a name="effect-of-using-the-cube-parameter"></a>使用 cube 參數的效果

這項測試的目的是要判斷是否 RevoScaleR 中的選項，即可使用預先計算**cube**參數可提升效能。 使用定型模型`rxLinMod`，使用下列公式：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在資料表中，的因素*DayOfWeek*儲存為字串。

| 測試名稱     | Cube 參數 | numTasks | 平均時間 | 單一資料列預測 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**結論**

Cube 參數引數使用明顯改善效能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>變更模型 rxDTree 的 maxDepth 效果

在此實驗中，`rxDTree`演算法用來在建立模型*airlineColumnar*資料表。 此測試的 *numTasks* 是設定為 4。 數個不同的值，如*maxDepth*來示範如何修改樹狀結構深度會影響執行的階段。

| 測試名稱       | maxDepth | 平均時間 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**結論**

樹狀結構深度增加時，會以指數方式增加的節點總數。 建立模型所經過時間也大幅增加。

### <a name="prediction-on-a-stored-model"></a>預存模型的預測

這項測試的目的是要判斷在評分定型的模型儲存至 SQL Server 資料表時的效能影響，而不是目前正在執行的程式碼中產生。 計分，預存的模型從資料庫載入，並使用 記憶體 （本機計算內容） 中的 單一資料列資料框架建立預測。

測試結果會顯示將儲存模型及載入模型並進行預測所花費的時間。

| 資料表名稱 | 測試名稱 | 平均時間 (用於訓練模型) | 儲存/載入模型的時間|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09 (包括用於預測的時間) |

**結論**

從資料表載入定型的模型，顯然是更快的方法，來進行預測。 我們建議您避免建立模型，以及執行評分全都放在相同的指令碼。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究：繼續比對工作的最佳化

繼續比對的模型開發由 Microsoft 資料科學家 Ke Huang 來測試 SQL Server 中的 R 程式碼的效能和進行如此說明資料科學家建立可調整的企業級解決方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 套件用來訓練預測模型中複雜的 R 解決方案，牽涉到大型資料集。 SQL 查詢和 R 程式碼是相同的所有測試。 SQL server 安裝在單一 Azure VM 上進行測試。 作者接著會比較評分的時間，而 SQL Server 所提供的下列最佳化：

- 記憶體中的資料表
- ssNoVersion
- [資源管理員]

若要評估軟體 NUMA 的 R 指令碼執行的效果，資料科學小組測試 20 個實體核心 Azure 虛擬機器上的解決方案。 這些實體的核心，在四個軟體 NUMA 節點已自動建立，使每個節點包含五個核心。

在繼續比對的情況下，評估對 R 作業的影響，已強制執行 CPU 分配。 四個**SQL 資源集區**和第四個**外部資源集區**所建立，並確保 Cpu 的同一組會用於每個節點指定 CPU 親和性。

每個資源集區已指派給不同的工作負載群組，以最佳化的硬體使用率。 原因是該軟體式 NUMA 和 CPU 親和性無法分割實體的 NUMA 節點; 中的實體記憶體因此，根據定義根據相同的實體 NUMA 節點的所有軟體 NUMA 節點必須使用記憶體中的相同作業系統記憶體區塊。 換句話說，是沒有記憶體對處理器親和性。

下列程序可用來建立此組態：

1. 降低預設配置給 SQL Server 的記憶體的數量。

2. 建立四個新的集區以平行方式執行 R 作業。

3. 每個工作負載群組是資源集區相關聯，請建立四個工作負載群組。

4. 重新啟動 Resource Governor，以使用新的工作負載群組和指派。

5. 建立使用者定義分類函數 (UDF) 來指派不同的工作負載群組的不同工作。

6. 更新資源管理員的組態使用適當的工作負載群組的函數。

### <a name="results"></a>結果

有最佳效能的繼續符合研究的組態如下所示：

-   （適用於 SQL Server) 的四個內部資源集區

-   （適用於外部指令碼工作） 的四個外部資源集區

-   每個資源集區是與特定的工作負載群組相關聯

-   每個資源集區指派給不同的 Cpu

-   內部記憶體使用量上限 （適用於 SQL Server) = 30%

-   R 工作階段所使用的最大記憶體 = 70%

繼續比對模型中，外部指令碼的用途是大量，而且已沒有其他資料庫引擎服務執行。 因此，配置給外部指令碼的資源已增加到 70%，已證明指令碼效能的最佳組態。

藉由試驗不同的值，這個組態已抵達。 如果您使用不同的硬體或不同的解決方案，最佳的組態可能會不同。 一律體驗來尋找適合您案例的最佳組態 ！

在最佳化解決方案中，在 20 個核心電腦上的 8.5 秒內計分 1.1 一百萬個 （含 100 的功能） 的資料列。 最佳化大幅改善了效能評分的時間。

結果也建議所**功能的數字**評分時間上有重大影響。 更多的功能用於預測模型時，甚至更為顯著改進。

我們建議您先閱讀此部落格文章及隨附的教學課程中詳細討論。

-   [最佳化的秘訣和訣竅，SQL Server 中的機器學習](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

許多使用者已記下會有小型的暫停 R （或 Python） 的執行階段載入第一次。 基於這個理由，這些測試，所述的第一次執行時間是通常長達，但之後捨棄。 後續快取可能會造成顯著的效能差異第一個和第二個執行。 另外還有一些額外負荷當資料移動會與 SQL Server 外部執行階段中，尤其是透過網路，而不是直接從 SQL Server 載入傳遞資料。

基於這些理由，沒有單一解決方案來降低此初始載入期間，因為工作而大幅有所不同的效能影響。 例如，快取執行的單一資料列批次; 中的評分因此，後續的計分作業更快而且模型和 R 執行階段都不會重新載入。 您也可以使用[原生評分](../sql-native-scoring.md)以避免完全載入的 R 執行階段。

對於訓練大型模型，或以大型批次評分，額外負荷可能微小的提升，避免資料移動或串流處理和平行處理。 請參閱此部落格文章的其他效能指導方針：

+ [使用 R 來偵測詐騙在 1 百萬個每秒交易數](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>資源

以下是資訊、 工具和開發的這些測試中使用指令碼的連結。

+ 效能測試指令碼和資料的連結：[範例資料和 SQL Server 最佳化研究的指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 描述繼續比對解決方案的文章：[最佳化提示和訣竅 SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 用於繼續比對方案最佳化 SQL 指令碼：[GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>深入了解 Windows server 管理

+ [如何判斷適用於 64 位元版本 Windows 的適當分頁檔大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支援 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>深入了解 SQL Server 最佳化

+ [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [記憶體最佳化的資料表簡介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [示範：記憶體中 OLTP 的效能改善](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [停用資料表或索引的壓縮](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [資源管理員](../../relational-databases/resource-governor/resource-governor.md)

+ [資源管理員簡介](https://technet.microsoft.com/library/bb895232.aspx)

+ [的資源管理](resource-governance-for-r-services.md)

+ [如何建立 R 的資源集區](how-to-create-a-resource-pool-for-r.md)

+ [設定資源管理員的範例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 儲存體負載產生器/效能測試工具 (英文)](https://github.com/microsoft/diskspd)

+ [FSUtil 公用程式參考 (英文)](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>在這一系列其他文章

[效能微調的 R-簡介](sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](sql-server-configuration-r-services.md)

[R-R 效能微調程式碼和資料最佳化](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
