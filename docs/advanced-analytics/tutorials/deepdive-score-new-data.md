---
title: 使用 RevoScaleR 和 rxPredict 對新資料評分
description: 有關如何在 SQL Server 上使用 R 語言對資料進行評分的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff3782fb760e4d3dd1059103bc835b94d9c7581f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714829"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>為新資料評分 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在此步驟中, 您會使用您在上一課中建立的羅吉斯回歸模型, 為另一個使用相同獨立變數做為輸入的資料集評分。

> [!div class="checklist"]
> * 為新資料評分
> * 建立分數的長條圖

> [!NOTE]
> 您需要有其中一些步驟的 DDL 系統管理員許可權。

## <a name="generate-and-save-scores"></a>產生並儲存分數
  
1. 更新 sqlScoreDS 資料來源 (在第[二課](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)中建立), 以使用上一課所建立的資料行資訊。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 為確保您不會遺失結果, 請建立新的資料來源物件。 然後, 使用新的資料來源物件來填入 RevoDeepDive 資料庫中的新資料表。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    此時，資料表尚未建立。 此陳述式只會定義資料的容器。
     
3. 使用**rxGetComputeCoNtext ()** 檢查目前的計算內容, 並視需要將計算內容設定為伺服器。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 基於預防措施, 請檢查輸出資料表是否存在。 如果已經存在同名的名稱, 當您嘗試寫入新的資料表時, 就會收到錯誤。
  
    若要這樣做，請呼叫函數 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 和 [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)，並傳遞資料表名稱作為輸入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists**會查詢 ODBC 驅動程式, 如果資料表存在則傳回 TRUE, 否則傳回 FALSE。
    + **rxSqlServerDropTable**會執行 DDL, 如果成功卸載資料表則傳回 TRUE, 否則傳回 FALSE。

5. 執行[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)以建立分數, 並將它們儲存在資料來源 sqlScoreDS 中所定義的新資料表。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 函數是支援在遠端計算內容中執行的另一個函數。 您可以使用**rxPredict**函數, 根據[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)、 [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)或[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm), 從模型建立分數。
  
    - 在此，參數 *writeModelVars* 設為 **TRUE** 。 這表示估計所用的變數將會包含在新的資料表中。
  
    - 參數 *predVarNames* 指定儲存結果的變數。 在這裡, `ccFraudLogitScore`您要傳遞新的變數。
  
    - *rxPredict* 的 **type** 參數定義您要如何計算預測。 根據回應變數的小數值, 指定要產生分數的關鍵字**回應**。 或者, 使用關鍵字**連結**來根據基礎連結函式產生分數, 在此情況下, 會使用羅吉斯小數值來建立預測。

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

## <a name="display-scores-in-a-histogram"></a>在長條圖中顯示分數

建立新資料表之後, 計算並顯示10000預測分數的長條圖。 如果您指定 low 和 high 值, 則計算速度會更快, 因此請從資料庫取得, 並將其新增至您的工作資料。

1. 建立新的資料來源 sqlMinMax, 查詢資料庫以取得下限和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     此範例中，您可以看到使用 **RxSqlServerData** 資料來源物件，根據 SQL 查詢、函數或預存程序定義任意資料集，然後在您的 R 程式碼中使用它們有多容易。 變數不會儲存實際的值，而只會儲存資料來源定義。唯有在您將它用於例如 **rxImport**的函數中時，才會執行查詢來產生值。
      
2. 呼叫[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函數, 將值放入可跨計算內容共用的資料框架中。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **結果**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 現在可以使用最大和最小值, 請使用這些值來為產生的分數建立另一個資料來源。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 使用 [資料來源物件 sqlOutScoreDS] 來取得分數, 並計算並顯示長條圖。 新增程式碼，視需要設定計算內容。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **結果**
  
    ![R 所建立的複雜長條圖](media/rsql-sue-complex-histogram.png "R 所建立的複雜長條圖")
  
## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 轉換資料](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)