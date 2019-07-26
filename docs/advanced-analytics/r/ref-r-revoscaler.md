---
title: RevoScaleR R 函數程式庫
description: 簡介 SQL Server 2016 R Services 中的 RevoScaleR 函式程式庫和使用 R 的 SQL Server 2017 Machine Learning Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: d73399522966a132b025244a1739afa01a194116
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470003"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (SQL Server 中的 R 程式庫)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR**是 Microsoft 提供的高效能資料科學函數程式庫。 函數支援資料匯入、資料轉換、摘要、視覺化和分析。

相較于基底 R 函式, RevoScaleR 作業可以針對非常大型的資料集、平行處理, 以及在分散式檔案系統上執行。 函數可以使用區塊化, 以及在作業完成時目的地重組結果, 來處理無法放入記憶體中的資料集。

RevoScaleR 函式會以**rx**或**rx**前置詞表示, 讓它們更容易識別。

RevoScaleR 可作為分散式資料科學的平臺。 例如, 您可以在[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)中使用 RevoScaleR 計算內容和轉換搭配最先進的演算法。 您也可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) , 以平行方式執行基底 R 函數。

## <a name="full-reference-documentation"></a>完整參考檔

**RevoScaleR**程式庫是散發在多個 Microsoft 產品中, 但不論您是在 SQL Server 或其他產品中取得程式庫, 使用方式都相同。 因為函式相同, 所以[個別 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)函式的檔集只會發佈到[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的一個位置, 以供 Microsoft Machine Learning Server。 若有任何產品特定行為存在, 則函式說明頁面中會注明不一致的情況。

## <a name="versions-and-platforms"></a>版本和平臺

**RevoScaleR**程式庫是以 R 3.4.3 為基礎, 只有在您安裝下列其中一個 Microsoft 產品或下載時, 才能使用:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 用戶端](set-up-a-data-science-client.md)

> [!NOTE]
> 完整產品發行版本僅限 Windows, 從 SQL Server 2017 開始。 **RevoScaleR**的 Linux 支援是[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)的新功能。

## <a name="functions-by-category"></a>依類別分類的函數

本節依類別列出函式, 讓您瞭解如何使用每一種功能。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)來依字母順序尋找函數。

## <a name="1-data-source-and-compute"></a>1-資料來源和計算

**RevoScaleR**包含用來建立資料來源的函數, 以及設定執行計算的位置或*計算內容*。 資料來源物件是可一起指定連接字串和您想要之資料集 (可定義為資料表、檢視或查詢) 的容器。 不支援預存程序呼叫。 下表列出與 SQL Server 案例相關的函數。

在某些情況下, SQL Server 和 R 會使用不同的資料類型。 如需 SQL 和 R 資料類型之間的對應清單, 請參閱[R 對 SQL 資料類型](r-libraries-and-data-types.md)。

| 函數| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  建立 SQL Server 計算內容物件, 以將計算推送至遠端實例。 有數個**RevoScaleR**函式會將計算內容視為引數。 |
|[rxGetComputeCoNtext/rxSetComputeCoNtext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 取得或設定使用中的計算內容。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 根據 SQL Server 查詢或資料表建立資料物件。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 建立以 ODBC 連接為基礎的資料來源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 建立以本機 XDF 檔案為基礎的資料來源。 XDF 檔案通常用來將記憶體內部資料卸載至磁片。 當您使用的資料量比可從一個批次中的資料庫傳輸更多, 或超過記憶體中可容納的資料時, XDF 檔會很有用。 例如, 如果您定期將大量資料從資料庫移到本機工作站, 而不是針對每個 R 作業重複查詢資料庫, 您可以使用 XDF 檔案做為一種快取, 將資料儲存在本機, 然後在您的 R 工作區中使用它。|

> [!TIP]
> 如果您不熟悉資料來源或計算內容, 建議您先從 Microsoft Machine Learning Server 檔中的[分散式運算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)開始。

### <a name="perform-ddl-statements"></a>執行 DDL 語句

如果您有實例和資料庫的必要許可權, 您可以從 R 執行 DDL 語句。 下列函數會使用 ODBC 呼叫來執行 DDL 語句或抓取資料庫架構。

| 函數| 描述|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]卸載資料表, 或檢查資料庫資料表或物件是否存在。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 執行定義或操作資料庫物件的資料定義語言 (DDL) 命令。 此函式無法傳回資料, 而且只會用來抓取或修改物件架構或中繼資料。|

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

建立資料來源物件之後, 您可以使用物件將資料載入其中、轉換資料, 或將新的資料寫入指定的目的地。 根據來源中的資料大小，您也可以定義資料來源中的批次大小，以及以區塊移動資料。

| 函數 | 描述 |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 請檢查資料來源是否可用、開啟或關閉資料來源、從來源讀取資料、將資料寫入目標, 以及關閉資料來源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 將資料從資料來源移到檔案儲存體或資料框架中。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 在資料來源之間移動資料時進行轉換。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3個圖形函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |從資料建立長條圖。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |從資料建立線條繪圖。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |計算可繪製的 Lorenz 曲線。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |從實際和預測的資料計算並繪製 ROC 曲線。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-描述性統計資料

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |計算 xdf 檔案和資料框架的近似分量, 而不進行排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |資料的基本摘要統計資料, 包括依群組計算。 不支援將群組計算寫入至 xdf 檔案。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |以公式為基礎的交叉資料表資料。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |以公式為基礎的替代交叉表, 為有效率的標記法傳回 cube 結果所設計。 不支援將輸出寫入至 xdf 檔案。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |跨 tabulations 的臨界摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |將交叉表結果轉換成 xtabs 物件。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |在 xtabs 物件上執行卡方測試。 用於小型資料集, 而且不會將資料區塊。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |在 xtabs 物件上執行費雪的精確測試。 用於小型資料集, 而且不會將資料區塊。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |使用 xtabs 物件計算肯德爾的 Tau 次序相互關聯係數。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |將函式套用至成對的 xtabs 物件的資料列和資料行組合。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩個 xtabs 物件的相對風險。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |計算兩個 xtabs 物件的機率比率。 | 

<sup>*</sup>表示此類別中最常用的函數。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-預測函數

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |將線性模型納入資料。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |將羅吉斯回歸模型納入資料。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)<sup>*</sup> |將一般化線性模型納入資料。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |計算一組變數的共變數、相互關聯或平方/交叉乘積矩陣的總和。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |將分類或迴歸樹狀結構納入資料。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)<sup>*</sup> |使用隨機梯度提升演算法, 將分類或回歸決策樹系納入資料。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |將分類或回歸決策樹系納入資料。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |計算適合模型的預測。 輸出必須是 XDF 的資料來源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans)<sup>*</sup> |執行 k 表示叢集。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes)<sup>*</sup> |執行貝氏貝氏機率分類分類。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |計算一組變數的共變數矩陣。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算一組變數的相互關聯矩陣。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |計算一組變數的平方/交叉乘積矩陣總和。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |使用二元分類器系統中實際和預測值的接收端操作特性 (ROC) 計算。 | 

<sup>*</sup>表示此類別中最常用的函數。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

**RevoScaleR**中的函式可在封裝于預存程式中的 R 程式碼中呼叫。 大部分的開發人員會在本機建立**RevoScaleR**解決方案, 然後將完成的 R 程式碼遷移至預存程式作為部署練習。

在本機執行時, 您通常會從命令列或從 R 開發環境執行 R 腳本, 並使用其中一個**RevoScaleR**函數來指定 SQL Server 計算內容。 您可以針對整個程式碼或個別函式使用遠端計算內容。 例如, 您可能想要將模型定型卸載至伺服器, 以使用最新的資料, 並避免資料移動。

當您準備好要在預存程式內封裝 R 腳本時, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), 建議您將程式碼重寫為已清楚定義輸入和輸出的單一函式。 

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [瞭解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用于 SQL 開發人員的 R:定型和讓模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
