---
title: "第 2 課︰建立及執行 R 指令碼 (資料科學深入探討) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/26/2016"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# 第 2 課︰建立及執行 R 指令碼 (資料科學深入探討)
現在您已設定資料來源並建立一或數個計算內容，您已準備好要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來執行一些強大的 R 指令碼。  在本課程中，您將使用伺服器計算內容來執行一些常見的機器學習服務工作：  
  
-   將資料視覺化，並產生一些摘要統計資料    
-   建立線性迴歸模型    
-   建立羅吉斯迴歸模型    
-   對新資料計分，並建立分數的長條圖  
  
## 將計算內容變更為伺服器  
執行任何 R 程式碼之前，您必須指定「目前」或「使用中」的計算內容。  
  
1.  若要啟用您已使用 R 定義的計算內容，請使用 *rxSetComputeContext* 函數，如下所示：  
  
    ```R  
    rxSetComputeContext(sqlCompute)   
    ```  
  
    當您執行此陳述式時，所有後續計算都將在 *sqlCompute* 參數中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上進行。  
  
  
2.  如果您決定在工作站上執行 R 程式碼，您可以使用  **local** 關鍵字，將計算內容切換回本機電腦。  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
    如需此函數支援之其他關鍵字的清單，請從 R 命令列輸入 `help("rxSetComputeContext")` 。  
  
> [!NOTE]  
> 指定計算內容之後，它會保持使用中，直到您變更為止。 不過，任何「無法」在遠端伺服器內容中執行的 R 指令碼都將在本機執行。  
  
## 計算摘要統計資料  
若要查看計算內容的運作方式，請嘗試使用 *sqlFraudDS* 資料來源產生一些摘要統計資料。  請記住，資料來源物件只會定義您將使用的資料，它不會變更計算內容。

+ 若要在本機執行摘要，請使用 *rxSetComputeContext* 並指定 "local" 關鍵字。
+ 若要在 SQL Server 電腦上建立相同的計算，請切換至您稍早定義的 SQL 計算內容。  

  
1.  呼叫 *rxSummary* 函數並傳遞必要引數，例如公式、資料來源，以及將結果指派給變數 *sumOut*。  
  
    ```R  
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)  
  
    ```  
  
    R 語言提供許多彙總函數，但 *rxSummary* 支援在各種遠端計算內容上執行，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  如需類似函數的詳細資訊，請參閱 [ScaleR reference](https://msdn.microsoft.com/microsoft-r/scaler/scaler) (ScaleR 參考) 中的 [Data Summaries](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) (資料摘要)。
  
2.  處理完成時，您可以將 *sumOut* 變數的內容列印到主控台。  
  
    ```R  
    sumOut  
    ```  
  
    > [!NOTE]  
    > 請勿嘗試在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦傳回結果之前就列印結果，否則可能會收到錯誤。  
  
  
**結果**  
  
*Summary Statistics Results for: ~gender + balance + numTrans +*   
 *numIntlTrans + creditLine*    
 *Data: sqlFraudDS (RxSqlServerData Data Source)*    
 *Number of valid observations: 10000*    
 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*    
 *balance       4075.0318 3926.558714            0   25626 100000*    
 *numTrans        29.1061   26.619923 0     100 10000    0           100000*    
 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*    
 *creditLine       9.1856    9.870364 1      75 10000    0          100000 Category Counts for gender*    
 *Number of categories: 2*    
 *Number of valid observations: 10000*   
 *Number of missing observations: 0*    
 *gender Counts*    
 *Male   6154*    
  *Female 3846*  
  
## 加入最大值和最小值  
根據計算的摘要統計資料，您發現與資料相關的一些實用資訊，並想要放入資料來源，以供進一步計算使用。 例如，您可以使用最小值和最大值來計算長條圖，因此您決定將最高值和最低值加入 *RxSqlServerData* 資料來源。  
  
所幸 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包含最佳化函數，可有效率地將整數資料轉換成類別因素資料。  
  
1.  一開始先設定一些暫存變數。  
  
    ```R  
    sumDF <- sumOut$sDataFrame   
    var <- sumDF$Name    
    ```  
  
2.  使用稍早建立的變數 *ccColInfo* 來定義資料來源中的資料行。  
  
    您也會將一些新的計算資料行 (*numTrans*、*numIntlTrans* 和 *creditLine*) 新增至資料行集合。  
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")), 
        cardholder = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
  
    ```  
  
3.  更新資料行集合之後，您可以套用下列陳述式，為您稍早定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源建立更新版本。  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlFraudTable,   
        colInfo = ccColInfo,        
        rowsPerRead = sqlRowsPerRead)   
    ```  
  
    *sqlFraudDS* 資料來源現在包含新增至 *ccColInfo* 的新資料行。  
  
請注意，這些修改只會影響 R 中的資料來源物件，尚未將任何新資料寫入資料庫資料表。 不過，您可以使用 *sumOut* 變數中所擷取的資料，以建立視覺效果和摘要。 在下一個步驟中，您將了解如何在切換計算內容時執行這項作業。 

> [!TIP]
> 如果您忘了正在使用哪個計算內容，請使用 `rxGetComputeContext()`。  如果傳回值是 `RxLocalSeq Compute Context`，則您正在使用本機計算內容。
  
## 下一個步驟  
[使用 R 將 SQL Server 資料視覺化 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/visualize-sql-server-data-using-r-data-science-deep-dive.md)  
  
## 上一個步驟  
[定義及使用計算內容 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
  
  
