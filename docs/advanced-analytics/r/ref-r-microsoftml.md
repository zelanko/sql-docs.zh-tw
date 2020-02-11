---
title: MicrosoftML R 函式程式庫
description: SQL Server 2016 R Services 與含 R 之 SQL Server 機器學習服務中的 MicrosoftML 函式程式庫簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 450091bba39cf10e551b8da5e62993ca676c64af
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73707924"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server 中的 R 程式庫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MicrosoftML** 是來自 Microsoft 的 R 函式程式庫，可提供高效能的機器學習演算法。 它包含用於定型與轉換、評分、文字與影像分析的函式，以及用於從現有資料衍生值的特徵擷取。

機器學習 API 是 Microsoft 為內部機器學習應用程式開發的 API，並已使用多核心處理和快速資料串流，經過數年的去蕪存菁而得以在巨量資料方面支援高效能。 MicrosoftML 也包含許多適用於文字與影像處理的轉換。

## <a name="full-reference-documentation"></a>完整參考文件

**MicrosoftML** 程式庫散佈在多個 Microsoft 產品中，但不論您是在 SQL Server 還是在另一個產品中取得此程式庫，其使用方式都相同。 由於函式相同，因此[個別 RevoScaleR 函式的文件](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)只發佈至 Microsoft Machine Learning Server 之 [R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

## <a name="versions-and-platforms"></a>版本與平台

**MicrosoftML** 程式庫以 R 3.4.3 為基礎，且只有當您安裝下列其中一個Microsoft 產品或下載項目時才會提供：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 用戶端](set-up-a-data-science-client.md)

> [!NOTE]
> 在 SQL Server 2017 中，完整產品發行版本僅適用於 Windows。 在 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) 中，**MicrosoftML** 則同時支援 Windows 和 Linux。

## <a name="package-dependencies"></a>套件相依性

**MicrosoftML** 中的演算法在下列方面倚賴 [RevoScaleR](ref-r-revoscaler.md)：

+ 資料來源物件。 **MicrosoftML** 函式所取用的資料是使用 **RevoScaleR** 函式來建立的資料。
+ 遠端計算 (將函式執行切換至遠端 SQL Server 執行個體)。 **RevoScaleR** 程式庫提供為 SQL Server 建立和啟用遠端計算內容的函式。

在大多數情況下，您會在每次使用 **MicrosoftML** 時一起載入套件。

## <a name="functions-by-category"></a>依類別區分的函式

本節依類別列出函式，讓您了解每個函式的使用方式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)來依字母順序尋找函式。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-機器學習演算法

| 函式名稱 | 描述 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank 的實作，MART 梯度提升演算法的有效實作。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 使用 [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) 的隨機樹系與分位數迴歸樹系實作。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 使用 L-BFGS 的羅吉斯迴歸。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 單一類別支援向量機器。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 二進位、多類別及迴歸類神經網路。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 適用於線性二進位分類與迴歸的推測雙座標堆疊最佳化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 將一些各種種類的模型定型，以取得與從單一模型取得的效能相比更佳的預測效能。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-轉換函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 從多個資料行建立單一向量值資料行的轉換。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 搭配字典使用類別目錄轉換來建立指標向量。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 透過雜湊將類別目錄值轉換成指標陣列。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 從指定的文字主體產生一包連續單字序列 (稱為 n-grams) 的計數。 這可提供語言偵測、Token 化、停用字詞移除、文字正規化及特徵產生。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 對自然語言文字進行評分，並建立包含文字中情緒為正面之機率的資料行。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 允許定義適用於計數型和雜湊型特徵擷取的引數。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 選取一組要重新定型的資料行，捨棄所有其他資料行。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 使用指定的模式從指定的變數中選取功能。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 載入影像資料。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 使用指定的調整大小方法，將影像大小調整成指定的維度。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 從影像中擷取像素值。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 使用預先定型的深度類神經網路模型將影像特徵化。|


## <a name="3-scoring-and-training-functions"></a>3-評分與定型函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 從 SQL Server、使用預存程序或從啟用即時評分功能的 R 程式碼來執行評分程式庫，以提供更快的預測效能。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 將資料從輸入資料集轉換至輸出資料集。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | 提供 Microsoft R Machine Learning 模型的摘要。|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-分類與迴歸的損失函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指數分類損失函式的規格。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 記錄分類損失函式的規格。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 鉸鏈分類損失函式的規格。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平滑鉸鏈分類損失函式的規格。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 波氏迴歸損失函式的規格。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平方迴歸損失函式的規格。   |   

## <a name="5-feature-selection-functions"></a>5-功能選取函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 計數模式中特徵選取的規格。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 相互資訊模式中特徵選取的規格。 |

## <a name="6-ensemble-modeling-functions"></a>6-整體模型化函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 建立包含可使用 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) 將「快速樹狀結構」模型定型之函式名稱與引數的清單。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 建立包含可使用 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) 將「快速樹系」模型定型之函式名稱與引數的清單。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 建立包含可使用 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) 將「快速線性」模型定型之函式名稱與引數的清單。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 建立包含可使用 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) 將「羅吉斯迴歸」模型定型之函式名稱與引數的清單。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 建立包含可使用 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) 將 OneClassSvm 模型定型之函式名稱與引數的清單。|

## <a name="7-neural-networking-functions"></a>7-類神經網路函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 指定 [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) 機器學習演算法的最佳化演算法。|


## <a name="8-package-state-functions"></a>8-套件狀態函式

| 函式名稱 | 描述 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 用來儲存全套件狀態的環境物件。 |


## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

封裝在預存程序中的 R 程式碼可呼叫 **MicrosoftML** 中的函式。 大多數開發人員會在本機建置 **MicrosoftML** 解決方案，然後將完成的 R 程式碼移轉至預存程序作為部署練習。

適用於 R 的 **MicrosoftML** 套件在 SQL Server 2017 中是「現成」安裝的項目。 它也可供與 SQL Server 2016 搭配使用，前提是您升級該執行個體的 R 元件：[使用繫結來升級 SQL Server 的執行個體](../install/upgrade-r-and-python.md)

預設並不會安裝此套件。 作為第一步，請載入 **MicrosoftML** 套件，然後如果您需要使用遠端計算內容、相關連線能力或資料來源物件，則載入 **RevoScaleR**。 接著，參考您需要的個別函式。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用於 SQL 的 R 開發人員：將模型定型並使其可運作](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples) \(英文\)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) \(英文\) 