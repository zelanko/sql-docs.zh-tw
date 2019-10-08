---
title: 使用 Python 和 SQL 資料類型和物件
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入門中，瞭解如何使用 Python 中的資料類型和資料物件，以及 SQL Server Machine Learning 服務的 SQL Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 06540305d84ea16b76363ebb21cea0a246fd9ed8
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006055"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>快速入門：在 SQL Server Machine Learning 服務中使用 Python 處理資料類型和物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何在 SQL Server Machine Learning 服務中使用 Python 時，使用資料結構。

SQL Server 依賴 Python **pandas**套件，這非常適合用來處理表格式資料。 不過，您無法將純量從 Python 傳遞至 SQL Server，並預期它「只是工作」。 在本快速入門中，您將會複習一些基本的資料類型定義，以準備您在 Python 和 SQL Server 之間傳遞表格式資料時，可能會遇到的其他問題。

事先瞭解的概念包括：

- 資料框架是包含_多個_資料行的資料表。
- 資料框架的單一資料行是一種類似清單的物件，稱為「數列」（series）。
- 資料框架的單一值稱為儲存格，並依索引存取。

如果資料框架需要表格式結構，您要如何將計算的單一結果公開為數據框架？ 其中一個答案是以數列的形式來表示單一純量值，這可以輕鬆地轉換成資料框架。 

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 Python 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

- 您也需要工具來執行包含 Python 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="scalar-value-as-a-series"></a>以純量值作為數列

這個範例會執行一些簡單的數學運算，並將純量轉換成數列。

1. 數列需要索引，您可以手動指派，如這裡所示，或以程式設計方式指派。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   因為數列尚未轉換成資料框架，所以這些值會在 [訊息] 視窗中傳回，但是您可以看到結果是以更表格式的格式顯示。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 若要增加數列的長度，您可以使用陣列來加入新的值。 

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   如果您未指定索引，則會產生值開頭為0且結尾為數組長度的索引。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. 如果您增加**索引**值的數目，但不加入新的**資料**值，則會重復資料值來填滿數列。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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

將純量運算結果轉換成表格式結構之後，您仍然需要將它們轉換成 SQL Server 可以處理的格式。

1. 若要將數列轉換成資料框架，請呼叫 pandas[資料框架](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   結果如下所示。 即使您使用索引來取得資料中的特定值，索引值也不是輸出的一部分。

   **結果**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>將值輸出至資料框架

現在您會從資料框架中的兩個數學運算結果輸出特定的值。 第一個具有由 Python 產生之順序值的索引。 第二個使用字串值的任意索引。

1. 下列範例會使用整數索引來取得數列中的值。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **結果**

   |ResultValue|
   |------|
   |2.0|

   請記住，自動產生的索引會從0開始。 請嘗試使用超出範圍的索引值，並查看會發生什麼事。

1. 現在使用字串索引，從另一個資料框架取得單一值。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **結果**

   |ResultValue|
   |------|
   |0.5|

   如果您嘗試使用數值索引來取得此數列中的值，就會收到錯誤。

## <a name="next-steps"></a>後續步驟

若要瞭解如何在 SQL Server 中撰寫 advanced Python 函式，請遵循此快速入門：

> [!div class="nextstepaction"]
> [使用 SQL Server Machine Learning 服務撰寫先進的 Python 功能](quickstart-python-functions.md)

如需在 SQL Server Machine Learning 服務中使用 Python 的詳細資訊，請參閱下列文章：

- [在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md)
- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
