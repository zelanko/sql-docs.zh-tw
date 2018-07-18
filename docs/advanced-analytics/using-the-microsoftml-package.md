---
title: 使用 MicrosoftML 封裝與 SQL Server |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 51ffa33bef7ab880704c9c1391a69feb3e194202
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984560"
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>使用 MicrosoftML 封裝與 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction)隨附 Microsoft R Server 和 SQL Server 2017 的套件包含多個機器學習演算法。 這些 Api 的內部的機器學習服務應用程式，由 Microsoft 所開發，並提出看法多年來支援高效能巨量資料，使用多核心處理和快速資料流。 MicrosoftML 也包含文字和映像處理的許多轉換。

在 SQL Server 2017 CTP 2.0 中已新增 Python 語言的支援。 **Microsoftml** Python 函式相當於 MicrosoftML 套件中包含 r 封裝 

+ **MicrosoftML for R**

    簡介和套件的參考： [MicrosoftML： 機器學習服務 R 演算法](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    因為 R 有區分大小寫，請確定您先正確參考名稱載入封裝時。

+ **適用於 Python 的 microsoftml**

    簡介和套件的參考： [microsoftml （適用於 Python 的函式程式庫）](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。 

## <a name="whats-in-microsoftml"></a>什麼是 MicrosoftML 中

MicrosoftML 包含各種不同的機器學習服務演算法已針對效能最佳化的轉換。

### <a name="machine-learning-algorithms"></a>機器學習服務演算法

-  線性模型：`rxFastLinear`線性學習根據可用於二元分類或迴歸的隨機雙座標堆疊。 此模型支援 L1 和 L2 正規化。

- 決策樹及決策樹系模型：`rxFastTree`是原先稱為 FastRank 開發使用 Bing 中的促進式的決策樹演算法。 它是最快且最受歡迎的學習工具之一。 支援二進位的分類和迴歸。

  `rxFastForest` 羅吉斯迴歸模型為基礎的隨機樹系的方法。 類似於 RevoScaleR 中的 `rxLogit` 函數，但支援 L1 和 L2 正規化。 支援二進位的分類和迴歸。

- 羅吉斯迴歸：`rxLogisticRegression`是羅吉斯迴歸模型類似於`rxLogit`RevoScaleR 中的函式，並另外支援 L1 和 L2 正規化。 支援二進位或多級分類。

- 類神經網路：`rxNeuralNet`函式支援二元分類、 多級分類，以及使用類神經網路迴歸。 可自訂且支援 GPU 加速功能，使用單一 GPU 的迂迴的網路。

- 異常偵測。  `rxOneClassSvm`函式以 SVM 方法為基礎，但適用於不對稱資料集的二元分類。

### <a name="transformation-functions"></a>轉換函數

MicrosoftML 包含許多可用於轉換資料和擷取功能的特製化函式。

- 文字處理功能包括`featurizeText`和`getSentiment`函式。 您可以計算 n-gram、 偵測所用的語言或執行文字正規化。 您也可以執行清除作業，例如停用字詞移除的一般文字，或從文字產生雜湊，或按一下 以計數為基礎的功能。

- 特徵選取和功能轉換函式，例如`selectFeatures`或`getSentiment`、 分析資料，並建立最適合用於模型化的功能。

- 搭配類別變數使用像是`categorical`或`categoricalHash`，它將類別值轉換成索引的陣列，以提升效能。

- 這類特定的映像處理和分析的函數`extractPixels`或`featurizeImage`，可讓您取得最多資訊的映像，並更快速地處理映像。

如需詳細資訊，請參閱 [MicrosoftML 函數 (英文)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。

## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

本節說明如何尋找並載入您的 R 和 Python 程式碼中的封裝。

+ R 的 MicrosoftML 套件會安裝 Microsoft R Server 9.1.0 與 SQL Server 2017 中的預設值。

    也會提供用於 SQL Server 2016 中，如果您升級的 R 元件的執行個體，如所述這裡使用 Microsoft R Server 安裝程式：[使用繫結的 SQL Server 執行個體進行升級](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ **Microsoftml**預設 SQL Server 2017 安裝 Python 封裝 

   若要使用此套件，我們建議您升級為 Release Candidate 2 或更新版本。 較早版本隨附 RC1，但程式庫已經過相當大的修訂，包括函式名稱的變更。 

不過，對 R 和 Python 中，不載入封裝的預設值;因此，您必須為您的程式碼，以使用其功能的一部分明確載入封裝。

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>從 SQL Server 中的 R 呼叫 MicrosoftML 函式

R 程式碼中載入 MicrosoftML 套件，並呼叫其功能，像是任何其他套件。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**注意**

+ MicrosoftML 封裝與 RevoScaleR 封裝所提供的資料處理管線完全整合。 因此，您可以使用 MicrosoftML 封裝在任何 Windows 為基礎的計算內容，包括已啟用的機器學習服務擴充功能的 SQL Server 的執行個體中。

    不過，MicrosoftML 需要參考 RevoScaleR 和函式才能使用遠端計算內容。

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>從 SQL Server 中的 Python 呼叫 microsoftml 函式

若要從封裝，請在您的 Python 程式碼，呼叫函式匯入**microsoftml**套件，並匯入**revoscalepy**如果您要使用遠端計算內容或相關的連線或資料來源物件。 然後，參考您需要個別的函式。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**注意**

+ 在 SQL Server 2017 **microsoftml**是 Python35 相容模組。 

+ 中的函式**microsoftml**整合在一起所支援的計算內容和資料來源**revoscalepy**。 因此，您可以使用**microsoftml** Python 套件建立，並從任何以 Windows 為基礎的計算內容，其中包括了機器學習服務延伸模組的 SQL Server 的執行個體中的模型評分。 已啟用。

    不過， **microsoftml** for Python 需要參考**revoscalepy**和其功能，才能使用遠端計算內容。

如需 revoscalepy 的詳細資訊，請參閱：

+ [Revoscalepy 是什麼](python/what-is-revoscalepy.md)

+ [revoscalepy 函式程式庫](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
