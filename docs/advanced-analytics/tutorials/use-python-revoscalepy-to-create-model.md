---
title: "使用 Python revoscalepy 建立模型 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
mms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 1ced0d05a74f43c6b80be6717826ab288ee25374
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>使用 Python revoscalepy 建立模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這個範例會示範如何建立線性迴歸模型，以及在 SQL server 會使用從演算法**revoscalepy**封裝。

**Revoscalepy**封裝 Python 包含轉換的物件，並提供類似的演算法**RevoScaleR**的 R 語言套件。 與此媒體櫃，您可以建立計算內容，移動之間的資料計算內容、 轉換資料，以及定型使用熱門的演算法，例如羅吉斯和線性迴歸、 決策樹，以及更多的預測模型。

如需詳細資訊，請參閱[revoscalepy 是什麼？](../python/what-is-revoscalepy.md)和[Python 函數參考](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="prerequisites"></a>필수 구성 요소

> [!IMPORTANT]
> 若要在 SQL Server 中執行 Python 程式碼，您必須已安裝 SQL Server 2017 CTP 2.0 或更新版本，以及您必須安裝並啟用功能，**機器學習服務**使用 Python。 其他版本的 SQL Server 不支援 Python 整合。

## <a name="run-the-sample-code"></a>執行範例程式碼

此程式碼執行下列步驟：

1. 匯入必要的程式庫和函式
2. 建立 SQL Server 的連接，並建立使用資料的資料來源物件
3. 修改資料，使其可以用於羅吉斯迴歸演算法
4. 呼叫`rx_lin_mod`並定義用來符合模型的公式
5. 會產生一組根據原始資料集的預測
6. 建立預測的值為基礎的摘要

使用 SQL Server 執行個體當成計算內容執行所有作業。

一般情況下，遠端計算內容中呼叫 Python 的程序是類似您在遠端計算內容中使用 R 的方式。 以 Python 指令碼從命令列中，或使用包含在此版本中提供的 Python 整合元件的 Python 開發環境中執行範例。 在您的程式碼，您會建立，並指出要執行的特定計算中使用的計算內容物件。

> [!NOTE]
> 請務必變更為適當的資料庫和環境名稱。
> 
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
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>討論

讓我們檢閱的程式碼，並反白顯示某些主要的步驟。

### <a name="defining-a-data-source-and-compute-context"></a>定義資料來源，並計算內容

資料來源與不同的計算內容。 _資料來源_定義您的程式碼中使用的資料。 _計算內容_定義執行程式碼。

1. 建立 Python 變數，例如`sql_query`和`sql_connection_string`，定義來源和您想要使用的資料。 將這些變數來傳遞[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)建構函式來實作**資料來源物件**名為`data_source`。
2. 使用建立的計算內容物件[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata)建構函式。 在此範例中，您可以傳遞定義前面，假設您將會當成計算內容使用的相同 SQL Server 執行個體上的資料相同的連接字串。 不過，在資料來源和計算內容可能會在不同伺服器上。 產生**計算內容物件**名為`sql_cc`。
3. 選擇 使用中的計算內容。 根據預設，作業會於本機執行，這表示，如果您未指定不同的計算內容、 將資料來源擷取資料和模型調整將會執行目前的 Python 環境中。

### <a name="changing-compute-contexts"></a>變更計算內容

在此範例中，您必須設定計算內容使用個別的引數**rx**函式。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

也是一樣的呼叫中**rxsummary**、 其中的計算內容可重複使用。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

您也可以使用此函式[rx_set_computecontext](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rx-set-compute-context)之間已定義的計算內容切換。

### <a name="setting-the-degree-of-parallelism"></a>設定平行處理原則程度

當您定義的計算內容時，您也可以設定參數的計算內容資料的處理方式來控制。 這些參數是根據資料來源類型而有所不同。

針對 SQL Server 計算內容，您可以設定批次大小，或提供有關使用中執行的工作平行處理原則程度提示。

因此我們設定此範例執行四個處理器的電腦上*num_tasks*參數設為 4。 如果您設定此值為 0 時，SQL Server 會使用預設值，也就是盡可能，伺服器目前的 MAXDOP 設定平行執行多工作。不過，即使在多處理器的伺服器，可能會配置工作的確切數目取決於許多其他因素，例如伺服器設定並執行其他工作。

## <a name="related-samples"></a>相關的範例

請參閱這些 Python 範例和進階的秘訣和示範端對端教學課程。

+ [資料庫中的 SQL 開發人員的 Python](sqldev-in-database-python-for-sql-developers.md)
+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [部署和使用 Python 模型](../python/publish-consume-python-code.md)
