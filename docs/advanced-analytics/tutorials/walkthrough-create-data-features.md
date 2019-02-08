---
title: 使用 R 和 SQL Server 函式-SQL Server Machine Learning 建立資料特徵
description: 本教學課程示範如何使用 SQL Server 函式的資料庫內分析建立資料特徵。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 527f88ed14adc0140cbca179177e85670f72cafd
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890009"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>使用 R 和 SQL Server （逐步解說） 建立資料特徵
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料工程是機器學習服務的重要部分。 資料通常需要轉換，才能用於預測模型。 如果資料沒有您所需的特徵，您就能從現有的值加以建立。

針對此模型工作，您希望在上車和下車位置之間有段距離 (以英哩為單位)，而不是使用這兩個位置的原始緯度和經度值。 若要建立這項功能，您可以計算之間的直線距離兩個點，利用[haversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)。

在此步驟中，了解兩個不同的方法，從資料建立一項功能：

> [!div class="checklist"]
> * 使用自訂 R 函數
> * 使用中的自訂 T-SQL 函數 [!INCLUDE[tsql](../../includes/tsql-md.md)]

目標是要建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包含的原始資料行，再加上新的數值特徵的資料集*direct_distance*。

## <a name="prerequisites"></a>先決條件

這個步驟會假設根據先前在本逐步解說的步驟進行中的 R 工作階段。 它會使用連接字串和資料來源中建立的物件執行這些步驟。 下列工具和套件來執行指令碼。

+ 若要執行 R 命令的 Rgui.exe
+ Management Studio 來執行 T-SQL

## <a name="featurization-using-r"></a>使用 R 特徵化

R 語言已知有各種豐富的統計程式庫，但您可能仍然需要自訂資料轉換。

首先，讓我們來試試方式 R 使用者已經習慣： 取得您的膝上型電腦上的資料，然後再執行自訂的 R 函數*ComputeDist*，計算由緯度和經度值所指定的兩個點之間的線性距離。

1. 請記住您稍早建立的資料來源物件中取得前 1000 個資料列。 讓我們定義的查詢會取得所有資料。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. 建立新的資料來源物件，使用查詢。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)可能需要有效的 SELECT 查詢，提供做為引數所組成的任何一項查詢_sqlQuery_參數或資料表物件的名稱，依現狀_表格_參數。
    
    - 如果您想要的範例資料從一個資料表，您必須使用_sqlQuery_參數，定義使用 T-SQL TABLESAMPLE 子句中，取樣參數，並將設定_rowBuffering_引數為 FALSE。

3. 執行下列的程式碼，以建立自訂 R 函數。 ComputeDist 中兩組經度和緯度的值，並計算之間的線性距離，傳回英哩遠的距離。

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

4. 定義函數之後，您將它套用至資料，以建立新的特徵資料行*direct_distance*。 但在執行轉換之前，將計算內容變更為本機。

    ```R
    rxSetComputeContext("local");
    ```

5. 呼叫[rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep)函式收到特性工程設計資料，並套用`env$ComputeDist`函式，在記憶體中的資料。

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

    + RxDataStep 函式支援各種方法來修改位置中的資料。 如需詳細資訊，請參閱這篇文章：[如何在 Microsoft R 中的轉換和子集資料](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    不過，有幾個要點值得注意的是關於 rxDataStep: 
    
    在其他資料來源，您可以使用引數*varsToKeep*並*varsToDrop*，但是這些不支援 SQL Server 資料來源。 因此，在此範例中，我們便_轉換_引數來指定傳遞的資料行和轉換的資料行。 此外，SQL Server 中的執行計算內容中，當_inData_引數只能採用 SQL Server 資料來源。

    上述程式碼可能也會產生較大的資料集上執行時的警告訊息。 當資料列數目乘以數目的資料行建立超過設定值 （預設為 3000000）、 rxDataStep 傳回警告，和在傳回的資料框架中的資料列數目將會被截斷。 若要移除警告，您可以修改_maxRowsByCols_ rxDataStep 函式中的引數。 不過，如果_maxRowsByCols_太大，載入記憶體中的資料框架時，您可能會遇到的問題。

7. （選擇性） 您可以呼叫[rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo)來檢查已轉換的資料來源的結構描述。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>使用 Transact-SQL 特徵化

在此練習中，了解如何完成相同的工作，而不自訂 R 函數中使用 SQL 函式。 

若要切換[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 」 或 「 執行 T-SQL 指令碼的另一個查詢編輯器。

1. 使用 SQL 函式，名為*fnCalculateDistance*。 NYCTaxi_Sample 資料庫中，應該已有此函式。 在 [物件總管] 中，確認函式存在於瀏覽此路徑：資料庫 > NYCTaxi_Sample > 可程式性 > 函式 > 純量值函式 > dbo.fnCalculateDistance。

    如果函式不存在，使用 SQL Server Management Studio 來產生 NYCTaxi_Sample 資料庫中的函式。

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

2. 在 Management Studio 中的 在新的查詢視窗中，執行下列[!INCLUDE[tsql](../../includes/tsql-md.md)]從任何支援的應用程式的陳述式[!INCLUDE[tsql](../../includes/tsql-md.md)]以查看函式的運作方式。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 若要將值直接插入新的資料表 （您必須先建立它），您可以新增**INTO**子句指定的資料表名稱。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. 您也可以從 R 程式碼呼叫 SQL 函數。 切換回 Rgui，並在 R 變數中儲存 SQL 特徵化查詢。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > 此查詢已經過修改，以取得較小的資料，以更快做出此逐步解說範例。 如果您想要取得所有資料，您可以移除 TABLESAMPLE 子句不過，根據您的環境，它可能會無法將完整資料集載入至 R，因而導致發生錯誤。
  
5. 使用下列程式碼行從 R 環境呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，並將它套用至 *featureEngineeringQuery* 中所定義的資料。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  現在，建立新的功能時，呼叫**rxGetVarsInfo**功能資料表中建立資料的摘要。
  
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
    > 在某些情況下，您可能會收到如下錯誤：*EXECUTE 權限遭拒的物件 'fnCalculateDistance'* 若是如此，請確定您使用的登入有執行指令碼，並在資料庫上，而不只是在執行個體建立物件的權限。
    > 檢查物件，fnCalculateDistance 的結構描述。 如果資料庫擁有者，建立物件，而且您的登入都屬於角色 db_datareader，您需要授與登入執行指令碼的明確權限。

## <a name="comparing-r-functions-and-sql-functions"></a>比較 R 函數和 SQL 函式

還記得此段程式碼使用以 R 程式碼的時間嗎？

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

您可以嘗試使用此 SQL 的自訂函式範例，看看多久資料轉換時，會呼叫 SQL 函數。 此外，請嘗試切換計算內容使用 rxSetComputeContext 並比較執行時間。

您的時間可能很大，視您的網路速度和硬體組態而定。 在我們的測試，設定[!INCLUDE[tsql](../../includes/tsql-md.md)]函式的方法是比使用自訂 R 函數更快。 因此，我們使用[!INCLUDE[tsql](../../includes/tsql-md.md)]函式進行後續步驟中的這些計算。

> [!TIP]
> 通常，功能工程使用[!INCLUDE[tsql](../../includes/tsql-md.md)]會比 r 更快比方說，T-SQL 包含快速的視窗化 」 與 「 可套用至常用的資料科學計算，例如移動平均的排名函式和*n*-圖格。 請根據您的資料和工作，選擇最有效率的方法。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [建立 R 模型，並將儲存至 SQL](walkthrough-build-and-save-the-model.md)

