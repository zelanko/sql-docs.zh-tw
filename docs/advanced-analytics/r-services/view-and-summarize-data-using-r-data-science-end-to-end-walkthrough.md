---
title: "使用 R 檢視及摘要資料 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 檢視及摘要資料 (資料科學端對端逐步解說)
現在，您將使用 R 程式碼來運用相同的資料。 您也將了解如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 隨附之 **RevoScaleR** 封裝中的函數，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器內容中產生資料摘要，並將結果傳回您的 R 環境。  

本逐步解說提供 R 指令碼，其中包含建立資料物件、產生摘要及建立模型需要的所有程式碼。 您可以在安裝 R 指令碼檔的位置找到 R 指令碼檔 **RSQL_RWalkthrough.R**。  
+ 如果您熟悉 R，就能立即執行指令碼。
+ 對於正在學習使用 RevoScaleR 的使用者，本教學課程將會逐行執行指令碼。
+ 若要執行指令碼中的個別行，您可以反白顯示檔案中的一或多行，然後按下 Ctrl + ENTER。    
  
> [!TIP]  如果您想要稍後再完成本逐步解說的其餘部分，請儲存您的 R 工作區。  如此一來，就能重複使用資料物件和其他變數。   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>定義 SQL Server 資料來源和計算內容
若要在 R 程式碼中從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取得要使用的資料，您需要：  
  
- 建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連線  
- 定義具有您所需資料的查詢，或是指定資料表或檢視    
- 定義一或多個在執行 R 程式碼時要使用的計算內容    
-   (選擇性) 定義可套用至資料來源的函數  
 

### <a name="load-the-revoscaler-library"></a>載入 RevoScaleR 程式庫

+  如果尚未載入 **RevoScaleR** 封裝，請執行：
    ```R
    library("RevoScaleR")`.  
    ```  
    如果您收到錯誤，請確定 R 開發環境使用包含 RevoScaleR 套件的程式庫。 使用類似 `.libPaths())` 的命令來檢視目前的路徑：  

    如果這是您第一次使用 **RevoScaleR** 封裝，請輸入 `help("RevoScaleR")` 或 `help("RxSqlServerData")` 來取得 R 環境的線上說明。  

### <a name="create-connection-strings"></a>建立連接字串


1. 定義連接字串。 在此逐步解說中，我們提供了 SQL 登入和 Windows 整合式驗證的範例。 我們建議您盡可能使用 Windows 驗證，以避免在 R 程式碼中儲存密碼。

    您使用的帳戶必須具有在指定資料庫中讀取資料及建立新資料表的權限。 如需如何將使用者新增至 SQL 資料庫並為其提供正確權限的資訊，請參閱[安裝後伺服器組態 &#40;SQL Server R Services&#41;](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md)。 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] 請務必視需要編輯伺服器名稱、資料庫名稱、使用者名稱和密碼。 
      
  
### <a name="define-and-set-a-compute-context"></a>定義和設定計算內容  

接下來，您將定義「計算內容」，讓 R 程式碼能夠在 SQL Server 電腦上執行。 一般而言，當您使用 R 時，所有作業都會在電腦記憶體中執行。 不過，藉由指示 R 作業應該在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行，您可以平行執行一些工作並利用伺服器資源。  

根據預設，計算內容是本機的，因此您必須根據作業來明確設定計算內容。  


1.  一開始先定義用來建立計算內容的一些變數。  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   在工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間來回序列化 R 物件時，R 會使用暫存目錄。 您可以指定本機目錄以用來做為 *sqlShareDir*，或接受預設值。  
  
    -   使用 *sqlWait* 來指出您是否想要 R 等待結果。  如需等待與非等待工作的討論，請參閱 [ScaleR 分散式運算](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。
  
    -   使用引數 *sqlConsoleOutput*，以指出您不想看到來自 R 主控台的輸出。  
  
2.  使用變數和已經定義的連接字串來建立計算內容物件，並將它儲存在 R 變數 *sqlcc* 中。  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. 設定計算內容。
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + `rxSetComputeContext` 會以隱藏方式傳回先前使用中的計算內容，讓您可以使用它
   + `rxGetComputeContext` 會傳回使用中的計算內容  
  
    請注意，設定計算內容僅適用於使用 **RevoScaleR** 封裝中的函數所執行的作業，不會影響開放原始碼 R 作業的執行方式。  
  
### <a name="create-an-rxsqlserver-data-object"></a>建立 RxSqlServer 資料物件  

定義要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接之後，您可以使用該資料連接物件做為基礎，來定義不同的資料來源。 「資料來源」會指定您要用於工作 (例如訓練、瀏覽、評分或產生功能) 的一些資料集。  
    
您可以使用 *RxSqlServer* 函數，並傳遞連接字串和要取得之資料的定義，藉以定義 SQL Server 資料集。  
  
1. 將 SQL 陳述式儲存為字串變數。 此查詢會定義您將用於定型模型的資料。    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. 將查詢定義做為引數傳遞至 SQL Server 資料來源。 *colClasses* 引數會藉由對應 SQL 來指定要傳回的資料結構描述。 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + 引數 *colClasses* 會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 之間移動資料時要使用的資料行類型。這很重要，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用與 R 不同的資料類型，而且具有更多資料類型。 如需詳細資訊，請參閱[使用 R 資料類型](../../advanced-analytics/r-services/working-with-r-data-types.md)。  
  
    + 引數 *rowsPerRead* 對於處理記憶體使用量和有效率的計算而言很重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。  藉由新增 `rowsPerRead` 參數，您可以控制讀入每個區塊以進行處理的資料列數目。  如果此參數的值太大，資料存取可能會變慢，因為您沒有足夠的記憶體，可有效率地處理這類大型資料區塊。  在某些系統上，將 `rowsPerRead` 設定為太小的值也可能使效能變慢。  

> [!TIP] 建立 *inDataSource* 資料物件之後，您可以視需要多次重複使用此物件，以取得關於所使用資料和變數的基本資訊、操作及轉換資料，或將它用於定型模型。  不過，*inDataSource* 物件本身尚未包含任何來自 SQL 查詢的資料。 在您執行像是 *rxImport* 或 *rxSummary* 的函數之前，不會將資料提取至本機環境中。          
  
## <a name="using-the-sql-server-data-in-r"></a>在 R 中使用 SQL Server 資料  
您現在可以將 R 函數套用至資料來源，來瀏覽、摘要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料及繪製圖表。 在本節中，您會試用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中所提供，支援遠端計算內容的幾個函數。  
  
-   `rxGetVarInfo`：使用此函數時，可以在遠端資料物件中搭配任何資料框架或資料集 (也可以搭配某些清單和矩陣)，以取得最大值和最小值、資料類型，以及因素資料行中的層級數目等資訊。  
  
    請考慮在任何類型的資料輸入、特徵轉換或特徵工程之後執行此函數。 這樣做可確保您要用於模型中的所有特徵都屬於預期的資料類型，並避免發生錯誤。  
 
  
-   `rxSummary`：使用此函數，取得有關個別變數的更詳細統計資料。 您也可以轉換值、使用因素層級計算摘要，以及儲存摘要供重複使用。  
  
  
### <a name="inspect-variables-in-the-data-source"></a>檢查資料來源中的變數  
    
+ 呼叫函數 `rxGetVarInfo`(使用資料來源  `inDataSource` 作為引數) 以取得資料來源中之變數及其資料類型的清單。  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    *結果：*  
    *Var 1: tipped, Type: integer*  
    *Var 2: fare_amount, Type: numeric*  
    *Var 3: passenger_count, Type: integer*  
    *Var 4: trip_time_in_secs, Type: numeric, Storage: int64*  
    *Var 5: trip_distance, Type: numeric*  
    *Var 6: pickup_datetime, Type: character*  
    *Var 7: dropoff_datetime, Type: character*  
    *Var 8: pickup_longitude, Type: numeric*  
    *Var 9: pickup_latitude, Type: numeric*  
    *Var 10: dropoff_longitude, Type: numeric*  
  
### <a name="create-a-summary-using-r"></a>使用 R 建立摘要

+ 呼叫 RevoScaleR 函數 `rxSummary`，根據乘客數來彙總費用金額。 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + `rxSummary` 的第一個引數指定摘要依據的公式或詞彙。 此處的 `F()` 函數可用來將 passenger_count 中的值轉換成因素，再進行摘要。  
    + 如果您未指定輸出的統計資料， `rxSummary` 預設會輸出平均值、標準差、最小值、最大值，以及有效和遺失的觀察值。  
    + 此範例也會包含一些程式碼來追蹤函數的開始和完成時間，讓您可以比較效能。  
  
    *結果*  
    *rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)*  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
    *Number of valid observations: 1000*   
    *Name                          Mean    StdDev   Min Max ValidObs MissingObs*  
    *fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0*   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>下一個步驟  
[使用 R 建立圖形和繪圖 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>上一課  
[第 1 課︰準備資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
