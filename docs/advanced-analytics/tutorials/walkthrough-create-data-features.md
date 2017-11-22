---
title: "建立資料的功能使用 R 和 SQL （逐步解說） |Microsoft 文件"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 095f5b9880a8f78a8d73461dd8cbeae28f30169e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>建立資料的功能使用 R 和 SQL （逐步解說）

資料工程是機器學習服務的重要部分。 資料往往需要轉換，才能使用的預測模型。 如果資料沒有您所需的特徵，您就能從現有的值加以建立。

針對此模型工作，您希望在上車和下車位置之間有段距離 (以英哩為單位)，而不是使用這兩個位置的原始緯度和經度值。 若要建立這項功能，您可以計算所使用的兩個點之間的直接線性距離[haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)。

在此步驟中，我們來比較兩個不同的方法，從資料建立一項功能：

- 使用自訂 R 函式
- 使用中的自訂 T-SQL 函式[!INCLUDE[tsql](../../includes/tsql-md.md)]

目標是要建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]整組資料，包括原始資料行加上新的數字特徵， *direct_distance*。

## <a name="featurization-using-r"></a>如何使用 R

R 語言已知有各種豐富的統計程式庫，但您可能仍然需要自訂資料轉換。

第一個，就來看看它方式 R 使用者習慣： 取得到您的膝上型電腦上的資料，然後再執行自訂的 R 函數， *ComputeDist*，其中計算緯度和經度值所指定的兩個點之間的線性距離。

1. 請記住您稍早建立的資料來源物件中取得前 1000 個資料列。 現在讓我們來定義查詢以取得所有資料。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 建立新的 SQL Server 資料來源使用查詢。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可組成有效的 SELECT 查詢，做為引數提供的任何一項查詢_sqlQuery_參數或資料表物件的名稱，作為_資料表_參數。
    
    - 如果您想要的範例資料的資料表中，您必須使用_sqlQuery_參數，定義取樣參數使用 T-SQL TABLESAMPLE 子句，並設定_rowBuffering_引數為 FALSE。

3. 執行下列程式碼來建立自訂的 R 函數。 ComputeDist 採用的緯度與經度值的兩個配對中，並計算線性之間的距離，傳回英里的距離。

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
  
    + 第一行會定義新的環境。 在 R 中，環境可用來封裝套件中的命名空間等等。  您可以使用 `search()` 函數來檢視工作區中的環境。 若要檢視特定環境中的物件，請輸入 `ls(<envname>)`。
    + 以 `$env.ComputeDistance` 開頭的行包含定義 Haversine 公式的程式碼，該公式可計算球面上兩個點之間的「大圓距離」  。

4. 定義函式，您將它套用到資料以建立新的特徵資料行， *direct_distance*。 但在執行轉換之前，將計算內容變更為本機。

    ```R
    rxSetComputeContext("local");
    ```

5. 呼叫[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函式收到工程資料，此功能，並套用`env$ComputeDist`函式在記憶體中的資料。

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
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

    + RxDataStep 函式支援各種方法的位置中修改資料。 如需詳細資訊，請參閱這篇文章：[如何 Microsft R 中的轉換和子集資料](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    不過，幾個要點值得注意的 rxDataStep 有關： 
    
    在其他資料來源，您可以使用引數*varsToKeep*和*varsToDrop*，但這些不支援 SQL Server 資料來源。 因此，在此範例中，我們使用_轉換_引數來指定傳遞的資料行和轉換資料行。 此外，執行 SQL Server 中的計算內容中，當_inData_引數只能接受 SQL Server 資料來源。

    上述程式碼也可產生較大的資料集上執行時的警告訊息。 時數的資料列數目的資料行建立超過設定的值 （預設為 3,000,000）、 rxDataStep 傳回警告，並傳回的資料框架中的資料列數目將會被截斷。 若要移除警告，您可以修改_maxRowsByCols_ rxDataStep 函式中的引數。 不過，如果_maxRowsByCols_太大，您可能會遇到問題時載入記憶體中的資料框架。

7. （選擇性） 您可以呼叫[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)檢查已轉換的資料來源的結構描述。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 特徵化

現在，建立自訂的 SQL 函式， *ComputeDist*，若要完成自訂 R 函式與相同的工作。

1. 定義新的自訂 SQL 函數，名稱為 *fnCalculateDistance*。 此使用者定義之 SQL 函數的程式碼，是您建立及設定資料庫所執行之 PowerShell 指令碼的一部分。  您的資料庫中應該已有此函數。

    如果不存在，請使用 SQL Server Management Studio，在計程車資料儲存所在的相同資料庫中產生該函數。

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
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

2. 從任何支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的應用程式執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，即可查看函數如何運作。

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. 定義此函式，它很容易建立您要使用 SQL 的功能，然後將值直接插入新的資料表：

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 不過，我們來看看如何從 R 程式碼呼叫自訂的 SQL 函數。 首先，在 R 變數中儲存 SQL 如何查詢。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 此查詢已經過修改，以取得較小的資料，以加快速度本逐步解說的範例。 您可以移除 TABLESAMPLE 子句，如果您想要讓所有資料。不過，根據您的環境，它可能無法將載入 R、 導致錯誤的完整資料集。
  
5. 使用下列程式碼行從 R 環境呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，並將它套用至 *featureEngineeringQuery* 中所定義的資料。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  現在，建立新的功能時，呼叫**rxGetVarsInfo**功能資料表中建立之資料的摘要。
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *結果*

    ```
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
    > 在某些情況下，您可能會收到這類錯誤： *EXECUTE 權限遭拒的物件 'fnCalculateDistance'*若是如此，請確定您使用的登入有執行指令碼，以及在資料庫上建立物件的權限不只是根據執行個體。
    > 請檢查該物件，fnCalculateDistance 結構描述。 如果物件已建立資料庫擁有者，而且您登入都屬於角色 db_datareader，您需要執行此指令碼的明確權限授與登入。

## <a name="comparing-r-functions-and-sql-functions"></a>比較 R 函式和 SQL 函式

請記住這段程式碼的 R 程式碼的時間？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

您可以嘗試使用此 SQL 的自訂函式範例，若要查看時間資料轉換時，會呼叫 SQL 函式。 此外，請嘗試切換 rxSetComputeContext 與計算內容，並比較時間。

您的時間可能會大大地改變，視您的網路速度和硬體組態而定。 我們所測試的組態中[!INCLUDE[tsql](../../includes/tsql-md.md)]函式方法，就是較快，使用自訂的 R 函數。 因此，我們使用[!INCLUDE[tsql](../../includes/tsql-md.md)]函式的後續步驟中，這些計算。

> [!TIP]
> 通常，功能 工程使用[!INCLUDE[tsql](../../includes/tsql-md.md)]會較快，。例如，T-SQL 包括快速的視窗化和可套用至一般資料科學計算，例如循環移動平均的排名函數和 *n* -磚。 請根據您的資料和工作，選擇最有效率的方法。

## <a name="next-lesson"></a>下一課

[建立 R 模型，並將儲存至 SQL](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>上一課

[檢視及使用 R 的資料摘要](walkthrough-view-and-summarize-data-using-r.md)

