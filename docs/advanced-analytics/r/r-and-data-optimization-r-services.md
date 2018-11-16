---
title: SQL Server R Services-資料最佳化的效能 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3fda560aedb7a0e1119a0524ffefe42a476c4aed
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699506"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services-資料最佳化的效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是說明兩個案例研究為基礎的 R 服務的效能最佳化一系列的第三場。 這篇文章討論效能最佳化，適用於 R 或 Python 指令碼在 SQL Server 中執行。 它也會描述您可用來更新 R 程式碼，以提升效能並避免已知的問題的方法。

## <a name="choosing-a-compute-context"></a>選擇計算內容

在 SQL Server 2016 和 2017年中，您可以使用其中一個**本機**或是**SQL**執行 R 或 Python 指令碼時，計算內容。

使用時**本機**計算內容中，分析會執行您的電腦上並不是在伺服器上。 因此，如果您要從 SQL Server 以使用您的程式碼中取得資料，必須擷取的資料在網路上。 因此網路傳送而產生的效能影響，取決於所傳送的資料大小、網路速度，以及同一時間發生的其他網路傳送。

使用時**SQL Server 計算內容**，在伺服器上執行的程式碼。 如果您要從 SQL Server 中取得資料，資料應該是本機伺服器執行的分析，並因此導入任何網路額外負荷。 如果您需要從其他來源匯入資料，請考慮事先排列 ETL。

使用大型資料集時，您一律應使用 SQL 計算內容。

## <a name="factors"></a>因素

R 語言有的概念*因素*，這是特殊的分類資料的變數。 資料科學家通常會在公式中使用因數變數，因為處理類別變數作為因素可確保資料正確地處理透過 machine learning 函式。 如需詳細資訊，請參閱 <<c0> [ 的 R for Dummies： 因素變數](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

根據設計，因素變數可以從轉換字串與整數，再進行儲存或處理。 R`data.frame`函式會處理所有字串作為因數變數，除非引數*stringsAsFactors*設定為**False**。 這表示為字串會自動轉換成整數進行處理，而且接著對應回原始的字串。

如果因數的來源資料儲存為整數時，效能會受到影響，因為 R 執行階段將因素整數轉換為字串，然後執行 自己內部的字串至整數轉換。

若要避免這種執行階段的轉換，請考慮將值儲存為整數，在 SQL Server 資料表中，並且使用_colInfo_引數來指定資料行做為因數層級。 RevoScaleR 中的大部分資料來源物件會採用參數_colInfo_。 您可以使用此參數命名的資料來源所使用的變數、 指定其型別，以及定義變數層級或轉換資料行值。

比方說，下列 R 函式呼叫從資料表取得 1、 2 和 3 的整數，但對應"banana"、 「 橙色 」 和成因素層級"的 apple"值。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

當來源資料行包含字串時，總是會比較有效率的方式是指定前面使用層級_colInfo_參數。 例如，下列 R 程式碼會將字串視為因素在讀取。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果沒有模型產生中的沒有語意差異，然後第二種方法可能會導致更好的效能。

## <a name="data-transformations"></a>資料轉換

資料科學家通常會使用以 R 撰寫的轉換函數做為分析的一部分。 轉換函數會套用至從資料表中擷取每個資料列。 在 SQL Server，這類轉換會套用至批次，而這需要的 R 解譯器和分析引擎之間的通訊中所擷取的所有資料列。 為了執行轉換，資料會在 SQL、分析引擎及 R 解譯器處理序之間來回移動。

基於這個理由，R 程式碼的過程中使用轉換可以有顯著的負面影響，對效能的演算法，牽涉的資料量而定。

會有所有必要的資料行中的資料表或檢視，然後才執行分析，並避免在計算期間的轉換更有效率。 如果無法在現有資料表中加入額外的資料行，請考慮建立其他含有已轉換資料行的資料表或檢視，並使用適當的查詢來擷取資料。

## <a name="batch-row-reads"></a>讀取批次資料列

如果您使用 SQL Server 資料來源 (`RxSqlServerData`) 在您的程式碼中，我們建議您嘗試將參數_rowsPerRead_指定批次大小。 此參數會定義查詢並再傳送到外部指令碼進行處理的資料列數目。 在執行階段，演算法就會看到每個批次中的資料列中指定數字。

控制處理一次的資料量的能力，可協助您解決或避免發生問題。 例如，如果您輸入的資料集是非常廣泛 （具有許多資料行），或如果資料集有幾個大型的資料行 （例如任意文字），您可以減少批次大小，以避免記憶體不足的分頁資料。

根據預設，此參數的值設為 50000，以確保適當的效能，即使在記憶體不足的電腦上。 如果伺服器有足夠的可用記憶體，則此值增加到 500,000 或甚至一百萬可以產生更好的效能，尤其是對大型資料表。

增加批次大小明顯大型資料集，在和中的工作，可以在多個處理序上執行的優點。 不過，增加此值不會一律產生最佳結果。 我們建議您試驗您的資料和演算法來決定最佳的值。

## <a name="parallel-processing"></a>平行處理

若要改善的效能**rx**分析函式，您可以利用 SQL Server 能夠在伺服器電腦上使用可用的核心平行執行工作。

有兩種方式可達到使用 SQL Server 中 R 的平行處理：

-   **使用\@平行。** 使用 `sp_execute_external_script` 預存程序來執行 R 指令碼時，請將 `@parallel` 參數設為 `1`。 這是最好的方法，如果您的 R 指令碼會執行**不**使用 RevoScaleR 函式，都有其他機制進行處理。 如果您的指令碼使用 RevoScaleR 函式 （通常具有前置的"rx"開頭）、 平行處理會自動執行，而且您不需要明確設定`@parallel`至`1`。

    如果可以平行處理 R 指令碼，而且可平行處理的 SQL 查詢，database engine 就會建立多個平行處理序。 您可以建立的程序的最大數目等於**的最大平行處理原則程度**(MAXDOP) 設定執行個體。 所有處理程序再執行相同的指令碼，但接收只包含資料的一部分。
    
    因此，此方法不一定會看到所有的資料，例如當的指令碼適用於定型模型。 不過，在以平行方式執行工作 (例如批次預測) 時非常實用。 如需使用平行處理原則的詳細資訊`sp_execute_external_script`，請參閱**進階提示︰ 平行處理**一節[TRANSACT-SQL 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

-   **使用 numTasks = 1。** 使用時**rx**函式在 SQL Server 計算內容中，會將值_numTasks_參數，以您想要建立的處理序數目。 建立處理序的數目不能超過**MAXDOP**; 不過，建立處理序的實際數目取決於資料庫引擎，而且可能會小於您要求。

    如果可以平行處理 R 指令碼，而且可平行處理的 SQL 查詢，然後 SQL Server 建立多個平行處理序執行 rx 函數時。 所建立的處理序的實際數目取決於各種因素，例如資源控管、 目前的資源使用量、 其他工作階段，以及搭配 R 指令碼使用查詢的查詢執行計畫。

## <a name="query-parallelization"></a>查詢平行化作業

在 Microsoft R 中，您可以使用 SQL Server 資料來源當做 RxSqlServerData 資料來源物件定義您的資料。

建立資料來源為基礎的整個資料表或檢視表：

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

建立 SQL 查詢為基礎的資料來源：

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果資料來源，而不是查詢中指定的是資料表，R Services 會使用內部的啟發學習法，在決定從表格中，擷取必要的資料行不過，這種方法不太可能會導致平行執行。

若要確保以平行方式，可分析資料，用來擷取資料的查詢應該進行框架處理的方式，database engine 可建立平行查詢計畫。 如果程式碼或演算法會使用大量的資料，請確定提供給查詢`RxSqlServerData`最適合用於平行執行。 不會導致平行執行計畫的查詢會導致單一處理序進行計算。

如果您需要使用大型資料集，使用 Management Studio 或另一個 SQL query analyzer 中的再執行 R 程式碼，來分析執行計畫。 然後，採取任何建議的步驟，以改善查詢效能。 例如，資料表上遺漏的索引可能會影響執行查詢所花費的時間。 如需詳細資訊，請參閱 <<c0> [ 效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

可能會影響效能的另一個常見錯誤是查詢擷取所需更多的資料行。 例如，如果公式根據只有三個資料行，但您的來源資料表有 30 個資料行，您會不必要地移動資料。

 + 請避免使用`SELECT *`！
 + 需要一些時間來檢閱資料集中的資料行，並識別分析所需的項目
 + 移除您的查詢包含的 R 程式碼，例如 GUID 和 rowguids 的資料與不相容資料類型的任何資料行
 + 不支援的日期和時間格式的檢查
 + 而不是載入資料表，請建立一個檢視，選取特定值或轉換資料行，以避免發生轉換錯誤

## <a name="optimizing-the-machine-learning-algorithm"></a>最佳化機器學習演算法

本節提供其他的祕訣和 RevoScaleR 和其他選項，Microsoft 特有的資源

> [!TIP]
> 最佳化 R 的一般討論已超出本文的範圍。 不過，如果您需要更快讓您的程式碼，我們建議受歡迎的文章中， [R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 它包含在 R 中的程式設計建構和逼真的語言和詳細資料，常見的錯誤，而提供的 R 程式設計技術的許多特定範例。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的最佳化

許多 RevoScaleR 演算法都支援參數來控制如何產生定型的模型。 雖然的精確度和模型的正確性很重要，演算法的效能可能同樣重要。 若要取得適當的平衡精確度和定型時間之間，您可以修改參數，以加快計算，而且在許多情況下，改善效能，而不會降低精確度或正確性。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` 支援`maxDepth`參數，控制的決策樹的深度。 為`maxDepth`會增加，效能可能會降低，因此務必要分析增加深度與影響效能的優點。

    您也可以控制時間複雜性和預測精確度，例如調整參數之間的平衡`maxNumBins`， `maxDepth`， `maxComplete`，和`maxSurrogate`。 將深度增加到超過 10 或 15 以上，會讓計算付出很高的代價。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    請嘗試使用`cube`引數，如果公式中的第一個相依變數是因數變數。
    
    當`cube`設為`TRUE`，迴歸是使用資料分割的反向，它可能會比較快，使用的記憶體比標準迴歸計算還要少。 如果公式含有大量變數，就會顯著提升效能。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    使用`cube`引數，如果第一個相依變數是因數變數。
    
    當`cube`設為`TRUE`，此演算法會使用資料分割的反向，它可能會更快，使用較少的記憶體。 如果公式含有大量變數，就會顯著提升效能。

如需其他指引 RevoScaleR 的最佳化的詳細資訊，請參閱下列文章：

+ 技術支援文件： [rxDForest 和 rxDTree 的效能調整選項](https://support.microsoft.com/kb/3104235)

+ 推進式決策的樹模型中的控制模型的方法符合：[估計模型使用隨機梯度促進](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR 如何移動及處理資料的概觀： [ScaleR 中撰寫自訂的區塊處理演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的程式設計模型：[管理 RevoScaleR 中的執行緒](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 函式參考[rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 函式參考[rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>使用 MicrosoftML

我們也建議您看看新**MicrosoftML**套件，提供可調整機器學習演算法，可以使用計算內容和提供的 RevoScaleR 的轉換。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何選擇 MicrosoftML 演算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>操作方案，使用 Microsoft R Server

如果您的案例牽涉到使用預存的模型，快速預測，或將機器學習服務整合到應用程式中，您可以使用[operationalization](https://docs.microsoft.com/r-server/what-is-operationalization) （之前稱為 DeployR） 的 Microsoft R Server 中的功能。

+ 作為**資料科學家**，使用[mrsdeploy 套件](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)與其他電腦共用 R 程式碼，並將 R 分析 web、 桌面、 行動及儀表板的應用程式整合：[如何發佈和管理 R 伺服器中的 R web 服務](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 作為**系統管理員**、 了解如何管理封裝、 監視 web 節點和計算節點，以及控制 R 作業上的安全性：[如何互動，並使用 R 中的 web 服務](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>在這一系列的文章

[效能微調 – 簡介](sql-server-r-services-performance-tuning.md)

[R-SQL Server 組態的效能微調](sql-server-configuration-r-services.md)

[R-R 效能微調程式碼和資料最佳化](r-and-data-optimization-r-services.md)

[效能微調-案例研究結果](performance-case-study-r-services.md)
