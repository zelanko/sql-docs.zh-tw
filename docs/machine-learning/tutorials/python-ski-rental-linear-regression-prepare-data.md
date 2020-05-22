---
title: Python 教學課程：準備資料
titleSuffix: SQL machine learning
description: 在本教學課程系列的第二部分 (總共四個部分) 中，您將會使用 Python 搭配 SQL 機器學習服務，來準備資料以預測雪橇租賃。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 75f475f8a2b4b0d23d95498a69f5e5d745f7510d
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606720"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-with-sql-machine-learning"></a>Python 教學課程：準備資料以使用 SQL 機器學習來定型線性迴歸模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在本教學課程系列的第二部分 (總共四個部分) 中，您將使用 Python 準備資料庫中的資料。 在本系列稍後，您將使用此資料搭配 SQL Server 機器學習服務，在 Python 中定型和部署線性迴歸模型，或在巨量資料叢集上進行此定型和部署。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在本教學課程系列的第二部分 (總共四個部分) 中，您將使用 Python 準備資料庫中的資料。 在本系列稍後，您將使用 SQL Server 機器學習服務，在 Python 中定型和部署線性迴歸模型。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 將 SQL Server 資料庫的資料載入到 **pandas** 資料框架
> * 透過移除一些資料行來準備 Python 中的資料

在[第一部分](python-ski-rental-linear-regression.md)，您已了解如何還原範例資料庫。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，您將了解如何在 Python 中定型線性迴歸機器學習模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，您將了解如何將模型儲存在資料庫中，然後從您在第二和第三部分中開發的 Python 指令碼建立預存程序。 預存程序將會在伺服器上中執行，以根據新資料進行預測。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程的第二部分會假設您已完成[第一部分](python-ski-rental-linear-regression.md)及其必要條件。

## <a name="explore-and-prepare-the-data"></a>探索和準備資料

為了使用 Python 中的資料，請將資料庫中的資料載入到 pandas 資料框架。

在 Azure Data Studio 中建立新的 Python 筆記本，並執行以下指令碼。 以您自己的 SQL Server 名稱取代 `<SQL Server>`。

下列 Python 指令碼會將資料集從資料庫中的 **dbo. rental_data** 資料表，匯入到 pandas 資料框架 **df**。

在連接字串中，視需要取代連線詳細資料。

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<SQL Server>; DATABASE=TutorialDB; Trusted_Connection=yes')

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

您應該會看見如下所示的結果。

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第二部分中，您已完成下列步驟：

* 將資料庫中的資料載入至 **pandas** 資料框架
* 透過移除一些資料行來準備 Python 中的資料

若要使用 TutorialDB 資料庫中的資料定型機器學習模型，請遵循此教學課程系列的第三部分：

> [!div class="nextstepaction"]
> [Python 教學課程：定型線性迴歸模型](python-ski-rental-linear-regression-train-model.md)