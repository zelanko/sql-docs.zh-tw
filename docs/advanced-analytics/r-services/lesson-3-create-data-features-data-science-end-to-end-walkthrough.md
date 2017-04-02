---
title: "第 3 課︰建立資料特徵 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 第 3 課︰建立資料特徵 (資料科學端對端逐步解說)
資料工程是機器學習服務的另一個重要部分。 資料通常必須先進行轉換，才能用於預測模型。 如果資料沒有您所需的特徵，您就能從現有的值加以建立。  
  
針對此模型工作，您希望在上車和下車位置之間有段距離 (以英哩為單位)，而不是使用這兩個位置的原始緯度和經度值。 為了建立這項特徵，您將使用 [aversine 公式](https://en.wikipedia.org/wiki/Haversine_formula)來計算兩個點之間的直線距離。  
您將會比較用於從資料建立特徵的兩個不同方法：  
  
-   使用 R 和 `rxDataStep` 函數    
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的自訂函數  
  
在這兩種方法中，程式碼的結果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源物件 `featureDataSource`，其中包含新的數值特徵 `direct_distance`。  
  
## <a name="creating-features-using-r"></a>使用 R 建立特徵  

R 語言已知有各種豐富的統計程式庫，但您可能仍然需要自訂資料轉換。 

+ 您將建立新的 R 函數 `ComputeDist` 來計算兩點之間的線性距離，這兩點是由緯度和經度值所指定。  
+ 您將呼叫函數來轉換稍早建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料物件中的資料，並將其儲存在新的資料來源 `featureDataSource` 中。  

### <a name="create-the-transformation-function"></a>建立轉換函數  
1.  建立自訂 R 函數 `ComputeDist`。 其會採用兩組經度和緯度值，並計算這兩個值之間的線性距離。  此函數會傳回以英哩為單位的距離。
  
    ```R  
    env <- new.env()  
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
  
    + 第一行會定義新的環境。 在 R 中，環境可用來封裝套件中的命名空間等等。
    + 您可以使用 `search()` 函數來檢視工作區中的環境。 若要檢視特定環境中的物件，請輸入 `ls(<envname>)`。 
    + 以 `$env.ComputeDistance` 開頭的行包含定義 Haversine 公式的程式碼，該公式可計算球面上兩個點之間的「大圓距離」。  
 
  
### <a name="apply-the-transformation-function-to-data"></a>將轉換函數套用至資料

定義函數之後，您會將其套用至資料，以建立新的特徵資料行 *direct_distance*。

1. 使用 `RxSqlServerData` 建構函式來建立要使用的資料來源。  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  呼叫 `rxDataStep` 函數，將 `env$ComputeDist` 函數套用至指定的資料。  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + `rxDataStep` 函數可就地修改資料。 引數包含要傳遞之資料行的字元向量 (*varsToKeep*)，以及定義轉換的清單。
    + 任何轉換的資料行都會自動輸出，因此不需要包含在 *varsToKeep* 引數中。
    + 或者，您可以使用 *varsToDrop* 引數，指定除了指定的變數以外，要包含來源中的所有資料行。  
  
4.  最後，呼叫 `rxGetVarInfo` 來檢查新資料來源的結構描述：  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *結果*
    
    *"It takes CPU Time=0.74 seconds, Elapsed Time=35.75 seconds to generate features."*  
    *Var 1: tipped, Type: integer*   
    *Var 2: fare_amount, Type: numeric*   
    *Var 3: passenger_count, Type: numeric*   
    *Var 4: trip_time_in_secs, Type: numeric*   
    *Var 5: trip_distance, Type: numeric*   
    *Var 6: pickup_datetime, Type: character*   
    *Var 7: dropoff_datetime, Type: character*   
    *Var 8: pickup_longitude, Type: numeric*   
    *Var 9: pickup_latitude, Type: numeric*   
    *Var 10: dropoff_longitude, Type: numeric*   
    *Var 11: dropoff_latitude, Type: numeric*   
    *Var 12: direct_distance, Type: numeric*   
  
## <a name="creating-features-using-transact-sql"></a>使用 Transact-SQL 建立特徵  
既然您已了解如何使用 R 函數建立特徵，您將使用自訂 SQL 函數 `ComputeDist` 來執行相同的作業。 SQL 函數 `ComputeDist` 會在現有的 `RxSqlServerData` 資料物件上運作，以從現有的緯度和經度值，建立新的距離特徵。  
  
您會將轉換的結果儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料物件 `featureDataSource`，就像是使用 R 一樣。  
  
使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的特徵工程通常會比 R 更快。請根據您的資料和工作，選擇最有效率的方法。  

### <a name="define-the-t-sql-custom-function"></a>定義 T-SQL 自訂函數
  
1.  定義新的 SQL 函數 `fnCalculateDistance`  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
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

    + 此 SQL「使用者定義函數」的程式碼會當作您為建立及設定資料庫所執行之 PowerShell 指令碼的一部分來提供。  您的資料庫中應該已有此函數。  如果不存在，請使用 SQL Server Management Studio，在計程車資料儲存所在的相同資料庫中產生該函數。

2.  從任何支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的應用程式執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，即可查看函數如何運作。   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>從 R 呼叫 SQL 函數

1. 儲存 SQL 陳述式，以在 R 變數中呼叫自訂函數。  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] 此查詢與稍早所使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢稍微不同。 它已經過修改，取樣的資料較小，讓本逐步解說能夠更快完成。  
  
4.  現在，使用下列程式碼行從 R 環境呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，並將它套用至 `featureEngineeringQuery`中所定義的資料。  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  現在已建立新的特徵，請呼叫 `rxGetVarsInfo` 來建立特徵資料表的摘要。  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>比較 R 函數和 SQL 函數

結果證明，針對此特定工作， [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數方法比自訂 R 函數更快。 因此，您將在後續步驟中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數進行這些計算。  

請繼續進行下一課，以了解如何使用此資料來建立預測模型，並將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
## <a name="next-lesson"></a>下一課  
[第 4 課︰建立和儲存模型 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>上一課  
[第 2 課︰檢視和瀏覽資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
