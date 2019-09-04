---
title: Python 教學課程:定型模型 (線性回歸)
description: 在本教學課程中, 您將在 SQL Server Machine Learning 服務中使用 Python 和線性回歸, 以預測 ski 租用的數目。 您將以 Python 訓練線性回歸模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242546"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教學課程:在 SQL Server Machine Learning 服務中訓練線性回歸模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分教學課程系列的第三部分中, 您將以 Python 訓練線性回歸模型。 在此系列的下一個部分中, 您將會在具有 Machine Learning 服務的 SQL Server 資料庫中部署此模型。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 訓練線性回歸模型
> * 使用線性回歸模型進行預測

在[第一部](python-ski-rental-linear-regression.md)中, 您已瞭解如何還原範例資料庫。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中, 您已瞭解如何將資料從 SQL Server 載入 python 資料框架, 並以 python 準備資料。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中, 您將瞭解如何將模型儲存至 SQL Server, 然後從您在第二部和第三部分所開發的 Python 腳本中建立預存程式。 預存程式將會在 SQL Server 中執行, 以根據新的資料進行預測。

## <a name="prerequisites"></a>必要條件

* 本教學課程的第三部分假設您已完成[第一部分](python-ski-rental-linear-regression.md)和其必要條件。

## <a name="train-the-model"></a>定型模型

為了進行預測, 您必須找出最能描述資料集內變數之間相依性的函數 (模型)。 這稱為「定型模型」。 訓練資料集會是您在本系列第二部分所建立之 pandas 資料框架**df**的整個資料集子集。

您將使用線性回歸演算法來定型模型**lin_model** 。

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

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

您應該會看到類似下面的結果。

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>進行預測

使用 predict 函數來預測使用模型**lin_model**的租用計數。

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第三部分中, 您已完成下列步驟:

* 訓練線性回歸模型
* 使用線性回歸模型進行預測

若要部署您已建立的機器學習模型, 請遵循本教學課程系列的第四部分:

> [!div class="nextstepaction"]
> [Python 教學課程:部署機器學習模型](python-ski-rental-linear-regression-deploy-model.md)