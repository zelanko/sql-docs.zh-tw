---
title: 使用 R 和 SQL Server 函數建立資料特徵
description: 本教學課程示範如何使用 SQL Server 函數來建立資料功能, 以進行資料庫內分析。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e799b1ccba38d7716f2987112573a1d2d07203cd
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468462"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>使用 R 和 SQL Server 建立資料特徵 (逐步解說)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

資料工程是機器學習服務的重要部分。 資料通常需要轉換, 您才能將它用於預測模型。 如果資料沒有您所需的特徵，您就能從現有的值加以建立。

針對此模型工作，您希望在上車和下車位置之間有段距離 (以英哩為單位)，而不是使用這兩個位置的原始緯度和經度值。 若要建立這項功能, 您可以使用[haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)來計算兩點之間的直接線性距離。

在此步驟中, 您將瞭解從資料建立功能的兩種不同方法:

> [!div class="checklist"]
> * 使用自訂 R 函數
> * 在中使用自訂 T-sql 函數[!INCLUDE[tsql](../../includes/tsql-md.md)]

目標是要建立一組新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料, 其中包含原始資料行加上新的數值功能*direct_distance*。

## <a name="prerequisites"></a>先決條件

此步驟會根據本逐步解說中的先前步驟, 假設正在進行中的 R 會話。 它會使用在這些步驟中建立的連接字串和資料來源物件。 下列工具和封裝是用來執行腳本。

+ 執行 R 命令的 rgui.exe
+ 執行 T-sql 的 Management Studio

## <a name="featurization-using-r"></a>使用 R 特徵化

R 語言已知有各種豐富的統計程式庫，但您可能仍然需要自訂資料轉換。

首先, 讓我們來看看 R 使用者習慣的方式: 將資料放入您的膝上型電腦上, 然後執行自訂 R 函數*ComputeDist*, 這會計算兩個點之間的線性距離, 而緯度和經度值所指定。

1. 請記住, 您稍早建立的資料來源物件只會取得前1000個數據列。 讓我們定義一個可取得所有資料的查詢。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 使用查詢建立新的資料來源物件。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可以接受由有效 SELECT 查詢所組成的查詢 (當做_sqlQuery_參數的引數提供), 或是當做 table 參數提供之資料表物件的名稱。
    
    - 如果您想要從資料表取樣資料, 則必須使用_sqlQuery_參數、使用 t-sql TABLESAMPLE 子句定義取樣參數, 然後將_rowBuffering_引數設定為 FALSE。

3. 執行下列程式碼來建立自訂 R 函數。 ComputeDist 會採用兩組緯度和經度值, 並計算兩者之間的線性距離, 並傳回以英里為單位的距離。

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

4. 定義函數之後, 您可以將它套用至資料, 以建立新的特徵資料行*direct_distance*。 但是在執行轉換之前, 請先將計算內容變更為 [本機]。

    ```R
    rxSetComputeContext("local");
    ```

5. 呼叫[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函式以取得特徵工程資料, 並將`env$ComputeDist`函數套用至記憶體中的資料。

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

    + RxDataStep 函數支援用來就地修改資料的各種方法。 如需詳細資訊, 請參閱這篇文章:[如何在 Microsft R 中轉換和子集資料](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    不過, 有幾個重點值得注意關於 rxDataStep: 
    
    在其他資料來源中, 您可以使用*varsToKeep*和*varsToDrop*引數, 但 SQL Server 資料來源不支援。 因此, 在此範例中, 我們使用了_轉換_引數來指定傳遞資料行和已轉換的資料行。 此外, 在 SQL Server 計算內容中執行時, _inData_引數只能接受 SQL Server 的資料來源。

    上述程式碼也可以在較大的資料集上執行時產生警告訊息。 當資料列數乘以所建立的資料行數目時, 會超過一個設定的值 (預設為 3000000), rxDataStep 會傳回警告, 並會截斷所傳回之資料框架中的資料列數目。 若要移除警告, 您可以修改 rxDataStep 函數中的_maxRowsByCols_引數。 不過, 如果_maxRowsByCols_太大, 您可能會在將資料框架載入記憶體時遇到問題。

7. (選擇性) 您可以呼叫[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)來檢查已轉換資料來源的架構。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 特徵化

在此練習中, 您將瞭解如何使用 SQL 函式 (而不是自訂 R 函數) 來完成相同的工作。 

切換至[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或其他查詢編輯器, 以執行 t-sql 腳本。

1. 使用名為*fnCalculateDistance*的 SQL 函數。 函數應該已經存在於 NYCTaxi_Sample 資料庫中。 在物件總管中, 流覽此路徑來確認函式是否存在:資料庫 > NYCTaxi_Sample > 可程式性 > 函數 > 純量值函式 > dbo. fnCalculateDistance。

    如果函數不存在, 請使用 SQL Server Management Studio 在 NYCTaxi_Sample 資料庫中產生函數。

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

2. 在 Management Studio 的新查詢視窗中, 從任何支援[!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]的應用程式執行下列語句, 以查看函數的運作方式。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 若要將值直接插入新的資料表 (您必須先建立), 您可以加入指定資料表名稱的**into**子句。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 您也可以從 R 程式碼呼叫 SQL 函數。 切換回 Rgui.exe, 並將 SQL 特徵化查詢儲存在 R 變數中。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 此查詢已修改為取得較小的資料範例, 讓此逐步解說更快速。 如果您想要取得所有資料, 可以移除 TABLESAMPLE 子句。不過, 視您的環境而定, 可能無法將完整的資料集載入 R, 因而導致錯誤。
  
5. 使用下列程式碼行從 R 環境呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，並將它套用至 *featureEngineeringQuery* 中所定義的資料。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  現在已建立新功能, 請呼叫**rxGetVarsInfo**以建立功能資料表中的資料摘要。
  
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
    > 在某些情況下, 您可能會收到類似下面的錯誤:*物件 ' fnCalculateDistance ' 上的 EXECUTE 許可權遭到拒絕*若是如此, 請確定您所使用的登入具有執行腳本的許可權, 並在資料庫上建立物件, 而不只是在實例上。
    > 檢查物件的架構 fnCalculateDistance。 如果物件是由資料庫擁有者所建立, 而且您的登入屬於角色 db_datareader, 則您必須授與登入明確的許可權, 才能執行腳本。

## <a name="comparing-r-functions-and-sql-functions"></a>比較 R 函數和 SQL 函數

記得這段程式碼是用來進行 R 程式碼的時間嗎？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

您可以嘗試使用此方法搭配 SQL 自訂函式範例, 以查看呼叫 SQL 函數時資料轉換所花的時間。 此外, 請嘗試使用 rxSetComputeCoNtext 來切換計算內容, 並比較時間。

視您的網路速度和硬體設定而定, 您的時間可能會有很大的差異。 在我們測試的設定中, [!INCLUDE[tsql](../../includes/tsql-md.md)]函式方法比使用自訂 R 函數更快。 因此, 我們在後續的[!INCLUDE[tsql](../../includes/tsql-md.md)]步驟中使用函數進行這些計算。

> [!TIP]
> 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的特徵工程通常會比 R 更快。例如, T-sql 包含快速的視窗化和順位函式, 可套用至常用的資料科學計算, 例如輪流移動平均值和*n*磚。 請根據您的資料和工作，選擇最有效率的方法。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [建立 R 模型並儲存至 SQL](walkthrough-build-and-save-the-model.md)

