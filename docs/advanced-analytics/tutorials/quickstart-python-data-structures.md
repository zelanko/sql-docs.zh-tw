---
title: 快速入門：Python 資料類型
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入門中，了解如何使用具有 SQL Server 機器學習服務的 Python 和 SQL Server 中的資料類型和資料物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1bac339105acdb7318b29426cd0bb4afdc2481e7
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727014"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>快速入門：在 SQL Server 機器學習服務中使用 Python 處理資料類型和物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何在 SQL Server 機器學習服務中使用 Python 時，使用資料結構。

SQL Server 依賴 Python **pandas** 套件，這非常適合用來處理表格式資料。 不過，您無法將純量從 Python 傳遞至 SQL Server，並預期它「能正常工作」。 在本快速入門中，您將會複習一些基本資料類型定義，讓您能夠針對在 Python 和 SQL Server 之間傳遞表格式資料時可能會遇到的其他問題做好準備。

首先要了解的概念包括：

- 資料框架是具有_多個_資料行的資料表。
- 資料框架的單一資料行是一種類似清單的物件，稱為「序列」。
- 資料框架的單一值稱為儲存格，並依索引存取。

如果 data.frame 需要表格式結構，您該如何將計算的單一結果公開為資料框架？ 答案是以序列形式來表示單一純量值，便可以輕鬆地轉換成資料框架。 

> [!NOTE]
> 傳回日期時，SQL 中的 Python 會使用 DATETIME，其日期範圍限制在 1753-01-01 (-53690) 到 9999-12-31 (2958463) 之間。 

## <a name="prerequisites"></a>Prerequisites

- 本快速入門需使用已安裝 Python 語言的 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)來存取 SQL Server 的執行個體。

- 您也需要工具來執行包含 Python 指令碼的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些指令碼，只要該工具可以連線到 SQL Server 執行個體，並執行 T-SQL 查詢或預存程序即可。 本快速入門使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="scalar-value-as-a-series"></a>以純量值作為序列

這個範例會執行一些簡單的數學運算，並將純量轉換成序列。

1. 序列需要索引，您可以手動指派 (如本文所示)，或以程式設計方式指派。

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

   因為序列尚未轉換成資料框架，所以這些值會在 [訊息] 視窗中傳回，但是您會看到結果更進一步以表格式格式顯示。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 若要增加序列的長度，您可以使用陣列來加入新的值。 

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

   如果您未指定索引，則會產生值開頭為 0 且結尾為陣列長度的索引。

   **結果**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. 如果您增加**索引**值的數目，但不新增新的**資料**值，則系統會重複資料值來填滿序列。

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

## <a name="convert-series-to-data-frame"></a>將序列轉換成資料框架

將純量數學運算結果轉換成表格式結構之後，您仍必須將它們轉換成 SQL Server 可以處理的格式。

1. 若要將數列轉換成 data.frame，請呼叫 pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) \(英文\) 方法。

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

   結果如下所示。 即使您使用索引來取得 data.frame 中的特定值，索引值也不是輸出的一部分。

   **結果**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>將值輸出至 data.frame

現在您會從 data.frame 中兩個數學運算結果序列輸出特定的值。 第一個具有由 Python 產生之循序值的索引。 第二個使用字串值的任意索引。

1. 下列範例會使用整數索引來取得序列中的值。

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

   請記住，自動產生的索引會從 0 開始。 請嘗試使用超出範圍的索引值，並查看會發生什麼事。

1. 現在使用字串索引從另一個資料框架取得單一值。

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

   如果您嘗試使用數值索引來取得此序列中的值，就會發生錯誤。

## <a name="next-steps"></a>後續步驟

若要了解如何在 SQL Server 中撰寫進階 Python 函式，請遵循此快速入門：

> [!div class="nextstepaction"]
> [使用 SQL Server 機器學習服務撰寫進階 Python 函數](quickstart-python-functions.md)

如需在 SQL Server 機器學習服務中使用 Python 的詳細資訊，請參閱下列文章：

- [在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md)
- [什麼是 SQL Server 機器學習服務 (Python 和 R)？](../what-is-sql-server-machine-learning.md)
