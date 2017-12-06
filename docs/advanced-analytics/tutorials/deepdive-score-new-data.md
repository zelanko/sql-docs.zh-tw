---
title: "評分新資料 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83beab637e3740dc41706c34ccfacffe985f2957
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="score-new-data"></a>為新資料評分

既然已有可用於預測的模型，請將來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料饋送給它，以產生一些預測。

您將使用羅吉斯迴歸模型 *logitObj*，為另一個具有相同獨立變數作為輸入的資料集建立分數。

> [!NOTE]
> 這些步驟中有一些會需要 DDL 系統管理員權限才能執行。

## <a name="generate-and-save-scores"></a>產生並儲存分數
  
1. 更新您稍早設定的資料來源 *sqlScoreDS*，新增必要的資料行資訊。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 為了確定您不會遺失結果，您將建立新的資料來源物件，並使用它將資料填入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的新資料表。
  
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
  
    -  函式 rxSqlServerTableExists 查詢的 ODBC 驅動程式，並傳回 TRUE，如果資料表存在，FALSE 否則。
    -  函式 rxSqlServerDropTable 函式執行 DDL，並傳回 TRUE，如果已成功卸除資料表，FALSE 否則。
  
5. 現在您已準備好使用 **rxPredict** 函數來建立分數，並將它們儲存在資料來源 *sqlScoreDS*中定義的新資料表。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    RxPredict 函式是支援在遠端計算內容中執行的另一個函式。 若要從使用 rxLinMod、 rxLogit 或 rxGlm 建立的模型建立分數，您可以使用 rxPredict 函式。
  
    - 在此，參數 *writeModelVars* 設為 **TRUE** 。 這表示估計所用的變數將會包含在新的資料表中。
  
    - 參數 *predVarNames* 指定儲存結果的變數。 這裡，您正在傳遞新的變數，名為 *ccFraudLogitScore*。
  
    - *類型*rxPredict 參數可讓您定義您要如何計算預測。 指定關鍵字 **response** 產生以回應變數之小數位數為基礎的分數，或使用關鍵字 **link** 產生以基礎連結函數為基礎的分數，在此情況下，預測將以羅吉斯小數位數為基礎。

6. 在一段時間之後，您可以在 Management Studio 中重新整理資料表清單，以查看新的資料表及其資料。

7. 若要新增其他變數到輸出預測，您可以使用 *extraVarsToWrite* 引數。  例如，在下列程式碼中，來自評分資料表的變數 *custID* 會新增到預測的輸出資料表。
  
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

在建立新的資料表之後，您將會計算並顯示 10000 個預測分數的長條圖。 指定下限和上限值可加快計算，因此您將從資料庫取得，並新增到您的工作資料。

1. 建立新的資料來源 *sqlMinMax*，查詢資料庫以取得下限和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     從這個範例中，您可以看到，以定義任意資料集，根據 SQL 查詢、 函數或預存程序，使用 RxSqlServerData 資料來源物件是多麼容易，，然後使用 R 程式碼中。 變數不會儲存實際的值，只要資料來源定義。產生的值，例如 rxImport 函式中使用它時，才會執行查詢。
      
2. 呼叫可共用的資料框架中的值放在計算內容 rxImport 函式。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **結果**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 現在可供使用的最大和最小值，使用值來建立分數的資料來源。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 最後，使用分數資料來源物件，取得評分資料，並計算及顯示長條圖。 新增程式碼，視需要設定計算內容。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **結果**
  
    ![R 所建立的複雜長條圖](media/rsql-sue-complex-histogram.png "R 所建立的複雜長條圖")
  
## <a name="next-step"></a>下一個步驟

[使用 R 的資料轉換](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>上一個步驟

[建立模型](../../advanced-analytics/tutorials/deepdive-create-models.md)


