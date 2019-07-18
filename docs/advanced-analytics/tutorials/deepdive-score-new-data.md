---
title: 使用 RevoScaleR 和 rxPredict-SQL Server 機器學習服務的新資料評分
description: 教學課程逐步解說如何使用 SQL Server 上的 R 語言的資料進行計分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 386daeb62262182d40ea0b15cca3eb9714c23d64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962191"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>評分新資料 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在此步驟中，您可以使用您在要評分的另一個使用相同的獨立變數做為輸入的資料集上一課中建立的羅吉斯迴歸模型。

> [!div class="checklist"]
> * 為新資料評分
> * 建立分數的長條圖

> [!NOTE]
> 對於其中一些步驟，您就會需要 DDL 系統管理員權限。

## <a name="generate-and-save-scores"></a>產生並儲存分數
  
1. 更新 sqlScoreDS 資料來源 (在中建立[兩個課程](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) 若要使用在上一課中建立的資料行資訊。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 若要確定您不會遺失結果，請建立新的資料來源物件。 然後，使用新的資料來源物件來填入 RevoDeepDive 資料庫中的新資料表。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    此時，資料表尚未建立。 此陳述式只會定義資料的容器。
     
3. 檢查目前的計算內容使用**rxGetComputeContext()** ，並視需要設定計算內容到伺服器。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 為求安全起見，請檢查輸出資料表存在。 如果已經存在具有相同名稱，您會在嘗試寫入新的資料表時，收到錯誤。
  
    若要這樣做，請呼叫函數 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 和 [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)，並傳遞資料表名稱作為輸入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists**會查詢 ODBC 驅動程式，並傳回 TRUE，如果資料表存在，FALSE 否則。
    + **rxSqlServerDropTable**執行 DDL，並傳回 TRUE，如果資料表順利卸除，FALSE 否則。

5. 執行[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)建立分數，並將其儲存在資料來源 sqlScoreDS 中定義的新資料表中。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 函數是支援在遠端計算內容中執行的另一個函數。 您可以使用**rxPredict**函式，若要從模型建立分數，根據[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)， [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)，或[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)。
  
    - 在此，參數 *writeModelVars* 設為 **TRUE** 。 這表示估計所用的變數將會包含在新的資料表中。
  
    - 參數 *predVarNames* 指定儲存結果的變數。 這裡您傳遞新的變數， `ccFraudLogitScore`。
  
    - *rxPredict* 的 **type** 參數定義您要如何計算預測。 指定關鍵字**回應**來產生以回應變數之小數位數的分數。 或者，您也可以使用關鍵字**連結**產生分數以基礎連結函數中，在此情況下的預測會建立使用羅吉斯小數位數。

6. 在一段時間之後，您可以在 Management Studio 中重新整理資料表清單，以查看新的資料表及其資料。

7. 若要新增其他變數到輸出預測，請使用 *extraVarsToWrite* 引數。  例如，在下列程式碼中，來自評分資料表的變數 *custID* 會新增到預測的輸出資料表。
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>以長條圖顯示分數

在建立新的資料表之後，計算並顯示 10000 個預測分數的長條圖。 計算速度，如果您指定下限和上限值，因此取得這兩個資料庫並將它們新增至您的工作資料。

1. 建立新的資料來源，sqlMinMax 查詢資料庫以取得下限和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     此範例中，您可以看到使用 **RxSqlServerData** 資料來源物件，根據 SQL 查詢、函數或預存程序定義任意資料集，然後在您的 R 程式碼中使用它們有多容易。 變數不會儲存實際的值，而只會儲存資料來源定義。唯有在您將它用於例如 **rxImport**的函數中時，才會執行查詢來產生值。
      
2. 呼叫[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)值放入可共用的資料框架，跨計算內容的函式。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **結果**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 現在可用的最大和最小值，使用值來建立另一個資料來源產生的分數。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 使用資料來源物件 sqlOutScoreDS 取得分數，並計算及顯示長條圖。 新增程式碼，視需要設定計算內容。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **結果**
  
    ![R 所建立的複雜長條圖](media/rsql-sue-complex-histogram.png "R 所建立的複雜長條圖")
  
## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 轉換資料](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)