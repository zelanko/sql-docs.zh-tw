---
title: RevoScaleR R 函式程式庫
description: SQL Server 2016 R Services 和 SQL Server 機器學習服務 (內含 R) 中的 RevoScaleR 函式程式庫簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7b24d5499e618a09c4d80e8614b08219e6c6f788
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706766"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (SQL Server 中的 R 程式庫)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** 是 Microsoft 提供的一個高效能資料科學函式程式庫。 函式支援資料匯入、資料轉換、摘要、視覺化和分析。

相較於基底 R 函式，RevoScaleR 作業可以針對非常大型的資料集、平行處理，以及在分散式檔案系統上執行。 函式可以使用區塊化，以及在作業完成時重組結果，來處理無法放入記憶體中的資料集。

RevoScaleR 函式會以 **rx** 或 **Rx** 首碼表示，讓它們易於識別。

RevoScaleR 可作為分散式資料科學的平台。 例如，您可以在 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package) 中，使用 RevoScaleR 計算內容和轉換搭配最先進的演算法。 您也可以使用 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 平行執行基底 R 函式。

## <a name="full-reference-documentation"></a>完整參考文件

**RevoScaleR** 程式庫散佈在多個 Microsoft 產品中，但不論您是在 SQL Server 還是在另一個產品中取得此程式庫，其使用方式都相同。 由於函式相同，因此[個別 RevoScaleR 函式的文件](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)只發佈至 Microsoft Machine Learning Server 之 [R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

## <a name="versions-and-platforms"></a>版本與平台

**RevoScaleR** 程式庫以 R 3.4.3 為基礎，且只有當您安裝下列其中一個 Microsoft 產品或下載項目時才會提供：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 用戶端](set-up-a-data-science-client.md)

> [!NOTE]
> 在 SQL Server 2017 中，完整產品發行版本僅適用於 Windows。 在 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) 中，**RevoScaleR** 則同時支援 Windows 和 Linux。

## <a name="functions-by-category"></a>依類別區分的函式

本節依類別列出函式，讓您了解每個函式的使用方式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)來依字母順序尋找函式。

## <a name="1-data-source-and-compute"></a>1-資料來源與計算

**RevoScaleR** 包含用於建立資料來源及設定計算執行位置 (或*計算內容*) 的函式。 資料來源物件是可一起指定連接字串和您想要之資料集 (可定義為資料表、檢視或查詢) 的容器。 不支援預存程序呼叫。 下表列出與 SQL Server 案例相關的函式。

在某些情況下，SQL Server 和 R 會使用不同的資料類型。 如需 SQL 與 R 資料類型間的對應清單，請參閱 [R 與 SQL 的對應資料類型](r-libraries-and-data-types.md)。

| 函數| Description|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  建立 SQL Server 計算內容物件以將計算推送至遠端執行個體。 數個 **RevoScaleR** 函式會以計算內容作為引數。 |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 取得或設定使用中的計算內容。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 根據 SQL Server 查詢或資料表來建立資料物件。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 根據 ODBC 連線來建立資料來源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 根據本機 XDF 檔案來建立資料來源。 XDF 檔案通常用來將記憶體內的資料卸載至磁碟。 當使用的資料超過可從資料庫以單一批次傳輸的資料，或是超過記憶體可容納的資料時，XDF 檔案非常實用。 例如，如果您會定期將大量資料從資料庫移到本機工作站，而不是針對每個 R 作業重複地查詢資料庫，則您可以使用 XDF 檔案作為一種快取以將資料儲存在本機，然後在您的 R 工作區中使用它。|

> [!TIP]
> 如果您不熟悉資料來源或計算內容，建議您從 Microsoft Machine Learning Server 文件中的[分散式計算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) \(英文\) 開始著手。

### <a name="perform-ddl-statements"></a>執行 DDL 陳述式

您可以從 R 執行 DDL 陳述式，前提是您具有執行個體及資料庫的必要權限。 下列函式會使用 ODBC 呼叫來執行 DDL 陳述式或擷取資料庫結構描述。

| 函數| Description|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | 置放 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料表，或檢查資料庫資料表或物件是否存在。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 執行定義或操作資料庫物件的資料定義語言 (DDL) 命令。 此函式無法傳回資料，而且只會用來擷取或修改物件結構描述或中繼資料。|

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

建立資料來源物件之後，您可以使用物件將資料載入其中、轉換資料，或將新的資料寫入至指定的目的地。 根據來源中的資料大小，您也可以定義資料來源中的批次大小，以及以區塊移動資料。

| 函數 | Description |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 檢查資料來源是否可用、開啟或關閉資料來源、從來源讀取資料、將資料寫入至目標，以及關閉資料來源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 將資料從資料來源移到檔案儲存體或資料框架中。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 在資料來源之間移動資料時進行轉換。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-圖形函式

| 函數名稱 | Description |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |從資料建立長條圖。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |從資料建立線繪圖。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |計算可繪製的 Lorenz 曲線。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |從實際和預測資料計算並繪製 ROC 曲線。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-描述性統計資料

| 函數名稱 | Description |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |計算 .xdf 檔案和資料框架的近似分位數，而不需要排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |資料的基本摘要統計資料，包括依群組計算。 不支援依群組計算寫入至 .xdf 檔案。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |資料以公式為基礎的交叉資料表。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |以公式為基礎的替代交叉資料表，針對有效表示傳回的 Cube 結果所設計。 不支援將輸出寫入至 .xdf 檔案。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |交叉資料表的臨界摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |將交叉資料表結果轉換為 xtabs 物件。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |針對 xtabs 物件執行卡方檢定。 搭配小型資料集使用，而且不會將資料區塊化。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |針對 xtabs 物件執行費雪精確檢定。 搭配小型資料集使用，而且不會將資料區塊化。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |使用 xtabs 物件計算肯德爾等級相關係數。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |將函式套用到成對組合的 xtabs 物件資料列與資料行。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩兩 xtabs 物件的相對風險。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩兩 xtabs 物件的勝算比。 | 

<sup>*</sup> 表示此類別中最常用的函式。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-預測函式

| 函數名稱 | Description |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |將線性模型套入資料。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |將羅吉斯迴歸模型套入資料。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |將廣義線性模型套入資料。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |計算一組變數的共變數、相關性或正方形 / 交叉乘積矩陣的總和。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |將分類或迴歸樹狀結構套入資料。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |使用隨機梯度提升演算法，將分類或迴歸決策樹系套入資料。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |將分類或迴歸決策樹系套入資料。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |計算適合模型的預測。 輸出必須是 XDF 資料來源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |執行 K 平均數叢集。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |執行貝氏機率分類。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |計算一組變數的共變數矩陣。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算一組變數的相關矩陣。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算一組變數的正方形/交叉乘積矩陣總和。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |使用二元分類器系統的實際與預測值的接收器操作特徵曲線 (ROC) 計算。 | 

<sup>*</sup> 表示此類別中最常用的函式。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

封裝在預存程序中的 R 程式碼可呼叫 **RevoScaleR** 中的函式。 大多數開發人員會在本機建置 **RevoScaleR** 解決方案，然後將完成的 R 程式碼移轉至預存程序作為部署練習。

在本機執行時，您通常會從命令列或從 R 開發環境執行 R 指令碼，然後使用其中一個 **RevoScaleR** 函式來指定 SQL Server 計算內容。 您可以將遠端計算內容用於整個程式碼，也可以用於個別函式。 例如，您可以將模型定型卸載至伺服器，以使用最新資料並避免資料移動。

當您準備好將 R 指令碼封裝在預存程序 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 內時，建議您將程式碼重寫成已清楚定義輸入和輸出的單一函式。 

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用於 SQL 的 R 開發人員：將模型定型並使其可運作](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples) \(英文\)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) \(英文\) 
