---
title: Python 教學課程：部署模型
titleSuffix: SQL machine learning
description: 在本教學課程系列的第四部分 (總共四個部分) 中，您會使用 SQL 機器學習服務，將預測雪橇租賃的 Python 模型部署到資料庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1771cc70a2e5b36109ba028c86939ce66fa00993
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606730"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-with-sql-machine-learning"></a>Python 教學課程：使用 SQL 機器學習部署線性迴歸模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在本教學課程系列的第四部分 (總共四個部分) 中，您將使用機器學習服務或巨量資料叢集，將以 Python 開發的線性迴歸模型部署到 SQL Server 資料庫。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在本教學課程系列的第四部分 (總共四個部分) 中，您將使用機器學習服務，將以 Python 開發的線性迴歸模型部署到 SQL Server 資料庫。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 建立會產生機器學習模型的預存程序
> * 將模型儲存在資料庫資料表中
> * 建立一個使用此模型進行預測的預存程序
> * 以新資料執行模型

在[第一部分](python-ski-rental-linear-regression.md)，您已了解如何還原範例資料庫。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，您已了解如何將資料從資料庫載入到 Python 資料框架，並以 Python 準備資料。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，您已了解如何在 Python 中定型線性迴歸機器學習模型。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程的第四部分會假設您已完成[第一部分](python-ski-rental-linear-regression.md)及其必要條件。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立一個會產生模型的預存程序

現在，使用您所開發的 Python 指令碼建立預存程序 **generate_rental_py_model**，以使用 scikit-learn 的 LinearRegression 來定型及產生線性迴歸模型。

在 Azure Data Studio 中執行下列 T-SQL 陳述式，以建立用來定型模型的預存程序。

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>將模型儲存在資料庫資料表中

在 TutorialDB 資料庫中建立資料表，然後將模型儲存至資料表。

1. 在 Azure Data Studio 中執行下列 T-SQL 陳述式，以建立名為 **dbo.rental_py_models** 的資料表以用於儲存模型。

   ```sql
   USE TutorialDB;
   DROP TABLE IF EXISTS dbo.rental_py_models;
   GO
   CREATE TABLE dbo.rental_py_models (
       model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
       model VARBINARY(MAX) NOT NULL
   );
   GO
   ```

1. 將模型以二進位物件形式儲存至資料表，並將模型命名為 **linear_model**。

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXECUTE generate_rental_py_model @model OUTPUT;
   
   INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
   ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>建立一個進行預測的預存程序

1. 建立預存程序 **py_predict_rentalcount**，以使用定型的模型和一組新資料進行預測。 在 Azure Data Studio 中執行下方的 T-SQL。

   ```sql
   DROP PROCEDURE IF EXISTS py_predict_rentalcount;
   GO
   CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
   AS
   BEGIN
       DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
   
       EXECUTE sp_execute_external_script
                   @language = N'Python',
                   @script = N'
   
   # Import the scikit-learn function to compute error.
   from sklearn.metrics import mean_squared_error
   import pickle
   import pandas
   
   rental_model = pickle.loads(py_model)
   
   df = rental_score_data
   
   # Get all the columns from the dataframe.
   columns = df.columns.tolist()
   
   # Variable you will be predicting on.
   target = "RentalCount"
   
   # Generate the predictions for the test set.
   lin_predictions = rental_model.predict(df[columns])
   print(lin_predictions)
   
   # Compute error between the test predictions and the actual values.
   lin_mse = mean_squared_error(lin_predictions, df[target])
   #print(lin_mse)
   
   predictions_df = pandas.DataFrame(lin_predictions)
   
   OutputDataSet = pandas.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
   '
   , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
   , @input_data_1_name = N'rental_score_data'
   , @params = N'@py_model varbinary(max)'
   , @py_model = @py_model
   with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
   
   END;
   GO
    ```

1. 建立用以儲存預測的資料表。

   ```sql
   DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
   GO
   
   CREATE TABLE [dbo].[py_rental_predictions](
    [RentalCount_Predicted] [int] NULL,
    [RentalCount_Actual] [int] NULL,
    [Month] [int] NULL,
    [Day] [int] NULL,
    [WeekDay] [int] NULL,
    [Snow] [int] NULL,
    [Holiday] [int] NULL,
    [Year] [int] NULL
   ) ON [PRIMARY]
   GO
   ```

1. 執行預存程序以預測租用次數

   ```sql
   --Insert the results of the predictions for test set into a table
   INSERT INTO py_rental_predictions
   EXEC py_predict_rentalcount 'linear_model';
   
   -- Select contents of the table
   SELECT * FROM py_rental_predictions;
   ```

   您應該會看見如下所示的結果。

   :::image type="content" source="media/python-tutorial-prediction-results.png" alt-text="來自預存程序的預測結果":::

您已成功建立、定型和部署模型。 接著您在預存程序中使用該模型根據新資料來預測值。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中，您已完成下列步驟：

* 建立會產生機器學習模型的預存程序
* 將模型儲存在資料庫資料表中
* 建立一個使用此模型進行預測的預存程序
* 以新資料執行模型

若要深入了解如何搭配 SQL 機器學習使用 Python，請參閱：

+ [Python 教學課程](python-tutorials.md)
