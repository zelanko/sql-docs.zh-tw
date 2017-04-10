---
title: "使用 rxDataStep 建立新的 SQL Server 資料表 (資料科學深入探討) | Microsoft Docs"
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
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 rxDataStep 建立新的 SQL Server 資料表 (資料科學深入探討)
在這一課，您將了解如何在記憶體中資料框架之間移動資料、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內容，以及本機檔案。  
  
> [!NOTE]  
> 在這一課，您將使用不同的資料集。 航空公司誤點資料集是廣泛用於機器學習實驗的公用資料集。 如果您才剛開始使用 R，這是很適合測試用的資料集，用於已和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 一起發行的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的各種產品範例。 這個範例所需的資料檔案提供於與其他產品範例相同的目錄。  
  
## 從本機資料建立 SQL Server 資料表  
在本教學課程的第一課，您已經使用 *RxTextData* 函數將資料從文字檔案匯入到 R，並使用 *RxDataStep* 函數將資料移入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
在這一課，您將使用不同的方式，以及從 [XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)儲存的檔案取得資料。 XDF 格式是針對高維度資料開發的 XML 標準。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。
  
使用 XDF 檔案對資料執行一些輕量型轉換之後，您會將轉換的資料儲存至新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
> [!NOTE]  
> 在此步驟，您將需要 DDL 權限。  
  
1.  將計算內容設為您的本機工作站。  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  使用 *RxXdfData* 函數，來定義新的資料來源物件。 針對 XDF 資料來源，您只需要指定資料檔案的路徑。  您可以使用文字變數指定檔案的路徑，但在此情況下，有一個很好用的捷徑，原因是範例資料檔案 (AirlineDemoSmall.xdf) 位於 *rxGetOption* 函數所傳回的目錄。
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  對記憶體中的資料呼叫 *rxGetVarInfo*，即可檢視資料集的摘要。  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**結果**  
  
*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*   
*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*  

> [!NOTE]
> 
> 是否注意到不需要呼叫任何其他函數就可以將資料載入至 XDF 檔案，而且可以立即對資料呼叫 *rxGetVarInfo* 嗎？ 原因是 XDF 是 RevoScaleR 的預設暫時儲存方法。 如需 XDF 檔案的詳細資訊，請參閱 [ScaleR 入門指南](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame)。 
  
4.  現在，您將此資料放入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，並將 _DayOfWeek_ 儲存為從 1 到 7 的整數值。  
  
    若要這樣做，請先定義 SQL Server 資料來源。  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  檢查是否有相同名稱的資料表存在，並刪除存在的資料表。  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  建立資料表，然後使用 `rxDataStep` 載入資料。  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```  
  
7.  將計算內容設定回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  使用簡單的 SQL 陳述式定義資料子集。  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. 呼叫 *rxSummary* 以檢閱查詢中的資料摘要。  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## 下一個步驟  
[使用 rxDataStep 執行區塊處理分析 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
## 上一個步驟  
[使用 rxImport 將資料載入記憶體 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
