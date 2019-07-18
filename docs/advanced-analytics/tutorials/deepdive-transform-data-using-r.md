---
title: 使用 RevoScaleR rxDataStep-SQL Server Machine Learning 來轉換資料
description: 教學課程逐步解說如何使用 SQL Server 上的 R 語言來轉換資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0da478798e87497da7828126b2168bbae5d980f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962170"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R （SQL Server 和 RevoScaleR 教學課程） 來轉換資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課中，深入了解**RevoScaleR**函式來轉換資料，在您的分析的各個階段。

> [!div class="checklist"]
> * 使用**rxDataStep**來建立及轉換資料子集
> * 使用**rxImport**匯入期間轉換與 XDF 檔案或記憶體中的資料框架的傳輸中資料

**rxSummary**、 **rxCube**、 **rxLinMod**和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 轉換變數

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函數會一次處理一個資料區塊，從一個資料來源讀取並寫入另一個資料來源。 您可以指定要轉換的資料行、要載入的轉換等等。

若要讓此範例的有趣，讓我們使用另一個 R 套件中的函式來轉換資料。 **boot** 套件是其中一個「建議」的套件；也就是說， **boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此，可用的套件應該已經在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]針對 R 整合所設定的執行個體。

從**開機**封裝，請使用此函式**inv.logit**，用以計算 logit 的反函數。 換句話說， **inv.logit** 函數會將 logit 轉換回 [0,1] 刻度的機率。

> [!TIP] 
> 另一個取得此刻度預測的方式，是在 *rxPredict* 的原始呼叫中，將 **type** 參數設定為 **response**。

1. 開始建立資料來源來保存資料的資料表， `ccScoreOutput`。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 新增另一個資料來源，以保存資料表的資料`ccScoreOutput2`。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的資料表中，儲存從先前的所有變數`ccScoreOutput`資料表，再加上新建立的變數。
  
3. 將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函式**rxSqlServerTableExists**檢查是否輸出資料表`ccScoreOutput2`已經存在;，而且如果是，使用此函式**rxSqlServerDropTable**刪除資料表。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. 呼叫 **rxDataStep** 函數，然後從清單中指定所需的轉換。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型的詳細資訊，請參閱 <<c0> [ 如何使用 RevoScaleR 的轉換和子集資料](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
6. 呼叫 **rxGetVarInfo** 檢視新資料集裡的變數摘要。
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**結果**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

會保留原始的 logit 分數，但新增了新的資料行 *ccFraudProb*，在其中 logit 分數以介於 0 和 1 之間的值代表。

請注意，因素變數已寫入至資料表，`ccScoreOutput2`為字元資料。 若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxImport 將資料載入記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)