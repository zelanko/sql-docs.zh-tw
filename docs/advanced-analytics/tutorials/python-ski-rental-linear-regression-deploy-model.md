---
title: Python 教學課程:部署模型 (線性回歸)
description: 在本教學課程中, 您將在 SQL Server Machine Learning 服務中使用 Python 和線性回歸, 以預測 ski 租用的數目。 您將使用 Machine Learning 服務, 將 Python 中開發的線性回歸模型部署到 SQL Server 資料庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f5d19af93ab180c660a264d5aaabc538d527a5
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242516"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-to-sql-server-machine-learning-services"></a>Python 教學課程:將線性回歸模型部署至 SQL Server Machine Learning 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分教學課程系列的第四部分中, 您將使用 Machine Learning 服務, 將 Python 中開發的線性回歸模型部署到 SQL Server 資料庫。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 建立會產生機器學習模型的預存程式
> * 將模型儲存在資料庫資料表中
> * 建立使用模型進行預測的預存程式
> * 以新資料執行模型

在[第一部](python-ski-rental-linear-regression.md)中, 您已瞭解如何還原範例資料庫。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中, 您已瞭解如何將資料從 SQL Server 載入 python 資料框架, 並以 python 準備資料。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中, 您已瞭解如何在 Python 中訓練線性回歸機器學習模型。

## <a name="prerequisites"></a>必要條件

* 本教學課程的第四部分假設您已完成[第一部分](python-ski-rental-linear-regression.md)和其必要條件。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立會產生模型的預存程式

現在, 使用您所開發的 Python 腳本, 建立預存程式**generate_rental_rx_model** , 使用 LinearRegression from scikit-learn-學習來定型和產生線性回歸模型。

在 Azure Data Studio 中執行下列 T-sql 語句, 以建立用來定型模型的預存程式。

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

在 TutorialDB 資料庫中建立資料表, 然後將模型儲存至資料表。

1. 在 Azure Data Studio 中執行下列 T-sql 語句, 以建立名為**rental_py_models**的資料表, 用來儲存模型。

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

1. 以二進位物件的形式將模型儲存至資料表, 並將模型名稱**linear_model**。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC generate_rental_py_model @model OUTPUT;
    
    INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>建立可進行預測的預存程式

1. 建立預存程式**py_predict_rentalcount** , 使用定型的模型和一組新的資料進行預測。 在 Azure Data Studio 中執行下列 T-sql。

    ```sql
    DROP PROCEDURE IF EXISTS py_predict_rentalcount;
    GO
    CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
    AS
    BEGIN
        DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
    
        EXEC sp_execute_external_script
                    @language = N'Python',
                    @script = N'
    
    # Import the scikit-learn function to compute error.
    from sklearn.metrics import mean_squared_error
    import pickle
    import pandas as pd
    
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
    
    predictions_df = pd.DataFrame(lin_predictions)
    
    OutputDataSet = pd.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
    '
    , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
    , @input_data_1_name = N'rental_score_data'
    , @params = N'@py_model varbinary(max)'
    , @py_model = @py_model
    with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
    
    END;
    GO
    ```

1. 建立用來儲存預測的資料表。

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

1. 執行預存程式來預測出租計數

    ```sql
    --Insert the results of the predictions for test set into a table
    INSERT INTO py_rental_predictions
    EXEC py_predict_rentalcount 'linear_model';

    -- Select contents of the table
    SELECT * FROM py_rental_predictions;
    ```

您已成功建立、定型和部署 SQL Server Machine Learning 服務中的模型。 然後, 您可以在預存程式中使用該模型, 根據新的資料來預測值。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中, 您已完成下列步驟:

* 建立會產生機器學習模型的預存程式
* 將模型儲存在資料庫資料表中
* 建立使用模型進行預測的預存程式
* 以新資料執行模型

若要深入瞭解如何在 SQL Server Machine Learning 服務中使用 Python, 請參閱:

+ [適用于 SQL Server Machine Learning 服務的 Python 教學課程](sql-server-python-tutorials.md)