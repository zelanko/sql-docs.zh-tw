---
title: microsoftml Python 套件
description: 介紹適用于 Python 的 Microsoft 機器學習演算法和模型, 與 SQL Server 機器學習服務工作負載相關。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 298328db563cac8183b14b47e5c75c850c782d58
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345459"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (SQL Server 中的 Python 模組)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml**是 Microsoft 的 Python35 相容模組, 可提供高效能的機器學習服務演算法。 其中包含用於定型和轉換的函式、評分、文字和影像分析, 以及從現有資料衍生值的功能解壓縮。

機器學習服務 Api 是由 Microsoft 針對內部機器學習應用程式所開發, 並已在多年來進行微調, 以支援大型資料的高效能, 使用多核心處理和快速資料串流。 此套件是以相當於 R 版本[MicrosoftML](../r/ref-r-microsoftml.md)(具有類似功能) 的 Python 來產生。 

## <a name="full-reference-documentation"></a>完整參考檔

**Microsoftml**程式庫是散發在多個 Microsoft 產品中, 但不論您是在 SQL Server 或其他產品中取得程式庫, 使用方式都相同。 因為函式相同, 所以[個別 microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)函式的檔集只會發佈到 Microsoft Machine Learning Server 的[Python 參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)底下的一個位置。 若有任何產品特定行為存在, 則函式說明頁面中會注明不一致的情況。

## <a name="versions-and-platforms"></a>版本和平臺

**Microsoftml**模組是以 Python 3.5 為基礎, 只有在您安裝下列其中一個 Microsoft 產品或下載時, 才能使用:

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [適用于資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整產品發行版本僅限 Windows, 從 SQL Server 2017 開始。 **Microsoftml**的 Linux 支援是[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)的新功能。

## <a name="package-dependencies"></a>封裝相依性

**Microsoftml**中的演算法相依于的[revoscalepy](ref-py-revoscalepy.md) :

+ 資料來源物件。 **Microsoftml**函數所使用的資料是使用**revoscalepy**函數所建立。
+ 遠端計算 (將函式執行切換至遠端 SQL Server 實例)。 **Revoscalepy**程式庫提供用來建立及啟用 SQL server 遠端計算內容的功能。

在大部分情況下, 當您使用**microsoftml**時, 您會將封裝一起載入。

## <a name="functions-by-category"></a>依類別分類的函數

本節依類別列出函式, 讓您瞭解如何使用每一種功能。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)來依字母順序尋找函數。

## <a name="1-training-functions"></a>1-訓練函式

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 定型模型的集團。 |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 隨機樹系。 |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 線性模型。 具有隨機雙重座標上升。 |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 提升樹狀結構。 |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 羅吉斯回歸。 |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 類神經網路。 |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 異常偵測。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-轉換函式

### <a name="categorical-variable-handling"></a>類別變數處理

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 將文字資料行轉換成類別目錄。 |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 雜湊並將文字資料行轉換成類別目錄。 |

### <a name="schema-manipulation"></a>架構操作

| 功能 | 說明 |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 將多個資料行串連成單一向量。 |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 從資料集卸載資料行。 |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 保留資料集的資料行。 |


### <a name="variable-selection"></a>變數選取

| 功能 | 說明 |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |以計數為基礎的特徵選取。 |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 以相互資訊為基礎的特徵選取。 |


### <a name="text-analytics"></a>文字分析

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 將文字資料行轉換成數值特徵。 |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 情感分析。 |


### <a name="image-analytics"></a>影像分析 

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 載入影像。 |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 調整影像大小。 |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 從影像中抽取圖元。 |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 將影像轉換成特徵。 |

### <a name="featurization-functions"></a>特徵化函式

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 資料來源的資料轉換 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-評分函數

| 功能 | 描述 |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | 使用 Microsoft 機器學習模型的分數 |

## <a name="how-to-call-microsoftml"></a>如何呼叫 microsoftml

**Microsoftml**中的函式可在封裝于預存程式中的 Python 程式碼中呼叫。 大部分的開發人員會在本機建立**microsoftml**解決方案, 然後將完成的 Python 程式碼遷移至預存程式作為部署練習。

預設會安裝適用于 Python 的**microsoftml**套件, 但與**revoscalepy**不同的是, 當您使用隨 SQL Server 安裝的 python 可執行檔來啟動 python 會話時, 預設不會載入它。

第一個步驟是匯入**microsoftml**封裝, 如果您需要使用遠端計算內容或相關的連線性或資料來源物件, 請匯入**revoscalepy** 。 然後, 參考您需要的個別函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)
+ [教學課程：在 T-sql 中內嵌 Python 程式碼](../tutorials/run-python-using-t-sql.md)
+ [Python 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

