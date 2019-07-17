---
title: 使用 Python-SQL Server Machine Learning 中的資料結構的快速入門
description: 在本快速入門中的 Python 指令碼，在 SQL Server 中，了解如何使用資料結構 sp_execute_external_script 的系統預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962085"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>快速入門：SQL Server 中的 Python 資料結構
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入門示範如何使用 Python 中 SQL Server Machine Learning 服務時，資料結構。

SQL Server 背後的 Python **pandas**套件，這也很適合使用表格式資料。 不過，您無法從 Python 中將 SQL Server 的純量，並預期它 「 只是工作 」。 在本快速入門中，我們將檢閱一些基本資料型別定義，若要準備您的 Python 和 SQL Server 之間傳遞的表格式資料時，可能發生的其他問題。

+ 為資料框架是使用資料表_多個_資料行。
+ 單一資料行的資料框架是呼叫一系列的類似清單中的物件。
+ 單一的值是資料框架的資料格，而且必須由索引呼叫。

如何會您公開 （expose) 單一的結果做為資料框架中，計算的如果 data.frame 需要表格式結構？ 答案是代表單一純量值為一系列，輕鬆地轉換成資料框架。 

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 Python 存在於 SQL Server](quickstart-python-verify.md)，提供資訊並連結設定本快速入門所需的 Python 環境。

## <a name="scalar-value-as-a-series"></a>以一系列的純量值

此範例沒有簡單的運算，並將轉換成一系列的純量。

1. 一系列需要索引，以便您可以指派以手動方式，如此處所示，或以程式設計的方式。

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

## <a name="convert-series-to-data-frame"></a>將序列轉換成資料框架

我們需要轉換成表格式結構時我們純量的數學運算的結果，仍然需要將它們轉換成 SQL Server 可以處理的格式。 

1. 若要將一系列轉換成 data.frame，呼叫 pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 結果如下所示。 即使您使用索引來從 data.frame 取得特定的值時，索引值不是輸出的一部分。

    **結果**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Data.frame 輸出值

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

## <a name="next-steps"></a>後續步驟

接下來，您將建置預測模型，在 SQL Server 中使用 Python。

> [!div class="nextstepaction"]
> [建立、 定型和使用 SQL Server 中的預存程序中的 Python 模型](quickstart-python-train-score-in-tsql.md)