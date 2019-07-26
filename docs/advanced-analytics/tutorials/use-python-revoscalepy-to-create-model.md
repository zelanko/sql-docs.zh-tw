---
title: 使用 Python 搭配 revoscalepy 來建立模型
description: 使用 revoscalepy 函數撰寫 Python 腳本, 以建立在 SQL Server 遠端執行的資料科學模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 11a155a9c679a18fefc7b3c91434a0ca241c23f7
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468510"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>使用 Python 搭配 revoscalepy 來建立可在 SQL Server 上遠端執行的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

來自 Microsoft 的[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 程式庫提供資料科學演算法, 以進行資料探索、視覺化、轉換和分析。 在 SQL Server 的 Python 整合案例中, 此程式庫具有策略性的重要性。 在多核心伺服器上, **revoscalepy**函數可以平行執行。 在中央伺服器和用戶端工作站 (個別的實體電腦, 全都擁有相同的**revoscalepy**程式庫) 的分散式架構中, 您可以撰寫在本機啟動的 Python 程式碼, 然後將執行轉移至遠端 SQL Server 實例資料所在的位置。

您可以在下列 Microsoft 產品和發行版本中找到**revoscalepy** :

+ [SQL Server Machine Learning 服務 (資料庫內)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (非 SQL、獨立伺服器)](https://docs.microsoft.com/machine-learning-server/index)
+ [用戶端 Python 程式庫 (適用于開發工作站)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

此練習示範如何根據[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)建立線性回歸模型, 這是**revoscalepy**中可接受計算內容做為輸入的演算法之一。 您將在此練習中執行的程式碼會將程式碼執行從本機移至遠端運算環境, 並由啟用遠端計算內容的**revoscalepy**功能啟用。

完成本教學課程後, 您將瞭解如何:

> [!div class="checklist"]
> * 使用**revoscalepy**建立線性模型
> * 從本機到遠端計算內容的移位作業

## <a name="prerequisites"></a>先決條件

此練習中使用的範例資料是[**flightdata.csv**](demo-data-airlinedemo-in-sql.md)資料庫。

您需要 IDE 才能執行本文中的範例程式碼, 而 IDE 必須連結至 Python 可執行檔。

若要練習計算內容轉移, 您需要[本機工作站](../python/setup-python-client-tools-sql.md)和 SQL Server 資料庫引擎實例, 並啟用[Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)和 Python。 

> [!Tip]
> 如果您沒有兩部電腦, 您可以藉由安裝相關的應用程式, 在一部實體電腦上模擬遠端計算內容。 首先, [SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)的安裝會以「遠端」實例的形式運作。 第二, 安裝[Python 用戶端程式庫](../python/setup-python-client-tools-sql.md)會以用戶端的身分運作。 相同的電腦上會有兩份相同的 Python 散發套件和 Microsoft Python 程式庫。 您必須追蹤檔案路徑, 以及您用來順利完成練習的 Python 複本。

## <a name="remote-compute-contexts-and-revoscalepy"></a>遠端計算內容和 revoscalepy

這個範例示範在遠端計算內容中建立 Python 模型的程式, 這可讓您從用戶端工作, 但選擇遠端環境, 例如 SQL Server、Spark 或 Machine Learning Server, 這是實際執行作業的位置。 遠端計算內容的目標是要將計算帶入資料所在的位置。

若要在 SQL Server 中執行 Python 程式碼, 必須要有**revoscalepy**套件。 這是 Microsoft 所提供的特殊 Python 套件, 類似于 R 語言的**RevoScaleR**套件。 **Revoscalepy**套件支援建立計算內容, 並提供在本機工作站與遠端伺服器之間傳遞資料和模型的基礎結構。 支援資料庫內程式碼執行的**revoscalepy**函數是[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在這一課, 您會使用 SQL Server 中的資料來定型以[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)為基礎的線性模型, 這是**revoscalepy**中支援非常大型資料集之回歸的函式。 

本課程也會示範如何在 Python 中設定及使用**SQL Server 計算內容**的基本概念。 如需計算內容如何與其他平臺搭配使用, 以及支援哪些計算內容的討論, 請參閱[Machine Learning Server 中腳本執行的計算內容](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。


## <a name="run-the-sample-code"></a>執行範例程式碼

在您備妥資料庫並將定型資料儲存在資料表中之後, 請開啟 Python 開發環境並執行程式碼範例。

此程式碼會執行下列步驟:

1. 匯入必要的程式庫和函式。
2. 建立 SQL Server 的連接。 建立用來處理資料的**資料來源**物件。
3. 使用**轉換**來修改資料, 使其可供羅吉斯回歸演算法使用。
4. 呼叫`rx_lin_mod`並定義用來配合模型的公式。
5. 根據原始資料產生一組預測。
6. 根據預測的值建立摘要。

所有作業都是使用 SQL Server 的實例作為計算內容來執行。

> [!NOTE]
> 如需從命令列執行此範例的示範, 請參閱這段影片:[SQL Server 2017 使用 Python 的先進分析](https://www.youtube.com/watch?v=FcoY795jTcc)

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

資料來源與計算內容不同。 *資料來源*會定義您的程式碼中所使用的資料。 計算內容會定義執行程式碼的位置。 不過, 它們會使用一些相同的資訊:

+ Python 變數 (例如`sql_query`和`sql_connection_string`) 會定義資料的來源。 

    將這些變數傳遞至[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)的函式, 以執行名為`data_source`的**資料來源物件**。

+ 您可以使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)的函式來建立**計算內容物件**。 產生的**計算內容物件**命名`sql_cc`為。

    這個範例會重新使用您在資料來源中使用的相同連接字串, 假設資料位於您將用來做為計算內容的相同 SQL Server 實例上。 
    
    不過, 資料來源和計算內容可能會在不同的伺服器上。
 
### <a name="changing-compute-contexts"></a>變更計算內容

定義計算內容之後, 您必須設定使用中的**計算內容**。 

根據預設, 大部分的作業都是在本機執行, 這表示如果您未指定不同的計算內容, 則會從資料來源提取資料, 而程式碼會在您目前的 Python 環境中執行。

有兩種方式可以設定使用中的計算內容:
+ 做為方法或函數的引數
+ 藉由呼叫`rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>將計算內容設定為方法或函數的引數

在此範例中, 您會使用個別**rx**函數的引數來設定計算內容。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

此計算內容會在[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)的呼叫中重複使用:

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>使用 rx_set_compute_coNtext 明確設定計算內容

函數[rx_set_compute_coNtext](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)可讓您在已定義的計算內容之間切換。

設定使用中的計算內容之後, 它會保持作用中狀態, 直到您變更為止。

### <a name="using-parallel-processing-and-streaming"></a>使用平行處理和串流

當您定義計算內容時, 您也可以設定參數來控制計算內容處理資料的方式。 這些參數會因數據源類型而有所不同。

針對 SQL Server 計算內容, 您可以設定批次大小, 或提供有關執行中工作所使用之平行處理原則程度的提示。

+ 此範例是在具有四個處理器的電腦上執行, `num_tasks`因此參數會設定為 4, 以允許資源的最大使用量。 
+ 如果您將此值設定為 0, SQL Server 會使用預設值, 也就是在伺服器目前的 MAXDOP 設定之下, 盡可能平行執行許多工作。 不過, 可能配置的確切工作數目取決於許多其他因素, 例如伺服器設定和其他正在執行的作業。

## <a name="next-steps"></a>後續步驟

這些額外的 Python 範例和教學課程會示範使用更複雜資料來源的端對端案例, 以及使用遠端計算內容。

+ [適用于 SQL 開發人員的資料庫內 Python](sqldev-in-database-python-for-sql-developers.md)
+ [使用 Python 和 SQL Server 建立預測模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
