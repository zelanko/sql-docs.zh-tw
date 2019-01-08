---
title: 使用 Python 使用 revoscalepy 建立模型-SQL Server Machine Learning
description: 撰寫使用 revoscalepy 函數來建立資料科學模型，從遠端執行 SQL Server 中的 Python 指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 18c5b801198946313e4f489902eb5f7c9ff0d7af
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596829"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>使用 Python 使用 revoscalepy 建立模型，是從遠端執行 SQL Server 上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[Revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)來自 Microsoft 的 Python 程式庫提供的資料探索、 視覺效果、 轉換和分析的資料科學演算法。 此程式庫有 SQL Server 中的 Python 整合案例中的策略的重要性。 在多核心伺服器上， **revoscalepy**函式可以平行執行。 使用中央伺服器與用戶端工作站的分散式架構中 (不同的實體電腦，全都具有相同**revoscalepy**程式庫)，您可以撰寫在本機啟動，但接著會轉移到執行的 Python 程式碼遠端資料所在的 SQL Server 執行個體。

您可以找到**revoscalepy**下列 Microsoft 產品和散發套件中：

+ [SQL Server Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning 伺服器 （非 SQL、 獨立伺服器）](https://docs.microsoft.com/machine-learning-server/index)
+ [用戶端 Python 程式庫 （適用於開發工作站）](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

本練習將示範如何建立線性迴歸模型，根據[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)，其中一種在演算法**revoscalepy**可接受做為輸入的計算內容。 在這個練習中，您將執行的程式碼會執行程式碼從本機轉移到遠端電腦的環境，啟用**revoscalepy**函數可讓遠端計算內容。

藉由完成本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 使用**revoscalepy**建立線性模型
> * 從本機轉換作業，到遠端計算內容

## <a name="prerequisites"></a>先決條件

此練習中所使用的範例資料[ **flightdata** ](demo-data-airlinedemo-in-sql.md)資料庫。

您需要在此文章中，執行範例程式碼的 IDE 和 IDE 必須連結至 Python 可執行檔。

若要練習計算內容 shift 鍵，您需要[本機工作站](../python/setup-python-client-tools-sql.md)和 SQL Server 資料庫引擎執行個體與[Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)和啟用的 Python。 

> [!Tip]
> 如果您沒有兩部電腦，您可以藉由安裝相關的應用程式來模擬一部實體電腦上的遠端計算內容。 首先，安裝[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)運作為 「 遠端 」 的執行個體。 第二個，安裝[Python 用戶端程式庫運作](../python/setup-python-client-tools-sql.md)與用戶端。 您必須在相同的 Python 散發套件和 Microsoft 的 Python 程式庫，在相同電腦上的兩個副本。 您必須持續追蹤的檔案路徑和用來成功地完成練習的 Python.exe 的複本。

## <a name="remote-compute-contexts-and-revoscalepy"></a>遠端計算內容和 revoscalepy

此範例示範的程序在遠端計算內容中，這可讓您從用戶端，運作，但選擇遠端環境，例如 SQL Server、 Spark 或實際執行的作業的 Machine Learning Server 建立 Python 模型。 遠端計算內容的目的是要讓資料所在的計算。

若要在 SQL Server 中執行 Python 程式碼需要**revoscalepy**封裝。 這是特殊的 Python 封裝，類似於 Microsoft 所提供**RevoScaleR**的 R 語言的封裝。 **Revoscalepy**套件支援建立計算內容，並提供基礎結構，在本機工作站與遠端伺服器之間傳遞資料和模型。 **Revoscalepy**函數中的資料庫程式碼執行該支援[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在這一課，您使用資料在 SQL Server 來訓練線性模型，根據[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的函式**revoscalepy**可支援非常大型資料集的迴歸。 

本課程也會示範如何設定，然後使用的基本概念**SQL Server 計算內容**在 Python 中。 討論如何計算內容使用其他平台，以及哪個計算內容支援，請參閱 <<c0> [ 計算內容，以便在 Machine Learning Server 中的指令碼執行](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。


## <a name="run-the-sample-code"></a>執行範例應用程式

您已備妥資料庫，並有之後儲存在資料表中，定型的資料就會開啟 Python 開發環境，並執行程式碼範例。

程式碼會執行下列步驟：

1. 匯入必要的程式庫和函式。
2. 建立 SQL Server 的連接。 會建立**資料來源**物件使用的資料。
3. 修改資料使用**轉換**供羅吉斯迴歸演算法。
4. 呼叫`rx_lin_mod`並定義用來符合模型的公式。
5. 會產生一組根據原始資料的預測。
6. 建立預測的值為基礎的摘要。

使用 SQL Server 的執行個體作為計算內容執行所有作業。

> [!NOTE]
> 從命令列執行此範例的示範，請參閱這段影片：[SQL Server 2017 進階的 Analytics 使用 Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

從計算內容的不同資料來源。 *資料來源*定義您的程式碼中使用的資料。 計算內容定義會執行程式碼。 不過，它們會使用一些相同的資訊：

+ Python 變數，例如`sql_query`和`sql_connection_string`，定義資料的來源。 

    將這些變數來傳遞[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)建構函式來實作**資料來源物件**名為`data_source`。

+ 您建立**計算內容物件**利用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)建構函式。 產生**計算內容物件**名為`sql_cc`。

    此範例中重複使用您所使用的相同連接字串，在資料來源中，假設您將使用做為計算內容的相同 SQL Server 執行個體上的資料。 
    
    不過，在資料來源和計算內容可能會在不同伺服器上。
 
### <a name="changing-compute-contexts"></a>變更計算內容

定義計算內容之後，您必須設定**作用中的計算內容**。 

根據預設，大部分的作業會在本機執行，這表示，如果您未指定不同的計算內容、 將資料來源擷取資料，和程式碼會執行目前的 Python 環境中。

有兩種方式可以設定作用中的計算內容：
+ 做為引數的方法或函式
+ 藉由呼叫 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>設定計算內容，做為引數的方法或函式

您可以在此範例中，設定計算內容來使用個別的引數**rx**函式。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

呼叫中重複使用此計算內容[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>設定計算內容，明確地使用 rx_set_compute_context

此函式[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)可讓您切換計算已定義的內容。

設定之後使用中的計算內容，您可以變更它之前維持作用中。

### <a name="using-parallel-processing-and-streaming"></a>使用平行處理和串流處理

當您定義計算內容時，您也可以設定參數可控制如何處理資料的計算內容。 這些參數是根據資料來源類型而有所不同。

SQL Server 計算內容，您可以設定批次大小，或提供有關要用於執行工作的平行處理原則程度的提示。

+ 具有四個處理器的電腦上執行範例，已因此`num_tasks`參數設為允許最大值使用的資源時為 4。 
+ 如果您設定此值為 0 時，SQL Server 會使用預設值，也就是盡可能，伺服器目前的 MAXDOP 設定平行執行多個工作。 不過，確切的可能配置的工作數目會取決於許多其他因素，例如伺服器設定，並執行其他作業。

## <a name="next-steps"></a>後續步驟

這些其他的 Python 範例和教學課程示範如何使用更複雜的資料來源，以及使用遠端計算內容的端對端案例。

+ [適用於 SQL 開發人員的資料庫內 Python](sqldev-in-database-python-for-sql-developers.md)
+ [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
