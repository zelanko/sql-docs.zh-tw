---
title: 使用 Python revoscalepy 建立模型 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d886466d7bf4f0c86c1cd9505480a3fadb6e66ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>使用 Python revoscalepy 建立模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在這一課，您可以了解如何從遠端的開發用戶端，在 SQL Server 中建立線性迴歸模型中執行 Python 程式碼。 

## <a name="prerequisites"></a>필수 구성 요소

+ 這一課使用不同的資料，比先前的課程。 您不需要先完成先前的課程。 不過，如果您已完成先前的課程，並已設定為執行 Python 的伺服器，使用該伺服器和資料庫做為運算環境。
+ 若要執行 Python 程式碼以計算中使用 SQL Server 內容需要 2017年或更新版本的 SQL Server。 此外，您必須明確地安裝並再啟用此功能**機器學習服務**，選擇 Python 語言選項。

    如果您安裝的 SQL Server 2017 發行前版本，您應該更新為至少 RTM 版本。 以展開和改善 Python 功能持續更新的服務版本。 本教學課程的某些功能可能不適用於早期發行前版本。

+ 這個範例會使用預先定義的 Python 環境，名為`PYTEST_SQL_SERVER`。 在環境已設定為包含**revoscalepy**及其他必要的程式庫。 

    如果您沒有設定為執行 Python 環境，您必須個別執行。 如何建立或修改 Python 環境的討論超出本教學課程的範圍。 如需如何設定包含正確的程式庫的 Python 用戶端的詳細資訊，請參閱[安裝 Python 用戶端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)和[連結的 Python 工具](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。

## <a name="remote-compute-contexts-and-revoscalepy"></a>遠端計算內容和 revoscalepy

此範例將示範如何在遠端建立 Python 模型的程序_計算內容_，可以讓您從用戶端，但選擇遠端環境，例如 SQL Server、 Spark 或機器學習伺服器，其中作業會實際執行。 使用的計算內容，可以更輕鬆地撰寫程式碼一次，並將它部署到任何支援的環境。

若要在 SQL Server 中執行 Python 程式碼需要**revoscalepy**封裝。 這是特殊的 Python 封裝，類似於 Microsoft 提供的**RevoScaleR**的 R 語言套件。 **Revoscalepy**套件支援建立的計算內容和提供的基礎結構，用來在本機工作站與遠端伺服器之間傳遞資料和模型。 **Revoscalepy**函式的支援的資料庫中的程式碼執行[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在這一課，您使用資料中 SQL Server 來根據為線性模型定型[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的函式**revoscalepy**的非常大型的資料集上支援迴歸。 

這一課還會示範如何設定，然後使用的基本概念**SQL Server 計算內容**Python 中。 討論如何計算內容使用其他平台，以及支援的計算內容，請參閱[Server 機器學習中的指令碼執行的計算內容](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>準備資料庫和範例資料

1. 這一課使用的資料庫`sqlpy`。 如果您尚未完成前面任何一課，您可以執行下列程式碼來建立資料庫：

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > 如果您想要使用不同的資料庫，請務必編輯範例程式碼和變更連接字串中的資料庫名稱。

2. 這個範例會使用 Airline 資料集，這是可在 R 和 Python。 Python 範例建立資料庫之後，填入資料的資料表與此處所述：[範例資料中 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data)。

3. 變更此環境，以便使用您的用戶端上的可用環境的名稱。

## <a name="run-the-sample-code"></a>執行範例程式碼

您已備妥的資料庫，且有之後儲存在資料表中，定型的資料就會開啟 Python 開發環境，並執行程式碼範例。

該程式碼執行下列步驟：

1. 匯入必要的程式庫和函式。
2. 建立 SQL Server 的連接。 建立**資料來源**物件使用的資料。
3. 修改資料使用**轉換**，以便供羅吉斯迴歸演算法。
4. 呼叫`rx_lin_mod`並定義用來符合模型的公式。
5. 會產生一組根據原始資料的預測。
6. 建立預測的值為基礎的摘要。

使用 SQL Server 執行個體當成計算內容執行所有作業。

> [!NOTE]
> 從命令列執行此範例的示範，請參閱這段影片： [SQL Server 2017 Advanced Analytics 使用 Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>範例程式碼

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>定義資料來源與定義的計算內容

資料來源與不同的計算內容。 _資料來源_定義您的程式碼中使用的資料。 _計算內容_定義執行程式碼。 不過，它們使用相同的資訊：

+ Python 變數，例如`sql_query`和`sql_connection_string`，定義的資料來源。 

    將這些變數來傳遞[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)建構函式來實作**資料來源物件**名為`data_source`。

+ 您建立**計算內容物件**使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata)建構函式。 產生**計算內容物件**名為`sql_cc`。

    這個範例會在資料來源中，假設您將會當成計算內容使用的相同 SQL Server 執行個體上的資料重複使用相同的連接字串使用。 
    
    不過，在資料來源和計算內容可能會在不同伺服器上。
 
### <a name="changing-compute-contexts"></a>變更計算內容

您定義的計算內容之後，您必須設定**作用中的計算內容**。 

根據預設，大部分的作業會於本機執行，這表示，如果您未指定不同的計算內容、 將資料來源擷取資料並執行程式碼將目前的 Python 環境中。

有兩種方式來設定主動式計算內容：
+ 做為引數的方法或函式
+ 藉由呼叫 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>設定計算內容做為引數的方法或函式

在此範例中，您必須設定計算內容使用個別的引數**rx**函式。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

此計算內容重複使用的呼叫中[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>設定使用 rx_set_compute_context 明確的計算內容

此函式[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)可讓您切換計算已定義的內容。

設定之後使用中計算內容，則在您變更它之前仍會保持作用中。

### <a name="using-parallel-processing-and-streaming"></a>使用平行處理和串流

當您定義的計算內容時，您也可以設定參數的計算內容資料的處理方式來控制。 這些參數是根據資料來源類型而有所不同。

針對 SQL Server 計算內容，您可以設定批次大小，或提供有關使用中執行的工作平行處理原則程度提示。

+ 具有四個處理器的電腦上執行範例所以`num_tasks`參數設為 4 以允許最大值使用的資源。 
+ 如果您設定此值為 0 時，SQL Server 會使用預設值，也就是盡可能，伺服器目前的 MAXDOP 設定平行執行多工作。 不過，工作可能會配置的確切數目取決於許多其他因素，例如伺服器設定並執行其他工作。

## <a name="related-samples"></a>相關的範例

這些其他的 Python 範例和教學課程會示範端對端案例，使用更複雜的資料來源，以及遠端計算內容使用。

+ [資料庫中的 SQL 開發人員的 Python](sqldev-in-database-python-for-sql-developers.md)
+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
