---
title: "評分新資料 （SQL 與 R 深入探討） |Microsoft 文件"
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
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 54cc4dd297357407592c953b54e04d0ae024f7aa
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>評分新資料 （SQL 與 R 深入探討）

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在此步驟中，您可以使用羅吉斯迴歸模型來建立另一個使用相同的獨立變數做為輸入的資料集的分數稍早建立。

> [!NOTE]
> 您的某些步驟需要 DDL 管理員權限。

## <a name="generate-and-save-scores"></a>產生並儲存分數
  
1. 更新您稍早，設定資料來源`sqlScoreDS`、 加入必要的資料行資訊。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 若要確定不會喪失結果，請建立新的資料來源物件。 然後，使用新的資料來源物件來擴展中的新資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    此時，資料表尚未建立。 此陳述式只會定義資料的容器。
     
3. 檢查目前的計算內容，並視需要將計算內容設定為伺服器。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 執行產生結果的預測函數前，您需要檢查現有的輸出資料表是否存在。 否則，您會得到錯誤，當您嘗試將寫入新的資料表。
  
    若要這樣做，請呼叫函數 **rxSqlServerTableExists** 和 **rxSqlServerDropTable**，並傳遞資料表名稱作為輸入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  **rxSqlServerTableExists** 函數會查詢 ODBC 驅動程式，如果資料表存在便傳回 TRUE，否則為 FALSE。
    -  此函式**rxSqlServerDropTable**執行 DDL，並傳回 TRUE，如果資料表已順利卸除，FALSE 否則。
    - 參考的兩個函數可以在這裡找到： [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. 現在您已準備好使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函式，建立分數，並將它們儲存在資料來源中定義的新資料表`sqlScoreDS`。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 函數是支援在遠端計算內容中執行的另一個函數。 您可以使用 **rxPredict** 函數，從使用 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)、 [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)或 [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)建立的模型建立分數。
  
    - 在此，參數 *writeModelVars* 設為 **TRUE** 。 這表示估計所用的變數將會包含在新的資料表中。
  
    - 參數 *predVarNames* 指定儲存結果的變數。 這裡您要將新的變數， `ccFraudLogitScore`。
  
    - *rxPredict* 的 **type** 參數定義您要如何計算預測。 指定關鍵字**回應**產生分數以回應變數的標尺上。 或者，您也可以使用關鍵字**連結**產生分數，根據基礎的連結函式，在此情況下預測會建立使用羅吉斯的小數位數。

6. 在一段時間之後，您可以在 Management Studio 中重新整理資料表清單，以查看新的資料表及其資料。

7. 若要新增其他變數到輸出預測，請使用 *extraVarsToWrite* 引數。  例如，在下列程式碼變數`custID`計分資料表加到輸出資料表的預測。
  
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

## <a name="display-scores-in-a-histogram"></a>顯示長條圖中的分數

在建立新的資料表之後，您可以計算並顯示 10000 的預測分數的長條圖。 如果您指定低和高的值，因此這些從資料庫並將它們加入至您的工作資料計算速度。

1. 建立新的資料來源、 `sqlMinMax`，查詢資料庫，以取得低和高的值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     此範例中，您可以看到使用 **RxSqlServerData** 資料來源物件，根據 SQL 查詢、函數或預存程序定義任意資料集，然後在您的 R 程式碼中使用它們有多容易。 變數不會儲存實際的值，而只會儲存資料來源定義。唯有在您將它用於例如 **rxImport**的函數中時，才會執行查詢來產生值。
      
2. 呼叫[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函式可以共用的資料框架中的值放在計算內容。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **結果**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 現在可供使用的最大和最小值，使用值來建立另一個資料來源產生的分數。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 使用資料來源物件`sqlOutScoreDS`取得分數，並計算並顯示長條圖。 新增程式碼，視需要設定計算內容。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **結果**
  
    ![R 所建立的複雜長條圖](media/rsql-sue-complex-histogram.png "R 所建立的複雜長條圖")
  
## <a name="next-step"></a>下一步

[使用 R 轉換資料](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>上一個步驟

[建立模型](../../advanced-analytics/tutorials/deepdive-create-models.md)


