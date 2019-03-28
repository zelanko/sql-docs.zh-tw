---
title: RevoScaleR R 函式程式庫-SQL Server Machine Learning 服務
description: 在 SQL Server 2016 R Services 和 SQL Server 2017 Machine Learning 服務 RevoScaleR 函式程式庫簡介
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3745c6cd8c340ce4ad89cac84c5b6286126e3f89
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511298"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR （SQL Server 中的 R 程式庫）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR**是來自 Microsoft 的高效能的資料科學函式的程式庫。 函式支援匯入資料、 資料轉換、 摘要、 視覺化和分析。

相較於基底 R 函數，您可以執行 RevoScaleR 作業，針對非常大型資料集，以平行方式，並在分散式的檔案系統上。 函式可以透過不適合在記憶體中藉由使用區塊處理和重組結果完成作業時的資料集作業。

RevoScaleR 函式皆加**rx**或是**Rx**前置詞，使其更容易識別。

RevoScaleR 作為分散式的資料科學平台。 比方說，您可以使用 RevoScaleR 計算內容和轉換中的新狀態的演算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 您也可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)以平行方式執行基底 R 函數。

## <a name="full-reference-documentation"></a>完整的參考文件

**RevoScaleR**程式庫會分散在多個 Microsoft 產品中，但不論您取得 SQL Server 或另一個產品中的程式庫使用方式都相同。 函式是相同的因為[個別 RevoScaleR 函式文件](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)發行到下一個位置[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 應該任何產品專屬行為存在時，差異會記錄在函式說明頁面。

## <a name="versions-and-platforms"></a>版本與平台

**RevoScaleR**程式庫是依據 R 3.4.3 以及是否可以使用只有當您安裝其中一個下列的 Microsoft 產品或下載項目時：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 完整的產品版本是 Windows 專屬，從 SQL Server 2017 開始。 Linux 支援**RevoScaleR**的新功能[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="functions-by-category"></a>依類別目錄的函式

此區段會列出依類別目錄，讓您了解如何使用每個函式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)依字母順序尋找函式。

## <a name="1-data-source-and-compute"></a>1-資料來源和計算

**RevoScaleR**包含函式來建立資料來源和設定的位置，或*計算內容*，執行計算。 資料來源物件是可一起指定連接字串和您想要之資料集 (可定義為資料表、檢視或查詢) 的容器。 不支援預存程序呼叫。 SQL Server 案例與相關的函式列在下表中。

SQL Server 和 R 使用不同的資料類型，在某些情況下。 如需 SQL 和 R 資料類型之間的對應，請參閱[R 到 SQL 資料型別](r-libraries-and-data-types.md)。

| 函數| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  建立 SQL Server 計算內容物件，將計算推送到遠端執行個體。 數個**RevoScaleR**函式會採用當做引數的計算內容。 |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 取得或設定作用中的計算內容。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 建立 SQL Server 查詢或資料表為基礎的資料物件。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 建立 ODBC 連接為基礎的資料來源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 建立本機 XDF 檔案為基礎的資料來源。 XDF 檔案通常用於記憶體中將資料卸載至磁碟。 使用更多的資料，比可以傳輸，從資料庫中一個批次或超過記憶體內可容納的資料時，XDF 檔案可以是很有用。 比方說，如果定期在資料庫的本機工作站之間移動大量資料，而不是查詢資料庫中重複的每個 R 作業，您可以使用 XDF 檔案為類型的快取來儲存在本機的資料，然後在您的 R 工作區中使用它。|

> [!TIP]
> 如果您不熟悉之資料來源的概念，或計算內容，建議您先使用[分散式運算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)Microsoft Machine Learning Server 文件中。

### <a name="perform-ddl-statements"></a>執行 DDL 陳述式

如果您有執行個體和資料庫的必要權限，您可以從 R 執行 DDL 陳述式。 下列函式會使用 ODBC 呼叫，來執行 DDL 陳述式，或擷取資料庫結構描述。

| 函數| 描述|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | 卸除[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料表，或檢查的資料庫資料表或物件是否存在。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 執行資料定義語言 (DDL) 命令定義或管理資料庫物件。 此函數無法傳回資料，並只會用於擷取或修改物件結構描述或中繼資料。|

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

建立資料來源物件之後，您可以使用物件資料載入、 轉換資料，或將新的資料寫入至指定的目的地。 根據來源中的資料大小，您也可以定義資料來源中的批次大小，以及以區塊移動資料。

| 函數 | 描述 |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 檢查資料來源是否可用，請開啟或關閉資料來源、 從來源讀取資料、 將資料寫入到目標，並關閉資料來源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 檔案儲存體或資料框架，請從資料來源移動資料。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 在資料來源之間移動它時轉換資料。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-繪圖函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |從資料建立長條圖。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |從資料建立線繪圖。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |計算可繪製的 Lorenz 曲線。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |計算並繪製 ROC 曲線，從實際和預測的資料。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 描述性統計資料

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |計算接近.xdf 檔案和資料框架的分位數不排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |基本的資料，包括依群組計算摘要統計資料。 群組計算.xdf 檔案不支援寫入。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |公式是根據交叉資料表的資料。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |替代公式是根據交叉資料表專為有效率的表示法傳回 cube 的結果。 寫入不支援的.xdf 檔案中的輸出。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |跨 tabulations 的臨界摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |將跨表格式結果 xtabs 物件。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 物件執行卡方測試。 搭配小型資料集，而且不區塊資料。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 物件執行費雪精確檢定。 搭配小型資料集，而且不區塊資料。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |計算肯 Tau 陣序規範相互關聯係數使用 xtabs 物件。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |將函數套用到成對組合的資料列和資料行 xtabs 物件。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩兩 xtabs 物件上的相對風險。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩兩 xtabs 物件上的勝算比。 | 

<sup>*</sup> 表示此類別中最受歡迎的函式。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-預測函數

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |將線性模型套入資料。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |將羅吉斯迴歸模型套入資料。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |將廣義線性模型套入資料。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |計算的共變數、 相互關聯或總和的正方形 / 交叉乘積矩陣的一組變數。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |符合資料的分類或迴歸樹狀結構。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |適用於使用隨機梯度促進式演算法的資料分類或迴歸決策樹系。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |符合分類或迴歸決策樹系的資料。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |計算適合模型的預測。 輸出必須是 XDF 資料來源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |執行 k 平均數叢集。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |執行貝氏機率分類分類。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |計算一組變數的共變數矩陣。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算一組變數的相關矩陣。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算總和的正方形 / 交叉乘積矩陣的一組變數。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |接收者作業特性 (ROC) 計算從二元分類器系統的實際與預測值。 | 

<sup>*</sup> 表示此類別中最受歡迎的函式。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

中的函式**RevoScaleR**封裝在預存程序中的 R 程式碼中呼叫。 大部分的開發人員建置**RevoScaleR**解決方案在本機，然後將完成的 R 程式碼移轉到預存程序中，部署練習變更。

本機執行時，您通常在執行 R 指令碼，從命令列中，或從 R 開發環境，並指定使用其中一種在 SQL Server 計算內容**RevoScaleR**函式。 完整的程式碼，或個別的函式，您可以使用遠端計算內容。 例如，您可能要卸載至伺服器，以使用最新的資料，以避免資料移動的模型定型。

當您準備好要將封裝的預存程序中，R 指令碼[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我們建議您為已清楚定義的輸入和輸出的單一函式重寫程式碼。 

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用於 SQL 開發人員的 R:訓練和運作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [在 GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
