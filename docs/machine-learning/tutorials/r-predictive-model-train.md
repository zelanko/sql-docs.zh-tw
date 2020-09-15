---
title: 教學課程：在 R 中定型和比較預測模型
titleSuffix: SQL machine learning
description: 在這個四部分教學課程系列的第三部分中，您將使用 SQL 機器學習，在 R 中開發兩個預測模型，然後選取最精確的模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 4c6ea97c242df2fc22e1b7a0a9d0d828e8f3859a
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178731"
---
# <a name="tutorial-create-a-predictive-model-in-r-with-sql-machine-learning"></a>教學課程：使用 SQL 機器學習在 R 中建立預測模型
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這四部分教學課程系列的第三部分中，您將在 R 中定型預測模型。在此系列的下一個部分中，您會使用機器學習服務在 SQL Server 資料庫中部署此模型，或在巨量資料叢集上進行此部署。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這四部分教學課程系列的第三部分中，您將在 R 中定型預測模型。在此系列的下一個部分中，您會使用機器學習服務在 SQL Server 資料庫中部署此模型。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在這四部分教學課程系列的第三部分中，您將在 R 中定型預測模型。在此系列的下一個部分中，您會使用 SQL Server R Services 在資料庫中部署此模型。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這四部分教學課程系列的第三部分中，您將在 R 中定型預測模型。在此系列的下一個部分中，您會使用機器學習服務在 Azure SQL 受控執行個體資料庫中部署此模型。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 定型兩個機器學習模型
> * 從這兩種模型進行預測
> * 比較結果以選擇最精確的模型

在[第一部分](r-predictive-model-introduction.md)，您已了解如何還原範例資料庫。

在[第二部分](r-predictive-model-prepare-data.md)中，您已了解如何將資料從資料庫載入到 Python 資料框架，並以 R 準備資料。

在[第四部分](r-predictive-model-deploy.md)中，您將了解如何將模型儲存在資料庫中，然後從您在第二和第三部分中開發的 Python 指令碼建立預存程序。 預存程序將會在伺服器上執行，以根據新資料進行預測。

## <a name="prerequisites"></a>Prerequisites

本教學課程系列的第三部分假設您已滿足[**第一部分**](r-predictive-model-introduction.md)的必要條件，並已完成[**第二部分**](r-predictive-model-prepare-data.md)中的步驟。

## <a name="train-two-models"></a>定型兩個模型

若要找出滑雪設備出租資料的最佳模型，請建立兩個不同的模型 (線性迴歸和決策樹)，並查看何者的預測較精確。 您將使用您在本系列的第一部分中建立的資料框架 `rentaldata`。

```r
#First, split the dataset into two different sets:
# one for training the model and the other for validating it
train_data = rentaldata[rentaldata$Year < 2015,];
test_data  = rentaldata[rentaldata$Year == 2015,];


#Use the RentalCount column to check the quality of the prediction against actual values
actual_counts <- test_data$RentalCount;

#Model 1: Use lm to create a linear regression model, trained with the training data set
model_lm <- lm(RentalCount ~  Month + Day + WeekDay + Snow + Holiday, data = train_data);

#Model 2: Use rpart to create a decision tree model, trained with the training data set
library(rpart);
model_rpart  <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = train_data);
```

## <a name="make-predictions-from-both-models"></a>從這兩種模型進行預測

使用預測函式和每個定型模型來預測出租計數。

```r
#Use both models to make predictions using the test data set.
predict_lm <- predict(model_lm, test_data)
predict_lm <- data.frame(RentalCount_Pred = predict_lm, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

predict_rpart  <- predict(model_rpart,  test_data)
predict_rpart <- data.frame(RentalCount_Pred = predict_rpart, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

#To verify it worked, look at the top rows of the two prediction data sets.
head(predict_lm);
head(predict_rpart);
```

```results
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1         27.45858          42       2     11     4      0       0
2        387.29344         360       3     29     1      0       0
3         16.37349          20       4     22     4      0       0
4         31.07058          42       3      6     6      0       0
5        463.97263         405       2     28     7      1       0
6        102.21695          38       1     12     2      1       0
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1          40.0000          42       2     11     4      0       0
2         332.5714         360       3     29     1      0       0
3          27.7500          20       4     22     4      0       0
4          34.2500          42       3      6     6      0       0
5         645.7059         405       2     28     7      1       0
6          40.0000          38       1     12     2      1       0
```

## <a name="compare-the-results"></a>比較結果

現在，您想要查看哪個模型做出最佳預測。 為此，使用基本繪圖函式來檢視您定型資料中的實際值與預測值之間的差異，將是快速輕鬆的方式。

```r
#Use the plotting functionality in R to visualize the results from the predictions
par(mfrow = c(1, 1));
plot(predict_lm$RentalCount_Pred - predict_lm$RentalCount, main = "Difference between actual and predicted. lm")
plot(predict_rpart$RentalCount_Pred  - predict_rpart$RentalCount,  main = "Difference between actual and predicted. rpart")
```

![比較兩個模型](./media/compare-models.png)

看來決策樹模型是兩個模型中較精確的一個。

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請刪除 TutorialDB 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第三部分中，您學到了如何：

* 定型兩個機器學習模型
* 從這兩種模型進行預測
* 比較結果以選擇最精確的模型

若要部署您已建立的機器學習模型，請遵循本教學課程系列的第四部分：

> [!div class="nextstepaction"]
> [使用 SQL 機器學習在 R 中部署預測模型](r-predictive-model-deploy.md)
