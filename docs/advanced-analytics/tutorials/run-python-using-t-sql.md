---
title: 執行 T-SQL 的 SQL Server 上使用 Python |Microsoft Docs
description: 了解執行 Python 整合已啟用的 SQL Server database engine 執行個體上使用 T-SQL 和預存程序的 Python 程式碼的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3b4a7987a0fc9d50bbc5c8803d741be13acf7433
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050891"
---
# <a name="run-python-using-t-sql"></a>使用 T-SQL 執行 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何執行 Python 程式碼，以及在 SQL Server 2017 中。 它會引導您透過 SQL Server 與 Python 之間移動資料的基本概念： 需求、 資料結構、 輸入和輸出。 它也會說明如何將格式正確的 Python 程式碼包裝在預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來建置、 定型和使用 SQL Server 中的機器學習服務模型。

## <a name="prerequisites"></a>先決條件

若要執行這些練習的範例程式碼，必須先安裝 SQL Server 2017 並啟用執行個體上的 Machine Learning 服務中所述[安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)。 

您也應該安裝[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 或者，您可以使用其他的資料庫管理或查詢工具，只要它可以連接到伺服器和資料庫，並執行 T-SQL 查詢或預存程序。

您的環境準備就緒時，返回此頁面，即可了解如何在預存程序的內容中執行 Python 程式碼。 

## <a name="verify-python-exists"></a>請確認有 Python

下列步驟確認 Python 已啟用，而且 SQL Server Launchpad 服務正在執行。

1. 請檢查資料庫引擎執行個體上是否已安裝 Python 整合。 您應該會發現**python.exe**中名為的資料夾**PYTHON_SERVICES**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\. 這是 SQL Server 用來執行 Python 程式碼的 Python 可執行檔。

2. 請檢查是否已啟用外部指令碼。 在 Management Studio 中，執行下列陳述式：

    ```sql
    sp_configure 'external scripts enabled'
    ```

    如果**run_value**為 1，機器學習功能已安裝且可供使用。

    常見錯誤的原因，在於[SQL Server Launchpad 服務](../concepts/extensibility-framework.md#launchpad)，其可管理 SQL Server 與 Python 之間的通訊已停止。 您也可以使用 Windows 來檢視 「 啟動控制板狀態**Services** ] 面板中，或藉由開啟 [SQL Server 組態管理員。 如果服務已停止，請將它重新啟動。

3. 確認 Python 執行階段使用且與 SQL Server 通訊。 若要這樣做，請開啟 [新**查詢**在 SQL Server Management Studio] 視窗，並連接到已安裝 Python 的執行個體。

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    如果一切正常，您應該會看到與下列類似的結果訊息

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 如果您收到錯誤，有各種您可以如何確保可以通訊的伺服器和 Python 的項目。 

    您必須加入 Windows 使用者群組`SQLRUserGroup`做為登入執行個體，以確定 Launchpad 可提供 Python 和 SQL Server 之間的通訊上。 （相同的群組會用於這兩個 R 和 Python 程式碼執行）。如需詳細資訊，請參閱 <<c0> [ 已啟用隱含的驗證](../security/add-sqlrusergroup-to-database.md)。
    
    此外，您可能需要啟用網路通訊協定已停用，或開啟防火牆，以便 SQL Server 可與外部用戶端通訊。 如需詳細資訊，請參閱 <<c0> [ 疑難排解安裝](../common-issues-external-script-execution.md)。

### <a name="call-revoscalepy-functions"></a>呼叫 revoscalepy 函式

若要確認**revoscalepy**可供使用，執行包含的指令碼[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)產生統計摘要資料。 此指令碼會示範如何從內建的範例包含在 revoscalepy 擷取範例.xdf 資料檔案。 RxOptions 函式會提供**sampleDataDir**傳回的範例檔案位置的參數。

因為 rx_summary 傳回型別的物件`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多個項目，您可以使用 pandas 資料框架以表格格式中擷取。

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="basic-python-interaction"></a>Python 的基本互動

有兩種方式可在 SQL Server 中執行 Python 程式碼：

+ 做為引數的系統預存程序中，新增 Python 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 從[遠端 Python 用戶端](../python/setup-python-client-tools-sql.md)、 連接到 SQL Server 和執行程式碼使用 SQL Server 作為計算內容。 這需要[revoscalepy](../python/what-is-revoscalepy.md)。

下列練習著重於第一次的互動模型： 如何將 Python 程式碼傳遞至預存程序。

1. 執行一些簡單的程式碼，以查看資料的 SQL Server 與 Python 之間的來回傳遞方式。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. 假設您有正確設定的所有項目，以及 Python 和 SQL Server 與彼此通訊，正確的結果計算，和 Python`print`函式會傳回結果**訊息**windows。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    取得時發生**stdout**測試您的程式碼時，訊息是好用，通常您需要以表格式格式傳回結果，以便您可以在應用程式中使用它，或寫入資料表。 

現在，請記住這些規則：

+ 所有東西放在`@script`引數必須是有效的 Python 程式碼。 
+ 程式碼必須遵循有關縮排、 變數名稱，以及其他等等的所有 Python 規則。 當您收到錯誤時，請檢查您的泛空白字元和大小寫。
+ 如果您使用預設不會載入任何程式庫，您必須在您的指令碼開頭使用匯入陳述式，載入它們。 SQL Server 將新增多個產品專屬程式庫。 如需詳細資訊，請參閱 < [Python 程式庫](../python/python-libraries-and-data-types.md)。
+ 如果尚未安裝的程式庫，停止，並安裝 SQL Server 外部 Python 套件，如下所示： [SQL Server 上安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>[指令碼轉換編輯器]

根據預設， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受單一輸入資料集，這通常是您提供有效的 SQL 查詢的形式。 

其他類型的輸入可以當做 SQL 變數： 比方說，您可以傳遞定型的模型為變數，例如使用序列化函式[pickle](https://docs.python.org/3.0/library/pickle.html)或是[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中撰寫模型二進位格式。

預存程序傳回單一的 Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html)資料框架做為輸出，但您也可以輸出純量和做為變數的模型。 例如，您可以輸出定型的模型，做為二進位的變數，並將它傳遞至 T-SQL INSERT 陳述式，以寫入該模型的資料表。 您也可以產生繪圖 （以二進位格式） 或純量 （個別的值，例如日期和時間，所經過的時間來定型模型，等等）。

現在，讓我們看看只是預設的 sp_execute_external_script 的輸入和輸出變數：`InputDataSet`和`OutputDataSet`。 

1. 執行下列程式碼，執行一些計算，並將結果輸出。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    OutputDataSet = c
    '
    WITH RESULT SETS ((ResultValue float))
    ```

2. 您應該先取得發生錯誤，因為 Python 程式碼會產生純量，而不是資料框架。

    **結果**

    ```text
    line 43, in transform
        raise TypeError('OutputDataSet should be of type pandas.DataFrame')
    ```

3. 現在可以看到當您傳遞的表格式資料集的 python，使用預設輸入的變數時，會發生什麼事`InputDataSet`。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    預存程序傳回 data.frame 自動執行，而不必執行任何額外的 Python 程式碼的動作。

    **結果**

    | 沒有 columnname|
    |------|
    | 1|

    根據預設，單一的表格式輸入資料集的名稱， `InputDataSet`。 不過，您可以變更該名稱，加上類似這行： `@input_data_1_name = N'myResultName'`。

    使用 Python 的資料行名稱會永遠不會保留在輸出中。 雖然輸入的查詢指定的資料行名稱`Col1`，不會傳回該名稱，也不會使用您的 Python 指令碼的任何資料行標題。 當您將資料傳回至 SQL Server，請指定資料行名稱和資料類型，請使用 T-SQL`WITH RESULT SETS`子句。

4. 此範例中提供新名稱的輸入和輸出的變數。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    使用結果集子句會定義輸出的結構描述因為 Python 資料行名稱永遠不會傳回與 data.frame。

    **結果**

    | ResultValue|
    |------|
    | 1|

5. 現在讓我們看看一般的 Python 時發生錯誤。 變更從上一個範例中的一行`@input_data_1_name = N'MyInput'`至`@input_data_1_name = N'myinput'`。

    Python 錯誤會傳遞至您的訊息，由 SQL Server 所使用的附屬服務。 訊息可以很長，且包含 SQL Server 錯誤或 Launchpad 錯誤除了 Python 錯誤，因此請耐心等候挖掘的文字。 主要訊息是在這一行：

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    請記住，例如 R、 Python 是區分大小寫。 因此，當您收到任何一種錯誤，請務必檢查您的變數名稱，並尋找的間距和縮排，以及資料類型問題。

## <a name="python-data-structures"></a>Python 資料結構

SQL Server 背後的 Python **pandas**套件，這也很適合使用表格式資料。 不過，您所見，您無法從 Python 中將 SQL Server 的純量，並且預期它 「 只是工作 」。 在本節中，我們將檢閱一些基本資料型別定義，若要準備您的 Python 和 SQL Server 之間傳遞的表格式資料時，可能發生的其他問題。

+ 為資料框架是使用資料表_多個_資料行。
+ 單一資料行的資料框架是呼叫一系列的類似清單中的物件。
+ 單一的值是資料框架的資料格，而且必須由索引呼叫。

到底會您公開 （expose) 單一的結果做為資料框架中，計算的如果 data.frame 需要表格式結構？ 答案是代表單一純量值為一系列，輕鬆地轉換成資料框架。 

1. 此範例沒有簡單的運算，並將轉換成一系列的純量。 一系列需要索引，以便您可以指派以手動方式，如此處所示，或以程式設計的方式。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. 因為數列尚未被轉換成 data.frame，會在訊息視窗中，傳回的值，但您可以看到結果會以更表格。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 若要增加序列的長度，您可以加入新的值，使用陣列。 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    如果您未指定的索引，索引會產生具有值從 0 開始和結尾陣列的長度。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 如果您增加的數目**索引**值，但不要加上新**資料**值、 資料值會重複來填滿數列。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    '
    ```

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    simple math example 2    0.5
    dtype: float64
    ```

### <a name="convert-series-to-data-frame"></a>將序列轉換成資料框架

我們需要轉換成表格式結構時我們純量的數學運算的結果，仍然需要將它們轉換成 SQL Server 可以處理的格式。 

1. 若要將一系列轉換成 data.frame，呼叫 pandas [DataFrame](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s)
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

2. 請注意索引值不是輸出中，即使您使用索引來從 data.frame 取得特定的值。

    **結果**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>使用索引的 data.frame 輸出值

我們來看看如何轉換成 data.frame 搭配兩個系列包含簡單的數學運算的結果。 第一個具有 Python 所產生的順序值的索引。 第二個會使用任意字串值的索引。

1. 此範例會取得值，從使用整數索引的數列。

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    請記住，自動產生索引 0 開始。 請嘗試使用超出範圍的索引值，並看看結果如何。

2. 現在讓我們從其他具有字串索引的資料框架中取得單一值。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **結果**

    |ResultValue|
    |------|
    |0.5|

    如果您嘗試使用數值索引取得值，此系列中，您會收到錯誤。

此練習是要用來讓您了解如何使用不同的 Python 資料結構，並確保您取得正確的結果做為資料框架。 您可能會因為資料框架是麻煩，值得比該輸出的單一值完成 ！ 幸運的是，您可以輕鬆地傳遞所有種類的流入和流出預存程序的值做為變數中。 這涵蓋在下一課。

## <a name="tips"></a>提示

+ 在程式設計語言，Python 是其中一個最具彈性方面單引號與雙引號括住;它們幾乎可以互換。 

    不過，T-SQL 會使用單引號來某些事，而`@script`引數會使用單引號來括住的 Unicode 字串的 Python 程式碼。 因此，您可能需要檢閱您的 Python 程式碼，並將一些單引號變更為雙引號括住。

+ 找不到預存程序中，`sp_execute_external_script`嗎？ 這表示您可能尚未完成設定要支援外部指令碼執行的執行個體。 執行 SQL Server 2017 安裝程式，並選取 Python 作為機器學習語言之後, 您必須明確地啟用功能使用`sp_configure`，然後重新啟動執行個體。 

    如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)。

## <a name="next-steps"></a>後續步驟

[設定鳶尾花示範資料集](demo-data-iris-in-sql.md)