---
title: Python 教學課程：定型模型
titleSuffix: SQL machine learning
description: 在這個教學課程系列的第三部分 (總共四個部分) 中，您將會使用 SQL 機器學習定型 Python 中的線性迴歸模型來預測雪橇租賃。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 827c79e39cd646b81b5ee79d440a8bc48574210c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730473"
---
# <a name="python-tutorial-train-a-linear-regression-model-with-sql-machine-learning"></a>Python 教學課程：使用 SQL 機器學習定型線性迴歸模型
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中， 您將使用 Python 來定型線性迴歸模型。 在本系列的下一部分中，您將使用機器學習服務在 SQL Server 資料庫中部署此模型，或在巨量資料叢集上進行此部署。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中， 您將使用 Python 來定型線性迴歸模型。 在本系列的下一部分中，您將使用機器學習服務在 SQL Server 資料庫中部署此模型。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中， 您將使用 Python 來定型線性迴歸模型。 在此系列的下一部份中，您將使用機器學習服務在 Azure SQL 受控執行個體資料庫中部署此模型。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 定型線性迴歸模型
> * 使用線性迴歸模型進行預測

在[第一部分](python-ski-rental-linear-regression.md)，您已了解如何還原範例資料庫。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，您已了解如何將資料從資料庫載入到 Python 資料框架，並以 Python 準備資料。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，您將了解如何將模型儲存在資料庫中，然後從您在第二和第三部分中開發的 Python 指令碼建立預存程序。 預存程序將會在伺服器上執行，以根據新資料進行預測。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程的第三部分會假設您已完成[第一部分](python-ski-rental-linear-regression.md)及其必要條件。

## <a name="train-the-model"></a>將模型定型

為了進行預測，您必須找出最能描述資料集內變數之間相依性的函數 (模型)。 這稱為「定型模型」。 定型的資料集會是您在本系列課程第二部分中所建立 pandas 資料框架 **df** 中整個資料集的子集。

您將使用線性迴歸演算法來定型模型 **lin_model**。

```python
# Store the variable we'll be predicting on.
target = "Rentalcount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

您應該會看見如下所示的結果。

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>進行預測

使用預測函數以使用 **lin_model** 模型來預測租用次數。

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

您應該會看見如下所示的結果。

```results
Predictions: [ 40.  38. 240.  39. 514.  48. 297.  25. 507.  24.  30.  54.  40.  26.
  30.  34.  42. 390. 336.  37.  22.  35.  55. 350. 252. 370. 499.  48.
  37. 494.  46.  25. 312. 390.  35.  35. 421.  39. 176.  21.  33. 452.
  34.  28.  37. 260.  49. 577. 312.  24.  24. 390.  34.  64.  26.  32.
  33. 358. 348.  25.  35.  48.  39.  44.  58.  24. 350. 651.  38. 468.
  26.  42. 310. 709. 155.  26. 648. 617.  26. 846. 729.  44. 432.  25.
  39.  28. 325.  46.  36.  50.  63.]
Computed error: 2.9960763804270902e-27
```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第三部分中，您已完成下列步驟：

* 定型線性迴歸模型
* 使用線性迴歸模型進行預測

若要部署您已建立的機器學習模型，請遵循本教學課程系列的第四部分：

> [!div class="nextstepaction"]
> [Python 教學課程：部署機器學習模型](python-ski-rental-linear-regression-deploy-model.md)
