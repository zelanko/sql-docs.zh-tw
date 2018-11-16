---
title: 簡介 SQL Server Machine Learning 中的 revoscalepy Python 套件 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8b2e217f599112019e96f3e20b727456b9da607f
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697566"
---
# <a name="introducing-revoscalepy-in-sql-server-machine-learning"></a>簡介 SQL Server Machine Learning 中的 revoscalepy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy**是新的 Python 程式庫，提供由 Microsoft 支援分散式運算遠端計算內容及高效能演算法適用於 Python 開發人員。

它根據**RevoScaleR** R、 Microsoft R Server 和 SQL Server R Services，以及目標是提供相同的功能中所提供的套件：

+ 支援多個計算內容，遠端和本機
+ 提供給資料轉換和視覺效果等同於 RevoScaleR 中的函式
+ 針對分散式或平行處理提供 RevoScaleR 機器學習演算法的 Python 的版本
+ 提升的效能，包括 Intel 數學程式庫使用

MicrosoftML 套件也會提供對 R 和 Python。 如需詳細資訊，請參閱[使用 SQL Server 中的 MicrosoftML](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>版本和支援的平台

**Revoscalepy**模組是使用只有當您安裝的其中一個下列的 Microsoft 產品才：

+ 機器學習服務，在 SQL Server 2017
+ Microsoft Machine Learning Server 9.2.0 或更新版本

若要取得 revoscalepy 的最新版本，請安裝 Cumulative Update 1 for SQL Server 2017。 它包含許多增強功能，在 Python 中，包括：

+ 新的 Python 函式`rx_create_col_info`，會取得從 SQL Server 資料來源的結構描述資訊等[rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)的 
+ 增強[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支援平行處理的案例使用`RxLocalParallel`計算內容。 

## <a name="supported-functions-and-data-types"></a>支援的函式和資料類型

本節提供的 Python 資料類型和支援新的 Python 函式的概觀**revoscalepy**模組，從 SQL Server 2017 CTP 2.0 版開始。 

最新發行的 Python 程式庫中的函式的最新清單，請參閱下列連結：

+ [適用於 Python 的 revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [適用於 Python 的 microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>資料類型、 資料來源和計算內容

SQL Server 和 Python 使用不同的資料類型，在某些情況下。 如需 SQL 和 Python 的資料類型之間的對應，請參閱[Python 延伸模組](../concepts/extension-python.md)。

在 SQL Server 中使用 Python 的 machine learning 支援的資料來源包含 ODBC 資料來源、 SQL Server 資料庫，以及本機檔案，包括 XDF 檔案。

您可以使用下表所列的函式，以建立資料來源物件。 定義資料來源之後, 載入或轉換資料，利用適當[ETL 函式](#bkmk_etl)。

> [!IMPORTANT]
> 許多函式名稱已變更自 CTP 2.0 中的 Python 的初始版本。

**SQL Server 資料**

+ 使用[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)定義來自查詢或資料表的資料來源
+ 使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver)建立 SQL Server 計算內容
+ 使用[RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata)從 ODBC 連接建立資料來源

**revoscalepy**也支援[XDF 資料來源](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata)，用於記憶體和其他資料來源之間移動資料。

> [!TIP]
> 如果您不熟悉之資料來源的概念，或計算內容，我們建議您一開始先了解分散式運算的運作中的機器學習[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)。


### <a name="bkmk_algorithms"></a>機器學習服務和摘要的函式

在 SQL Server 2017 中，從 CTP 2.0 開始包含下列機器學習服務演算法和摘要 RevoScaleR 函式。

| 函數| 描述|注意|
| ------ | ------ |------ |
|`rx_btrees` | 符合隨機梯度促進式的決策樹|`rx_btrees_ex` 在 CTP 2.0|
|`rx_dforest` | 符合分類和迴歸的決策樹系|`rx_dforest_ex` 在 CTP 2.0|
|`rx_dtree` | 調整的分類和迴歸樹狀結構 |`rx_dtree_ex` 在 CTP 2.0|
|`rx_lin_mod` | 建立的線性模型|`rx_lin_mod_ex` 在 CTP 2.0|
|`rx_logit` | 建立羅吉斯迴歸模型|`rx_logit_ex` 在 CTP 2.0|
|`rx_predict` | 從定型的模型產生預測|`rx_predict_ex` 在 CTP 2.0|
|`rx_summary` | 產生模型的摘要||

新的機器學習服務演算法也會提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| 函數| 描述|
| ------ | ------ |
|`rx_fast_forest` |建立決策樹系模型|
|`rx_fast_linear` | 使用隨機的雙座標堆疊的線性迴歸|
|`rx_fast_trees` | 建立推進式決策的樹模型 |
|`rx_logistic_regression` | 建立羅吉斯迴歸模型|
|`rx_neural_network` | 建立可自訂的類神經網路模型 |
|`rx_oneclass_svm` | 上的不平衡的資料集，以用於異常偵測建立 SVM 模型|

> [!TIP]
> 許多這些演算法已提供 Azure Machine Learning 中的模組。

適用於 Python 的 MicrosoftML 也包含各種不同的轉換和協助程式函式，例如：

+ `rx_predict` 從定型的模型產生預測，而且可以用於即時評分
+ 影像特徵化函式
+ 文字處理和人氣擷取的函式

如需詳細資訊，請參閱[MicrosoftML 簡介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社群中，會使用可能會與您所用，包括所有小寫字母和底線，而非參數名稱的 camel 命名法大小寫不同的程式碼撰寫慣例。 此外，或許您已注意到**revoscalepy**程式庫一律為小寫。 沒錯 ！ 另一個 Python 慣例。
> 
> 查看 Microsoft: [Python 函式說明] 的 Python 參考文件的相關秘訣[Python 函式的說明](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>範例

您可以執行程式碼，其中包含**revoscalepy**函式在本機或遠端計算內容中。 您也可以藉由在預存程序中內嵌 Python 程式碼來執行 SQL server 中的 Python。

本機執行時，您通常在從命令列中，或從 Python 開發環境中，執行 Python 指令碼，並指定使用其中一種在 SQL Server 計算內容**revoscalepy**函式。 完整的程式碼，或個別的函式，您可以使用遠端計算內容。 例如，您可能要卸載至伺服器，以使用最新的資料，以避免資料移動的模型定型。

如果您想要將預存程序中，完整的 Python 指令碼放[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我們建議您在為具有清楚定義的輸入和輸出的單一函式重寫程式碼。 輸入和輸出必須是**pandas**資料框架。 時這麼做，您可以從任何用戶端，支援 T-SQL 呼叫預存程序，輕鬆做為輸入，將 SQL 查詢和結果儲存至 SQL 資料表。 如需範例，請參閱[適用於 SQL 開發人員的資料庫內 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-remote-compute-contexts"></a>使用遠端計算內容

+ [使用 revoscalepy 建立模型](../tutorials/use-python-revoscalepy-to-create-model.md)

  此範例示範如何執行 Python 當作計算內容中使用的 SQL Server 執行個體。

### <a name="using-a-stored-procedure"></a>使用預存程序

+ [使用 T-SQL 執行 Python](../tutorials/run-python-using-t-sql.md)

  此範例會示範呼叫預存程序中內嵌的 Python 指令碼的基本機制。

### <a name="using-revoscalepy-with-microsoftml"></a>使用 MicrosoftML 中的 revoscalepy

Python 函式，對於 MicrosoftML 整合在一起的計算內容和 revoscalepy 中提供的資料來源。 因此，您可以定義，並在 Python 中，將模型定型中使用 MicrosoftML 演算法，並且在本機或在 SQl Server 計算內容中執行 Python 程式碼中使用 revoscalepy 函式。

只需匯入 Python 程式碼中的模組，並接著參考您需要個別的函式。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>需求

若要在 SQL Server 中執行 Python 程式碼，您必須已安裝 SQL Server 2017 功能連同**Machine Learning 服務**，並啟用 Python 語言。 舊版的 SQL Server 不支援 Python 整合。

> [!NOTE]
> 開放原始碼散發套件的 Python 不支援 SQL Server 計算內容。 不過，如果您要發佈和取用從 Windows 的 Python 應用程式時，您可以安裝 Microsoft Machine Learning Server 而不需要安裝 SQL Server。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server 2017 Machine Learning Server （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)。

## <a name="get-more-help"></a>取得更多說明

在產品正式發行時，會提供這些 Api 的完整文件。 在此同時，我們建議您參考 RevoScaleR 或 MicrosoftML 程式庫中對應的函式。

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

您可以取得說明的任何 Python 函式匯入模組，然後再呼叫`help()`。 例如，執行`help(revoscalepy)`從您的 Python IDE 會傳回一份所有函式中的 revoscalepy 模組，其簽章。

如果您使用 Python Tools for Visual Studio 時，您可以使用 IntelliSense，以取得語法和引數的說明。 如需詳細資訊，請參閱 < [Visual Studio 中的 Python 支援](https://docs.microsoft.com/visualstudio/python/installation)，並下載符合您的 Visual Studio 版本的延伸模組。 您可以使用 Python 與 Visual Studio 2015 和 2017 年或更早版本。

## <a name="see-also"></a>另請參閱

[Python 教學課程](../tutorials/sql-server-python-tutorials.md)
