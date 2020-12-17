---
title: 資料的效能微調
description: 此文章討論在 SQL Server 中執行之 R 或 Python 指令碼的效能最佳化。 它也說明您可以用來更新 R 程式碼的方法，以提高效能並避免已知的問題。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/20/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 995b30e9c69b14148a67f18c36e0f42d01c419eb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470819"
---
# <a name="performance-tuning-and-data-optimization-for-r"></a>適用於 R 的效能微調和資料最佳化
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

此文章討論在 SQL Server 中執行之 R 或 Python 指令碼的效能最佳化。 您也可以使用這些方法來更新 R 程式碼，以提高效能並避免已知的問題。

## <a name="choosing-a-compute-context"></a>選擇計算內容

在 SQL Server 中，您可以在執行 R 或 Python 指令碼時，使用 **本機** 或 **SQL** 計算內容。

使用 **本機** 計算內容時，會在您的電腦上執行分析，而不是在伺服器上執行。 因此，如果您要從 SQL Server 取得要在程式碼中使用的資料，則必須透過網路擷取資料。 因此網路傳送而產生的效能影響，取決於所傳送的資料大小、網路速度，以及同一時間發生的其他網路傳送。

使用 **SQL Server 計算內容** 時，會在伺服器上執行程式碼。 若要從 SQL Server 取得資料，資料應該位於執行分析的伺服器本機，因此不會產生任何網路額外負荷。 若需要從其他來源匯入資料，請考慮事先安排 ETL。

使用大型資料集時，您一律應使用 SQL 計算內容。

## <a name="factors"></a>因素

R 語言具有「因數」的概念，這是類別資料的特殊變數。 資料科學家通常會在其公式中使用因素變數，因為將類別變數當作因素來處理可確保機器學習服務函式會正確處理資料。

根據設計，因數變數可以從字串轉換為整數，然後再轉換回來以進行儲存或處理。 R `data.frame` 函式會將所有字串當作因數變數來處理，除非 *stringsAsFactors* 引數設定為 **False**。 這表示字串會自動轉換成整數以進行處理，然後對應回原始字串。

如果因數的來源資料是儲存為整數，效能可能會受到影響，因為 R 會在執行階段將因數整數轉換為字串，然後執行它自己內部的字串對整數轉換。

為避免此類執行階段轉換，請考慮將值儲存為 SQL Server 資料表中的整數，然後使用 _colInfo_ 引數來指定當做因數使用之資料行的層級。 RevoScaleR 中的大部分資料來源物件都接受參數 _colInfo_。 您可以使用此參數來命名資料來源所使用的變數、指定其類型，以及定義資料行值的變數層級或轉換。

例如，下列 R 函式呼叫會從資料表取得整數1、2 與 3，但會將值對應至層級為 "apple"、"orange" 與 "banana" 的因數。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

當來源資料行包含字串時，事先使用 _colInfo_ 參數來指定層級一律更有效率。 例如，當讀取字串時，下列 R 程式碼會將字串視為因數。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果模型世代中沒有任何語意差異，則此方法會有更好的效能。

## <a name="data-transformations"></a>資料轉換

資料科學家通常會使用以 R 撰寫的轉換函數做為分析的一部分。 轉換函式會套用到從資料表擷取的每個資料列。 在 SQL Server 中，此類轉換會套用到在批次中擷取的所有資料列，而這需要 R 解譯器與分析引擎之間的通訊。 為了執行轉換，資料會在 SQL、分析引擎及 R 解譯器處理序之間來回移動。

基於此原因，視所涉及的資料量而定，使用轉換作為 R 程式碼的一部分可能會對演算法的效能產生顯著的負面影響。

更有效率的方式是，在執行分析之前，擁有資料表或檢視中的所有必要資料行，因為這樣可避免在計算期間進行轉換。 如果無法在現有資料表中加入額外的資料行，請考慮建立其他含有已轉換資料行的資料表或檢視，並使用適當的查詢來擷取資料。

## <a name="batch-row-reads"></a>批次資料列讀取

如果在程式碼中使用 SQL Server 資料來源 (`RxSqlServerData`)，我們建議您嘗試使用參數 _rowsPerRead_ 來指定批次大小。 此參數定義查詢的資料列數目，然後傳送至外部指令碼進行處理。 在執行階段，演算法只會看到每個批次中指定的資料列數目。

能夠控制一次處理的資料量，可以協助您解決或避免問題。 例如，如果您的輸入資料集非常寬 (有許多資料行)，或如果資料集有幾個大型資料行 (例如自由文字)，您可以減少批次大小，以避免從記憶體分頁到磁碟。

根據預設，此參數的值會設定為 50000，以確保即使在記憶體不足的電腦上可有不錯的效能。 如果伺服器有足夠的可用記憶體，將此值增加到 500,000 或甚至一百萬，都能產生更好的效能，對大型資料表而言更是如此。

增加批次大小的優點會大型資料集上與可在多個處理序上執行的工作中會更明顯。 不過，增加這個值並不一定會產生最佳結果。 我們建議您試驗資料與演算法，以判斷最佳值。

## <a name="parallel-processing"></a>平行處理

若要改善 **rx** 分析函式的效能，您可以利用伺服器電腦上的可用核心，使用 SQL Server 平行執行工作的能力。

有兩種方式可利用 SQL Server 中的 R 達到平行處理：

+ **使用 \@parallel.** 使用 `sp_execute_external_script` 預存程序來執行 R 指令碼時，請將 `@parallel` 參數設為 `1`。 若您的 R 指令碼 **不** 使用具有其他處理機制的 RevoScaleR函式，這是最佳方法。 若您的指令碼使用 RevoScaleR 函式 (通常會加上 "rx")，平行處理會自動執行，因此您不需要明確地將 `@parallel` 設定為 `1`。

  若可以平行處理 R 指令碼，而且可平行處理 SQL 查詢，則資料庫引擎將建立多個平行處理序。 可以建立的處理序數目上限等於執行個體的 [平行處理原則的最大程度] \(MAXDOP\) 設定。 接著，所有處理常式都會執行相同的指令碼，但只會接收部分資料。
  
  因此，此方法不適用於一定要看到所有資料的指令碼，例如將模型定型時。 不過，在以平行方式執行工作 (例如批次預測) 時非常實用。 如需使用平行處理原則搭配 `sp_execute_external_script` 的詳細資訊，請參閱 [在 Transact-SQL 中使用 R 程式碼](../tutorials/quickstart-r-create-script.md)中的 **進階提示︰平行處理** 一節。

+ **使用 numTasks =1。** 在 SQL Server 計算內容中使用 **rx** 函式時，請將 _numTasks_ 參數的值設定為您要建立的處理序數目。 建立的處理序數目一律不能超過 **MAXDOP**；不過，建立的實際處理序數目是由資料庫引擎所決定，而且可能會比您要求的少。

  如果可以平行處理 R 指令碼，而且可平行處理 SQL 查詢，則 SQL Server 將在執行 rx 函式時建立多個平行處理序。 實際所建立的處理序數目會取決於數種不同的因素。 這些包括資源治理、目前的資源使用量、其他工作階段，以及搭配 R 指令碼使用之查詢的查詢執行計畫。

## <a name="query-parallelization"></a>查詢平行處理

在 Microsoft R 中，您可以透過將資料定義為 RxSqlServerData 資料來源物件，來使用 SQL Server 資料來源。

根據整個資料表或檢視來建立資料來源：

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

根據 SQL 查詢建立資料來源：

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果在資料來源中指定資料表，而不是查詢，R Services 將使用內部啟發學習法決定需要從資料表擷取的資料行數目；不過，這種方法不太可能會導致平行處理。

若要確保資料會以平行方式進行分析，用來擷取資料的查詢應透過一種資料庫引擎可建立平行查詢計畫的方式進行框架處理。 若程式碼或演算法使用大量資料，請確定提供給 `RxSqlServerData` 的查詢已針對平行執行最佳化。 不會導致平行執行計畫的查詢會導致單一處理序進行計算。

若需要處理大型資料集，請在執行 R 程式碼之前，使用 Management Studio 或另一個 SQL 查詢分析器來分析執行計畫。 接著，採取任何建議的步驟來改善查詢的效能。 例如，資料表上遺漏的索引可能會影響執行查詢所花費的時間。 如需詳細資訊，請參閱[監視及調整效能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

另一個會影響效能的常見錯誤是查詢擷取的資料行數比所需的還多。 例如，如果公式僅以三個資料行為基礎，但您的來源資料表有 30 個資料行，則會不必要地移動資料。

+ 避免使用 `SELECT *`！
+ 請花一些時間檢閱資料集中的資料行，並只找出分析所需的資料行
+ 從查詢移除任何包含與 R 程式碼不相容之資料類型的資料行，例如 GUID 與 rowguids
+ 檢查是否有不支援的日期和時間格式
+ 建立會選取特定值或轉換資料行以避免轉換錯誤的檢視，而不是載入資料表

## <a name="optimizing-the-machine-learning-algorithm"></a>最佳化機器學習演算法

此節提供 Microsoft R 中 RevoScaleR 與其他選項特有的其他祕訣與資源。

> [!TIP]
> R 最佳化的一般討論不在此文章的範圍內。 不過，若需要加快程式碼執行速度，建議您閱讀熱門文章 [R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 該文章涵蓋 R 中的程式設計結構，以及逼真語言和詳細資料中的常見錯誤，並提供許多 R 程式設計技巧的特定範例。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的最佳化

許多 RevoScaleR 演算法都支援參數來控制產生定型模型的方法。 雖然模型的精確度和正確性很重要，但演算法的效能可能同樣重要。 若要在精確度與定型時間之間取得平衡，您可以修改型參數來提高計算速度，而且在許多案例中，您可以在不降低精確度或正確性的情況下提升效能。

+ [rxDTree](/r-server/r-reference/revoscaler/rxdtree)

  `rxDTree` 支援 `maxDepth` 參數，其可控制決策樹深度。 因為增加 `maxDepth`，就會降低效能，因此分析增加深度的優點與效能影響很重要。

  您可以控制時間複雜性和預測精確度之間的平衡，方式則是調整如下的參數：`maxNumBins`、`maxDepth`、`maxComplete` 與 `maxSurrogate`。 將深度增加到超過 10 或 15 以上，會讓計算付出很高的代價。

+ [rxLinMod](/r-server/r-reference/revoscaler/rxlinmod)

  若公式中的第一個相依變數是因數變數，請嘗試使用 `cube` 引數。
  
  當 `cube` 設定為 `TRUE` 時，就會使用資料分割的反向來執行迴歸，這樣可能比較快，而且所使用的記憶體比標準迴歸計算還要少。 如果公式含有大量變數，就會顯著提升效能。

+ [rxLogit](/r-server/r-reference/revoscaler/rxlogit)

  若第一個相依變數是因數變數，請嘗試使用 `cube` 引數。
  
  當 `cube` 設定為 `TRUE` 時，演算法會使用資料分割反向，這可能比較快且使用較少的記憶體。 如果公式含有大量變數，就會顯著提升效能。

如需 RevoScaleR 最佳化的詳細資訊，請參閱下列文章：

+ 支援文章：[RxDForest 與 rxDTree 的效能調整選項](https://support.microsoft.com/kb/3104235) \(機器翻譯\)

+ 控制模型的方法可納入增效樹狀結構模型中：[使用推測漸層增效估計模型](/r-server/r/how-to-revoscaler-boosting) \(英文\)

+ 有關 RevoScaleR 如何移動及處理資料的概觀：[在 ScaleR 中撰寫自訂區塊化演算法](/r-server/r/how-to-developer-write-chunking-algorithms) \(英文\)

+ RevoScaleR 的程式設計模型：[在 RevoScaleR 中管理執行緒](/r-server/r/how-to-developer-manage-threads) \(英文\)

+ [rxDForest](/r-server/r-reference/revoscaler/rxdforest) 的函式參考

+ [rxBTrees](/r-server/r-reference/revoscaler/rxbtrees) 的函式參考

### <a name="use-microsoftml"></a>使用 MicrosoftML

我們也建議您查看新的 **MicrosoftML** 套件，其提供可使用 RevoScaleR 所提供之計算內容與轉換的可調整規模機器學習演算法。

+ [開始使用 MFA SDK](/r-server/r/concept-what-is-the-microsoftml-package) \(英文\)

+ [如何選擇 MicrosoftML 演算法](/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet) \(英文\)

## <a name="next-steps"></a>後續步驟

+ 如需可用來改善 R 程式碼效能的 R 函式，請參閱[使用 R 分析函式來改善效能](using-r-code-profiling-functions.md)。

+ 如需 SQL Server 上效能微調的更完整資訊，請參閱 [SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database)。
