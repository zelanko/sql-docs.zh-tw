---
title: MicrosoftML R 函數程式庫
description: 簡介 SQL Server 2016 R Services 中的 MicrosoftML 函式程式庫和使用 R 的 SQL Server 2017 Machine Learning Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6808fa01bd4b62a67b220cec86d025820958298d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470015"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server 中的 R 程式庫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MicrosoftML**是 Microsoft 提供高效能機器學習服務演算法的 R 函式程式庫。 其中包含用於定型和轉換的函式、評分、文字和影像分析, 以及從現有資料衍生值的功能解壓縮。

機器學習服務 Api 是由 Microsoft 針對內部機器學習應用程式所開發, 並已在多年來進行調整, 以支援大量資料的高效能, 使用多核心處理和快速資料串流。 MicrosoftML 也包含多個文字和影像處理轉換。

## <a name="full-reference-documentation"></a>完整參考檔

**MicrosoftML**程式庫是散發在多個 Microsoft 產品中, 但不論您是在 SQL Server 或其他產品中取得程式庫, 使用方式都相同。 因為函式相同, 所以[個別 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)函式的檔集只會發佈到[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的一個位置, 以供 Microsoft Machine Learning Server。 若有任何產品特定行為存在, 則函式說明頁面中會注明不一致的情況。

## <a name="versions-and-platforms"></a>版本和平臺

**MicrosoftML**程式庫是以 R 3.4.3 為基礎, 只有在您安裝下列其中一個 Microsoft 產品或下載時, 才能使用:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 用戶端](set-up-a-data-science-client.md)

> [!NOTE]
> 完整產品發行版本僅限 Windows, 從 SQL Server 2017 開始。 **MicrosoftML**的 Linux 支援是[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)的新功能。

## <a name="package-dependencies"></a>封裝相依性

**MicrosoftML**中的演算法相依于的[RevoScaleR](ref-r-revoscaler.md) :

+ 資料來源物件。 **MicrosoftML**函數所使用的資料是使用**RevoScaleR**函數所建立。
+ 遠端計算 (將函式執行切換至遠端 SQL Server 實例)。 **RevoScaleR**程式庫提供用來建立及啟用 SQL server 遠端計算內容的功能。

在大部分情況下, 當您使用**MicrosoftML**時, 您會將封裝一起載入。

## <a name="functions-by-category"></a>依類別分類的函數

本節依類別列出函式, 讓您瞭解如何使用每一種功能。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)來依字母順序尋找函數。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-機器學習演算法

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank 的實行, 這是一種有效率的超市漸層提升演算法的執行。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 使用[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)的隨機樹系和分量迴歸樹系執行。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 使用 L BFGS 羅吉斯回歸。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 一個類別支援向量機器。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 二進位、多類別和回歸類神經網路。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 隨機線性二元分類和回歸的雙重座標上升優化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 將各種不同種類的模型定型, 以取得比從單一模型取得更佳的預測效能。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-轉換函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 轉換, 以從多個資料行建立單一向量值資料行。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 使用具有字典的類別轉換來建立指標向量。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 藉由雜湊將類別值轉換成指標陣列。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 從指定的文字主體, 產生一系列連續單字的計數, 稱為 n 字母。 它提供語言偵測、token 化、停用字詞移除、文字正規化和功能產生。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 將自然語言文字評分, 並建立一個資料行, 其中包含文字中的情緒為正數的機率。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 可定義以計數為基礎和以雜湊為基礎的功能解壓縮的引數。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 選取一組要重新定型的資料行, 捨棄所有其他資料行。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 使用指定的模式, 從指定的變數中選取特徵。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 載入影像資料。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 使用指定的調整大小方法, 將影像大小調整為指定的維度。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 從影像中解壓縮圖元值。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 使用預先定型的深度類神經網路模型來會將影像。|


## <a name="3-scoring-and-training-functions"></a>3-評分和定型函數

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 從 SQL Server、使用預存程式, 或從 R 程式碼執行計分程式庫, 以提供更快的預測效能。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 將輸入資料集的資料轉換成輸出資料集。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | 提供 Microsoft R Machine Learning 模型的摘要。|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-分類和回歸的遺失函數

| 函數名稱 | 描述 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指數分類損失功能的規格。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 記錄分類遺失功能的規格。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 轉軸分類遺失功能的規格。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平滑轉軸分類損失功能的規格。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 波氏回歸損失函數的規格。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平方回歸損失函數的規格。   |   

## <a name="5-feature-selection-functions"></a>5-特徵選取函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | [計數] 模式中的特徵選取規格。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 相互資訊模式中特徵選取的規格。 |

## <a name="6-ensemble-modeling-functions"></a>6-集團模型化函數

| 函數名稱 | 描述 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 建立包含函式名稱和引數的清單, 以使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)訓練快速樹狀模型。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 建立包含函式名稱和引數的清單, 以使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)訓練快速樹系模型。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 建立包含函式名稱和引數的清單, 以使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)訓練快速線性模型。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 建立包含函式名稱和引數的清單, 以使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)訓練羅吉斯回歸模型。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 建立包含函式名稱和引數的清單, 以便使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)來定型 OneClassSvm 模型。|

## <a name="7-neural-networking-functions"></a>7-類神經網路功能

| 函數名稱 | 描述 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 指定[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)機器學習演算法的優化演算法。|


## <a name="8-package-state-functions"></a>8-封裝狀態函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 用來儲存全封裝狀態的環境物件。 |


## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

**MicrosoftML**中的函式可在封裝于預存程式中的 R 程式碼中呼叫。 大部分的開發人員會在本機建立**MicrosoftML**解決方案, 然後將完成的 R 程式碼遷移至預存程式作為部署練習。

適用于 R 的**MicrosoftML**套件會在 SQL Server 2017 中安裝為「現成」。 如果您升級實例的 R 元件, 它也可以搭配 SQL Server 2016 使用:[使用系結升級 SQL Server 的實例](../install/upgrade-r-and-python.md)

預設不會載入封裝。 第一個步驟是載入**MicrosoftML**封裝, 然後載入**RevoScaleR** (如果您需要使用遠端計算內容或相關的連線性或資料來源物件)。 然後, 參考您需要的個別函式。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [瞭解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用于 SQL 開發人員的 R:定型和讓模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 