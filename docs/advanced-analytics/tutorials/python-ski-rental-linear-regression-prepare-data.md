---
title: Python 教學課程:準備資料 (線性回歸)
description: 在本教學課程中, 您將在 SQL Server Machine Learning 服務中使用 Python 和線性回歸, 以預測 ski 租用的數目。 您將使用 Python, 從 SQL Server 資料庫準備資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242496"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教學課程:準備資料以在 SQL Server Machine Learning 服務中定型線性回歸模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分教學課程系列的第二部分中, 您將使用 Python, 從 SQL Server 資料庫準備資料。 稍後在此系列中, 您將使用這項資料, 以 SQL Server Machine Learning 服務來定型和部署 Python 中的線性回歸模型。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 將資料從 SQL Server 資料庫載入**pandas**資料框架中
> * 藉由移除一些資料行來準備 Python 中的資料

在[第一部](python-ski-rental-linear-regression.md)中, 您已瞭解如何還原範例資料庫。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中, 您將瞭解如何在 Python 中訓練線性回歸機器學習模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中, 您將瞭解如何將模型儲存至 SQL Server, 然後從您在第二部和第三部分所開發的 Python 腳本中建立預存程式。 預存程式將會在 SQL Server 中執行, 以根據新的資料進行預測。

## <a name="prerequisites"></a>必要條件

* 本教學課程的第二部分假設您已完成[第一部分](python-ski-rental-linear-regression.md)和其必要條件。

## <a name="explore-and-prepare-the-data"></a>探索和準備資料

若要在 Python 中使用資料, 您會將 SQL Server 資料庫中的資料載入至 pandas 資料框架。

在 Azure Data Studio 中建立新的 Python 筆記本, 然後執行下列腳本。 以`<SQL Server>`您自己的 SQL Server 名稱取代。

下列 Python 腳本會將資料集從資料庫中的**rental_data**資料表匯入 pandas 資料框架**df**。

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

您應該會看到類似下面的結果。

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第二部分中, 您已完成下列步驟:

* 將資料從 SQL Server 資料庫載入**pandas**資料框架中
* 藉由移除一些資料行來準備 Python 中的資料

若要將機器學習模型定型, 以使用 TutorialDB 資料庫中的資料, 請遵循本教學課程系列的第三部分:

> [!div class="nextstepaction"]
> [Python 教學課程:訓練線性回歸模型](python-ski-rental-linear-regression-train-model.md)