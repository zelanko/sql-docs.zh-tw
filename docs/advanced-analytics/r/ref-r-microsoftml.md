---
title: MicrosoftML R 函式程式庫-SQL Server Machine Learning 服務
description: 在 SQL Server 2016 R Services 和 SQL Server 2017 Machine Learning 服務與 r 的 MicrosoftML 函式程式庫簡介
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 73d9dcf56c0eb5e69704adf169946f6aa28a432c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512255"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML （SQL Server 中的 R 程式庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML**是 microsoft 提供高效能的機器學習演算法的 R 函式程式庫。 它包含訓練和轉換、 評分、 文字和影像分析和功能擷取，衍生自現有資料的值的函式。

機器學習 Api 內部的機器學習應用程式，由 Microsoft 所開發，並提出看法多年來支援高效能巨量資料，使用多核心處理和快速資料流。 MicrosoftML 也包含文字和映像處理的許多轉換。

## <a name="full-reference-documentation"></a>完整的參考文件

**MicrosoftML**程式庫會分散在多個 Microsoft 產品中，但不論您取得 SQL Server 或另一個產品中的程式庫使用方式都相同。 函式是相同的因為[個別 RevoScaleR 函式文件](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)發行到下一個位置[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 應該任何產品專屬行為存在時，差異會記錄在函式說明頁面。

## <a name="versions-and-platforms"></a>版本與平台

**MicrosoftML**程式庫是依據 R 3.4.3 以及是否可以使用只有當您安裝其中一個下列的 Microsoft 產品或下載項目時：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 完整的產品版本是 Windows 專屬，從 SQL Server 2017 開始。 Linux 支援**MicrosoftML**的新功能[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="package-dependencies"></a>封裝相依性

中的演算法**MicrosoftML**依賴[RevoScaleR](ref-r-revoscaler.md)的：

+ 資料來源物件。 資料供**MicrosoftML**函式會建立使用**RevoScaleR**函式。
+ 遠端運算 （變動函式執行遠端 SQL Server 執行個體）。 **RevoScaleR**程式庫提供的函式，建立和啟用遠端計算內容適用於 SQL server。

在大部分情況下，您將載入封裝在一起每當您使用**MicrosoftML**。

## <a name="functions-by-category"></a>依類別目錄的函式

此區段會列出依類別目錄，讓您了解如何使用每個函式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)依字母順序尋找函式。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-機器學習服務演算法

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank，MART 梯度促進式演算法的有效實作的實作。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 隨機樹系和分量迴歸樹系實作使用[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 使用左 BFGS 的羅吉斯迴歸。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 一級支援向量機器。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 二進位檔、 多類別和迴歸類神經網路。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 線性的二進位分類和迴歸的隨機雙座標堆疊最佳化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 定型模型，以取得更好預測的效能比無法從單一模型中取得的各種類型的的數目。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-轉換函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 若要從多個資料行建立單一向量值的資料行的轉換。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 建立使用字典中的類別轉換指標向量。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 將類別值轉換成指標陣列中，進行雜湊處理。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 會產生計數的連續呼叫 n-grams、 從文字指定主體的單字序列的封包。 它提供語言偵測、 token 化、 移除停用字詞、 文字正規化和產生功能。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 分數的自然語言文字，並建立包含在文字情感是正面的機率的資料行。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 可定義引數來擷取計數和雜湊為基礎的特徵。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 選取一組資料行重新定型，卸除其他所有人。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 從指定的變數，使用指定的模式中，選取功能。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 載入影像資料。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 調整大小的影像到指定的維度，使用指定的調整大小方法。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 從映像擷取的像素值。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 開始使用預先定型的深度類神經網路模型的映像。|


## <a name="3-scoring-and-training-functions"></a>3-評分和訓練函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 從 SQL Server 中，使用預存程序中，或是從啟用即時評分，以提供更快速的預測效能的 R 程式碼，請執行評分的文件庫。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 轉換至輸出資料集的資料從輸入資料集。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | 提供 Microsoft R 機器學習服務模型的摘要。|


## <a name="4-loss-functions-for-classification-and-regression"></a>分類和迴歸的 4 損失函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指數分類損失函式的規格。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 記錄檔分類損失函式的規格。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 關鍵分類損失函式的規格。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Smooth 關鍵分類損失函式的規格。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 波氏迴歸損失函式的規格。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平方迴歸損失函式的規格。   |   

## <a name="5-feature-selection-functions"></a>5-特徵選取的函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 計數模式的特徵選取的規格。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 相互資訊模式中的特徵選取的規格。 |

## <a name="6-ensemble-modeling-functions"></a>6-集團模型化函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 建立包含使用快速的樹狀結構模型定型的引數與函式名稱的清單[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 建立包含訓練與快速樹系模型的引數與函式名稱的清單[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 建立包含訓練與快速線性模型的引數與函式名稱的清單[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 建立包含定型羅吉斯迴歸模型使用的引數與函式名稱的清單[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 建立包含定型 OneClassSvm 模型使用的引數與函式名稱的清單[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|

## <a name="7-neural-networking-functions"></a>7 類神經網路的函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 指定最佳化演算法[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)機器學習演算法。|


## <a name="8-package-state-functions"></a>8-套件狀態函式

| 函數名稱 | 描述 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 環境物件，用來儲存整個套件的狀態。 |


## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

中的函式**MicrosoftML**封裝在預存程序中的 R 程式碼中呼叫。 大部分的開發人員建置**MicrosoftML**解決方案在本機，然後將完成的 R 程式碼移轉到預存程序中，部署練習變更。

**MicrosoftML** R 是已安裝 「--現成的 「 SQL Server 2017 中的封裝。 如果您升級執行個體的 R 元件，它是也適用於 SQL Server 2016:[使用繫結的 SQL Server 執行個體進行升級](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

預設不會載入封裝。 第一個步驟中，載入**MicrosoftML**套件，並接著載入**RevoScaleR**如果您要使用遠端計算內容或相關的連線或資料來源物件。 然後，參考您需要個別的函式。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>另請參閱

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [適用於 SQL 開發人員的 R:訓練和運作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [在 GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 