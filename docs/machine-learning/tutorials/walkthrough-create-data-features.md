---
title: R 教學課程：特徵設計
description: 本教學課程會示範如何使用 SQL Server 函數進行資料庫內分析來建立資料特徵。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8ae7adc2285a9888778a1d0d560f36e64bafcef0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781800"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>使用 R 和 SQL Server 來建立資料特徵 (逐步解說)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

資料工程是機器學習服務的重要部分。 資料通常必須先進行轉換，才能用於預測模型。 如果資料沒有您所需的特徵，您就能從現有的值加以建立。

針對此模型工作，您希望在上車和下車位置之間有段距離 (以英哩為單位)，而不是使用這兩個位置的原始緯度和經度值。 為了建立此特徵，您會使用[半正矢公式](https://en.wikipedia.org/wiki/Haversine_formula)來計算兩個點之間的直線距離。

在此步驟中，了解用來從資料建立特徵的兩個不同方法：

> [!div class="checklist"]
> * 使用自訂 R 函數
> * 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用自訂 T-SQL 函數

目標是建立一組新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料，其中包含原始資料行及新的數值特徵 *direct_distance*。

## <a name="prerequisites"></a>Prerequisites

此步驟會假設您有以本逐步解說中先前步驟為基礎的進行中 R 工作階段。 它會使用在那些步驟中建立的連接字串和資料來源物件。 會使用下列工具和套件來執行指令碼。

+ Rgui.exe 來執行 R 命令
+ Management Studio 來執行 T-SQL

## <a name="featurization-using-r"></a>使用 R 進行特徵化

R 語言已知有各種豐富的統計程式庫，但您可能仍然需要自訂資料轉換。

首先，讓我們使用 R 使用者習慣的方法：將資料移至您的膝上型電腦，然後執行自訂 R 函數 *ComputeDist*，它會計算以緯度和經度值指定的兩個點之間的直線距離。

1. 您應該還記得您先前所建立的資料來源物件只會取得前 1000 個資料列。 讓我們來定義一個會取得所有資料的查詢。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 使用該查詢建立新的資料來源物件。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) \(英文\) 可以接受包含有效 SELECT 查詢的查詢 (以 _sqlQuery_ 參數的引數形式提供)，或是資料表物件的名稱 (以 _table_ 參數的形式提供)。
    
    - 如果您想要對資料表中的資料進行取樣，便必須使用 _sqlQuery_ 參數，使用 T-SQL TABLESAMPLE 子句定義範例參數，然後將 _rowBuffering_ 引數設定為 FALSE。

3. 執行下列程式碼以建立自訂 R 函數。 ComputeDist 會採用兩組緯度和經度值，並計算它們之間的直線距離，然後傳回以英哩為單位的距離。

    ```R
    env <- new.env();
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){
      R <- 6371/1.609344 #radius in mile
      delta_lat <- dropoff_lat - pickup_lat
      delta_long <- dropoff_long - pickup_long
      degrees_to_radians = pi/180.0
      a1 <- sin(delta_lat/2*degrees_to_radians)
      a2 <- as.numeric(a1)^2
      a3 <- cos(pickup_lat*degrees_to_radians)
      a4 <- cos(dropoff_lat*degrees_to_radians)
      a5 <- sin(delta_long/2*degrees_to_radians)
      a6 <- as.numeric(a5)^2
      a <- a2+a3*a4*a6
      c <- 2*atan2(sqrt(a),sqrt(1-a))
      d <- R*c
      return (d)
    }
    ```
  
    + 第一行會定義新的環境。 在 R 中，環境可用來封裝套件中的命名空間等等。 您可以使用 `search()` 函數來檢視工作區中的環境。 若要檢視特定環境中的物件，請輸入 `ls(<envname>)`。
    + 以 `$env.ComputeDist` 開頭的行包含定義 Haversine 公式的程式碼，該公式可計算球面上兩個點之間的「大圓距離」  。

4. 定義函數之後，您會將它套用至資料，以建立新的特徵資料行 *direct_distance*。 但在您執行轉換之前，請將計算內容變更為本機。

    ```R
    rxSetComputeContext("local");
    ```

5. 呼叫 [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) \(英文\) 函數以取得特徵工程資料，然後將 `env$ComputeDist` 函數套用到記憶體中的資料。

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + rxDataStep 函數支援多種可用來修改就地資料的方法。 如需詳細資訊，請參閱此文件：[如何在 Microsoft R 中對資料進行轉換及子集化](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform) \(英文\)
    
    不過，關於 rxDataStep 有幾個值得注意的重點： 
    
    在其他資料來源中，您可以使用 *varsToKeep* 和 *varsToDrop* 引數，但 SQL Server 資料來源並不支援這些引數。 因此，在此範例中，我們會使用 _transforms_ 引數來指定通過的資料行和已轉換的資料行。 此外，在 SQL Server 計算內容中執行時，_inData_ 引數只能接受 SQL Server 資料來源。

    在較大的資料集上執行上述程式碼時，也有可能會產生警告訊息。 當資料列數目乘以要建立之資料行數目的結果超過設定值 (預設為 3,000,000) 時，rxDataStep 會傳回警告，而且傳回資料框架中的資料列數目將會被截斷。 若要移除該警告，您可以修改 rxDataStep 函數中的 _maxRowsByCols_ 引數。 不過，如果 _maxRowsByCols_ 太大，您可能會在將資料框架載入記憶體時遇到問題。

7. 或者，您可以呼叫 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) \(英文\) 來檢查已轉換資料來源的結構描述。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 特徵化

在本練習中，了解如何使用 SQL 函數取代自訂 R 函數來完成相同的工作。 

切換至 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 或另一個查詢編輯器來執行 T-SQL 指令碼。

1. 使用名為 *fnCalculateDistance* 的 SQL 函數。 NYCTaxi_Sample 資料庫中應該已有此函數。 在 [物件總管] 中，透過瀏覽此路徑來確認該函數是否存在：[Databases] > [NYCTaxi_Sample] > [Programmability] > [Functions] > [Scalar-valued Functions] > dbo.fnCalculateDistance。

    如果該函數不存在，請使用 SQL Server Management Studio 來在 NYCTaxi_Sample 資料庫中產生該函數。

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS decimal(28, 10)
    AS
    BEGIN
      DECLARE @distance decimal(28, 10)
      -- Convert to radians
      SET @Lat1 = @Lat1 / 57.2958
      SET @Long1 = @Long1 / 57.2958
      SET @Lat2 = @Lat2 / 57.2958
      SET @Long2 = @Long2 / 57.2958
      -- Calculate distance
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
      --Convert to miles
      IF @distance <> 0
      BEGIN
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
      END
      RETURN @distance
    END
    ```

2. 在 Management Studio 中的新查詢視窗中，從任何支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的應用程式執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以查看該函數的運作方式。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 若要將值直接插入新的資料表 (您必須先建立它)，您可以新增指定資料表名稱的 **INTO** 子句。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 您也可以從 R 程式碼呼叫 SQL 函數。 切換回 Rgui 並將 SQL 特徵化查詢儲存在 R 變數中。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 此查詢已經過修改，並會取得規模較小的資料樣本，來讓本逐步解說能夠更快完成。 如果您想要取得所有資料，可以移除 TABLESAMPLE 子句；不過，視您的環境而定，系統可能會無法將完整的資料集載入 R 中，因而導致錯誤。
  
5. 使用下列程式碼行從 R 環境呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，並將它套用至 *featureEngineeringQuery* 中所定義的資料。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  您已建立新的特徵，現在請呼叫 **rxGetVarsInfo** 來建立特徵資料表中資料的摘要。
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **結果**

    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > 在某些情況下，您可能會收到類似下面的錯誤：「物件 'fnCalculateDistance' 沒有 EXECUTE 權限」  如果收到的話，請確定您使用的登入具有在資料庫 (而非只是執行個體) 上執行指令碼及建立物件的權限。
    > 檢查物件的結構描述 fnCalculateDistance。 如果物件是由資料庫擁有者所建立，且您的登入屬於 db_datareader 角色，您必須為登入授與執行指令碼的明確權限。

## <a name="comparing-r-functions-and-sql-functions"></a>比較 R 函數和 SQL 函數

還記得用來對 R 程式碼計時的這段程式碼嗎？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

您可以嘗試將它用於 SQL 自訂函數範例，來查看資料轉換在呼叫 SQL 函數時需要花費多少時間。 此外，請嘗試使用 rxSetComputeContext 來切換計算內容並比較時間。

根據您的網路速度及硬體設定，您的時間可能會有很大的差異。 在我們測試的設定中，[!INCLUDE[tsql](../../includes/tsql-md.md)] 函數作法比使用自訂 R 函數還要快。 因此，我們會在後續步驟中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數進行這些計算。

> [!TIP]
> 通常，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的特徵工程會比 R 更快。例如，T-SQL 會包含可套用到常見資料科學計算 (例如移動平均和 *n*-tiles) 的快速視窗化和次序函數。 請根據您的資料和工作，選擇最有效率的方法。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [建置 R 模型並儲存至 SQL](walkthrough-build-and-save-the-model.md)

