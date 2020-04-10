---
title: 建立 Python 模型 - revoscalepy
description: 使用 revoscalepy 函數撰寫 Python 指令碼，以建立在 SQL Server 遠端執行的資料科學模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5faa8688f3036f80b947ccc5d99c09c4612f26fb
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116021"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>使用 Python 搭配 revoscalepy 建立可在 SQL Server 上遠端執行的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft 的 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 程式庫提供資料科學演算法，以進行資料探索、視覺化、轉換和分析。 在 SQL Server 的 Python 整合案例中，此程式庫具有策略重要性。 **revoscalepy** 函數可以在多核心伺服器上平行執行。 您可以在中央伺服器和用戶端工作站 (個別的實體電腦，全部都具有相同的 **revoscalepy** 程式庫) 的分散式架構中，撰寫在本機啟動的 Python 程式碼，然後將執行作業轉移至資料所在的遠端 SQL Server 執行個體。

您可以在下列 Microsoft 產品和發佈中找到 **revoscalepy**：

+ [SQL Server 機器學習服務 (資料庫內)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (非 SQL，獨立伺服器)](https://docs.microsoft.com/machine-learning-server/index)
+ [用戶端 Python 程式庫 (適用於開發工作站)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

此練習會示範如何根據 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) (**revoscalepy** 的其中一個演算法，可接受計算內容做為輸入) 建立線性回歸模型。 您在此練習中執行的程式碼會從本機將程式碼執行移至遠端運算環境，這是由啟用遠端計算內容的 **revoscalepy** 函數所啟用。

完成本教學課程時，您將學會如何：

> [!div class="checklist"]
> * 使用 **revoscalepy** 建立線性模型
> * 將作業從本機移至遠端計算內容

## <a name="prerequisites"></a>Prerequisites

本練習中使用的範例資料是 [**flightdata.csv**](demo-data-airlinedemo-in-sql.md) 資料庫。

您需要 IDE 才能執行本文中的範例程式碼，而且 IDE 必須連結至 Python 可執行檔。

若要練習計算內容轉移，您需要[本機工作站](../python/setup-python-client-tools-sql.md)，以及已啟用 [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 和 Python 的 SQL Server 的資料庫引擎執行個體。 

> [!Tip]
> 如果您沒有兩台電腦，您可以安裝相關的應用程式，在一台實體電腦上模擬遠端計算內容。 首先，[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)的安裝作業會以「遠端」執行個體的形式運作。 接下來，[Python 用戶端程式庫的安裝作業會以用戶端運作](../python/setup-python-client-tools-sql.md)。 相同的電腦上會有兩份相同的 Python 散發套件和 Microsoft Python 程式庫。 您必須追蹤檔案路徑，以及您用來順利完成練習的 Python 複本。

## <a name="remote-compute-contexts-and-revoscalepy"></a>遠端計算內容和 revoscalepy

這個範例示範在遠端計算內容中建立 Python 模型的流程，您可透過這項流程從用戶端工作，不過需要選擇實際執行作業的遠端環境，例如 SQL Server、Spark 或 Machine Learning Server。 遠端計算內容的目標是為了將計算帶入資料所在的位置。

若要在 SQL Server 中執行 Python 程式碼，需要 **revoscalepy** 套件。 這是 Microsoft 所提供的特殊 Python 套件，類似於 R 語言的 **RevoScaleR** 套件。 **revoscalepy** package 支援建立計算內容，並在本機工作站與遠端伺服器之間，提供傳遞資料和模型的基礎結構。 支援資料庫內程式碼執行的 **revoscalepy** 函數為 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在這個課程中，您會根據 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) (**revoscalepy** 中的函數，支援相當大型資料集的回歸) 使用 SQL Server 中的資料將線性模型定型。 

本課程也會示範基本概念，讓您了解如何在 Python 中設定及使用 **SQL Server 計算內容**。 如需計算內容如何與其他平台搭配使用，以及支援哪些計算內容的討論，請參閱 [Machine Learning Server 中指令碼執行的計算內容](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。


## <a name="run-the-sample-code"></a>執行範例程式碼

在您備妥資料庫並將定型資料儲存在資料表中之後，請開啟 Python 開發環境並執行程式碼範例。

程式碼會執行下列步驟：

1. 匯入必要的程式庫和函數。
2. 建立 SQL Server 的連線。 建立處理資料的**資料來源**物件。
3. 使用**轉換**修改資料，以便可由邏輯迴歸演算法使用。
4. 呼叫 `rx_lin_mod` 並定義用來配合模型的公式。
5. 根據原始資料產生一組預測。
6. 根據預測的值建立摘要。

所有作業都是使用 SQL Server 的執行個體做為計算內容來執行。

> [!NOTE]
> 如需從命令列執行此範例的示範，請觀看下列影片：[使用 Python 的 SQL Server 2017 進階分析](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>範例程式碼

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>定義資料來源與定義計算內容

資料來源與計算內容不同。 *資料來源* 會定義程式碼中使用的資料。 計算內容會定義執行程式碼的位置。 不過，這兩者使用一些相同的資訊：

+ Python 變數 (例如 `sql_query` 和 `sql_connection_string` 定義資料的來源)。 

    將這些變數傳遞至 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 的函數，以執行名為 `data_source` 的**資料來源物件**。

+ 您可以使用 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) 的函數建立**計算內容物件**。 產生的**計算內容物件** 會命名為 `sql_cc`。

    這個範例會假設資料位於您將用來做為計算內容的同一個 SQL Server 執行個體上，並依此重複使用您在資料來源中使用的相同連接字串。 
    
    不過，資料來源和計算內容可能會在不同的伺服器上。
 
### <a name="changing-compute-contexts"></a>變更計算內容

定義計算內容之後，您必須設定**使用中的計算內容**。 

大部分的作業預設都是在本機執行，這表示如果您未指定不同的計算內容，系統則會從資料來源擷取資料，而程式碼會在您目前的 Python 環境中執行。

有兩種方法可以設定使用中的計算內容：
+ 做為方法或函數的引數
+ 藉由呼叫 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>將計算內容設定為方法或函數的引數

在此範例中，您會使用個別 **rx** 函數的引數來設定計算內容。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

此計算內容會在 [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 的呼叫中重複使用：

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>使用 rx_set_compute_context 明確設定計算內容

函數 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 可讓您在已定義的計算內容之間切換。

設定使用中的計算內容之後，它會保持使用中，直到您變更為止。

### <a name="using-parallel-processing-and-streaming"></a>使用平行處理和串流

您定義計算內容時，也可以設定參數來控制計算內容處理資料的方式。 這些參數會因資料來源類型而不同。

針對 SQL Server 計算內容，您可以設定批次大小，也可以提供執行中工作所使用的平行處理原則程度有關的提示。

+ 此範例是在具有四個處理器的電腦上執行，因此 `num_tasks` 參數會設定為 4，以允許最大的資源使用量。 
+ 如果您將此值設定為 0，SQL Server 會使用預設值，也就是在伺服器目前的 MAXDOP 設定之下，盡可能平行執行許多工作。 不過，可能配置的確切工作數目取決於其他許多因素，例如伺服器設定和正在執行的其他作業。

## <a name="next-steps"></a>後續步驟

這些額外的 Python 範例和教學課程會示範使用資料來源更複雜的端對端案例，以及使用遠端計算內容。

+ [適用於 SQL 開發人員的資料庫內 Python](sqldev-in-database-python-for-sql-developers.md)
+ [使用 Python 和 SQL Server 建置預測模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
