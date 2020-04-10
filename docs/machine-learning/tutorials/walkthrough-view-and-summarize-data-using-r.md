---
title: R 教學課程：探索資料
description: 本教學課程示範如何使用 R 函式在 SQL Server 上進行資料庫內分析，以產生統計摘要並將其視覺化。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e74224851d2c475cd89160b362ba163d53c00f61
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115691"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>使用 R 來檢視及摘要 SQL Server 資料 (逐步解說)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本課程會向您介紹 **RevoScaleR** 套件中的函式，並逐步引導您完成下列工作：

> [!div class="checklist"]
> * 連接至 SQL Server
> * 定義具有您所需資料的查詢，或是指定資料表或檢視
> * 定義一或多個在執行 R 程式碼時要使用的計算內容
> * (選擇性) 定義從來源讀取資料來源時，套用至該資料來源的轉換

## <a name="define-a-sql-server-compute-context"></a>定義 SQL Server 計算內容

在用戶端工作站上的 R 環境中執行下列 R 陳述式。 本節會假設有一個[具有 Microsoft R Client 的 資料科學工作站](../r/set-up-a-data-science-client.md)，因為它包含所有 RevoScaleR 套件，以及一組基本、輕量型的 R 工具。 例如，您可以使用 Rgui.exe 來執行本節中的 R 指令碼。

1. 如果尚未載入 **RevoScaleR** 套件，請執行這一行 R 程式碼：

    ```R
    library("RevoScaleR")
    ```

     引號是選擇性的，不過，在此案例中建議使用。
     
     如果您收到錯誤，請確定 R 開發環境使用包含 RevoScaleR 套件的程式庫。 使用 `.libPaths()` 之類的命令來檢視目前的程式庫路徑。

2. 建立 SQL Server 的連接字串，並將其儲存在 R 變數 *connStr* 中。

   您必須將預留位置 "your_server_name" 變更為有效的 SQL Server 執行個體名稱。 在伺服器名稱方面，視您的網路而定，您可能可以只使用執行個體名稱，或是可能需要完整限定該名稱。
    
   SQL Server 驗證的連線語法如下：

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Windows 驗證的語法略有不同：
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    一般而言，建議您儘可能使用 Windows 驗證，以避免在 R 程式碼中儲存密碼。

3. 定義要用於建立新「計算內容」  的變數。 建立計算內容物件之後，您可以使用它在 SQL Server 執行個體上執行 R 程式碼。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間來回序列化 R 物件時，R 會使用暫存目錄。 您可以指定本機目錄以用來做為 *sqlShareDir*，或接受預設值。
  
    - 使用 *sqlWait* 來指出您是否想讓 R 等待來自伺服器的結果。  如需有關等待與非等待作業之比較的討論，請參閱 [Microsoft R 中 RevoScaleR 的分散式計算與平行計算](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用引數 *sqlConsoleOutput* 來指出您不想看到來自 R 主控台的輸出。

4. 您需呼叫 [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)建構函式，以使用變數和已經定義的連接字串來建立計算內容物件，並將新物件儲存在 R 變數 *sqlcc* 中。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 計算內容預設為本機內容，因此您必須明確設定「作用中」  計算內容。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 會以隱藏方式傳回先前作用中的計算內容，讓您可以使用它
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 會傳回作用中計算內容
    
    請注意，設定計算內容只會影響使用 **RevoScaleR** 套件中函式的作業；計算內容不會影響開放原始碼 R 作業的執行方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>使用 RxSqlServer 來建立資料來源

使用 Microsoft R 程式庫 (例如 RevoScaleR 和 MicrosoftML) 時，「資料來源」  係指您使用 RevoScaleR 函式來建立的物件。 資料來源物件會指定您要用於工作 (例如模型定型或特徵擷取) 的某組資料。 您可以從各種來源 (包括 SQL Server) 取得資料。 如需目前支援的來源清單，請參閱 [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) \(英文\)。

您在稍早已定義連接字串，並將該資訊儲存在 R 變數中。 您可以重複使用該連線資訊來指定想要取得的資料。

1. 將 SQL 查詢儲存為字串變數。 此查詢會定義用於將模型定型的資料。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我們在這裡使用了 TOP 子句來加快執行速度，但查詢所傳回的實際資料列可能依順序而有所不同。 因此，您的摘要結果可能也與下面所列出的不同。 請隨意移除 TOP 子句。

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
    
    + 引數  *colClasses* 會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 之間移動資料時要使用的資料行類型。這很重要，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用與 R 不同的資料類型，而且具有更多資料類型。 如需詳細資訊，請參閱 [R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。
  
    + 引數 *rowsPerRead* 對於管理記憶體使用量和有效率的計算而言很重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。  藉由新增 *rowsPerRead* 參數，您可以控制讀入每個區塊以進行處理的資料列數目。  如果此參數的值太大，資料存取可能會較慢，因為您沒有足夠的記憶體，無法有效率地處理這樣大的資料區塊。  在某些系統上，將 *rowsPerRead* 設定為過小的值也可能使效能變慢。

3. 目前，您已建立 *inDataSource* 物件，但它並未包含任何資料。 必須在您執行 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 或 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)之類的函式之後，才會將資料從 SQL 查詢提取至本機環境。

    不過，既然您已定義資料物件，您便可以使用它作為其他函式的引數。

## <a name="use-the-sql-server-data-in-r-summaries"></a>在 R 摘要中使用 SQL Server 資料

在本節中，您將試用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中所提供、數個支援遠端計算內容的函式。 您可以將 R 函式套用至資料來源，來探索、摘要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料及為其繪製圖表。

1. 呼叫函式 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)以取得資料來源中之變數及其資料類型的清單。

    **rxGetVarInfo** 是一個便利的函式；您可以在任何資料框架上或在遠端資料物件中的一組資料上呼叫它，以取得最大值和最小值、資料類型，以及因數資料行中的層級數目等資訊。
    
    請考慮在任何類型的資料輸入、特徵轉換或特徵工程之後執行此函數。 這樣做可確保您要在模型中使用的所有特徵都屬於預期的資料類型，而避免發生錯誤。
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **結果**
    
    ```R
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

2. 現在，呼叫 RevoScaleR 函式 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) 以取得有關個別變數的更詳細統計資料。

    rxSummary 以 R `summary` 函式為基礎，但有一些額外的功能和優點。 rxSummary 可在多個計算內容中運作，並且支援區塊化。  您也可以使用 rxSummary 來轉換值，或根據因數層級進行摘要。
    
    在此範例中，您會根據乘客數來摘要費用金額。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + rxSummary 的第一個引數會指定作為摘要方式的公式或詞彙。 此處的 `F()` 函式可用來在摘要之前，先將 _passenger\_count_ 中的值轉換成因數。 您也必須指定 _passenger\_count_ 因數變數的最小值 (1) 和最大值 (6)。
    + 如果您未指定要輸出的統計資料，rxSummary 預設會輸出平均值、標準差、最小值、最大值，以及有效和遺失的觀察值。
    + 此範例也會包含一些程式碼來追蹤函數的開始和完成時間，讓您可以比較效能。
  
    **結果**

    如果 rxSummary 函式成功執行，您應該會看到類似以下的結果，後面接著依類別區分的統計資料清單。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>巨量資料的額外練習

嘗試使用所有資料列來定義新的查詢字串。 建議您為此實驗設定一個新的資料來源物件。 您也可以嘗試變更 *rowsToRead* 參數，來查看它如何影響輸送量。

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
> 當此作業執行時，您可以使用[處理序總管](https://technet.microsoft.com/sysinternals/processexplorer.aspx) 或 SQL Profiler 之類的工具，來查看如何使用 SQL Server 服務來建立連線及執行 R 程式碼。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 建立圖表及繪圖](walkthrough-create-graphs-and-plots-using-r.md)