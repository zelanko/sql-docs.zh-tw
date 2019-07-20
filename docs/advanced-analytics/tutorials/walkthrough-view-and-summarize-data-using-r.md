---
title: 使用 R 函數來查看和摘要 SQL Server 資料
description: 本教學課程示範如何在 SQL Server 上使用適用于資料庫內分析的 R 函數來視覺化和產生統計摘要。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 52ba1a8f036037ade42c8483b1735c84cc72867e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345790"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>使用 R 查看和摘要 SQL Server 資料 (逐步解說)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本課程將為您介紹**RevoScaleR**套件中的函式, 並逐步引導您完成下列工作:

> [!div class="checklist"]
> * 連接至 SQL Server
> * 定義具有您所需資料的查詢，或是指定資料表或檢視
> * 定義一或多個在執行 R 程式碼時要使用的計算內容
> * (選擇性) 定義從來源讀取資料來源時所套用的轉換

## <a name="define-a-sql-server-compute-context"></a>定義 SQL Server 計算內容

在用戶端工作站上的 R 環境中執行下列 R 語句。 本節假設[資料科學工作站具有 Microsoft R Client](../r/set-up-a-data-science-client.md), 因為它包含所有 RevoScaleR 的套件, 以及一組基本、輕量的 R 工具。 例如, 您可以使用 Rgui.exe 來執行本節中的 R 腳本。

1. 如果尚未載入**RevoScaleR**封裝, 請執行這行 R 程式碼:

    ```R
    library("RevoScaleR")
    ```

     引號是選擇性的, 但在此案例中是建議的做法。
     
     如果您收到錯誤, 請確定您的 R 開發環境使用包含 RevoScaleR 套件的程式庫。 使用之類`.libPaths()`的命令來查看目前的程式庫路徑。

2. 建立 SQL Server 的連接字串, 並將它儲存在 R 變數*connStr*中。

   您必須將預留位置 "your_server_name" 變更為有效的 SQL Server 實例名稱。 針對 [伺服器名稱], 您可以只使用實例名稱, 或者您可能需要完整限定名稱 (視您的網路而定)。
    
   針對 SQL Server 驗證, 連接語法如下所示:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    對於 Windows 驗證而言, 語法有點不同:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    一般來說, 我們建議您盡可能使用 Windows 驗證, 以避免在 R 程式碼中儲存密碼。

3. 定義用來建立新*計算內容*的變數。 建立計算內容物件之後, 您可以使用它在 SQL Server 實例上執行 R 程式碼。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - 在工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間來回序列化 R 物件時，R 會使用暫存目錄。 您可以指定本機目錄以用來做為 *sqlShareDir*，或接受預設值。
  
    - 使用*sqlWait*來指出您是否想要 R 等待伺服器的結果。  如需等待與非等待工作的討論, 請參閱[Microsoft R 中的使用 RevoScaleR 的分散式和平行](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)運算。
  
    - 使用引數*sqlConsoleOutput* , 以指出您不想看到來自 R 主控台的輸出。

4. 您可以呼叫[RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver)函式, 以使用已定義的變數和連接字串來建立計算內容物件, 並將新的物件儲存在 R 變數*sqlcc*中。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 根據預設, 計算內容是本機的, 因此您必須明確設定使用中  的計算內容。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeCoNtext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)會以不可見的方式傳回先前作用中的計算內容, 讓您可以使用它
    + [rxGetComputeCoNtext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)會傳回使用中的計算內容
    
    請注意, 設定計算內容只會影響使用**RevoScaleR**封裝中之函數的作業;計算內容不會影響開放原始碼 R 作業的執行方式。

## <a name="create-a-data-source-using-rxsqlserver"></a>使用 RxSqlServer 建立資料來源

使用 Microsoft R 程式庫 (例如 RevoScaleR 和 MicrosoftML) 時,*資料來源*是您使用 RevoScaleR 函數建立的物件。 資料來源物件會指定您想要用於工作的一些資料集, 例如模型定型或功能解壓縮。 您可以從各種來源 (包括 SQL Server) 取得資料。 如需目前支援的來源清單, 請參閱[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)。

先前您已定義連接字串, 並將該資訊儲存在 R 變數中。 您可以重複使用該連接資訊來指定您想要取得的資料。

1. 將 SQL 查詢儲存為字串變數。 此查詢會定義用於定型模型的資料。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    我們在這裡使用了 TOP 子句來加快執行速度, 但查詢所傳回的實際資料列會依順序而有所不同。 因此, 您的摘要結果可能也會與下面所列的不同。 請隨意移除 TOP 子句。

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
    
    + 引數  *colClasses* 會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 之間移動資料時要使用的資料行類型。這很重要，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用與 R 不同的資料類型，而且具有更多資料類型。 如需詳細資訊, 請參閱[R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。
  
    + 引數*rowsPerRead*對於管理記憶體使用量和有效率的計算而言很重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。  藉由新增*rowsPerRead*參數, 您可以控制要將多少資料列讀入每個區塊以進行處理。  如果此參數的值太大, 資料存取可能會變慢, 因為您沒有足夠的記憶體可以有效率地處理這類大型資料區塊。  在某些系統上, 將*rowsPerRead*設定為過小的值也可以提供較慢的效能。

3. 此時, 您已建立*inDataSource*物件, 但它不包含任何資料。 除非您執行[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)或[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary)之類的函式, 否則資料不會從 SQL 查詢提取到本機環境中。

    不過, 現在您已定義資料物件, 您可以使用它做為其他函數的引數。

## <a name="use-the-sql-server-data-in-r-summaries"></a>使用 R 摘要中的 SQL Server 資料

在本節中, 您會試用中所提供的數個功能[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] , 以支援遠端計算內容。 藉由將 R 函數套用至資料來源, 您可以流覽、摘要資料並繪製[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其圖表。

1. 呼叫函數[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) , 以取得資料來源中的變數及其資料類型的清單。

    **rxGetVarInfo**是一個方便的函式;您可以在任何資料框架或遠端資料物件中的一組資料上呼叫它, 以取得資訊, 例如最大值和最小值、資料類型, 以及因素資料行中的層級數目。
    
    請考慮在任何類型的資料輸入、特徵轉換或特徵工程之後執行此函數。 如此一來, 您就可以確保您想要在模型中使用的所有功能都是預期的資料類型, 並避免發生錯誤。
  
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

2. 現在, 呼叫 RevoScaleR 函數[rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) , 以取得有關個別變數的更詳細統計資料。

    rxSummary 是以 R `summary`函數為基礎, 但有一些額外的功能和優點。 rxSummary 適用于多個計算內容, 並支援區塊化。  您也可以使用 rxSummary 來轉換值, 或根據因素層級摘要。
    
    在此範例中, 您會根據乘客數目摘要說明費用金額。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + RxSummary 的第一個引數會指定要做為摘要依據的公式或詞彙。 在這裡, `F()`函式會用來將_乘客\_計數_中的值轉換成在總結前的因素。 您也必須指定_乘客\_計數_因數變數的最小值 (1) 和最大值 (6)。
    + 如果您未指定輸出的統計資料, 則根據預設, rxSummary 會輸出 Mean、StDev、Min、Max 和有效和遺失的觀察值。
    + 此範例也會包含一些程式碼來追蹤函數的開始和完成時間，讓您可以比較效能。
  
    **結果**

    如果 rxSummary 函式執行成功, 您應該會看到像這樣的結果, 後面接著依類別列出的統計資料。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Big data 的額外練習

嘗試使用所有資料列來定義新的查詢字串。 我們建議您為此實驗設定新的資料來源物件。 您也可以嘗試變更*rowsToRead*參數, 以查看它對輸送量的影響。

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
> 執行此作業時, 您可以使用[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx)或 SQL Profiler 之類的工具, 來查看如何建立連接, 以及如何使用 SQL Server 服務來執行 R 程式碼。
> 
> 另一個選項是使用這些[自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)來監視在 SQL Server 上執行的 R 作業。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 建立圖表及繪圖](walkthrough-create-graphs-and-plots-using-r.md)