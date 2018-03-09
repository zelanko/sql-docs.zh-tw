---
title: "R 服務-結果和資源的效能 |Microsoft 文件"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 83c3590714660201d7411c360958f9ff4263240b
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="performance-for-r-services-results-and-resources"></a>R 服務的效能： 結果和資源
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是第四個和數列中最後一個說明 R 服務的效能最佳化。 本文摘要說明的方法、 發現和測試各種不同的最佳化方法的兩個案例研究的結論。

兩個案例研究都有不同的目標：

+ 第一個案例研究、 R 服務開發小組所要搜尋來測量特定的最佳化技術的影響
+ 第二個案例研究，資料科學家小組所實驗多個方法來判斷特定的大量的計分案例最理想的最佳化。

本主題列出第一個案例研究的詳細的的結果。 第二個案例研究，摘要描述的整體結果。 在本主題的結尾都是所有的指令碼和範例資料，以及原始作者所使用的資源的連結。

## <a name="performance-case-study-airline-dataset"></a>效能案例研究： Airline 資料集

此案例研究，SQL Server R Services 開發小組所測試各種自訂的效果。 建立單一 rxLogit 模型及計分 Airline 資料集上執行。 在定型和計分評估影響個別的處理程序期間套用的最佳化。

- Github:[範例資料和指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)如 SQL Server 最佳化的研究

### <a name="test-methods"></a>測試方法

1. Airline 資料集包含單一 10 M 個資料列的資料表。 它已下載並大量載入到 SQL Server。
2. 進行變更之資料表的 6 個複本。
3. 各種修改已套用至資料表，以測試 SQL Server 功能，例如 page 壓縮，資料列壓縮，等單欄式資料存放區索引副本。
4. 效能測量每個最佳化已套用之前和之後。

| 資料表名稱| Description|
|------|------|
| *airline* | 使用 `rxDataStep` 從原始 xdf 檔案轉換的資料|                          |
| *airlineWithIntCol*   | 轉換成整數而不是字串的 *DayOfWeek*。 會一併新增 *rowNum* 資料行。|
| *airlineWithIndex*    | 與 *airlineWithIntCol* 資料表的資料相同，但是具有使用 *rowNum* 資料行的單一叢集索引。|
| *airlineWithPageComp* | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用頁面壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineWithRowComp*  | 與 *airlineWithIndex* 資料表的資料相同，但是已啟用資料列壓縮。 會一併新增 *CRSDepHour* 和 *Late* 這兩個資料行，這些是從 *CRSDepTime* 和 *ArrDelay* 計算而得。 |
| *airlineColumnar*     | 具有單一叢集索引的單欄式存放區。 此資料表中會填入來自已清除之 csv 檔案的資料。|

每個測試包括下列步驟：

1. 在每次測試之前都引發了 R 記憶體回收。
2. 羅吉斯迴歸模型是根據資料表資料所建立。 每個測試的 *rowsPerRead* 的值是設定為 500000。
3. 使用定型的模型產生分數
4. 每個測試執行六倍。 第一次執行 （「 冷執行 」） 的時間已卸除。 若要偶爾的極端值，允許**最大**也已卸除其餘的五個執行之間的時間。 系統取剩餘四次執行的平均值，來計算每個測試的平均經過執行時間。
5. 使用已執行測試*reportProgress*參數的值是 3 （= 報表執行時間和進度）。 每個輸出檔案包含花費在 IO、 轉換時間和運算時間的時間相關資訊。 這些時間對於進行疑難排解和診斷相當有用。
6. 主控台輸出也已導向至輸出目錄中檔案。
7. 測試指令碼處理這些檔案，以透過執行計算的平均時間的時間。

例如，下列的結果會是從單一測試時間。 主要的相關時間為「總讀取時間」(IO 時間) 和「轉換時間」(在設定處理序以進行計算方面的負擔)。

**範例時間**

```
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

我們建議您下載並修改測試指令碼，可協助您疑難排解問題與 R Services 或使用 RevoScaleR 函式。

### <a name="test-results-all"></a>測試結果 （全部）

本節將比較每個測試之前和之後的結果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>資料壓縮與單欄式資料表存放區的大小

第一項測試會比較使用壓縮和單欄式資料表，以減少資料大小。

| 資料表名稱            | 資料列     | 已保留   | 資料       | index_size | 未使用  | 節省 % (已保留) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/a        | 368 KB  | 93%                 |

**結論**

最大的減少資料大小被藉由套用資料行存放區索引，後面接著頁面壓縮。

#### <a name="effects-of-compression"></a>壓縮的影響

這項測試會比較資料列壓縮、 頁面壓縮和未壓縮的優點。 使用來定型模型`rxLinMod`三個不同資料表的資料。 針對所有資料表都使用了相同的公式和查詢。

| 資料表名稱            | 測試名稱       | numTasks | 平均時間 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-平行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-平行 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-平行  | 4        | 5.2375       |

**結論**

壓縮單獨似乎無法幫助。 在此範例中，增加的 CPU 處理壓縮會大幅減少 IO 時間補償。

不過，當透過將 *numTasks* 設定為 4 來平行執行測試時，平均時間就會減少。

針對較大的資料集，壓縮的效果可能較為明顯。 壓縮取決於資料集和值，因此可能需要透過實驗，才能判斷壓縮對您資料集的影響。

### <a name="effect-of-windows-power-plan-options"></a>Windows 電源計劃選項的效果

在此實驗中，`rxLinMod` 是與 *airlineWithIntCol* 資料表搭配使用。 Windows 電源計劃已設為**平衡**或**高效能**。 所有測試的 *numTasks* 都是設定為 1。 測試執行六次，並執行兩次下這兩個電源選項 以調查變化性的結果。

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

執行時間會更一致且更快時使用 Windows**高效能**電源計劃。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整數和字串比較

這項測試會評估修改 R 程式碼，以避免常見的問題，以字串因素的影響。 具體而言，此模型已培訓使用`rxLinMod`使用兩個資料表： 首先，因素會儲存為字串，在第二個資料表中，因素儲存為整數。

+ 如*airline*資料表中，[DayOfWeek] 資料行包含字串。 _ColInfo_參數用來指定因素層級 （星期一、 星期二、...）

+  如*airlineWithIndex*資料表，[DayOfWeek] 是一個整數。 _ColInfo_未指定參數。

+ 在這兩個案例中，使用了相同的公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 資料表名稱          | 測試名稱   | 平均時間 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**結論**

使用整數，而不是字串的因素時，沒有明顯的好處。

### <a name="avoiding-transformation-functions"></a>避免轉換函式

在這項測試，來定型模型使用`rxLinMod`，但兩個回合已變更的程式碼：

+ 在第一次執行中，轉換函式套用做為模型建立的一部分。 
+ 在第二個執行中，功能值提供了預先計算的而且可以使用，以便轉換函式所需。

| 測試名稱             | 平均時間 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**結論**

定型時間已短時**不**使用轉換函式。 換句話說，此模型定型速度時使用預先計算並保存資料表中的資料行。

節省卻會比較大，如果沒有提供還有許多其他的轉換，而且是較大的資料集 (\> 100 萬)。

### <a name="using-columnar-store"></a>使用單欄式儲存區

這項測試，評估使用單欄式資料存放區和索引的效能優勢。 此相同的模型定型使用`rxLinMod`和任何資料轉換。

+ 在第一次執行中，資料表會使用標準資料列存放區。
+ 如果您在第二個執行中，使用資料行存放區。

| 資料表名稱         | 測試名稱 | 平均時間 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**結論**

效能會更好的單欄式儲存比與標準資料列存放區。 在較大的資料集的預期效能顯著的差異 (\> 100 萬)。

### <a name="effect-of-using-the-cube-parameter"></a>使用 cube 參數的效果

這項測試的目的是要判斷是否使用預先計算的選項中 RevoScaleR **cube**參數可提升效能。 使用來定型模型`rxLinMod`，使用以下公式：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在資料表中，因素*DayOfWeek*儲存為字串。

| 測試名稱     | Cube 參數 | numTasks | 平均時間 | 單一資料列的預測 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**結論**

Cube 參數引數使用清楚可以改善效能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>變更 maxDepth rxDTree 模型產生的影響

在這項實驗，`rxDTree`演算法用來建立模型上*airlineColumnar*資料表。 此測試的 *numTasks* 是設定為 4。 數個不同的值，如*maxDepth*用於示範如何修改樹狀結構深度會影響執行的階段。

| 測試名稱       | maxDepth | 平均時間 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**結論**

樹狀結構深度增加時，會以指數方式增加的節點總數。 建立模型所經過的時間也大幅增加。

### <a name="prediction-on-a-stored-model"></a>預存的模型上的預測

這項測試的目的是要判斷評分定型的模型儲存到 SQL Server 資料表時的效能影響會，而不是產生做為目前執行的程式碼的一部分。 計分，預存的模型從資料庫載入和使用的一個資料列的資料範圍在記憶體 （本機計算內容） 中建立預測。

測試結果會顯示將儲存模式及來載入模型，並預測所花費的時間。

| 資料表名稱 | 測試名稱 | 平均時間 (用於訓練模型) | 儲存/載入模型的時間|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09 (包括用於預測的時間) |

**結論**

從資料表中載入已定型的模型，顯然是更快的方法進行預測。 我們建議您避免建立模型，以及執行評分所有在相同的指令碼。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究： 繼續比對工作的最佳化

繼續比對模型所開發的 Microsoft 資料科學家 Ke Huang 測試 SQL Server 中的 R 程式碼的效能和執行動作，說明資料科學家建立可擴充、 企業級解決方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 封裝用來定型中複雜的 R 解決方案，牽涉到大型資料集的預測模型。 SQL 查詢和 R 程式碼是相同的所有測試。 測試已安裝的 SQL server 在單一 Azure VM 上進行。 作者然後比較計分的時間，而不需要 SQL Server 提供下列最佳化：

- 記憶體中資料表
- ssNoVersion
- 資源管理員

若要評估軟體 NUMA 的 R 指令碼執行的效果，資料科學團隊會測試在 Azure 虛擬機器與實體的 20 個核心方案。 四個軟體 NUMA 節點的每個節點包含五個核心的自動建立這些實體的核心上。

CPU 分配已強制在繼續比對案例中，以評估 R 作業的影響。 四個**SQL 資源集區**和第四個**外部資源集區**所建立，以確保組相同的 Cpu 可用於每個節點指定 CPU 相似性。

每個資源集區已指派給不同的工作負載群組，以最佳化的硬體使用率。 原因是軟體式 NUMA 和 CPU 相似性無法除以實體記憶體中實體的 NUMA 節點。因此，根據定義根據相同的實體 NUMA 節點的所有軟體 NUMA 節點必須使用記憶體中相同作業系統記憶體區塊。 換句話說，沒有無記憶體對處理器親和性。

下列程序用來建立此組態：

1. 減少至 SQL Server 預設配置的記憶體數量。

2. 建立四個新的集區以平行方式執行的 R 作業。

3. 因此，每個工作負載群組就會與資源集區相關聯，請建立四個工作負載群組。

4. 使用新的工作負載群組和指派，重新啟動資源管理員。

5. 建立使用者定義分類函數 (UDF)，來指派不同的工作負載群組中不同的工作。

6. 更新資源管理員組態，使用適當的工作負載群組的函數。

### <a name="results"></a>結果

有最佳效能的繼續符合研究的組態如下所示：

-   四個內部資源集區 （適用於 SQL Server)

-   （適用於外部指令碼工作） 的四個外部資源集區

-   每個資源集區都與特定的工作負載群組

-   每個資源集區指派給不同的 Cpu

-   內部記憶體使用上限 （適用於 SQL Server) = 30%

-   R 工作階段所使用的最大記憶體 = 70%

繼續比對模型中，外部指令碼的用途是大量且沒有任何其他資料庫引擎服務執行。 因此，配置給外部指令碼的資源都增加到 70%，證實該指令碼效能的最佳組態。

此設定已抵達藉由試驗不同的值。 如果您使用不同的硬體或不同的方案，最佳的設定可能會不同。 一律體驗來尋找您案例的最佳組態 ！

在最佳化解決方案中，在 20 核心電腦上的 8.5 秒內計分 1.1 百萬個資料列 （具有 100 個功能） 的資料。 最佳化會大幅提升效能計分的時間。

結果也建議，**的功能數目**計分時間上有顯著的影響。 預測模型中所使用的更多的功能時，更明顯的改進。

我們建議您先閱讀此部落格文章及隨附的教學課程的詳細討論。

-   [最佳化秘訣和訣竅 SQL Server 中的機器學習服務](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

許多使用者必須注意的一點是小型暫停 R （或 Python） 執行階段載入第一次。 基於這個理由，這些測試中所述的第一次的執行時間是通常測量，但稍後捨棄。 後續快取可能會造成顯著的效能差異第一個和第二個執行。 另外還有一些額外負荷當資料移動 SQL Server 之間的外部執行階段，特別是當資料會透過網路，而不是直接從 SQL Server 正在載入。

基於這些理由，沒有任何單一方案減輕這個初始載入時間，因為根據工作大幅的效能影響。 例如，執行快取的單一資料列批次; 計分因此，後續的計分作業更快，模型和 R 執行階段都不會重新載入。 您也可以使用[原生計分](../sql-native-scoring.md)以避免完全載入的 R 執行階段。

對於定型大型模型，或以大型批次計分，則負擔可能會最小相較於從避免資料移動，或從資料流處理和平行處理的提升。 請參閱這些新的部落格和其他效能指引的範例：

+ [使用 SQL Server 2016 R Services 的貸款分類](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [早期的客戶經驗與 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [使用 R 偵測詐騙等等，在每秒的 1 百萬個交易](http://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>資源

以下是資訊、 工具和指令碼使用這些測試的開發工作的連結。

+ 效能測試指令碼和資料的連結：[範例資料和 SQL Server 最佳化研究的指令碼](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 文件說明了繼續比對方案：[最佳化秘訣和訣竅 SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 用於繼續比對方案中 SQL 最佳化的指令碼： [GitHub 儲存機制](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>深入了解 Windows server 管理

+ [如何判斷適用於 64 位元版本 Windows 的適當分頁檔大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支援 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [軟體 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>深入了解 SQL Server 最佳化

+ [重新組織與重建索引](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [記憶體最佳化資料表簡介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [示範： 記憶體內部 OLTP 的效能改善](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [資料壓縮](../../relational-databases/data-compression/data-compression.md)

+ [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [停用資料表或索引的壓縮](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [資源管理員](../../relational-databases/resource-governor/resource-governor.md)

+ [資源管理員簡介](https://technet.microsoft.com/library/bb895232.aspx)

+ [的資源管理](resource-governance-for-r-services.md)

+ [如何建立 R 資源集區](how-to-create-a-resource-pool-for-r.md)

+ [設定資源管理員的範例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 儲存體負載產生器/效能測試工具 (英文)](https://github.com/microsoft/diskspd)

+ [FSUtil 公用程式參考 (英文)](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>在這一系列的其他文件

[效能調整的 R-簡介](sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](sql-server-configuration-r-services.md)

[效能調整的 R-R 程式碼和資料最佳化](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
