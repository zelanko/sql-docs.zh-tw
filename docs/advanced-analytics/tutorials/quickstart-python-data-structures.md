---
title: 在 Python 中使用資料結構的快速入門
description: 在 SQL Server 的 Python 腳本快速入門中, 瞭解如何搭配 sp_execute_external_script 系統預存程式來使用資料結構。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 13fb37bee355ce1d379d8348734293baaeb481d8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714805"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>快速入門：SQL Server 中的 Python 資料結構
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何在 SQL Server Machine Learning 服務中使用 Python 時, 使用資料結構。

SQL Server 依賴 Python **pandas**套件, 這非常適合用來處理表格式資料。 不過, 您無法將純量從 Python 傳遞至 SQL Server, 並預期它「只是工作」。 在本快速入門中, 我們將探討一些基本的資料類型定義, 以準備您在 Python 和 SQL Server 之間傳遞表格式資料時, 可能會遇到的其他問題。

+ 資料框架是包含_多個_資料行的資料表。
+ 資料框架的單一資料行是一種類似清單的物件, 稱為「數列」 (Series)。
+ 單一值是資料框架的儲存格, 必須由 index 呼叫。

如果資料框架需要表格式結構, 您要如何將計算的單一結果公開為數據框架？ 其中一個答案是以數列的形式來表示單一純量值, 這可以輕鬆地轉換成資料框架。 

## <a name="prerequisites"></a>先決條件

先前的快速入門中, 請[確認 Python 存在於 SQL Server](quickstart-python-verify.md)中, 提供設定本快速入門所需之 python 環境的相關資訊和連結。

## <a name="scalar-value-as-a-series"></a>以純量值作為數列

這個範例會執行一些簡單的數學運算, 並將純量轉換成數列。

1. 數列需要索引, 您可以手動指派, 如這裡所示, 或以程式設計方式指派。

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

2. 因為數列尚未轉換成資料框架, 所以這些值會在 [訊息] 視窗中傳回, 但是您可以看到結果是以更表格式的格式顯示。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 若要增加數列的長度, 您可以使用陣列來加入新的值。 

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

    如果您未指定索引, 則會產生值開頭為0且結尾為數組長度的索引。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 如果您增加**索引**值的數目, 但不加入新的**資料**值, 則會重復資料值來填滿數列。

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

## <a name="convert-series-to-data-frame"></a>將數列轉換成資料框架

將純量數學運算結果轉換成表格式結構, 我們仍然需要將它們轉換成 SQL Server 可以處理的格式。 

1. 若要將數列轉換成資料框架, 請呼叫 pandas[資料框架](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 結果如下所示。 即使您使用索引來取得資料中的特定值, 索引值也不是輸出的一部分。

    **結果**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>將值輸出至資料框架

讓我們看看如何轉換成資料。框架會與我們的兩個包含簡單數學運算結果的數列搭配運作。 第一個具有由 Python 產生之順序值的索引。 第二個使用字串值的任意索引。

1. 這個範例會從序列中取得使用整數索引的值。

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

    請記住, 自動產生的索引會從0開始。 請嘗試使用超出範圍的索引值, 並查看會發生什麼事。

2. 現在讓我們從另一個具有字串索引的資料框架取得單一值。 

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

    如果您嘗試使用數值索引來取得此數列中的值, 就會收到錯誤。

## <a name="next-steps"></a>後續步驟

接下來, 您將在 SQL Server 中使用 Python 建立預測模型。

> [!div class="nextstepaction"]
> [在 SQL Server 中使用預存程式來建立、定型和使用 Python 模型](quickstart-python-train-score-in-tsql.md)