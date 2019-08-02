---
title: 資料優化的效能微調
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a65afba9455fb475b760439e92ad8d4d38a70be8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715651"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services 的效能-資料優化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列中的第三篇, 描述以兩個個案研究為基礎的 R 服務效能優化。 本文討論在 SQL Server 中執行之 R 或 Python 腳本的效能優化。 它也會描述您可以用來更新 R 程式碼的方法, 以提高效能並避免已知的問題。

## <a name="choosing-a-compute-context"></a>選擇計算內容

在 SQL Server 2016 和2017中, 您可以在執行 R 或 Python 腳本時, 使用**本機**或**SQL**計算內容。

使用**本機**計算內容時, 分析會在您的電腦上執行, 而不是在伺服器上執行。 因此, 如果您要從 SQL Server 取得要在程式碼中使用的資料, 則必須透過網路提取資料。 因此網路傳送而產生的效能影響，取決於所傳送的資料大小、網路速度，以及同一時間發生的其他網路傳送。

使用**SQL Server 計算內容**時, 會在伺服器上執行程式碼。 如果您要從 SQL Server 取得資料, 資料應該是執行分析的伺服器本機, 因此不會引進任何網路額外負荷。 如果您需要從其他來源匯入資料, 請考慮事先安排 ETL。

使用大型資料集時，您一律應使用 SQL 計算內容。

## <a name="factors"></a>因素

R 語言具有*因素*的概念, 這是類別資料的特殊變數。 資料科學家通常會在其公式中使用因素變數, 因為將類別變數當做因素來處理, 可確保機器學習服務函式會正確處理資料。 如需詳細資訊, [請參閱 R for Dummies:因素變數](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

根據設計, 因素變數可以從字串轉換成整數, 然後再傳回以進行儲存或處理。 R `data.frame`函式會將所有字串當做因數變數來處理, 除非引數*stringsAsFactors*設定為**False**。 這表示字串會自動轉換成整數以進行處理, 然後對應回原始字串。

如果因數的來源資料是儲存為整數, 效能可能會受到影響, 因為 R 會在執行時間將因數整數轉換成字串, 然後執行它自己的內部字串對整數轉換。

若要避免這類的執行時間轉換, 請考慮將值儲存為 SQL Server 資料表中的整數, 並使用_colInfo_引數來指定當做因數使用之資料行的層級。 RevoScaleR 中的大部分資料來源物件都會接受參數_colInfo_。 您可以使用這個參數來命名資料來源所使用的變數、指定其類型, 以及定義資料行值的變數層級或轉換。

例如, 下列 R 函式呼叫會從資料表取得整數1、2和 3, 但會將值對應至層級為「apple」、「橙色」和「香蕉」的因素。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

當來源資料行包含字串時, 一定要使用_colInfo_參數, 以更有效率的方式來指定層級。 例如, 下列 R 程式碼會將字串視為正在讀取的因素。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果模型產生中沒有任何語義差異, 則後者的方法可能會導致較佳的效能。

## <a name="data-transformations"></a>資料轉換

資料科學家通常會使用以 R 撰寫的轉換函數做為分析的一部分。 轉換函數會套用至每個從資料表中抓取的資料列。 在 SQL Server 中, 這類轉換會套用至批次中所抓取的所有資料列, 而這需要 R 解譯器和分析引擎之間的通訊。 為了執行轉換，資料會在 SQL、分析引擎及 R 解譯器處理序之間來回移動。

基於這個理由, 使用轉換做為 R 程式碼的一部分可能會對演算法的效能造成重大影響, 視所涉及的資料量而定。

在執行分析之前, 在資料表或視圖中擁有所有必要的資料行, 並避免在計算期間進行轉換, 會比較有效率。 如果無法在現有資料表中加入額外的資料行，請考慮建立其他含有已轉換資料行的資料表或檢視，並使用適當的查詢來擷取資料。

## <a name="batch-row-reads"></a>批次資料列讀取

如果您在程式碼中使用 SQL Server`RxSqlServerData`的資料來源 (), 我們建議您嘗試使用參數_rowsPerRead_來指定批次大小。 這個參數會定義查詢的資料列數目, 然後傳送至外部腳本進行處理。 在執行時間, 演算法只會查看每個批次中指定的資料列數目。

能夠控制一次處理的資料量, 可以協助您解決或避免問題。 例如, 如果您的輸入資料集非常寬 (有許多資料行), 或如果資料集有幾個大型資料行 (例如自由文字), 您可以減少批次大小, 以避免將記憶體分頁。

根據預設, 此參數的值會設定為 50000, 以確保即使在記憶體不足的電腦上也能提供適當的效能。 如果伺服器有足夠的可用記憶體, 將此值增加到500000或甚至一百萬可以產生較佳的效能, 特別是針對大型資料表。

增加批次大小的優點會在大型資料集上, 以及可在多個進程上執行的工作中明顯地出現。 不過, 增加這個值並不一定會產生最佳的結果。 我們建議您試驗資料和演算法, 以判斷最佳的值。

## <a name="parallel-processing"></a>平行處理

若要改善**rx**分析函式的效能, 您可以利用 SQL Server 的功能, 使用伺服器電腦上的可用核心來平行執行工作。

有兩種方式可在 SQL Server 中使用 R 來達到平行處理:

-   **使用\@parallel。** 使用 `sp_execute_external_script` 預存程序來執行 R 指令碼時，請將 `@parallel` 參數設為 `1`。 如果您的 R 腳本不使用具有其他處理機制的 RevoScaleR 函式, 這就是最佳的方法。 如果您的腳本使用 RevoScaleR 函式 (通常會加上 "rx"), 平行處理會自動執行, 您不需要明確`@parallel`地`1`設定為。

    如果可以平行處理 R 腳本, 而且 SQL 查詢可以平行化, 則資料庫引擎會建立多個平行進程。 可以建立的進程數目上限等於實例的平行處理原則的**最大程度**(MAXDOP) 設定。 接著, 所有處理常式都會執行相同的腳本, 但只會接收部分資料。
    
    因此, 此方法不適用於必須查看所有資料的腳本, 例如在定型模型時。 不過，在以平行方式執行工作 (例如批次預測) 時非常實用。 如需搭配使用平行`sp_execute_external_script`處理原則的詳細資訊, 請參閱在[transact-sql 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)的**Advanced 秘訣: 平行處理**一節。

-   **請使用 numTasks = 1。** 在 SQL Server 計算內容中使用**rx**函數時, 請將_numTasks_參數的值設定為您想要建立的進程數目。 建立的進程數目不能超過**MAXDOP**;不過, 所建立的實際進程數目是由 database engine 所決定, 而且可能會小於您的要求。

    如果 R 腳本可以平行處理, 而且 SQL 查詢可以平行化, 則 SQL Server 在執行 rx 函數時建立多個平行進程。 所建立的實際進程數目取決於各種因素, 例如資源管理、資源的目前使用量、其他會話, 以及與 R 腳本搭配使用之查詢的查詢執行計畫。

## <a name="query-parallelization"></a>平行處理查詢

在 Microsoft R 中, 您可以藉由將資料定義為 RxSqlServerData 資料來源物件, 來使用 SQL Server 資料來源。

根據整個資料表或視圖來建立資料來源:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

根據 SQL 查詢建立資料來源:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果資料表是在資料來源中指定, 而不是查詢, R 服務就會使用內部啟發學習法來判斷要從資料表提取的必要資料行。不過, 這種方法不太可能會導致平行執行。

為了確保資料可以平行分析, 用來抓取資料的查詢應該以資料庫引擎可建立平行查詢計劃的方式來括住。 如果程式碼或演算法使用大量的資料, 請確定提供給`RxSqlServerData`的查詢已針對平行執行優化。 不會導致平行執行計畫的查詢會導致單一處理序進行計算。

如果您需要處理大型資料集, 請在執行 R 程式碼之前, 使用 Management Studio 或另一個 SQL 查詢分析器來分析執行計畫。 然後, 採取任何建議的步驟來改善查詢的效能。 例如，資料表上遺漏的索引可能會影響執行查詢所花費的時間。 如需詳細資訊, 請參閱[效能的監視和微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

另一個可能會影響效能的常見錯誤是, 查詢會抓取比所需更多的資料行。 例如, 如果公式僅以三個數據行為基礎, 但您的來源資料表有30個數據行, 則會不必要地移動資料。

 + 請避免`SELECT *`使用!
 + 請花一些時間檢查資料集內的資料行, 並只找出分析所需的欄位
 + 從查詢中移除任何包含與 R 程式碼不相容之資料類型的資料行, 例如 GUID 和 rowguids
 + 檢查是否有不支援的日期和時間格式
 + 請建立一個可選取特定值或轉換資料行以避免轉換錯誤的視圖, 而不是載入資料表。

## <a name="optimizing-the-machine-learning-algorithm"></a>優化機器學習演算法

本節提供 Microsoft R 中 RevoScaleR 和其他選項特有的其他秘訣和資源。

> [!TIP]
> R 優化的一般討論不在本文的範圍內。 不過, 如果您需要更快速地讓程式碼, 建議您參閱熱門文章, 也就[是 R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 其中涵蓋 R 中的程式設計結構, 以及逼真語言和詳細資料的常見錯誤, 並提供許多 R 程式設計技巧的特定範例。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的優化

許多 RevoScaleR 演算法都支援參數來控制定型模型的產生方式。 雖然模型的精確度和正確性很重要, 但演算法的效能可能同樣重要。 若要在精確度和定型時間之間取得適當的平衡, 您可以修改參數來增加計算的速度, 而且在許多情況下, 會改善效能, 而不會降低精確度或正確性。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree``maxDepth`支援參數, 其控制決策樹的深度。 隨著`maxDepth`增加, 效能可能會降低, 因此請務必分析增加深度與影響效能的優點。

    您也可以藉由調整參數`maxNumBins`(例如、、 `maxComplete`和`maxSurrogate`), `maxDepth`來控制時間複雜性和預測精確度之間的平衡。 將深度增加到超過 10 或 15 以上，會讓計算付出很高的代價。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    如果公式中`cube`的第一個相依變數是因數變數, 請嘗試使用引數。
    
    當`cube`設定為時`TRUE`, 會使用已分割的反向來執行回歸, 這可能會比標準回歸計算更快且使用較少的記憶體。 如果公式含有大量變數，就會顯著提升效能。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    如果第一個相依變數是因素變數, 請使用引數。`cube`
    
    當`cube`設定為`TRUE`時, 演算法會使用已分割的反向, 這可能會更快且使用較少的記憶體。 如果公式含有大量變數，就會顯著提升效能。

如需有關 RevoScaleR 優化的其他指引, 請參閱下列文章:

+ 支援文章:[RxDForest 和 rxDTree 的效能微調選項](https://support.microsoft.com/kb/3104235)

+ 控制模型的方法可納入推進式樹狀結構模型中:[使用隨機梯度提升來估計模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ 概述 RevoScaleR 如何移動和處理資料:[在 ScaleR 中撰寫自訂區塊化演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的程式設計模型:[在 RevoScaleR 中管理執行緒](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ [RxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)的函數參考

+ [RxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)的函數參考

### <a name="use-microsoftml"></a>使用 MicrosoftML

我們也建議您查看新的**MicrosoftML**套件, 它提供可調整的機器學習服務演算法, 可以使用 RevoScaleR 所提供的計算內容和轉換。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何選擇 MicrosoftML 演算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>使用 Microsoft R Server 讓解決方案

如果您的案例涉及使用預存模型的快速預測, 或將機器學習服務整合到應用程式中, 您可以使用 Microsoft R Server 中的[運算化](https://docs.microsoft.com/r-server/what-is-operationalization)功能 (先前稱為 DeployR)。

+ 身為**資料科學家**, 使用[mrsdeploy 套件](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)與其他電腦共用 r 程式碼, 並整合 web、桌面、行動和儀表板應用程式內的 r 分析:[如何在 R Server 中發佈和管理 R web 服務](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 身為**系統管理員**, 瞭解如何管理封裝、監視 web 節點和計算節點, 以及控制 R 作業的安全性:[如何在 R 中與 web 服務互動及使用](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>本系列文章

[R 效能微調-簡介](sql-server-r-services-performance-tuning.md)

[R SQL Server 設定的效能微調](sql-server-configuration-r-services.md)

[R-R 程式碼和資料優化的效能微調](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
