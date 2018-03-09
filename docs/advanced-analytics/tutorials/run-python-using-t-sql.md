---
title: "執行 Python 使用 T-SQL |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 5c6145d3af6918a5f3daa954aae5522ffffebb89
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="run-python-using-t-sql"></a>執行 Python 使用 T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本教學課程說明如何執行 Python 程式碼，以及在 SQL Server 2017 中。 它會引導您完成 SQL Server 和 Python 之間移動資料的程序，並說明如何將語式正確的 Python 程式碼包裝在預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)建置、 定型和使用在 SQL 中的機器學習模型伺服器。

## <a name="prerequisites"></a>필수 구성 요소

若要完成本教學課程中，您必須先安裝 SQL Server 2017 並啟用機器學習服務的執行個體中所述[本文](../python/setup-python-machine-learning-services.md)。 

您也應該安裝[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 或者，您可以使用其他的資料庫管理或查詢工具，只要可以連線至伺服器和資料庫，並執行 T-SQL 查詢或預存程序。

在您完成設定之後，請返回這個教學課程中，以了解如何在預存程序的內容中執行 Python 程式碼。 

## <a name="overview"></a>概觀

本教學課程包含四個課程：

+ SQL Server，並將 Python 之間移動資料的基本概念： 了解基本的需求，資料結構、 輸入和輸出。
+ 練習使用 Python 等簡單的工作，範例資料載入預存程序。
+ 若要建立 Python 機器學習模型，使用預存程序，從模型產生分數。
+ 選擇性課程中的使用者想要從遠端用戶端，使用 SQL Server 作為執行 Python_計算內容_。 包含程式碼建立模型。不過，需要您已熟悉 Python 環境和 Python 工具。

這裡會提供其他的 Python 範例特定的 SQL Server 2017: [SQL Server Python 教學課程](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>請確認已啟用 Python，執行 [啟動列]

1. 在 Management Studio 中執行此陳述式，確定已啟用服務。

    ```sql
    sp_configure 'external scripts enabled'
    ```

    如果**run_value**為 1，機器學習功能已安裝且可供使用。

    錯誤的常見原因是 [啟動列]，為您管理 SQL Server，並將 Python 之間的通訊，已停止。 您可以將 啟動列 狀態檢視使用 Windows**服務**面板，或藉由開啟 SQL Server 組態管理員。 如果服務已停止，請將它重新啟動。

2. 接下來，請確認 Python 執行階段使用，且與 SQL Server 通訊。 若要這樣做，請開啟 [新**查詢**在 SQL Server Management Studio] 視窗，並連接到安裝 Python 的執行個體。

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    如果一切正常，您應該會看到與下列類似的結果訊息

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 如果您收到錯誤，有各種項目，您可以以確保伺服器和 Python 可以通訊。 

    您必須新增 Windows 使用者群組`SQLRUserGroup`做為登入執行個體上，以確定 [啟動列] 可提供 Python 和 SQL Server 之間的通訊。 （這兩個使用相同的群組和 Python 程式碼執行）。如需詳細資訊，請參閱[啟用隱含的驗證](../r/add-sqlrusergroup-to-database.md)。
    
    此外，您可能需要啟用網路通訊協定已停用，或開啟防火牆，以便 SQL Server 可以與外部用戶端通訊。 如需詳細資訊，請參閱[疑難排解安裝](../common-issues-external-script-execution.md)。

## <a name="basic-python-interaction"></a>基本的 Python 互動

有兩種方式可在 SQL Server 中執行 Python 程式碼：

+ 做為引數的系統預存程序，新增的 Python 指令碼**sp_execute_external_script**
+ 從遠端的 Python 用戶端，連接到 SQL Server，並執行當成計算內容中使用 SQL Server 程式碼。 這需要[revoscalepy](../python/what-is-revoscalepy.md)。

本教學課程的主要目標是確保您可以在預存程序中使用 Python。

1. 執行一些簡單的程式碼，以查看資料 Python SQL Server 之間的來回傳遞方式。

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

2. 假設您有設定正確的所有項目和 Python 和 SQL Server 會提到彼此，正確的結果計算，並將 Python`print`函式會傳回結果**訊息**windows。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    取得時**stdout**訊息是很方便，測試您的程式碼時，您需要更常表格式格式傳回結果時，讓您可以使用應用程式中，或寫入資料表。 

現在，請記住這些規則：

+ 內的所有項目`@script`引數必須是有效的 Python 程式碼。 
+ 程式碼必須遵循所有 Pythonic 規則縮排、 變數名稱，以及其他等等。 當您取得發生錯誤時，請檢查您的泛空白字元和大小寫。
+ 如果您使用預設不會載入任何文件庫，您必須在您的指令碼開頭使用匯入陳述式將其載入。 
+ 如果尚未安裝的程式庫，停止，而且安裝 SQL Server 外部的 Python 封裝，如這裡所述： [SQL Server 上安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>[指令碼轉換編輯器]

根據預設， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受單一輸入資料集，通常在有效的 SQL 查詢的形式提供。 其他類型的輸入可以當做 SQL 變數傳遞： 例如，您可以將定型的模型當做變數中，使用的序列化函式，例如[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中撰寫模型二進位格式。

預存程序傳回單一的 Python[熊](http://pandas.pydata.org/pandas-docs/stable/index.html)做為輸出資料框架。 不過您可以將輸出的純量與模型做為變數。 比方說，您可以輸出定型的模型做為二進位的變數，並將其傳遞至 T-SQL INSERT 陳述式，將該模型寫入資料表。 您也可以產生繪圖 （以二進位格式） 或純量 （個別的值，例如日期和時間，所經過的時間來定型此模型，等等）。

現在，讓我們來看為預設值輸入和輸出變數`InputDataSet`和`OutputDataSet`。 

1. 執行下列程式碼進行一些運算，並將結果輸出。

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

2. 您應該取得發生錯誤，因為 Python 程式碼會產生純量資料框架。

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. 現在會看到當您將傳遞的表格式資料集至 Python，使用預設輸入的變數，會發生什麼事`InputDataSet`。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    預存程序傳回 data.frame 自動執行，您不必執行任何額外的 Python 程式碼中的動作。

    **結果**

    | 沒有 columnname|
    |------|
    | 1|

    根據預設，單一表格式的輸入資料集的名稱， `InputDataSet`。 不過，您可以變更該名稱將類似這一行加入： `@input_data_1_name = N'myResultName'`。

    在輸出中，將永不保留 Python 所使用的資料行名稱。 雖然輸入的查詢指定的資料行名稱`Col1`，不會傳回該名稱，也不會使用您的 Python 指令碼的任何資料行標題。 若要指定資料行名稱和資料類型，當您將資料傳回至 SQL Server 時，使用 T-SQL`WITH RESULT SETS`子句。

4. 此範例中提供的輸入和輸出變數的新名稱。

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

    與結果集子句定義的結構描述的輸出，因為 Python 資料行名稱永遠不會傳回與 data.frame。

    **結果**

    | ResultValue|
    |------|
    | 1|

5. 現在讓我們看看常見的 Python 錯誤。 從上一個範例中的行`@input_data_1_name = N'MyInput'`至`@input_data_1_name = N'myinput'`。

    Python 錯誤被傳遞給您做為訊息，使用 SQL Server 的附屬項目服務。 訊息可以很長，且包含 SQL Server 錯誤或啟動控制板錯誤除了 Python 錯誤，所以請在文字間挖掘病患。 索引鍵的訊息是在這一行：

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    請記住，像 R、 Python 是區分大小寫。 因此，當您取得任何類型的錯誤時，務必檢查您的變數名稱，並尋找間距、 縮排，與資料類型的問題。

## <a name="python-data-structures"></a>Python 資料結構

SQL Server 依賴 Python**熊**封裝，最適合用於使用表格式資料。 不過，您已經了解您不能用來傳送來自 Python 的純量給 SQL Server，而且預期只運作 」。 在本節中，我們會檢閱一些基本資料型別定義，以準備好將 Python 和 SQL Server 之間的表格式資料時，您可能會執行跨的其他問題。

+ 資料框架是包含的資料表_多個_資料行。
+ 單一資料行的資料框架中，是呼叫一系列的清單類似的物件。
+ 單一的值是資料格的資料框架，而且必須由索引所呼叫。

您如何將公開單一計算結果的成為資料框架，如果 data.frame 需要表格式結構？ 答案是代表單一純量值為一系列，輕鬆地轉換成資料框架。 

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

2. 因為數列尚未轉換成 data.frame 時，會在訊息視窗中，傳回的值，但您可以看到結果會以更表格格式。

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

4. 如果您增加數目**索引**值，但不要加上新**資料**值，資料值會重複來填滿數列。

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

我們具有會將我們純量的數學運算的結果轉換成表格式結構，還是需要將它們轉換成 SQL Server 可以處理的格式。 

1. 若要將一系列轉換成 data.frame，呼叫 熊[資料框架](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 請注意索引值不是輸出，即使您使用索引來從 data.frame 取得特定的值。

    **結果**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>使用索引的 data.frame 輸出值

我們來看看使用我們的兩個數列包含簡單的數學運算的結果轉換成 data.frame 的運作方式。 第一個有 Python 所產生的循序值的索引。 第二個會使用任意字串值的索引。

1. 這個範例會取得值，從序列的整數索引。

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

    請記住，自動產生索引 0 開始。 請嘗試使用超出範圍的索引值，請參閱 會發生什麼事。

2. 現在讓我們從具有字串索引的其他資料框架中取得單一值。 

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

    如果您嘗試使用的數字索引，以取得此系列中的值，您會收到錯誤。

這個練習中，是要用來讓您了解如何使用不同的 Python 資料結構，並確定您得到正確的結果，成為資料框架。 您可能會因為資料框架是多個問題，其價值高於該輸出的單一值得到 ！ 幸運的是，您可以輕鬆地傳遞所有種類的預存程序內外的值做為變數中。 下一個課程涵蓋的。

## <a name="tips"></a>提示

+ 在程式語言之間 Python 是其中一個最有彈性方面單引號與雙引號括住。它們是幾乎可互換。 

    不過，T-SQL 針對會使用單引號某些事，而`@script`引數會使用單引號來括住的 Unicode 字串的 Python 程式碼。 因此，您可能需要檢閱您的 Python 程式碼，並將某些單引號變更為雙引號。

+ 找不到預存程序，`sp_execute_external_script`嗎？ 這表示您可能尚未完成設定要支援外部指令碼執行的執行個體。 執行 SQL Server 2017 安裝程式並選取後 Python 和機器學習語言，您必須同時也可以明確啟用功能使用`sp_configure`，然後重新啟動執行個體。 

    如需詳細資訊，請參閱[安裝程式的機器學習服務使用 Python](../python/setup-python-machine-learning-services.md)。

## <a name="next-steps"></a>後續的步驟

[Python 程式碼包裝在 SQL 預存程序](wrap-python-in-tsql-stored-procedure.md)