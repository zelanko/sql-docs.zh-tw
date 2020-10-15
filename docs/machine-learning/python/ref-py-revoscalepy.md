---
title: revoscalepy Python 套件
description: revoscalepy 是來自 Microsoft 的 Python 套件，其支援分散式計算、遠端計算內容，以及高效能資料科學演算法。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3d435340ec276de3dd2b08f340ecd49bb8c03787
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956899"
---
# <a name="revoscalepy-python-package-in-sql-server-machine-learning-services"></a>revoscalepy (SQL Server 機器學習服務中的 Python 套件)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**revoscalepy** 是來自 Microsoft 的 Python 套件，其支援分散式計算、遠端計算內容，以及高效能資料科學演算法。 該套件包含在 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)中。

套件提供下列功能：

+ 系統上的本機和遠端計算內容具有相同版本的 **revoscalepy**
+ 資料轉換與視覺化函式
+ 資料科學函式 (可透過分散式或平行處理進行調整)
+ 提升效能 (包括使用 Intel 數學程式庫)

您在 **revoscalepy**中建立的資料來源和計算內容也可以在機器學習演算法中使用。 如需這些演算法的簡介，請參閱 [SQL Server 中的 microsoftml Python 模組](ref-py-microsoftml.md)。

## <a name="full-reference-documentation"></a>完整參考文件

**revoscalepy** 套件分散在多個 Microsoft 產品中，但不論是在 SQL Server 還是其他產品中取得該套件，其使用方式都相同。 由於函式相同，因此[個別 revoscalepy 函式的文件](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)只發佈至 Microsoft Machine Learning Server 之 [Python 參考](/machine-learning-server/python-reference/introducing-python-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

## <a name="versions-and-platforms"></a>版本與平台

**revoscalepy** 模組以 Python 3.5 為基礎，且只有當您安裝下列其中一個Microsoft 產品或下載項目時才會提供：

+ [SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](/machine-learning-server/)
+ [適用於資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 在 SQL Server 2017 中，完整產品發行版本僅適用於 Windows。 在 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) 及更新版本中，**revoscalepy** 同時支援 Windows 和 Linux。

## <a name="functions-by-category"></a>依類別區分的函式

本節依類別列出函式，讓您了解每個函式的使用方式。 您也可以使用[目錄](/machine-learning-server/python-reference/introducing-python-package-reference)來依字母順序尋找函式。

## <a name="1-data-source-and-compute"></a>1-資料來源與計算

**revoscalepy** 包含用於建立資料來源及設定計算執行位置 (或「計算內容」  ) 的函式。 下表列出與 SQL Server 案例相關的函式。

在某些情況下，SQL Server 和 Python 會使用不同的資料類型。 如需 SQL 與 Python 資料類型間的對應清單，請參閱 [Python 與 SQL 的對應資料類型](python-libraries-and-data-types.md)。

| 函式| 描述|
| ------- | ---------- |
| [RxInSqlServer](/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  建立 SQL Server 計算內容物件以將計算推送至遠端執行個體。 數個 **revoscalepy** 函式會以計算內容作為引數。 如需內容切換範例，請參閱[使用 revoscalepy 來建立模型](../tutorials/use-python-revoscalepy-to-create-model.md)。|
| [RxSqlServerData](/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | 根據 SQL Server 查詢或資料表來建立資料物件。 |
| [RxOdbcData](/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| 根據 ODBC 連線來建立資料來源。 |
| [RxXdfData](/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 根據本機 XDF 檔案來建立資料來源。 XDF 檔案通常用來將記憶體內的資料卸載至磁碟。 當使用的資料超過可從資料庫以單一批次傳輸的資料，或是超過記憶體可容納的資料時，XDF 檔案非常實用。 例如，如果您會定期將大量資料從資料庫移到本機工作站，而不是針對每個 R 作業重複地查詢資料庫，則您可以使用 XDF 檔案作為一種快取以將資料儲存在本機，然後在您的 R 工作區中使用它。 |

> [!TIP]
> 如果您不熟悉資料來源或計算內容，建議您從 Microsoft Machine Learning Server 文件中的[分散式計算](/machine-learning-server/r/how-to-revoscaler-distributed-computing) \(英文\) 開始著手。

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

| 函式 | 描述 |
|----------|-------------|
|[rx_import](/machine-learning-server/python-reference/revoscalepy/rx-import) | 將資料匯入至 .xdf 檔案或資料框架。|
|[rx_data_step](/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 將資料從輸入資料集轉換至輸出資料集。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-定型與摘要

| 函式| 描述|
| ------- | ---------- |
|[rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 符合隨機梯度提升決策樹|
|[rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 符合分類與迴歸決策樹系|
|[rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 符合分類與迴歸樹 |
|[rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 建立線性迴歸模型|
|[rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) | 建立羅吉斯迴歸模型|
|[rx_summary](/machine-learning-server/python-reference/revoscalepy/rx-summary) | 在 revoscalepy 中產生單變量物件摘要。|

您也應該檢閱 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) 中的函式來了解額外的方法。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-評分函式

| 函式| 描述|
| ------- | ---------- |
| [rx_predict](/machine-learning-server/python-reference/revoscalepy/rx-predict) | 從已定型的模型產生預測|) | 從已定型的模型產生預測，並可用於即時評分。 |
|[rx_predict_default](/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 使用 rx_lin_mod 和 rx_logit 物件來計算預測值和殘差。 |
|[rx_predict_rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | 從 rx_dforest 或 rx_btrees 物件計算資料集的預測值或擬合值。 |
|[rx_predict_rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | 從 rx_dtree 物件計算資料集的預測值或擬合值。 |

## <a name="how-to-work-with-revoscalepy"></a>如何使用 revoscalepy

封裝在預存程序中的 Python 程式碼可呼叫 **revoscalepy** 中的函式。 大多數開發人員會在本機建置 **revoscalepy**解決方案，然後將完成的 Python 程式碼移轉至預存程序作為部署練習。

在本機執行時，您通常會從命令列或從 Python 開發環境執行 Python 指令碼，然後使用其中一個 **revoscalepy** 函式來指定 SQL Server 計算內容。 您可以將遠端計算內容用於整個程式碼，也可以用於個別函式。 例如，您可以將模型定型卸載至伺服器，以使用最新資料並避免資料移動。

當您準備好將 Python 指令碼封裝在預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 內時，建議您將程式碼重寫成已清楚定義輸入和輸出的單一函式。 

輸入和輸出必須是 **pandas** 資料框架。 完成此作業後，您就可以從任何支援 T-SQL 的用戶端呼叫該預存程序、輕鬆傳遞 SQL 查詢作為輸入，然後將結果儲存至 SQL 資料表。 如需範例，請參閱[了解適用於 SQL 開發人員的資料庫內 Python 分析](../tutorials/python-taxi-classification-introduction.md)。

### <a name="using-revoscalepy-with-microsoftml"></a>搭配 microsoftml 使用 revoscalepy

[microsoftml](ref-py-microsoftml.md) 的 Python 函式已與 revoscalepy 中提供的計算內容和資料來源整合。 從 microsoftml 呼叫函式時 (例如定義模型並將其定型時)，請使用 revoscalepy 函式在本機或 SQL Server 遠端計算內容中執行 Python 程式碼。

下列範例說明匯入您 Python 程式碼中模組的語法。 您可以接著參考所需的個別函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/python-tutorials.md)
+ [Python 參考 (Microsoft Machine Learning Server)](/machine-learning-server/python-reference/introducing-python-package-reference) \(英文\)