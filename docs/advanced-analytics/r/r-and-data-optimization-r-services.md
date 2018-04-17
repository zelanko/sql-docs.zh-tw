---
title: SQL Server R Services-資料最佳化的效能 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 98605a5eb5291444e0bd46d64bd3b84ab7c1b008
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="performance-for-r-services---data-optimization"></a>R Services-資料最佳化的效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是說明兩個案例研究為基礎的 R 服務的效能最佳化的數列中的第三個。 本文將討論效能最佳化或 Python 指令碼，在 SQL Server 中執行。 此外也說明您可以使用更新 R 程式碼，以提高效能並避免已知的問題的方法。

## <a name="choosing-a-compute-context"></a>選擇的計算內容

在 SQL Server 2016 和 2017年，您可以使用**本機**或**SQL**計算內容執行 R 或 Python 指令碼時。

當使用**本機**運算環境，分析會執行您的電腦上，並不在伺服器上。 因此，如果您要從 SQL Server 以使用您的程式碼中取得資料，資料必須透過網路擷取。 因此網路傳送而產生的效能影響，取決於所傳送的資料大小、網路速度，以及同一時間發生的其他網路傳送。

當使用**SQL Server 計算內容**，在伺服器上執行的程式碼。 如果您要從 SQL Server 中取得資料，資料應該是本機伺服器執行的分析，並因此導入了沒有網路負擔。 如果您需要從其他來源匯入資料，請考慮事先排列 ETL。

使用大型資料集時，您一律應使用 SQL 計算內容。

## <a name="factors"></a>因素

R 語言有"因素 」，也就是特殊的變數的分類資料的概念。 資料科學家通常使用其公式中的因數變數，因為處理當做因素類別變數時，可確保資料正確地處理由機器學習服務函式。 如需詳細資訊，請參閱 [傻瓜 R： 因數變數] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

根據設計，因數變數可以從轉換字串至整數一次的存放裝置或處理。 R`data.frame`函式會處理所有字串做為因數變數，除非引數*stringsAsFactors*設**False**。 這表示字串會自動轉換成整數進行處理，並且接著對應回原始的字串。

如果因數的來源資料儲存為整數，效能會受到影響，因為 R 執行階段將因素整數轉換為字串，然後執行它自己的內部字串至整數轉換。

若要避免這類的執行階段轉換，請考慮將值儲存為整數，在 SQL Server 資料表中，並使用_colInfo_引數來指定做為因數的資料行層級。 RevoScaleR 中大部分的資料來源物件會接受參數_colInfo_。 您可以使用這個參數來命名資料來源所使用的變數，指定其型別，並定義變數的層級或轉換資料行值。

例如，下列 R 函式呼叫取得資料表、 1、 2 和 3 的整數，但對應使用層級"的 apple"的因數的值、 「 橙色 」 和 「 banana"。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

當來源資料行包含字串時，總是會比較有效率的方式指定時間，使用前面的層級_colInfo_參數。 例如，下列 R 程式碼會將字串視為因素在讀取。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果沒有任何模型層代中的語意差異，然後第二種方法可能會導致更好的效能。

## <a name="data-transformations"></a>資料轉換

資料科學家通常會使用以 R 撰寫的轉換函數做為分析的一部分。 轉換函式會套用到從資料表中擷取每個資料列。 在 SQL Server，這類轉換會套用至需要的 R 解譯器和分析引擎之間的通訊以批次擷取所有資料列。 為了執行轉換，資料會在 SQL、分析引擎及 R 解譯器處理序之間來回移動。

基於這個理由，您的 R 程式碼中使用轉換可以有大幅的演算法，視資料量而定的效能負面影響。

會有所有必要的資料行中的資料表或檢視，然後再執行分析，並避免轉換計算期間更有效率。 如果無法在現有資料表中加入額外的資料行，請考慮建立其他含有已轉換資料行的資料表或檢視，並使用適當的查詢來擷取資料。

## <a name="batch-row-reads"></a>讀取批次的資料列

如果您使用 SQL Server 資料來源 (`RxSqlServerData`) 在您的程式碼中，我們建議您嘗試使用參數_rowsPerRead_指定批次大小。 此參數會定義查詢並再傳送至外部指令碼進行處理的資料列數目。 在執行階段，此演算法會看到每個批次中的資料列中指定數字。

控制處理一次的資料量的能力，可協助您解決或避免發生問題。 例如，如果您輸入的資料集是很寬 （具有許多資料行），或如果資料集有幾個大型資料行 （例如任意文字），您可以減少批次大小，以避免記憶體不足的資料分頁。

根據預設，此參數的值設為 50000，確保不錯的效能，甚至在記憶體不足的電腦上。 如果伺服器有足夠的記憶體可用時，增加到 500,000 個以上甚至百萬個此值可能會產生較佳的效能，尤其對於大型資料表。

增加明顯大型資料集，在和中的工作，可以在多個處理序上執行的批次大小的優點。 不過，增加此值不會一律產生最佳的結果。 我們建議您試驗資料和演算法來決定最佳的值。

## <a name="parallel-processing"></a>平行處理

若要改善效能的**rx**分析函式，您可以利用 SQL Server 平行地使用可用的核心伺服器電腦上執行工作的能力。

有兩種方式可達到使用 SQL Server 中 R 的平行化作業：

-   **使用\@平行。** 使用 `sp_execute_external_script` 預存程序來執行 R 指令碼時，請將 `@parallel` 參數設為 `1`。 這是最佳方法，如果您的 R 指令碼會執行**不**使用 RevoScaleR 函式，也有其他的機制進行處理。 如果您的指令碼會使用 RevoScaleR 函式 （通常做為前置詞與 「 接收 」）、 平行處理會自動執行，而且您不需要明確地設定`@parallel`至`1`。

    如果 R 指令碼可平行處理，而且可平行處理的 SQL 查詢，database engine 就會建立多個平行處理序。 可以建立的處理序的最大數目等於**的最大平行處理原則程度**(MAXDOP) 設定執行個體。 然後所有處理程序執行相同的指令碼，但接收資料的一部分。
    
    因此，這個方法不適合用於指令碼，一定會看到所有的資料，例如當定型模型。 不過，在以平行方式執行工作 (例如批次預測) 時非常實用。 如需有關使用平行處理原則與`sp_execute_external_script`，請參閱**進階秘訣： 平行處理**區段[TRANSACT-SQL 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

-   **使用 numTasks = 1。** 當使用**rx**函式在 SQL Server 計算內容中，設定的值_numTasks_參數，以您想要建立的處理序數目。 建立處理序的數目不可以超過**MAXDOP**; 不過，建立處理序的實際數目取決於資料庫引擎，因此可能會小於您要求。

    如果 R 指令碼可平行處理，而且可平行處理的 SQL 查詢，然後 SQL Server 時，建立多個平行處理序執行 rx 函式。 所建立的處理序的實際數目取決於各種因素，例如資源控管、 目前使用量的資源，其他工作階段中，與 R 指令碼搭配使用查詢的查詢執行計畫。

## <a name="query-parallelization"></a>查詢的平行處理

Microsoft 時，您可以使用 SQL Server 資料來源定義您的資料來當做 RxSqlServerData 資料來源物件。

建立資料來源為基礎的整個資料表或檢視表：

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

建立 SQL 查詢為基礎的資料來源：

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果資料來源，而不是查詢中指定的資料表，則 R 服務會使用內部的啟發學習法來判斷所需的資料行來擷取資料表;不過，這個方法不太可能會導致平行執行。

若要確保以平行方式，可分析資料，用來擷取資料的查詢應該包覆 database engine 可建立平行查詢計畫的方式。 如果程式碼或演算法使用的大量資料，請確定提供給查詢`RxSqlServerData`最適合用於平行執行。 不會導致平行執行計畫的查詢會導致單一處理序進行計算。

如果您要使用大型資料集，請使用 Management Studio 或另一個 SQL query analyzer 中的才能執行 R 程式碼，來分析執行計劃。 接著，採取任何建議的步驟，以改善查詢效能。 例如，資料表上遺漏的索引可能會影響執行查詢所花費的時間。 如需詳細資訊，請參閱[效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

另一個常見的錯誤，可能會影響效能是查詢擷取多個資料行，比所需。 例如，如果公式根據只有三個資料行，但來源資料表有 30 的資料行，您會不必要地移動資料。

 + 請避免使用`SELECT *`！
 + 需要一些時間來檢閱資料集中的資料行，並識別分析所需的項目
 + 從您的查詢中移除包含的資料類型與 R 程式碼，例如 GUID 和 rowguids 的資料不相容的任何資料行
 + 不支援的日期和時間格式的檢查
 + 而不是載入資料表，請建立一個檢視，選取特定值或投射資料行，以避免發生轉換錯誤

## <a name="optimizing-the-machine-learning-algorithm"></a>最佳化機器學習演算法

本節提供其他的秘訣和 RevoScaleR 和 Microsoft R 中的其他選項特定的資源

> [!TIP]
> R 最佳化的一般討論已超出本文的範圍。 不過，如果您需要做出更快速的程式碼，我們建議熱門文章[R 煉獄](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 它涵蓋了在 R 中的程式設計建構和常見的問題，在生動的語言和詳細資料，並提供許多 R 程式設計技巧的範例。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的最佳化

許多 RevoScaleR 演算法都支援參數，來控制定型的模型產生方式。 雖然精確度和模型的正確性很重要，則可能同樣重要演算法的效能。 若要取得精確度和定型時間之間的正確平衡，您可以修改參數來增加的速度，計算，而且在許多情況下，而不會降低精確度或正確性改善效能。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` 支援`maxDepth`參數，控制的決策樹的深度。 做為`maxDepth`會增加，效能可能會降低，所以分析優點增加與影響效能的深度。

    您也可以控制時間複雜性和預測精確度，例如調整參數之間的平衡`maxNumBins`， `maxDepth`， `maxComplete`，和`maxSurrogate`。 將深度增加到超過 10 或 15 以上，會讓計算付出很高的代價。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    請嘗試使用`cube`引數，如果第一個相依變數中的公式是因數變數。
    
    當`cube`設`TRUE`，就會使用資料分割的反向，可能會比較快，並使用較少的記憶體比標準迴歸計算執行迴歸。 如果公式含有大量變數，就會顯著提升效能。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    使用`cube`引數，如果第一個相依變數是因數變數。
    
    當`cube`設`TRUE`，此演算法會使用資料分割的反向，可能會比較快，並使用較少的記憶體。 如果公式含有大量變數，就會顯著提升效能。

如需其他指引 RevoScaleR 的最佳化的詳細資訊，請參閱下列文章：

+ 技術支援文件：[效能微調 rxDForest 和 rxDTree 選項](https://support.microsoft.com/kb/3104235)

+ 控制模型的方法納入促進式樹狀結構模型：[估計模型使用隨機梯度促進](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR 如何移動和處理資料的概觀： [ScaleR 中撰寫自訂的區塊處理演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的程式設計模型：[管理 RevoScaleR 中的執行緒](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 函式的參考[rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 函式的參考[rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>使用 MicrosoftML

我們也建議您查看到新**MicrosoftML**封裝，提供可調整的機器學習演算法，可以使用的計算內容和提供的 RevoScaleR 轉換。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何選擇 MicrosoftML 演算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>實施使用 Microsoft R Server 的方案

如果您的案例涉及快速預測使用預存的模型，或將機器學習服務整合到應用程式，您可以使用[實施](https://docs.microsoft.com/r-server/what-is-operationalization)Microsoft R Server （先前稱為 DeployR） 中的功能。

+ 做為**資料科學家**，使用[mrsdeploy 封裝](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)共用 R 程式碼與其他電腦，以及整合 web、 桌面、 行動裝置版和儀表板應用程式內的 R 分析：[如何發行和管理在 R 伺服器 R web 服務](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 做為**管理員**、 了解如何管理封裝、 監視網頁的節點和計算節點，以及控制 R 工作的安全性：[如何互動，以及在 R 中使用 web 服務](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>在這一系列的文章

[效能調整的 R-簡介](sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](sql-server-configuration-r-services.md)

[效能調整的 R-R 程式碼和資料最佳化](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
