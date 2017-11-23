---
title: "搭配 SQL Server 使用 MicrosoftML 封裝 |Microsoft 文件"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: "132"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d4e4081ba4722f2c7aa468cf70f3a3238d6e9ee
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>搭配 SQL Server 使用 MicrosoftML 封裝

[ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction)套件會提供 Microsoft R Server 與 SQL Server 2017 包含多個機器學習演算法。 這些 Api 為內部的機器學習服務應用程式，由 Microsoft 所開發，而且已調整過數年來支援高效能巨量資料，使用多核心的處理和快速的資料流。 MicrosoftML 也包含許多轉換文字和映像處理。

在 SQL Server 2017 CTP 2.0 中，已加入之 Python 語言的支援。 **Microsoftml** Python 包含函式相當於 MicrosoftML 封裝中的 r 封裝 

+ **MicrosoftML**

    簡介與封裝的參考： [MicrosoftML： 機器學習 R 演算法](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    因為 R 會區分大小寫，請確定您先正確參考名稱載入封裝時。

+ **python microsoftml**

    簡介與封裝的參考： [microsoftml （函式程式庫 Python）](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。 

## <a name="whats-in-microsoftml"></a>什麼是 MicrosoftML 中

MicrosoftML 包含各種不同的機器學習演算法和都已針對效能最佳化的轉換。

### <a name="machine-learning-algorithms"></a>機器學習演算法

-  線性模型：`rxFastLinear`線性學習者根據隨機雙重座標 （堆疊） 可以用於二元分類或迴歸。 此模型支援 L1 和 L2 正規化。

- 決策樹狀結構和決策樹系模型：`rxFastTree`是原先稱為 FastRank，以便用於 Bing 所開發的促進式的決策樹演算法。 它是最快且最受歡迎的學習工具之一。 支援二進位的分類和迴歸。

  `rxFastForest`羅吉斯迴歸模型根據隨機樹系方法。 類似於 RevoScaleR 中的 `rxLogit` 函數，但支援 L1 和 L2 正規化。 支援二進位的分類和迴歸。

- 羅吉斯迴歸：`rxLogisticRegression`是羅吉斯迴歸模型類似於`rxLogit`RevoScaleR，在函式的 L1 與 L2 正則化的額外支援。 支援二進位或多級分類。

- 類神經網路：`rxNeuralNet`函式支援二元分類、 多級分類，以及使用類神經網路迴歸。 GPU 加速功能，使用單一的 GPU 的可自訂，並支援迂迴的網路。

- 異常偵測。  `rxOneClassSvm`函式 SVM 方法為基礎，但最適合用於二元分類不對稱的資料集。

### <a name="transformation-functions"></a>轉換函數

MicrosoftML 包含許多可用於將資料轉換，和擷取功能的特殊函式。

- 文字處理功能包括`featurizeText`和`getSentiment`函式。 您可以計算 n 字母組、 偵測所用的語言或執行文字正規化。 您也可以執行清除作業，例如停用字詞移除一般文字，或從文字產生雜湊，或按一下 以計數為基礎的功能。

- 特徵選取和功能轉換函式，例如`selectFeatures`或`getSentiment`、 分析資料，以及建立模型最有用的功能。

- 使用類別變數則會使用像是`categorical`或`categoricalHash`，它將類別值轉換成索引陣列以進行更好的效能。

- 特定的映像處理和分析，這類函數`extractPixels`或`featurizeImage`，讓您取得最多資訊的影像，並更快速地處理映像。

如需詳細資訊，請參閱 [MicrosoftML 函數 (英文)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。

## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

本節說明如何尋找並載入您的 R，並將 Python 程式碼中的封裝。

+ 根據預設，使用 Microsoft R Server 9.1.0 並在 SQL Server 2017 安裝 MicrosoftML 封裝。

    也會提供用於 SQL Server 2016 中，如果您升級 R 元件的執行個體，Microsoft R Server 安裝程式所述方式使用這裡：[升級 SQL Server 使用的繫結的執行個體](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ **Microsoftml** Python 會根據預設，使用 SQL Server 2017 安裝封裝 

   若要使用此套件，我們建議您升級至候選版 2 或更新版本。 較早版本隨附於 RC1 但程式庫已經過相當大的修訂，包括對函式名稱的變更。 

不過，如 R 和 Python，不載入封裝預設;因此，您必須做為程式碼以使用其函式的一部分明確載入封裝。

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>從 SQL Server 中的 R 呼叫 MicrosoftML 函式

在 R 程式碼載入 MicrosoftML 封裝並呼叫其函式，像任何其他套件。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**注意**

+ MicrosoftML 封裝完全整合在一起的 RevoScaleR 封裝所提供的資料處理管線。 因此，您可以使用 MicrosoftML 封裝在任何 Windows 為基礎的計算內容中，包括已啟用的機器學習擴充功能的 SQL Server 執行個體。

    不過，MicrosoftML 需要參考 RevoScaleR 和它的函式，才能使用遠端計算內容。

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>從 SQL Server 中的 Python 呼叫 microsoftml 函式

若要從封裝，Python 程式碼中呼叫函式匯入**microsoftml**封裝，並匯入**revoscalepy**如果您要使用遠端計算內容或相關的連接或資料來源物件。 請參考您需要個別的函式。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**注意**

+ 在 SQL Server 2017， **microsoftml** Python35 相容的模組。 

+ 中的函式**microsoftml**整合在一起所支援的計算內容和資料來源**revoscalepy**。 因此，您可以使用**microsoftml** Python 封裝，建立並從任何 windows 運算環境，包括了機器學習服務延伸模組的 SQL Server 執行個體中的模型評分。 啟用。

    不過， **microsoftml**進行 Python，您需要的參考**revoscalepy**和其函式，才能使用遠端計算內容。

如需 revoscalepy 的詳細資訊，請參閱：

+ [什麼是 revoscalepy](python/what-is-revoscalepy.md)

+ [revoscalepy 函式程式庫](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
