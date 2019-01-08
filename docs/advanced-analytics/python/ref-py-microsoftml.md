---
title: microsoftml Python 封裝-SQL Server Machine Learning 服務
description: 介紹 Microsoft 的機器學習演算法，並針對 Python，模型與 SQL Server 機器學習工作負載相關。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b892af192be2cea441004adca8e9297f1947b313
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645093"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml （SQL Server 中的 Python 模組）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml**是 microsoft 提供高效能的機器學習服務演算法 Python35 相容模組。 它包含訓練和轉換、 評分、 文字和影像分析和功能擷取，衍生自現有資料的值的函式。

機器學習服務 Api 的內部的機器學習應用程式由 Microsoft 所開發，並提出看法多年來支援高效能巨量資料，使用多核心處理和快速資料流。 產生的 R 版本，Python 對應項目為此套件[MicrosoftML](../r/ref-r-microsoftml.md)，具有類似的函式。 

## <a name="full-reference-documentation"></a>完整的參考文件

**Microsoftml**程式庫會分散在多個 Microsoft 產品中，但不論您取得 SQL Server 或另一個產品中的程式庫使用方式都相同。 函式是相同的因為[個別 microsoftml 函式文件](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)發行到下一個位置[Python 參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)的 Microsoft Machine Learning Server。 應該任何產品專屬行為存在時，差異會記錄在函式說明頁面。

## <a name="versions-and-platforms"></a>版本與平台

**Microsoftml**模組是根據 Python 3.5 和可用只有當您安裝其中一個下列的 Microsoft 產品或下載項目時：

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整的產品版本是 Windows 專屬，從 SQL Server 2017 開始。 Linux 支援**microsoftml**的新功能[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="package-dependencies"></a>封裝相依性

中的演算法**microsoftml**依賴[revoscalepy](ref-py-revoscalepy.md)的：

+ 資料來源物件。 資料供**microsoftml**函式會建立使用**revoscalepy**函式。
+ 遠端運算 （變動函式執行遠端 SQL Server 執行個體）。 **Revoscalepy**程式庫提供的函式，建立和啟用遠端計算內容適用於 SQL server。

在大部分情況下，您將載入封裝在一起每當您使用**microsoftml**。

## <a name="functions-by-category"></a>依類別目錄的函式

此區段會列出依類別目錄，讓您了解如何使用每個函式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)依字母順序尋找函式。

## <a name="1-training-functions"></a>1-訓練函式

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 訓練一整團的模型。 |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 隨機樹系。 |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 線性模型。 使用隨機的雙座標堆疊。 |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 推進式決策的樹。 |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 羅吉斯迴歸。 |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 類神經網路。 |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 異常偵測。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-轉換函式

### <a name="categorical-variable-handling"></a>類別變數的處理

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 將文字資料行轉換成類別目錄。 |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 雜湊，並將文字資料行轉換成類別目錄。 |

### <a name="schema-manipulation"></a>結構描述管理

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 將多個資料行串連成單一的向量。 |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 從資料集，卸除資料行。 |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 會保留資料集的資料行。 |


### <a name="variable-selection"></a>變數選取

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |計數為基礎的特徵選取。 |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 相互資訊為基礎的特徵選取。 |


### <a name="text-analytics"></a>文字分析

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 將文字資料行轉換成數值特徵。 |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 情感分析。 |


### <a name="image-analytics"></a>影像分析 

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 載入影像。 |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 調整影像的大小。 |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 擷取映像素為單位。 |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 您可以將映像轉換功能。 |

### <a name="featurization-functions"></a>特徵化函式

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 資料來源的資料轉換 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3 評分函式

| 函數 | 描述 |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | 使用 Microsoft machine learning 模型的分數 |

## <a name="how-to-call-microsoftml"></a>如何呼叫 microsoftml

中的函式**microsoftml**封裝在預存程序中的 Python 程式碼中呼叫。 大部分的開發人員建置**microsoftml**解決方案在本機，然後將完成的 Python 程式碼移轉到預存程序中，部署練習變更。

**Microsoftml**根據預設，但不同於安裝 Python 封裝**revoscalepy**，當您開始使用 Python 可執行檔與 SQL Server 一起安裝的 Python 工作階段時，它不會預設載入。

第一個步驟中，匯入**microsoftml**套件，並匯入**revoscalepy**如果您要使用遠端計算內容或相關的連線或資料來源物件。 然後，參考您需要個別的函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)
+ [教學課程：內嵌在 T-SQL 中的 Python 程式碼](../tutorials/run-python-using-t-sql.md)
+ [Python 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

