---
title: 使用 RevoScaleR rxDataStep 轉換資料
description: 有關如何在 SQL Server 上使用 R 語言來轉換資料的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c76bdf56febd06ecba6f2d9d11f1710eefdc23e6
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715508"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 轉換資料 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在這一課, 您將瞭解在分析的各種階段轉換資料的**RevoScaleR**函數。

> [!div class="checklist"]
> * 使用**rxDataStep**來建立和轉換資料子集
> * 在匯入期間, 使用**rxImport**將傳輸中的資料轉換為 XDF 檔案或記憶體中的資料框架

**rxSummary**、 **rxCube**、 **rxLinMod**和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 來轉換變數

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函數會一次處理一個資料區塊，從一個資料來源讀取並寫入另一個資料來源。 您可以指定要轉換的資料行、要載入的轉換等等。

為了讓這個範例更有趣, 讓我們使用另一個 R 封裝的函式來轉換資料。 **boot** 套件是其中一個「建議」的套件；也就是說， **boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此, 在針對 R 整合所[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定的實例上, 應該已經可以使用此套件。

從**開機**封裝, 使用**logit**函數來計算 logit 的反向。 換句話說， **inv.logit** 函數會將 logit 轉換回 [0,1] 刻度的機率。

> [!TIP] 
> 另一個取得此刻度預測的方式，是在 *rxPredict* 的原始呼叫中，將 **type** 參數設定為 **response**。

1. 首先, `ccScoreOutput`建立資料來源來保存資料表的目標資料。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 加入另一個資料來源來保存資料表`ccScoreOutput2`的資料。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的資料表中, 儲存前一個`ccScoreOutput`資料表中的所有變數, 再加上新建立的變數。
  
3. 將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函數**rxSqlServerTableExists**來檢查輸出資料表`ccScoreOutput2`是否已經存在; 如果是的話, 請使用函數**rxSqlServerDropTable**來刪除資料表。
  
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

    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型的詳細資訊, 請參閱[如何使用 RevoScaleR 轉換和子集資料](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
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

請注意, 因素變數已以字元資料的形式`ccScoreOutput2`寫入資料表。 若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxImport 將資料載入記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)