---
title: "為新資料評分 (資料科學深入探討) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 為新資料評分 (資料科學深入探討)
既然已有可用於預測的模型，請將來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料饋送給它，以產生一些預測。  
  
## 為新資料評分  
您將使用羅吉斯迴歸模型 *logitObj*，為另一個具有相同獨立變數作為輸入的資料集建立分數。  
  
> [!NOTE]  
> 這些步驟中有一些會需要 DDL 系統管理員權限才能執行。  
  
1.  更新您稍早設定的資料來源 *sqlScoreDS*，新增必要的資料行資訊。  
  
    ```R  
    sqlScoreDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlScoreTable,   
        colInfo = ccColInfo,   
        rowsPerRead = sqlRowsPerRead)    
    ```  
  
2.  為了確定您不會遺失結果，您將建立新的資料來源物件，並使用它將資料填入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的新資料表。  
  
    ```R    
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",   
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead )    
    ```  
     此時，資料表尚未建立。 此陳述式只會定義資料的容器。
     
3.  檢查目前的計算內容，並視需要將計算內容設定為伺服器。  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
4.  執行產生結果的預測函數前，您需要檢查現有的輸出資料表是否存在。 否則，您會在嘗試寫入新資料表時得到錯誤  
  
    若要這樣做，請呼叫函數 *rxSqlServerTableExists* 和 *rxSqlServerDropTable*，並傳遞資料表名稱作為輸入。  
  
    ```R  
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")   
    ```  
  
    -   *rxSqlServerTableExists* 函數會查詢 ODBC 驅動程式，如果資料表存在便傳回 TRUE，否則為 FALSE。    
    -   *rxSqlServerDropTable* 函數會執行 DDL，如果資料表順利卸除便傳回 TRUE，否則為 FALSE。   
  
5.  現在您已準備好使用 *rxPredict* 函數來建立分數，並將它們儲存在資料來源 *sqlScoreDS* 中定義的新資料表。  
  
    ```R  
    rxPredict(modelObject = logitObj,   
        data = sqlScoreDS,        
        outData = sqlServerOutDS,     
        predVarNames = "ccFraudLogitScore",   
          type = "link",      
        writeModelVars = TRUE,        
        overwrite = TRUE)    
    ```  
  
    *rxPredict* 函數是支援在遠端計算內容中執行的另一個函數。 您可以使用 *rxPredict* 函數，從使用 *rxLinMod*、*rxLogit* 或 *rxGlm* 建立的模型建立分數。  
  
    -   在此，參數 *writeModelVars* 設為 **TRUE**。 這表示估計所用的變數將會包含在新的資料表中。  
  
    -   參數 *predVarNames* 指定儲存結果的變數。 這裡，您正在傳遞新的變數，名為 *ccFraudLogitScore*。  
  
    -   *rxPredict* 的 *type* 參數定義您要如何計算預測。 指定關鍵字 **response** 產生以回應變數之小數位數為基礎的分數，或使用關鍵字 **link** 產生以基礎連結函數為基礎的分數，在此情況下，預測將以羅吉斯小數位數為基礎。  

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
  
## 以長條圖顯示分數  
在建立新的資料表之後，您將會計算並顯示 10000 個預測分數的長條圖。 指定下限和上限值可加快計算，因此您將從資料庫取得，並新增到您的工作資料。  
  
1.  建立新的資料來源 *sqlMinMax*，查詢資料庫以取得下限和上限值。  
  
    ```R  
    sqlMinMax <- RxSqlServerData(  
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",   
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),   
        connectionString = sqlConnString)    
    ```  
     此範例中，您可以看到使用 *RxSqlServerData* 資料來源物件，根據 SQL 查詢、函數或預存程序定義任意資料集，然後在您的 R 程式碼中使用它們有多容易。 變數不會儲存實際的值，而只會儲存資料來源定義。唯有在您將它用於例如 *rxImport* 的函數中時，才會執行查詢來產生值。  
      
2.  呼叫 *rxImport* 函數將值放入可跨計算內容共用的資料框架。  
  
    ```R  
    minMaxVals <- rxImport(sqlMinMax)   
    minMaxVals <- as.vector(unlist(minMaxVals))  
  
    ```  
     **結果**
 
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3.  既然有最大和最小值可用，請用它們來建立分數資料來源。  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",    
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead,   
            colInfo = list(ccFraudLogitScore = list(   
                low = floor(minMaxVals[1]),    
                        high = ceiling(minMaxVals[2]) ) ) )  
  
    ```  

  
4.  最後，使用分數資料來源物件，取得評分資料，並計算及顯示長條圖。 新增程式碼，視需要設定計算內容。  
  
    ```R  
    # rxSetComputeContext(sqlCompute)   
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)  
  
    ```  
  
    **結果**  
  
    ![complex histogram created by R](../../advanced-analytics/r-services/media/rsql-sue-complex-histogram.png "complex histogram created by R")  
  
## 下一個步驟  
[第 3 課：使用 R 轉換資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## 上一個步驟  
[建立模型 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰概觀 &#40;SQL Server R 服務&#41;](http://msdn.microsoft.com/library/mt637368(SQL.130).aspx)  
  
  
  
