---
title: 教學課程：在 R 中部署預測模型
titleSuffix: SQL machine learning
description: 在這個四部分教學課程的第四部分中，您將使用 SQL 機器學習，在 R 中部署預測模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: af3826d5153e2be157a74c96037bff51c6039e7c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728565"
---
# <a name="tutorial-deploy-a-predictive-model-in-r-with-sql-machine-learning"></a>教學課程：使用 SQL 機器學習在 R 中部署預測模型
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您會將以 R 開發的機器學習模型部署到 SQL Server 機器學習服務或巨量資料叢集。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用機器學習服務，將以 R 開發的機器學習模型部署到 SQL Serve。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用 SQL Server R Services，將以 R 開發的機器學習模型部署到 SQL Serve。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用機器學習服務，將以 R 開發的機器學習模型部署到 Azure SQL 受控執行個體。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 建立會產生機器學習模型的預存程序
> * 將模型儲存在資料庫資料表中
> * 建立一個使用此模型進行預測的預存程序
> * 以新資料執行模型

在[第一部分](r-predictive-model-introduction.md)，您已了解如何還原範例資料庫。

在[第二部分](r-predictive-model-prepare-data.md)中，您已了解如何匯入資料庫範例，然後準備要用來在 R 中定型預測模型的資料。

在[第三部分](r-predictive-model-train.md)中，您已了解如何在 R 中建立及定型多個機器學習模型，然後選擇最精確的模型。

## <a name="prerequisites"></a>Prerequisites

本教學課程的第四部分假設您已滿足[**第一部分**](r-predictive-model-introduction.md)的必要條件，並已完成[**第二部分**](r-predictive-model-prepare-data.md)和[**第三部分**](r-predictive-model-train.md)中的步驟。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立一個會產生模型的預存程序

在本教學課程系列的第三部分中，您已判定決策樹 (dtree) 是最精確的模型。 現在，請使用所開發的 R 指令碼建立預存程序 (`generate_rental_model`)，以使用 R 套件中的 rpart 來定型及產生 dtree 模型。

在 Azure Data Studio 中執行下列命令。

```sql
USE [TutorialDB]
DROP PROCEDURE IF EXISTS generate_rental_model;
GO
CREATE PROCEDURE generate_rental_model (@trained_model VARBINARY(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
rental_train_data$Month   <- factor(rental_train_data$Month);
rental_train_data$Day     <- factor(rental_train_data$Day);
rental_train_data$Holiday <- factor(rental_train_data$Holiday);
rental_train_data$Snow    <- factor(rental_train_data$Snow);
rental_train_data$WeekDay <- factor(rental_train_data$WeekDay);

#Create a dtree model and train it using the training data set
library(rpart);
model_dtree <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = rental_train_data);
#Serialize the model before saving it to the database table
trained_model <- as.raw(serialize(model_dtree, connection=NULL));
'
        , @input_data_1 = N'
            SELECT RentalCount
                 , Year
                 , Month
                 , Day
                 , WeekDay
                 , Snow
                 , Holiday
            FROM dbo.rental_data
            WHERE Year < 2015
            '
        , @input_data_1_name = N'rental_train_data'
        , @params = N'@trained_model varbinary(max) OUTPUT'
        , @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>將模型儲存在資料庫資料表中

在 TutorialDB 資料庫中建立資料表，然後將模型儲存至資料表。

1. 建立用來儲存模型的資料表 (`rental_models`)。

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS rental_models;
    GO
    CREATE TABLE rental_models (
          model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY
        , model VARBINARY(MAX) NOT NULL
        );
    GO
    ```

1. 使用模型名稱 "DTree"，將模型以二進位物件的形式儲存至資料表。

    ```sql
    -- Save model to table
    TRUNCATE TABLE rental_models;
    
    DECLARE @model VARBINARY(MAX);
    
    EXECUTE generate_rental_model @model OUTPUT;
    
    INSERT INTO rental_models (
          model_name
        , model
        )
    VALUES (
         'DTree'
        , @model
        );
    
    SELECT *
    FROM rental_models;
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>建立一個進行預測的預存程序

建立會使用定型的模型和一組新資料進行預測的預存程序 (`predict_rentalcount_new`)。

```sql
-- Stored procedure that takes model name and new data as input parameters and predicts the rental count for the new data
USE [TutorialDB]
DROP PROCEDURE IF EXISTS predict_rentalcount_new;
GO
CREATE PROCEDURE predict_rentalcount_new (
      @model_name VARCHAR(100)
    , @input_query NVARCHAR(MAX)
    )
AS
BEGIN
    DECLARE @model VARBINARY(MAX) = (
            SELECT model
            FROM rental_models
            WHERE model_name = @model_name
            );

    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
#Convert types to factors
rentals$Month   <- factor(rentals$Month);
rentals$Day     <- factor(rentals$Day);
rentals$Holiday <- factor(rentals$Holiday);
rentals$Snow    <- factor(rentals$Snow);
rentals$WeekDay <- factor(rentals$WeekDay);

#Before using the model to predict, we need to unserialize it
rental_model <- unserialize(model);

#Call prediction function
rental_predictions <- predict(rental_model, rentals);
rental_predictions <- data.frame(rental_predictions);
'
        , @input_data_1 = @input_query
        , @input_data_1_name = N'rentals'
        , @output_data_1_name = N'rental_predictions'
        , @params = N'@model varbinary(max)'
        , @model = @model
    WITH RESULT SETS(("RentalCount_Predicted" FLOAT));
END;
GO
```

## <a name="execute-the-model-with-new-data"></a>以新資料執行模型

現在，您可以使用預存程序 `predict_rentalcount_new` 從新資料預測出租計數。

```sql
-- Use the predict_rentalcount_new stored procedure with the model name and a set of features to predict the rental count
EXECUTE dbo.predict_rentalcount_new @model_name = 'DTree'
    , @input_query = '
        SELECT CONVERT(INT,  3) AS Month
             , CONVERT(INT, 24) AS Day
             , CONVERT(INT,  4) AS WeekDay
             , CONVERT(INT,  1) AS Snow
             , CONVERT(INT,  1) AS Holiday
        ';
GO
```

您應該會看到如下的結果。

```results
RentalCount_Predicted
332.571428571429
```

您已在資料庫中成功建立、定型和部署模型。 接著您在預存程序中使用該模型根據新資料來預測值。


## <a name="clean-up-resources"></a>清除資源

在使用完 TutorialDB 資料庫後，請從您的伺服器將其刪除。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中，您學到了如何：

* 建立會產生機器學習模型的預存程序
* 將模型儲存在資料庫資料表中
* 建立一個使用此模型進行預測的預存程序
* 以新資料執行模型

若要深入了解如何在機器學習服務中使用 R，請參閱：

* [執行簡單的 R 指令碼](quickstart-r-create-script.md)
* [R 資料結構、類型與物件](quickstart-r-data-types-and-objects.md)
* [R 函式](quickstart-r-functions.md)
