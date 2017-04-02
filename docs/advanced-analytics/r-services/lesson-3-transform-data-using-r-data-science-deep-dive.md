---
title: "第 3 課：使用 R 轉換資料 (資料科學深入探討) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/03/2016"
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# 第 3 課：使用 R 轉換資料 (資料科學深入探討)
**RevoScaleR** 套件提供適用於在各種分析階段轉換資料的多個函數：  
  
-   **rxDataStep** 可用來建立及轉換資料子集。  
  
-   **rxImport** 支援在將資料匯入 XDF 檔案或記憶體內資料框架，或是從中匯入資料時，對資料進行轉換。  
  
-   **rxSummary**、**rxCube**、**rxLinMod** 和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。  
  
在本節中，您將了解如何使用這些函數。 讓我們從  *rxDataStep* 開始。  
  
## 使用 rxDataStep 轉換變數  
*rxDataStep* 函數會一次處理一個資料區塊，從一個資料來源讀取並寫入另一個資料來源。 您可以指定要轉換的資料行、要載入的轉換等等。  
  
為了讓此範例更有趣，您將使用另一個 R 套件中的函數來轉換資料。  **boot** 套件是其中一個「建議」的套件；也就是說，**boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此，您搭配 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，應該已提供此套件。  
  
從 **boot** 套件，您將使用 *inv.logit* 函數，它會計算 logit 的反函數。 換句話說，*inv.logit* 函數會將 logit 轉換回 [0,1] 刻度的機率。  
  
> [!TIP]  
> 另一個取得此刻度預測的方式，是在 *rxPredict* 的原始呼叫中，將 *type* 參數設定為 **response**。  
  
1.  一開始先建立一個資料來源以保存資料表 *ccScoreOutput* 的資料。  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )  
  
    ```  
  
2.  再加入另一個資料來源以保存資料表 ccScoreOutput2 的資料。  
  
    ```R  
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )  
  
    ```  
  
    在新的資料表中，您會從先前的 *ccScoreOutput* 資料表取得所有變數，再加上新建立的變數。  
  
3.  將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
  
    ```  
  
4.  使用 *rxSqlServerTableExists* 函數來檢查輸出資料表 *ccScoreOutput2* 是否已經存在，而且如果是的話，則使用 *rxSqlServerDropTable* 函數刪除資料表。  
  
    ```R    
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")  
  
    ```  
  
5.  呼叫 *rxDataStep* 函數，然後從清單中指定所需的轉換。  
  
    ```R  
    rxDataStep(inData = sqlOutScoreDS,   
        outFile = sqlOutScoreDS2,         
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),        
        transformPackages = "boot",   
        overwrite = TRUE)    
    ```  
  
    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型的詳細資訊，請參閱 [Transforming 和內嵌資料](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform)
  
6.  呼叫 *rxGetVarInfo* 檢視新資料集裡的變數摘要。  
  
    ```R  
    rxGetVarInfo(sqlOutScoreDS2)  
    ```  
  
**結果**  
  
*Var 1: ccFraudLogitScore, Type: numeric*  
*Var 2: state, Type: character*  
*Var 3: gender, Type: character*  
*Var 4: cardholder, Type: character*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: ccFraudProb, Type: numeric*  
  
會保留原始的 logit 分數，但新增了新的資料行 *ccFraudProb*，在其中 logit 分數以介於 0 和 1 之間的值代表。 

請注意，因素變數已寫入資料表 *ccScoreOutput2* 作為字元資料。  若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。  

  
## 下一個步驟  
[使用 rxImport 將資料載入記憶體 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## 上一個步驟  
[第 2 課︰建立及執行 R 指令碼 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
  
  
