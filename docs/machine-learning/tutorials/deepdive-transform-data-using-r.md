---
title: 使用 RevoScaleR 轉換資料
description: RevoScaleR 教學課程 9：如何在 SQL Server 上使用 R 語言轉換資料。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ed1884b1d4dc6f2b1b32a06d348307171edd592
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757111"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 轉換資料 (SQL Server 和 RevoScaleR 教學課程)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 9 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將會了解在分析的各個階段用於轉換資料的 **RevoScaleR** 函式。

> [!div class="checklist"]
> * 使用 **rxDataStep** 建立和轉換資料子集
> * 使用 **rxImport**，在匯入期間將傳輸中資料於 XDF 檔案或記憶體內部資料框架之間進行轉換

**rxSummary**、 **rxCube**、 **rxLinMod**和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 轉換變數

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函數會一次處理一個資料區塊，從一個資料來源讀取並寫入另一個資料來源。 您可以指定要轉換的資料行、要載入的轉換等等。

為了讓此範例更有趣，讓我們使用另一個 R 套件中的函式來轉換資料。 **boot** 套件是其中一個「建議」的套件；也就是說， **boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此，在針對 R 整合所設定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，應該已經可以使用此套件。

從 **boot** 套件，使用 **inv.logit** 函式，它會計算 logit 的反函式。 換句話說， **inv.logit** 函數會將 logit 轉換回 [0,1] 刻度的機率。

> [!TIP] 
> 另一個取得此刻度預測的方式，是在 *rxPredict* 的原始呼叫中，將 **type** 參數設定為 **response**。

1. 一開始先建立一個資料來源以保存資料表 `ccScoreOutput` 的資料。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 再加入另一個資料來源以保存資料表 `ccScoreOutput2` 的資料。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的資料表中，從先前的 `ccScoreOutput` 資料表取得所有變數，再加上新建立的變數。
  
3. 將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用 **rxSqlServerTableExists** 函式來檢查輸出資料表 `ccScoreOutput2` 是否已經存在，如果是的話，則使用 **rxSqlServerDropTable** 函式刪除資料表。
  
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

    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型詳細資訊，請參閱[如何使用 RevoScaleR 轉換資料和建立子集](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform) (英文)。
  
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

請注意，因素變數已寫入 `ccScoreOutput2` 資料庫作為字元資料。 若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxImport 將資料載入記憶體](../../machine-learning/tutorials/deepdive-load-data-into-memory-using-rximport.md)