---
title: 針對結果進行效能微調
description: 本文將摘要說明兩個測試過各種最佳化方法之案例研究的方法、結果和結論。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6afdda3975fc8f6c269f9c1fcbca35318f0c4da
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179990"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services 的效能：結果和資源
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文是一系列文章中的第四篇 (也是最後一篇)，會描述 R Services 的效能最佳化。 本文將摘要說明兩個測試過各種最佳化方法之案例研究的方法、結果和結論。

這兩個案例研究具有不同的目標：

+ 第一個案例研究是由 R Services 開發小組所進行，其試圖測量特定最佳化技術的影響
+ 第二個案例研究是由資料科學家小組所進行，其使用了多種方法進行實驗，以針對特定的大量評分案例決定最佳化的最好方式。

本主題將列出第一個案例研究的詳細結果。 針對第二個案例研究，則會摘要說明整體調查結果。 此主題的結尾將提供所有指令碼和範例資料的連結，以及原始作者所使用的資源。

## <a name="performance-case-study-airline-dataset"></a>效能案例研究：航空公司資料集

這個由 SQL Server R Services 開發小組所進行的案例研究已測試過各種最佳化的效果。 建立單一 rxLogit 模型，並對航空公司資料集執行評分。 最佳化會在定型和評分期間套用，以評估個別的影響。

- GitHub：適用於 SQL Server 最佳化研究的[範例資料和指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) \(英文\)

### <a name="test-methods"></a>測試方法

1. 航空公司資料集包含具有 1000 萬筆資料列的單一資料表。 已將它下載並大量載入到 SQL Server。
2. 已針對該資料表製作六份複本。
3. 已將各種修改套用到資料表的複本，以測試 SQL Server 功能，例如，頁面壓縮、資料列壓縮、編製索引、單欄式資料存放區等。
4. 效能會在套用每個最佳化前後進行測量。

| 資料表名稱| 描述|
|------|------|
| *airline* | 使用 `rxDataStep` 從原始 xdf 檔案轉換的資料|                          |
| *airlineWithIntCol*   | 轉換成整數而不是字串的 *DayOfWeek*。 會一併新增 *rowNum* 資料行。|
| *airlineWithIndex*    | 與 *airlineWithIntCol* 資料表的資料相同，但是具有使用 *rowNum* 資料行的單一叢集索引。|
| *airlineWithPageComp* | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用頁面壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineWithRowComp*  | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用資料列壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineColumnar*     | 具有單一叢集索引的單欄式存放區。 此資料表中會填入來自已清除之 csv 檔案的資料。|

每個測試都是由下列步驟所組成：

1. 在每次測試之前都引發了 R 記憶體回收。
2. 羅吉斯迴歸模型會根據資料表資料來建立。 每個測試的 *rowsPerRead* 的值是設定為 500000。
3. 分數會使用定型的模型來產生。
4. 每個測試都會執行六次。 已將第一次執行 (冷執行) 的時間捨棄不用。 考慮到偶爾會有極端值的情況，因此也會將剩餘五次執行之間**最長**的時間捨棄不用。 系統取剩餘四次執行的平均值，來計算每個測試的平均經過執行時間。
5. 測試會使用值為 3 (= 報告時間和進度) 的 *reportProgress* 參數來執行。 每個輸出檔都包含在 IO、轉換時間及計算時間上所花費時間的相關資訊。 這些時間對於進行疑難排解和診斷相當有用。
6. 系統也會將主控台輸出導向到輸出目錄中的檔案。
7. 測試指令碼會處理這些檔案中的時間，以計算每次執行的平均時間。

例如，下列結果是來自單一測試的時間。 主要的相關時間為「總讀取時間」  (IO 時間) 和「轉換時間」  (在設定處理序以進行計算方面的負擔)。

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

我們建議您下載並修改測試指令碼，以協助您針對 R Services 或 RevoScaleR 函式的問題進行疑難排解。

### <a name="test-results-all"></a>測試結果 (全部)

本節將比較每個測試的前後結果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>壓縮後的資料大小和單欄式資料表存放區

第一個測試會比較壓縮和單欄式資料表的使用方式，以縮減資料大小。

| 資料表名稱            | 資料列     | Reserved   | 資料       | index_size | 未使用  | 節省 % (已保留) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/a        | 368 KB  | 93%                 |

**結論**

藉由套用資料行存放區索引，然後進行頁面壓縮，即可達到最大程度的資料大小縮減。

#### <a name="effects-of-compression"></a>壓縮的效果

此測試會比較資料列壓縮、頁面壓縮和無壓縮的優點。 已根據來自三個不同資料表的資料，使用 `rxLinMod` 來將模型定型。 針對所有資料表都使用了相同的公式和查詢。

| 資料表名稱            | 測試名稱       | numTasks | 平均時間 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - parallel| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - parallel  | 4        | 5.2375       |

**結論**

單獨使用壓縮似乎無濟於事。 在此範例中，提高用來處理壓縮的 CPU 可補償 IO 時間的減少。

不過，當透過將 *numTasks* 設定為 4 來平行執行測試時，平均時間就會減少。

針對較大的資料集，壓縮的效果可能較為明顯。 壓縮取決於資料集和值，因此可能需要透過實驗，才能判斷壓縮對您資料集的影響。

### <a name="effect-of-windows-power-plan-options"></a>Windows 電源計劃選項的效果

在此實驗中，`rxLinMod` 是與 *airlineWithIntCol* 資料表搭配使用。 Windows 電源計劃已設定為 [平衡]  或 [高效能]  。 所有測試的 *numTasks* 都是設定為 1。 此測試執行了六次，並且在這兩種電源選項下各執行了兩次，以調查結果的變化性。

**高效能**電源選項：

| 測試名稱 | \#執行 | 經過時間 | 平均時間 |
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

「平衡」  電源選項：

| 測試名稱 | \#執行 | 經過時間 | 平均時間 |
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

使用 Windows **高效能**電源計劃時，執行時間較為一致且速度更快。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整數和字串

此測試會評估對於修改 R 程式碼以避免發生字串因數常見問題的影響。 具體而言，模型會利用兩個資料表，使用 `rxLinMod`來定型：在第一個資料表中，將因數儲存為字串；在第二個資料表中，則會將因數儲存為整數。

+ 針對 *airline* 資料表，[DayOfWeek] 資料行包含字串。 _colInfo_ 參數可用來指定因數層級 (星期一、星期二、…)

+  針對 *airlineWithIndex* 資料表，[DayOfWeek] 是整數。 未指定 _colInfo_ 參數。

+ 在這兩個案例中，使用了相同的公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 資料表名稱          | 測試名稱   | 平均時間 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**結論**

使用整數而非字串作為因數時，有一個明顯的優點。

### <a name="avoiding-transformation-functions"></a>避免使用轉換函式

在此測試中，模型會使用 `rxLinMod` 來定型，但程式碼已在兩次執行之間加以變更：

+ 第一次執行時，會在模型建置期間套用轉換函式。 
+ 第二次執行時，則會預先計算並提供功能值，因而不需任何轉換函式。

| 測試名稱             | 平均時間 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**結論**

**未**使用轉換函式時，定型時間較短。 換句話說，使用在資料表中預先計算並保存的資料行時，模型的定型速度較快。

如果有更多轉換且資料集更大 (\> 100M)，預期節省量將更為明顯。

### <a name="using-columnar-store"></a>使用單欄式存放區

此測試會評估使用單欄式資料存放區和索引的效能優點。 相同模型會使用 `rxLinMod` 來定型，而且不需任何資料轉換。

+ 第一次執行時，資料表使用的是標準資料列存放區。
+ 第二次執行時，則會使用資料行存放區。

| 資料表名稱         | 測試名稱 | 平均時間 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**結論**

單欄式存放區的效能優於標準資料列存放區。 在較大型資料集 (\> 100 M) 上，預期會有更顯著的效能差異。

### <a name="effect-of-using-the-cube-parameter"></a>使用 Cube 參數的效果

此測試的目的是判斷 RevoScaleR 中使用預先計算之 **cube** 參數的選項是否可以改善效能。 模型會利用下列公式，使用 `rxLinMod` 來定型：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在資料表中，因數 *DayOfWeek* 會儲存為字串。

| 測試名稱     | Cube 參數 | numTasks | 平均時間 | 單一資料列預測 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**結論**

使用 cube 參數引數可明確地改善效能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>針對 rxDTree 模型變更 maxDepth 的效果

在此實驗中，`rxDTree` 演算法會用來在 *airlineColumnar* 資料表上建立模型。 此測試的 *numTasks* 是設定為 4。 我們使用了數個不同的 *maxDepth* 值，來示範更改樹狀結構深度會對執行時間產生何種影響。

| 測試名稱       | maxDepth | 平均時間 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**結論**

當樹狀結構的深度增加時，節點總數會以倍數成長。 建立模型所耗用的時間也會大幅增加。

### <a name="prediction-on-a-stored-model"></a>對預存模型進行的預測

此測試的目的是判斷在將定型的模型儲存至 SQL Server 資料表，而不是產生來作為目前執行程式碼的一部分時對評分的效能影響。 若要進行評分，從資料庫載入該預存模型，並使用記憶體內部 (本機計算內容) 的一列資料框架來建立預測。

測試結果顯示儲存模型所需的時間，以及載入模型並進行預測所花費的時間。

| 資料表名稱 | 測試名稱 | 平均時間 (用於訓練模型) | 儲存/載入模型的時間|
|------------|------------|------------|------------|
| 航空    | SaveModel| 21.59| 2.08|
| 航空    | LoadModelAndPredict | | 2.09 (包括用於預測的時間) |

**結論**

從資料表載入定型的模型，顯然是更快速進行預測的方式。 我們建議您避免使用相同指令碼來建立模型並執行評分。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究：針對繼續比對工作進行的最佳化

繼續比對模型是由 Microsoft 資料科學家 Ke Huang 所開發，可在 SQL Server 中測試 R 程式碼的效能，並藉此協助資料科學家建立可調整的企業級解決方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 套件都會在包含大型資料集的複雜 R 解決方案中，用來將預測模型定型。 所有測試中的 SQL 查詢和 R 程式碼都一樣。 測試會在安裝 SQL Server 的單一 Azure VM 上執行。 作者接著對由 SQL Server 提供下列最佳化或未提供最佳化的評分時間進行比較：

- 記憶體內部資料表
- ssNoVersion
- 資源管理員

為了評估軟體 NUMA 會對 R 指令碼執行產生何種效果，資料科學小組在具有 20 個實體核心的 Azure 虛擬機器上測試了此解決方案。 在這些實體核心上，自動建立四個軟體 NUMA 節點，讓每個節點均包含五個核心。

CPU 親和性會在繼續比對案例中強制執行，以評估對 R 作業的影響。 已建立四個 **SQL 資源集區**和四個**外部資源集區**，並指定了 CPU 親和性，以確保每個節點都使用同一組 CPU。

每個資源集區均會指派給不同的工作負載群組，以將硬體使用率最佳化。 原因在於軟體 NUMA 和 CPU 親和性無法分割實體 NUMA 節點中的實體記憶體；因此，根據定義，所有以相同實體 NUMA 節點為基礎的軟體 NUMA 節點，都必須使用相同 OS 記憶體區塊中的記憶體。 換句話說，沒有記憶體對處理器的親和性。

您可以使用下列流程來建立此設定：

1. 降低預設配置給 SQL Server 的記憶體數量。

2. 建立四個新集區，以平行方式執行 R 作業。

3. 建立四個工作負載群組，讓每個工作負載群組都與資源集區相關聯。

4. 使用新的工作負載群組和指派，重新啟動 Resource Governor。

5. 建立使用者定義的分類器函式 (UDF)，以在各種工作負載群組上指派不同的工作。

6. 更新 Resource Governor 設定，以針對適當的工作負載群組使用該函式。

### <a name="results"></a>結果

以下為繼續比對研究中具有最佳效能的設定：

-   四個內部資源集區 (適用於 SQL Server)

-   四個外部資源集區 (適用於外部指令碼作業)

-   每個資源集區都會與特定的工作負載群組相關聯

-   每個資源集區都會指派給不同的 CPU

-   最大的內部記憶體使用量 (適用於 SQL Server) = 30%

-   供 R 工作階段使用的最大記憶體 = 70%

對於繼續比對模型，外部指令碼的使用非常頻繁，而且沒有其他執行中的資料庫引擎服務。 因此，配置給外部指令碼的資源已增加至 70%，這證明了對於指令碼效能的最佳設定。

此設定會透過實驗不同的值來達成。 如果您使用不同的硬體或不同的解決方案，最佳設定可能就不同。 一律進行實驗，以尋找適合您案例的最佳設定！

在最佳化的解決方案中，可以在具有 20 個核心的電腦上，於 8.5 秒內對 110 萬筆資料列 (具有 100 個功能) 進行評分。 最佳化在計分時間方面大幅改善了效能。

結果也建議**功能數目**對評分時間有顯著的影響。 當預測模型中使用更多功能時，改善效果更明顯。

我們建議您閱讀下列部落格文章及隨附的教學課程，以進行詳細討論。

-   [適用於 SQL Server 中機器學習的最佳化秘訣和訣竅](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/) \(英文\)

許多使用者都注意到，第一次載入 R (或 Python) 執行階段時，會有短暫的暫停。 基於這個理由，如這些測試所述，通常會測量第一次執行的時間，但稍後就會捨棄。 後續的快取可能導致第一次和第二次執行之間產生顯著的效能差異。 在 SQL Server 和外部執行階段之間移動資料時，也有一些額外負荷，特別是當資料是透過網路傳遞，而不是直接從 SQL Server 載入時。

基於上述所有原因，沒有單一解決方案可減輕此初始載入時間，因為效能影響會因工作而有顯著差異。 例如，針對批次中的單一資料列評分執行快取；因此，後續評分作業的速度會更快，而且不需重新載入模型和 R 執行階段。 您也可以使用[原生評分](../predictions/native-scoring-predict-transact-sql.md)，以避免完全載入 R 執行階段。

若要將大型模型定型，或在大型批次中進行評分，相較於從避免資料移動或是從串流處理和平行處理中所獲得的利益，額外負荷可能是最低的。 如需其他效能指引，請參閱下列部落格文章：

+ [使用 R 以每秒100 萬筆交易偵測詐騙](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/) \(英文\)

## <a name="resources"></a>資源

以下是開發這些測試時所使用的資訊、工具及指令碼的連結。

+ 效能測試指令碼和資料的連結：[適用於 SQL Server 最佳化研究的範例資料和指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) \(英文\)

+ 描述繼續比對解決方案的文章：[適用於 SQL Server R Services 的最佳化秘訣和訣竅](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/) \(英文\)

+ 繼續比對解決方案之 SQL 最佳化中所使用的指令碼：[GitHub 存放庫](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>了解 Windows Server 管理

+ [如何判斷適用於 64 位元版本 Windows 的適當分頁檔大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支援 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>了解 SQL Server 最佳化

+ [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [記憶體最佳化的資料表簡介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [示範：記憶體內部 OLTP 的效能改善](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [停用資料表或索引的壓縮](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [資源管理員](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor 簡介](https://technet.microsoft.com/library/bb895232.aspx)

+ [設定 Resource Governor 的範例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/) \(英文\)

### <a name="tools"></a>工具

+ [DISKSPD 儲存體負載產生器/效能測試工具 (英文)](https://github.com/microsoft/diskspd)

+ [FSUtil 公用程式參考 (英文)](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>此系列的其他文章

[R 的效能調整 - 簡介](sql-server-r-services-performance-tuning.md)

[R 的效能調整 - SQL Server 設定](sql-server-configuration-r-services.md)

[R 的效能調整 - R 程式碼和資料最佳化](r-and-data-optimization-r-services.md)

[效能調整 - 案例研究結果](performance-case-study-r-services.md)
