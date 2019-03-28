---
title: revoscalepy Python 封裝-SQL Server Machine Learning 服務
description: 在 SQL Server 2017 Machine Learning 服務使用 Python 中的 revoscalepy 模組簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e0cded793f6017398641ffa055deec62010b2b3d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510605"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy （SQL Server 中的 Python 模組）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy**是從 Microsoft 支援分散式運算、 遠端計算內容和高效能的資料科學演算法 Python35 相容模組。 它根據**RevoScaleR** （隨附於 Microsoft R Server 和 SQL Server R Services），提供類似功能的封裝：

+ 本機和遠端計算內容，在具有相同版本的系統上**revoscalepy**
+ 資料轉換和視覺效果函式
+ 資料科學功能，透過分散式或平行處理可調整
+ 提升的效能，包括 Intel 數學程式庫使用

資料來源和您在中建立的計算內容**revoscalepy**也用於機器學習服務演算法。 如需這些演算法，請參閱 < [microsoftml SQL Server 中的 Python 模組](ref-py-microsoftml.md)。

## <a name="full-reference-documentation"></a>完整的參考文件

**Revoscalepy**程式庫會分散在多個 Microsoft 產品中，但不論您取得 SQL Server 或另一個產品中的程式庫使用方式都相同。 函式是相同的因為[個別 revoscalepy 函式文件](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)發行到下一個位置[Python 參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)的 Microsoft Machine Learning Server。 應該任何產品專屬行為存在時，差異會記錄在函式說明頁面。

## <a name="versions-and-platforms"></a>版本與平台

**Revoscalepy**模組是根據 Python 3.5 和可用只有當您安裝其中一個下列的 Microsoft 產品或下載項目時：

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更新版本](https://docs.microsoft.com/machine-learning-server/)
+ [資料科學用戶端的 Python 用戶端程式庫](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整的產品版本是 Windows 專屬，從 SQL Server 2017 開始。 Linux 支援**revoscalepy**的新功能[SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="functions-by-category"></a>依類別目錄的函式

此區段會列出依類別目錄，讓您了解如何使用每個函式。 您也可以使用[目錄](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)依字母順序尋找函式。

## <a name="1-data-source-and-compute"></a>1-資料來源和計算

**revoscalepy**包含函式來建立資料來源和設定的位置，或*計算內容*，執行計算。 SQL Server 案例與相關的函式列在下表中。

SQL Server 和 Python 使用不同的資料類型，在某些情況下。 如需 SQL 和 Python 的資料類型之間的對應，請參閱[Python 到 SQL 資料型別](python-libraries-and-data-types.md)。

| 函數| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  建立 SQL Server 計算內容物件，將計算推送到遠端執行個體。 數個**revoscalepy**函式會採用當做引數的計算內容。 如需內容切換的範例，請參閱 <<c0> [ 使用 revoscalepy 建立模型](../tutorials/use-python-revoscalepy-to-create-model.md)。|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | 建立 SQL Server 查詢或資料表為基礎的資料物件。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| 建立 ODBC 連接為基礎的資料來源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 建立本機 XDF 檔案為基礎的資料來源。 XDF 檔案通常用於記憶體中將資料卸載至磁碟。 使用更多的資料，比可以傳輸，從資料庫中一個批次或超過記憶體內可容納的資料時，XDF 檔案可以是很有用。 比方說，如果定期在資料庫的本機工作站之間移動大量資料，而不是查詢資料庫中重複的每個 R 作業，您可以使用 XDF 檔案為類型的快取來儲存在本機的資料，然後在您的 R 工作區中使用它。 |

> [!TIP]
> 如果您不熟悉之資料來源的概念，或計算內容，建議您先使用[分散式運算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)Microsoft Machine Learning Server 文件中。

## <a name="2-data-manipulation-etl"></a>2-資料操作 (ETL)

| 函數 | 描述 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | 資料匯入.xdf 檔案或資料框架。|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 轉換至輸出資料集的資料從輸入資料集。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-訓練和摘要

| 函數| 描述|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 符合隨機梯度促進式的決策樹|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 符合分類和迴歸的決策樹系|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 調整的分類和迴歸樹狀結構 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 建立線性迴歸模型|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 建立羅吉斯迴歸模型|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | 產生單一摘要 revoscalepy 中的物件。|

您也應該檢閱中的函式[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)針對其他的方法。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 評分函式

| 函數| 描述|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 從定型的模型產生預測|) | 從定型的模型產生預測，而且可以用於即時評分。 |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 計算預測的值，並使用 rx_lin_mod 和 rx_logit 物件的殘差。 |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | 計算預測或適合 rx_dforest 或 rx_btrees 物件從資料集的值。 |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | 計算預測或適合 rx_dtree 物件從資料集的值。 |

## <a name="how-to-work-with-revoscalepy"></a>如何使用 revoscalepy

中的函式**revoscalepy**封裝在預存程序中的 Python 程式碼中呼叫。 大部分的開發人員建置**revoscalepy**解決方案在本機，然後將完成的 Python 程式碼移轉到預存程序中，部署練習變更。

本機執行時，您通常在從命令列中，或從 Python 開發環境中，執行 Python 指令碼，並指定使用其中一種在 SQL Server 計算內容**revoscalepy**函式。 完整的程式碼，或個別的函式，您可以使用遠端計算內容。 例如，您可能要卸載至伺服器，以使用最新的資料，以避免資料移動的模型定型。

當您準備好要封裝的預存程序，在 Python 指令碼[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我們建議您為已清楚定義的輸入和輸出的單一函式重寫程式碼。 

輸入和輸出必須是**pandas**資料框架。 時這麼做，您可以從任何用戶端，支援 T-SQL 呼叫預存程序，輕鬆做為輸入，將 SQL 查詢和結果儲存至 SQL 資料表。 如需範例，請參閱[了解適用於 SQL 開發人員的資料庫內 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-revoscalepy-with-microsoftml"></a>使用 microsoftml 中的 revoscalepy

Python 函式的[microsoftml](ref-py-microsoftml.md)整合在一起 revoscalepy 中提供的計算內容和資料來源。 當從 microsoftml 中呼叫函式，例如當定義及定型模型，使用 revoscalepy 函式來執行 Python 程式碼是在本機或在遠端 SQl Server 計算內容。

下列範例會顯示匯入您的 Python 程式碼中的模組的語法。 然後，您可以參考您需要個別的函式。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另請參閱

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)
+ [教學課程：內嵌在 T-SQL 中的 Python 程式碼](../tutorials/run-python-using-t-sql.md)
+ [Python 參考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
