---
title: "簡介 revoscalepy |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: e7135947e2a8ed23b960575cae0689a77bcdd97d
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="introducing-revoscalepy"></a>介紹 revoscalepy

**revoscalepy**是新的程式庫，支援分散式運算環境的 microsoft 遠端計算內容中，與高效能演算法 for Python 提供。

它基礎**RevoScaleR** Microsoft R Server 和 SQL Server R 服務，以及其目的是提供相同的功能中提供的封裝：

+ 支援多個計算內容，遠端和本機
+ 提供相當於 RevoScaleR 函數來資料轉換和視覺效果
+ 分散式或平行處理提供 RevoScaleR 機器學習演算法的 Python 的版本
+ 提升的效能，包括 Intel 數學程式庫的使用情況

MicrosoftML 封裝也會提供 R 和 Python。 如需詳細資訊，請參閱[使用 MicrosoftML SQL Server 中](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>版本和支援的平台

**Revoscalepy**模組是使用只在您安裝時下列 Microsoft 產品的其中一個：

+ 機器學習服務，在 SQL Server 2017
+ Microsoft 的機器學習 Server 9.2.0 或更新版本

若要取得 revoscalepy 的最新版本，安裝 SQL Server 2017 累計更新 1。 它包含 Python，包括許多增強功能：

+ 新的 Python 函式， `rx_create_col_info`，來取得結構描述資訊，從 SQL Server 資料來源，例如[rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)的 
+ 若要增強功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)支援平行案例使用`RxLocalParallel`計算內容。 

## <a name="supported-functions-and-data-types"></a>支援的函式和資料類型

本節提供的 Python 資料類型與支援中新的 Python 函式概觀**revoscalepy**模組，從 SQL Server 2017 CTP 2.0 版本開始。 

最新發行的 Python 程式庫中的函式的最新清單，請參閱以下連結：

+ [python revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>資料型別、 資料來源和計算內容

SQL Server，並將 Python 某些情況下使用不同的資料類型。 如需 SQL 和 Python 資料類型之間的對應，請參閱[Python 程式庫和資料型別](python-libraries-and-data-types.md)。

支援使用 SQL Server 中的 Python 的機器學習的資料來源包含 ODBC 資料來源、 SQL Server 資料庫，以及本機檔案，包括 XDF 檔案。

您可以使用下表所列的函式，以建立資料來源物件。 定義資料來源之後, 載入或使用適當轉換資料[ETL 函式](#bkmk_etl)。

> [!IMPORTANT]
> 在 CTP 2.0 中的 Python 的初始版本之後，已變更許多函式名稱。

**SQL Server 資料**

+ 使用[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)定義來自查詢或資料表的資料來源
+ 使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver)建立 SQL Server 計算內容
+ 使用[RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata)從 ODBC 連接建立資料來源

**revoscalepy**也支援[XDF 資料來源](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata)，用於記憶體與其他資料來源之間移動資料。

> [!TIP]
> 如果您不熟悉資料來源的概念，或計算內容，我們建議您先在機器學習的分散式運算工作的相關的讀取[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)。


### <a name="bkmk_algorithms"></a>機器學習和彙總函數

下列機器學習演算法和彙總從 RevoScaleR 函數會包含在 SQL Server 2017，開頭 CTP 2.0 中。

| 函數| Description|注意|
| ------ | ------ |------ |
|`rx_btrees` | 符合隨機梯度促進式的決策樹|`rx_btrees_ex`在 CTP 2.0|
|`rx_dforest` | 符合分類和迴歸的決策樹系|`rx_dforest_ex`在 CTP 2.0|
|`rx_dtree` | 調整的分類和迴歸樹狀結構 |`rx_dtree_ex`在 CTP 2.0|
|`rx_lin_mod` | 建立線性模型|`rx_lin_mod_ex`在 CTP 2.0|
|`rx_logit` | 建立羅吉斯迴歸模型|`rx_logit_ex`在 CTP 2.0|
|`rx_predict` | 產生從定型模型的預測|`rx_predict_ex`在 CTP 2.0|
|`rx_summary` | 產生模型的摘要||

新的機器學習演算法也會提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| 函數| Description|
| ------ | ------ |
|`rx_fast_forest` |建立決策樹系模型|
|`rx_fast_linear` | 線性迴歸與隨機雙重座標 （堆疊）|
|`rx_fast_trees` | 建立促進式樹狀結構的模型 |
|`rx_logistic_regression` | 建立羅吉斯迴歸模型|
|`rx_neural_network` | 建立可自訂類神經網路模型 |
|`rx_oneclass_svm` | 平衡資料集，以用於異常偵測上建立 SVM 模型|

> [!TIP]
> 許多這些演算法已提供做為 Azure Machine Learning 中的模組。

Python MicrosoftML 也包括各種不同的轉換和 helper 函式，例如：

+ `rx_predict`產生從定型模型的預測，而且可以用於即時計分
+ 映像功能，其潛在函式
+ 進行文字處理和人氣擷取函式

如需詳細資訊，請參閱[MicrosoftML 簡介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社群使用可能不同於您所用，包括所有小寫字母和底線，而非 camel 命名法的大小寫的參數名稱的程式碼撰寫慣例。 此外，也許您注意到， **revoscalepy**程式庫一律為小寫。 沒錯 ！ 其他的 Python 慣例。
> 
> 查看 Microsoft: [Python 函式說明] 的 Python 參考文件上的提示[Python 函式的說明](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>範例

您可以執行包含的程式碼**revoscalepy**函式在本機或遠端計算內容中。 您也可以在預存程序中內嵌的 Python 程式碼，以執行 SQL Server 內的 Python。

當在本機執行，您通常從命令列中，或 Python 開發環境中，執行 Python 指令碼，並指定使用其中一種 SQL Server 計算內容**revoscalepy**函式。 您可以使用遠端計算內容的整個程式碼，或個別的函式。 例如，您可能要卸載至伺服器，以使用最新的資料，以避免資料移動的模型定型。

如果您想要將完整的 Python 指令碼預存程序， [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我們建議您在單一函數清楚地定義輸入和輸出為重寫程式碼。 必須是輸入和輸出**熊**資料框架。 完成此動作後，您可以從任何用戶端可支援 T-SQL 呼叫預存程序、 輕鬆地傳遞 SQL 查詢做為輸入，以及將結果儲存至 SQL 資料表。 如需範例，請參閱[L 開發人員的資料庫中 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-remote-compute-contexts"></a>使用遠端計算內容

+ [使用 revoscalepy 建立模型](../tutorials/use-python-revoscalepy-to-create-model.md)

  此範例示範如何執行 Python 當成計算內容中使用的 SQL Server 執行個體。

### <a name="using-a-stored-procedure"></a>使用預存程序

+ [執行 Python 使用 T-SQL](../tutorials/run-python-using-t-sql.md)

  此範例會示範呼叫預存程序中內嵌的 Python 指令碼的基本機制。

### <a name="using-revoscalepy-with-microsoftml"></a>使用 MicrosoftML revoscalepy

MicrosoftML Python 的功能整合在一起的計算內容和 revoscalepy 中所提供的資料來源。 因此，您無法使用 MicrosoftML 演算法來定義和 Python 中定型模型，並使用在本機或 SQl Server 計算內容中執行 Python 程式碼的 revoscalepy 函式。

只需匯入您的 Python 程式碼中的模組，然後參考您需要個別的函式。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>需求

若要在 SQL Server 中執行 Python 程式碼，您必須已安裝 SQL Server 2017 和功能**機器學習服務**，並啟用 Python 語言。 舊版的 SQL Server 不支援 Python 整合。

> [!NOTE]
> Python 的開放原始碼散發套件不支援 SQL Server 計算內容。 不過，如果您要發佈和取用從 Windows 的 Python 應用程式，您可以安裝 Microsoft Machine Learning 伺服器而不需要安裝 SQL Server。 如需詳細資訊，請參閱[建立獨立 R 伺服器](../r/create-a-standalone-r-server.md)

## <a name="get-more-help"></a>取得更多說明

產品發行時，會使用這些 Api 的完整文件。 在此同時，我們建議您參考 RevoScaleR 或 MicrosoftML 文件庫中的對應函式。

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

您可以取得說明的任何 Python 函式匯入模組，然後再呼叫`help()`。 例如，執行`help(revoscalepy)`從 Python IDE 會傳回一份所有函式在 revoscalepy 模組中，以其簽章。

如果您使用 Python Tools for Visual Studio 時，您可以使用 IntelliSense，取得語法和引數的說明。 如需詳細資訊，請參閱[Python 支援 Visual Studio 中](http://docs.microsoft.com/visualstudio/python/installation)，並下載符合您的 Visual Studio 版本的擴充功能。 您可以使用 Visual Studio 2015 和 2017，具有 Python 或更早版本。

## <a name="see-also"></a>另請參閱

[Python 教學課程](../tutorials/sql-server-python-tutorials.md)
