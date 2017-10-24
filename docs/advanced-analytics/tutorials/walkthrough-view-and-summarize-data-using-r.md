---
title: "檢視及彙總資料使用 R （逐步解說） |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/08/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 22
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 8d94b671e88eb512cd763dc7660df6d3ac986370
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="view-and-summarize-data-using-r"></a>檢視及使用 R 的資料摘要

現在讓我們使用相同的資料使用 R 程式碼。 在這一課，您會了解如何使用中的函式**RevoScaleR**封裝。

本逐步解說提供 R 指令碼，其中包含建立資料物件、產生摘要及建立模型需要的所有程式碼。 您可以在安裝 R 指令碼檔的位置找到 R 指令碼檔 **RSQL_RWalkthrough.R**。

+ 如果您熟悉 R，就能立即執行指令碼。
+ 對學習使用 RevoScaleR 人員來說，本教學課程會經歷逐行指令碼。
+ 若要執行指令碼中的個別行，您可以反白顯示檔案中的一或多行，然後按下 Ctrl + ENTER。

> [!TIP]
> 如果您想要稍後再完成本逐步解說的其餘部分，請儲存您的 R 工作區。  如此一來的資料物件和其他變數是供重複使用。

## <a name="define-a-sql-server-compute-context"></a>定義 SQL Server 計算內容

Microsoft R 可讓您輕鬆地取得從資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]R 程式碼中使用。 此程序如下：
  
- 建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連線
- 定義具有您所需資料的查詢，或是指定資料表或檢視
- 定義一或多個在執行 R 程式碼時要使用的計算內容
- （選擇性） 定義會套用至資料來源，而讀取來源的轉換

下列步驟是所有的 R 程式碼的一部分，而且應該的 R 環境中執行。 我們會使用 Microsoft R 用戶端，因為它包含所有 RevoScaleR 封裝，以及一組基本、 輕量的 R 工具。

1. 如果**RevoScaleR**封裝尚未載入，執行這行程式 R 程式碼：

    ```R
    library("RevoScaleR")
    ```

     引號是選擇性的在此情況下，不過建議。
     
     如果您收到錯誤，請確定您的 R 開發環境使用的程式庫，包括 RevoScaleR 封裝。 使用命令，例如`.libPaths()`來檢視目前的程式庫路徑。

2. 建立 SQL Server 連接字串，並將它儲存在 R 變數中， _connStr_。
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=Your_Database_Name;Uid=Your_User_Name;Pwd=Your_Password"
    ```

    伺服器名稱，您可以只使用執行個體名稱，或您可能需要完整限定名稱，根據您的網路。

    Windows 驗證的語法是有點不同：
    
    ```R
    connStrWin <- "Driver=SQL Server;Server=SQL_instance_name;Database=database_name;Trusted_Connection=Yes"
    ```

    提供下載的 R 指令碼只會使用 SQL 登入。 一般而言，我們建議您，盡可能避免將密碼儲存在 R 程式碼中使用 Windows 驗證。 不過，若要確保此教學課程中的程式碼符合從 Github 下載的程式碼，我們會使用 SQL 登入逐步解說的其餘部分。

3. 定義要用來建立新的變數_計算內容_。 建立計算內容物件之後，您可以在 SQL Server 執行個體上執行 R 程式碼中使用它。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間來回序列化 R 物件時，R 會使用暫存目錄。 您可以指定本機目錄以用來做為 *sqlShareDir*，或接受預設值。
  
    - 使用*sqlWait*指出是否要讓 R 等候從伺服器的結果。  如需非等待工作與等候的討論，請參閱[分散式和平行計算，與 Microsoft ScaleR](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用引數*sqlConsoleOutput*來指出您不想要看到從 R 主控台輸出。


4. 您呼叫[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)建構函式以建立計算內容物件的變數和連接字串已經定義過了，R 變數中儲存新物件*sqlcc*。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 根據預設，計算內容是本機電腦，因此您必須明確設定*active*計算內容。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` 會以隱藏方式傳回先前使用中的計算內容，讓您可以使用它
    + `rxGetComputeContext` 會傳回使用中的計算內容
    
    請注意，設定計算內容僅適用於使用 **RevoScaleR** 封裝中的函數所執行的作業，不會影響開放原始碼 R 作業的執行方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>建立資料來源使用 RxSqlServer

在 Microsoft R*資料來源*是您使用 RevoScaleR 函式所建立的物件。 資料來源物件會指定某些您想要使用工作，例如模型訓練或功能擷取的資料集。 您可以從各種來源; 取得資料如需目前支援的來源的清單，請參閱[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

先前您定義的連接字串，並 R 變數中儲存該資訊。 您可以重複使用您想要取得該連接資訊來指定的資料。

1. SQL 查詢儲存為字串變數。 查詢定義用於定型模型的資料。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

2. 將查詢定義做為引數傳遞至 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 函數。

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + 引數  *colClasses* 會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 之間移動資料時要使用的資料行類型。這很重要，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用與 R 不同的資料類型，而且具有更多資料類型。 如需詳細資訊，請參閱[R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。
  
    + 引數*rowsPerRead*是很重要的管理記憶體使用量和有效率的計算。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。  藉由新增*rowsPerRead*參數，您可以控制多少個資料列被讀入處理每個區塊。  如果此參數的值太大，資料存取可能會變慢，因為您沒有足夠的記憶體，可有效率地處理這類大型資料區塊。  在某些系統上，設定*rowsPerRead*極小的值也可以提供效能變慢。

3. 此時，您已建立*inDataSource*物件，但它不包含任何資料。 資料就會不提取從 SQL 查詢到本機的環境直到您執行的函式，例如[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)。

    不過，既然您已定義的資料物件，您可以使用它當做其他函數的引數。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 SQL Server 資料的 R 摘要

在本節中，您會試著中提供的函數的數個[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]支援遠端計算內容。 藉由套用至資料來源的 R 函數，您可以探索、 彙總，及圖表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。

1. 呼叫此函式[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)來取得變數的清單中的資料來源和資料類型。

    **rxGetVarInfo**是很方便的函式; 您可以呼叫它的任何資料框架，或上的遠端資料物件中的資料集，取得資訊，例如最大值與最小值、 資料類型和因數的資料行中的層級數目。
    
    請考慮在任何類型的資料輸入、特徵轉換或特徵工程之後執行此函數。 如此一來，您可以確保所有您想要使用模型中的功能是預期的資料類型，並避免發生錯誤。
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **結果**
    
    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. 現在，呼叫 RevoScaleR 函式[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)以取得有關個別變數的詳細統計資料。

    rxSummary 基礎 R`summary`運作，但有一些額外的功能和優點。 rxSummary 在多個計算內容中運作，並支援區塊處理。  您也可以使用轉換的值，或彙總 rxSummary 因素層級為基礎。
    
    在此範例中，您將摘要說明根據乘客數目價位量。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一個引數指定公式或詞彙的摘要。 在這裡，`F()`函數用來轉換中的值_旅客\_計數_到之前來摘述的因素。 您也必須指定最小值 (1) 和 (6) 的最大值為_旅客\_計數_因數變數。
    + 如果您未指定輸出的統計資料，根據預設 rxSummary 輸出平均值、 標準差、 Min、 Max 和有效且遺失的觀察值的數目。
    + 此範例也會包含一些程式碼來追蹤函數的開始和完成時間，讓您可以比較效能。
  
    **結果**

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    Name  Mean    StdDev   Min Max ValidObs MissingObs
    fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0
    Statistics by category (6 categories):*
    Category                             F_passenger_count Means    StdDev    Min
    fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5
    fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0
    fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5
    fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5
    fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5
    fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0
    Max ValidObs
    55  666
    52  206
    52   51
    39   21
    64   55
    12    1
    "It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."
    ```

您未得到不同的結果嗎？ 這是因為不保證會傳回相同的結果每次較小的查詢使用 TOP 關鍵字。

### <a name="bonus-exercise-on-big-data"></a>再次練習巨量資料

請嘗試定義新的查詢字串的所有資料列。 我們建議您設定此實驗的新資料來源物件。 您也可能會嘗試變更*rowsToRead*參數，以查看它如何影響輸送量。

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> 這執行時，您可以使用這類工具[處理序總管](https://technet.microsoft.com/sysinternals/processexplorer.aspx)或 SQL Profiler 查看建立連接的方式，在 R 程式碼時使用 SQL Server 服務執行。
> 
> 另一個選項是監視使用這些 SQL Server 上執行的 R 作業[自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="next-lesson"></a>下一課

[使用 R 建立圖表和繪圖](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>上一課

[使用 SQL 瀏覽資料](walkthrough-view-and-explore-the-data.md)

