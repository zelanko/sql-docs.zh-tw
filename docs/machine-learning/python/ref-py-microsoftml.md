---
title: microsoftml Python 套件
description: microsoftml 為 Microsoft 的 Python 套件，提供高效能的機器學習演算法。 它包含用於定型與轉換、評分、文字與影像分析的函式，以及用於從現有資料衍生值的特徵擷取。 該套件包含在 SQL Server 機器學習服務中。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15'
ms.openlocfilehash: ec421e1b0e112a535e3caa59cf83e01c4e02086c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470939"
---
# <a name="microsoftml-python-package-in-sql-server-machine-learning-services"></a>microsoftml (SQL Server 機器學習服務中的 Python 套件)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**microsoftml** 為 Microsoft 的 Python 套件，提供高效能的機器學習演算法。 它包含用於定型與轉換、評分、文字與影像分析的函式，以及用於從現有資料衍生值的特徵擷取。 該套件包含在 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)中，並支援高效能巨量資料，同時使用多核心處理，以及快速的資料串流。

## <a name="full-reference-documentation"></a>完整參考文件

**microsoftml** 套件分散在多個 Microsoft 產品中，但不論您是從 SQL Server 或其他產品中取得該套件，使用方式都相同。 由於函式相同，因此[個別 microsoftml 函式的文件](/machine-learning-server/python-reference/microsoftml/microsoftml-package)只發佈至 Microsoft Machine Learning Server 之 [Python 參考](/machine-learning-server/python-reference/introducing-python-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

## <a name="versions-and-platforms"></a>版本與平台

**microsoftml** 模組以 Python 3.5 為基礎，且只有當您安裝下列其中一個Microsoft 產品或下載項目時才會提供：

+ [SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](/machine-learning-server/)
+ [適用於資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 在 SQL Server 2017 中，完整產品發行版本僅適用於 Windows。 在 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) 中，**microsoftml** 則同時支援 Windows 和 Linux。

## <a name="package-dependencies"></a>套件相依性

**microsoftml** 中的演算法在下列方面倚賴 [revoscalepy](ref-py-revoscalepy.md)：

+ 資料來源物件。 **microsoftml** 函式所取用的資料是使用 **revoscalepy** 函式來建立的資料。
+ 遠端計算 (將函式執行切換至遠端 SQL Server 執行個體)。 **revoscalepy** 套件提供建立與啟用 SQL Server 遠端計算內容的函數。

在大多數情況下，您會在每次使用 **microsoftml** 時一起載入套件。

## <a name="functions-by-category"></a>依類別區分的函式

本節依類別列出函式，讓您了解每個函式的使用方式。 您也可以使用[目錄](/machine-learning-server/python-reference/introducing-python-package-reference)來依字母順序尋找函式。

## <a name="1-training-functions"></a>1-定型函式

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.rx_ensemble](/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 將一整團模型定型。 |
|[microsoftml.rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 隨機樹系。 |
|[microsoftml.rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 線性模型。 具有推測雙座標堆疊。 |
|[microsoftml.rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 強化樹。 |
|[microsoftml.rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 羅吉斯迴歸。 |
|[microsoftml.rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 類神經網路。 |
|[microsoftml.rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 異常偵測。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-轉換函式

### <a name="categorical-variable-handling"></a>類別目錄變數處理

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.categorical](/machine-learning-server/python-reference/microsoftml/categorical) | 將文字資料行轉換成類別。 |
|[microsoftml.categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash) | 將文字資料行雜湊並轉換成類別。 |

### <a name="schema-manipulation"></a>結構描述操作

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.concat](/machine-learning-server/python-reference/microsoftml/concat) | 將多個資料行串連成單一向量。 |
|[microsoftml.drop_columns](/machine-learning-server/python-reference/microsoftml/drop-columns) | 置放來自資料集的資料行。 |
|[microsoftml.select_columns](/machine-learning-server/python-reference/microsoftml/select-columns) | 保留資料集的資料行。 |


### <a name="variable-selection"></a>變數選取

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.count_select](/machine-learning-server/python-reference/microsoftml/count-select) |以計數為基礎的特徵選取。 |
|[microsoftml.mutualinformation_select](/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 以相互資訊為基礎的特徵選取。 |


### <a name="text-analytics"></a>文字分析

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text) | 將文字資料行轉換成數值特徵。 |
|[microsoftml.get_sentiment](/machine-learning-server/python-reference/microsoftml/get-sentiment) | 情感分析。 |


### <a name="image-analytics"></a>影像分析 

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.load_image](/machine-learning-server/python-reference/microsoftml/load-image) | 載入影像。 |
|[microsoftml.resize_image](/machine-learning-server/python-reference/microsoftml/resize-image) | 調整影像的大小。 |
|[microsoftml.extract_pixels](/machine-learning-server/python-reference/microsoftml/extract-pixels) | 從影像中擷取像素。 |
|[microsoftml.featurize_image](/machine-learning-server/python-reference/microsoftml/featurize-image) | 將影像轉換成特徵。 |

### <a name="featurization-functions"></a>特徵化函式

| 函式 | 說明 |
|----------|-------------|
|[microsoftml.rx_featurize](/machine-learning-server/python-reference/microsoftml/rx-featurize) | 資料來源的資料轉換 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-評分函式

| 函式 | 描述 |
|----------|-------------|
|[microsoftml.rx_predict](/machine-learning-server/python-reference/microsoftml/rx-predict) | 使用 Microsoft 機器學習模型進行評分 |

## <a name="how-to-call-microsoftml"></a>如何呼叫 microsoftml

封裝在預存程序中的 Python 程式碼可呼叫 **microsoftml** 中的函式。 大多數開發人員會在本機建置 **microsoftml** 解決方案，然後將完成的 Python 程式碼移轉至預存程序作為部署練習。

適用於 Python 的 **microsoftml** 套件是預設的安裝項目，但與 **revoscalepy** 不同，當您使用與 SQL Server 一起安裝的 Python 可執行檔來啟動 Python 工作階段時，預設並不會載入此套件。

作為第一步，請載入 **microsoftml** 套件，然後如果您需要使用遠端計算內容、相關連線能力或資料來源物件，則載入 **revoscalepy**。 接著，參考您需要的個別函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/python-tutorials.md)
+ [Python 參考 (Microsoft Machine Learning Server)](/machine-learning-server/python-reference/introducing-python-package-reference) \(英文\)