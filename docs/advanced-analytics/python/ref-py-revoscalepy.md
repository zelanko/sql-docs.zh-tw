---
title: revoscalepy Python 套件
description: 使用 Python SQL Server 2017 Machine Learning 服務中的 revoscalepy 模組簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 297e58fe089b0f68670a9d2a994f05d9c8bf4344
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470322"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (SQL Server 中的 Python 模組)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy**是 Microsoft 的 Python35 相容模組, 支援分散式運算、遠端計算內容和高效能資料科學演算法。 它是以 R 的**RevoScaleR**套件為基礎 (與 Microsoft r Server 和 SQL Server R Services 一起散發), 提供類似的功能:

+ 具有相同版本**revoscalepy**之系統上的本機和遠端計算內容
+ 資料轉換和視覺化功能
+ 資料科學函式, 可透過分散式或平行處理進行調整
+ 改善的效能, 包括使用 Intel 數學程式庫

您在**revoscalepy**中建立的資料來源和計算內容也可以在機器學習演算法中使用。 如需這些演算法的簡介, 請參閱[SQL Server 中的 Microsoftml Python 模組](ref-py-microsoftml.md)。

## <a name="full-reference-documentation"></a>完整參考檔

**Revoscalepy**程式庫是散發在多個 Microsoft 產品中, 但不論您是在 SQL Server 或其他產品中取得程式庫, 使用方式都相同。 因為函式相同, 所以[個別 revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)函式的檔集只會發佈到 Microsoft Machine Learning Server 的[Python 參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)底下的一個位置。 若有任何產品特定行為存在, 則函式說明頁面中會注明不一致的情況。

## <a name="versions-and-platforms"></a>版本和平臺

**Revoscalepy**模組是以 Python 3.5 為基礎, 只有在您安裝下列其中一個 Microsoft 產品或下載時, 才能使用:

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [適用于資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整產品發行版本僅限 Windows, 從 SQL Server 2017 開始。 **Revoscalepy**的 Linux 支援是[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)的新功能。

## <a name="functions-by-category"></a>依類別分類的函數

本節依類別列出函式, 讓您瞭解如何使用每一種功能。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)來依字母順序尋找函數。

## <a name="1-data-source-and-compute"></a>1-資料來源和計算

**revoscalepy**包含用來建立資料來源的函數, 以及設定執行計算的位置或*計算內容*。 下表列出與 SQL Server 案例相關的函數。

在某些情況下, SQL Server 和 Python 會使用不同的資料類型。 如需 SQL 和 Python 資料類型之間的對應清單, 請參閱[Python 對 SQL 資料類型](python-libraries-and-data-types.md)。

| 函數| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  建立 SQL Server 計算內容物件, 以將計算推送至遠端實例。 有數個**revoscalepy**函式會將計算內容視為引數。 如需內容切換範例, 請參閱[使用 Revoscalepy 建立模型](../tutorials/use-python-revoscalepy-to-create-model.md)。|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | 根據 SQL Server 查詢或資料表建立資料物件。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| 建立以 ODBC 連接為基礎的資料來源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 建立以本機 XDF 檔案為基礎的資料來源。 XDF 檔案通常用來將記憶體內部資料卸載至磁片。 當您使用的資料量比可從一個批次中的資料庫傳輸更多, 或超過記憶體中可容納的資料時, XDF 檔會很有用。 例如, 如果您定期將大量資料從資料庫移到本機工作站, 而不是針對每個 R 作業重複查詢資料庫, 您可以使用 XDF 檔案做為一種快取, 將資料儲存在本機, 然後在您的 R 工作區中使用它。 |

> [!TIP]
> 如果您不熟悉資料來源或計算內容, 建議您先從 Microsoft Machine Learning Server 檔中的[分散式運算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)開始。

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

| 函數 | 描述 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | 將資料匯入 xdf 檔案或資料框架中。|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 將輸入資料集的資料轉換成輸出資料集。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-定型和摘要

| 函數| 描述|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 調整隨機梯度促進式決策樹|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 調整分類和回歸決策樹系|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 調整分類和迴歸樹狀結構 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 建立線性迴歸模型|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 建立羅吉斯迴歸模型|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | 在 revoscalepy 中產生物件的單一變數摘要。|

您也應該參閱[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)中的函數, 以取得其他方法。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-計分函數

| 函數| 描述|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 從定型的模型產生預測|) | 從定型的模型產生預測, 並可用於即時評分。 |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 使用 rx_lin_mod 和 rx_logit 物件計算預測值和殘差。 |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | 從 rx_dforest 或 rx_btrees 物件計算資料集的預測或擬合值。 |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | 針對 rx_dtree 物件中的資料集計算預測或擬合的值。 |

## <a name="how-to-work-with-revoscalepy"></a>如何使用 revoscalepy

**Revoscalepy**中的函式可在封裝于預存程式中的 Python 程式碼中呼叫。 大部分的開發人員會在本機建立**revoscalepy**解決方案, 然後將完成的 Python 程式碼遷移至預存程式作為部署練習。

在本機執行時, 您通常會從命令列或從 Python 開發環境執行 Python 腳本, 並使用其中一個**revoscalepy**函數來指定 SQL Server 計算內容。 您可以針對整個程式碼或個別函式使用遠端計算內容。 例如, 您可能想要將模型定型卸載至伺服器, 以使用最新的資料, 並避免資料移動。

當您準備好要在預存程式內封裝 Python 腳本時, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), 建議您將程式碼重寫為已清楚定義輸入和輸出的單一函式。 

輸入和輸出必須為**pandas**資料框架。 完成此作業時, 您可以從任何支援 T-sql 的用戶端呼叫預存程式, 輕鬆地將 SQL 查詢傳遞為輸入, 並將結果儲存至 SQL 資料表。 如需範例, 請參閱[瞭解適用于 SQL 開發人員的資料庫內 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-revoscalepy-with-microsoftml"></a>搭配使用 revoscalepy 與 microsoftml

適用于[microsoftml](ref-py-microsoftml.md)的 Python 函式會與 revoscalepy 中提供的計算內容和資料來源整合。 從 microsoftml 呼叫函式時 (例如在定義和定型模型時), 請使用 revoscalepy 函式, 在本機或在 SQl Server 遠端計算內容中執行 Python 程式碼。

下列範例顯示在 Python 程式碼中匯入模組的語法。 接著, 您可以參考所需的個別函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)
+ [教學課程：在 T-sql 中內嵌 Python 程式碼](../tutorials/run-python-using-t-sql.md)
+ [Python 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
