---
title: "建立 R 模型 （SQL 與 R 深入探討） |Microsoft 文件"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: a195d5e2-72e2-4dd6-bf43-947312e4a52a
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: cbd11a6c7bd27341e5a2b62e85e7c29cec926e4d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>建立 R 模型 （SQL 與 R 深入探討）

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

現在您已擴充定型資料，您可以使用線性迴歸來分析資料。 線性模型是預測分析世界中很重要的工具，而 **中的** RevoScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 套件包含高效能的可調式演算法。

## <a name="create-a-linear-regression-model"></a>建立線性迴歸模型

在此步驟中，您會建立簡單的線性模型估計信用卡結餘的客戶，使用做為獨立變數中的值*性別*和*creditLine*資料行。
  
若要這樣做，請使用[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)函式，以支援遠端計算內容。
  
1. 建立 R 變數來儲存已完成模型，並呼叫**rxLinMod**，傳遞適當的公式。
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 若要檢視結果的摘要，呼叫標準 R`summary`模型物件上的函式。
  
     ```R
     summary(linModObj)
     ```

您可能會認為它罕見純文字的 R 函數類似`summary`可行，因為在上一個步驟中，您必須設定計算內容到伺服器。 不過， **rxLinMod** 函數使用遠端計算內容建立模組時，也會將包含模型的物件傳回本機工作站，並將它儲存在共用目錄中。

因此，您可以對模型執行標準 R 命令，就像它是使用「本機」內容所建立一樣。

**結果**

```
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
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>建立羅吉斯迴歸模型

接下來，您可以建立羅吉斯迴歸模型，指出特定客戶是否有詐騙的風險。 您將使用**RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)函式，在遠端的羅吉斯迴歸模型的哪些支援調整計算內容。

1.  保持計算內容不變。 您也將繼續使用相同的資料來源。

2.  呼叫 **rxLogit** 函數，並傳遞定義模型所需的公式。

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    因為它是大型模型，其中包含 60 個獨立變數，並包括三個已卸除的虛擬變數，所以您可能必須等候一些時間，讓計算內容傳回物件。
    
    模型之所以很大的原因是在 R 和 **RevoScaleR** 套件中，類別因素變數的每個層級都會自動視為個別的虛擬變數來處理。
  
3.  若要檢視傳回模型的摘要，呼叫 R`summary`函式。
  
    ```R
    summary(logitObj)
    ```
  
**部分結果**

```
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

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>下一步

[分數新的資料](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>上一個步驟

[使用 R 將 SQL Server 資料視覺化](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
