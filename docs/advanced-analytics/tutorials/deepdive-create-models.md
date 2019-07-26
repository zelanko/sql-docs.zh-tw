---
title: 建立 R 模型 RevoScaleR 教學課程
description: 有關如何在 SQL Server 上使用 R 語言建立模型的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 65d5d999df39909a5419883736686c5bc22e0062
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469802"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>建立 R 模型 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

既然您已經擴充定型資料, 現在可以使用回歸模型來分析資料。 線性模型是預測性分析世界中很重要的工具, 而**RevoScaleR**套件包含的回歸演算法可以細分工作負載並平行執行。

> [!div class="checklist"]
> * 建立線性迴歸模型
> * 建立羅吉斯迴歸模型

## <a name="create-a-linear-regression-model"></a>建立線性迴歸模型

在此步驟中, 請建立一個簡單的線性模型, 其會使用 as 獨立變數作為*性別*和*creditLine*資料行中的值, 來估計客戶的信用卡餘額。
  
若要這麼做, 請使用支援遠端計算內容的[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)函數。
  
1. 建立 R 變數以儲存完成的模型, 並呼叫**rxLinMod**, 並傳遞適當的公式。
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 若要查看結果的摘要, 請在模型物件上呼叫標準 R **summary**函數。
  
     ```R
     summary(linModObj)
     ```

純 R 函數 (例如 **summary** ) 在這裡運作十分罕見，因為在前一個步驟中，您將計算內容設定成伺服器。 不過， **rxLinMod** 函數使用遠端計算內容建立模組時，也會將包含模型的物件傳回本機工作站，並將它儲存在共用目錄中。

因此，您可以對模型執行標準 R 命令，就像它是使用「本機」內容所建立一樣。

**結果**

```R
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>建立羅吉斯迴歸模型

接下來, 建立羅吉斯回歸模型, 以指出特定客戶是否為詐騙風險。 您將使用**RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)函式, 此函式支援在遠端計算內容中調整羅吉斯回歸模型的功能。

保持計算內容不變。 您也會繼續使用相同的資料來源。

1. 呼叫 **rxLogit** 函數，並傳遞定義模型所需的公式。

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    因為它是大型模型，其中包含 60 個獨立變數，並包括三個已卸除的虛擬變數，所以您可能必須等候一些時間，讓計算內容傳回物件。
    
    模型之所以很大的原因是在 R 和 **RevoScaleR** 套件中，類別因素變數的每個層級都會自動視為個別的虛擬變數來處理。
  
2. 若要檢視所傳回模型的摘要，請呼叫 R **summary** 函數。
  
    ```R
    summary(logitObj)
    ```
  
**部分結果**

```R
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [為新資料評分](../../advanced-analytics/tutorials/deepdive-score-new-data.md)