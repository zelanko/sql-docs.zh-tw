---
title: 檢視及摘要使用 R 函式-SQL Server Machine Learning 的 SQL Server 資料
description: 本教學課程示範如何以視覺化方式檢視和產生的 SQL Server 上的資料庫內分析中使用 R 函式的統計摘要。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 368caa21545e534c393aca29ce8fd3a59f9d9837
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644557"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>檢視及摘要使用 R （逐步解說） 的 SQL Server 資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課會為您介紹中的函式**RevoScaleR**封裝，並引導您完成下列工作：

> [!div class="checklist"]
> * 連接至 SQL Server
> * 定義具有您所需資料的查詢，或是指定資料表或檢視
> * 定義一或多個在執行 R 程式碼時要使用的計算內容
> * （選擇性） 定義從來源讀取時套用至資料來源的轉換

## <a name="define-a-sql-server-compute-context"></a>定義 SQL Server 計算內容

用戶端工作站上，在 R 環境中執行下列 R 陳述式。 本節假設[使用 Microsoft R 用戶端的資料科學工作站](../r/set-up-a-data-science-client.md)，因為它包含所有 RevoScaleR 套件，以及一組基本且輕量級的 R 工具。 例如，您可以使用 Rgui.exe 這一節中執行 R 指令碼。

1. 如果**RevoScaleR**套件尚未載入，執行 R 程式碼的這一行：

    ```R
    library("RevoScaleR")
    ```

     引號是選擇性的在此情況下，雖然建議使用。
     
     如果您收到錯誤，請確定您的 R 開發環境使用包含 RevoScaleR 套件的程式庫。 使用命令，例如`.libPaths()`來檢視目前的程式庫路徑。

2. 建立 SQL Server 的連接字串，並將它儲存在 R 變數*connStr*。

   您必須變更預留位置"your_server_name 」 為有效的 SQL Server 執行個體名稱。 伺服器名稱，您可以使用 僅執行個體名稱，或您可能需要完整限定名稱，根據您的網路。
    
   SQL Server 驗證的連接語法如下所示：

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    對於 Windows 驗證，語法會有點不同：
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    一般而言，我們建議您盡可能避免將密碼儲存在 R 程式碼時，才使用 Windows 驗證。

3. 定義要用來建立新的變數*計算內容*。 建立計算內容物件之後，您可以在 SQL Server 執行個體上執行 R 程式碼中使用它。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間來回序列化 R 物件時，R 會使用暫存目錄。 您可以指定本機目錄以用來做為 *sqlShareDir*，或接受預設值。
  
    - 使用*sqlWait*指出是否要 R 等待來自伺服器的結果。  如需等待與非等待工作的討論，請參閱 <<c0> [ 分散式和使用 Microsoft R 中的 RevoScaleR 的平行運算](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。
  
    - 使用引數*sqlConsoleOutput*來表示您不想要看到從 R 主控台的輸出。

4. 您呼叫[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)建構函式使用變數和連接字串已定義，來建立計算內容物件，並將新的物件儲存在 R 變數*sqlcc*。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 根據預設，計算內容是本機，因此您必須明確設定*active*計算內容。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)無形的方式傳回先前使用的計算內容，以便您可以使用它
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)傳回使用中的計算內容
    
    請注意，設定計算內容只會影響使用中的函式的作業**RevoScaleR**套件內容不會影響開放原始碼 R 作業的執行方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>建立 RxSqlServer 資料來源

使用 Microsoft R 程式庫，例如 RevoScaleR 和 MicrosoftML 時*資料來源*是您使用 RevoScaleR 函式所建立的物件。 資料來源物件會指定一些您想要用來執行工作，例如模型訓練或功能擷取的資料集。 您可以從各種來源包括 SQL Server，以取得資料。 如需目前支援的來源清單，請參閱[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

更早版本，您定義的連接字串，且該資訊儲存在 R 變數中。 您可以重複使用您想要取得該連接資訊來指定的資料。

1. 將 SQL 查詢儲存為字串變數。 查詢會定義用於定型模型的資料。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我們利用這裡 TOP 子句來讓執行速度更快，但查詢所傳回的實際資料列而異的順序。 因此，您的摘要結果可能也會不同於下面所列。 放心地移除 TOP 子句。

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
    
    + 引數  *colClasses* 會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 之間移動資料時要使用的資料行類型。這很重要，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用與 R 不同的資料類型，而且具有更多資料類型。 如需詳細資訊，請參閱 < [R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。
  
    + 引數*rowsPerRead*是很重要的管理記憶體使用量和有效率的計算。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。  藉由新增*rowsPerRead*參數，您可以控制多少個資料列被讀入每個區塊以進行處理。  如果此參數的值太大，資料存取可能會變慢，因為您沒有足夠的記憶體來有效率地處理這類大型資料區塊。  在某些系統上，設定*rowsPerRead*為極小的值也可能使效能變慢。

3. 此時，您已建立*inDataSource*物件，但它不包含任何資料。 資料不會提取來自 SQL 查詢至本機環境直到您執行的函式，例如[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或是[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)。

    不過，既然您已定義的資料物件，您可以使用它當做其他函數的引數。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 R 摘要中的 SQL Server 資料

在本節中，您會試用中提供的函數的數個[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，支援遠端計算內容。 藉由將 R 函數套用至資料來源，您可以探索、 總結來說，與圖表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。

1. 呼叫函式[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)來取得變數的清單中的資料來源和資料類型。

    **rxGetVarInfo**是一個好用的函式; 您可以在任何資料框架上，呼叫它，或在一組的遠端資料物件中的資料，以取得資訊，例如最大值和最小值，資料類型，以及因數資料行中的層級數目。
    
    請考慮在任何類型的資料輸入、特徵轉換或特徵工程之後執行此函數。 如此一來，您可以確保所有您想要使用您在模型中的功能都是預期的資料類型，並避免發生錯誤。
  
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

2. 現在，呼叫 RevoScaleR 函數[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)以取得有關個別變數的更詳細統計資料。

    rxSummary 以 R 為基礎`summary`函式，但有一些額外的功能和優點。 rxSummary 在多個計算內容中運作，以及支援區塊處理。  您也可以使用因素層級為基礎的 rxSummary 來轉換值，或彙總。
    
    在此範例中，您將摘要說明根據乘客數的費用金額。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一個引數指定的公式或詞彙，摘要方式。 在這裡，`F()`函數用來轉換中的值_乘客\_計數_成因素，再進行摘要。 您也必須指定最小值 (1) 和 (6) 的最大值為_乘客\_計數_因素變數。
    + 如果您未指定輸出的統計資料，根據預設 rxSummary 會輸出平均值、 StDev、 Min、 Max 和有效和遺失的觀察的次數。
    + 此範例也會包含一些程式碼來追蹤函數的開始和完成時間，讓您可以比較效能。
  
    **結果**

    如果 rxSummary 函式執行成功，您應該會看到結果，這些項目，後面依類別目錄的統計資料的清單。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>巨量資料的額外練習

請嘗試定義新的查詢字串，包含所有資料列。 我們建議您設定新的資料來源物件對於這項實驗。 您也可以嘗試變更*rowsToRead*參數，以查看它如何影響輸送量。

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
> 當這執行時，您可以使用之類的工具[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx)或 SQL Profiler，以查看如何建立連接，在 R 程式碼時使用 SQL Server 服務執行。
> 
> 另一個選項是監視 SQL Server 上使用這些執行的 R 作業[自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 建立圖表及繪圖](walkthrough-create-graphs-and-plots-using-r.md)