---
title: 使用 R 和 T-SQL 函式-SQL Server 機器學習的第 2 課建立的資料功能
description: 本教學課程示範如何將計算加入至用於 R 機器學習服務模型中的預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 32f762de13a844f12144e89f4742409c3afcbab0
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511965"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>第 2 課：使用 R 和 T-SQL 建立資料特徵
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，從原始資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

## <a name="about-feature-engineering"></a>關於特徵工程設計

瀏覽資料幾回合之後，您已從資料收集一些深入資訊，並準備好繼續進行「特徵工程」。 此程序，從未經處理的資料建立有意義的功能是建立分析模型的重要步驟。

在此資料集中，距離值會根據報告的計量表距離，並不一定代表地理距離或行車實際距離。 因此，您必須使用來源紐約市計程車資料集中可用的座標，來計算上車和下車點之間的直線距離。 您可以使用自訂 [函數中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 公式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來執行這項運算。

您將會使用一個自訂 T-SQL 函數 _fnCalculateDistance_，透過 Haversine 公式來計算距離，並使用第二個自訂 T-SQL 函數 _fnEngineerFeatures_，建立包含所有特徵的資料表。

整個程序如下所示：

- 建立會執行計算的 T-SQL 函式

- 呼叫函數來產生功能資料

- 功能資料儲存至資料表

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>計算使用 fnCalculateDistance 車程距離

此函式_fnCalculateDistance_應該下載並向[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]準備本教學課程的過程。 花點時間檢閱程式碼。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依序展開 [可程式性]、[函數] 和 [純量值函式]。   

2. 以滑鼠右鍵按一下 [fnCalculateDistance]，然後選取 [修改]，在新的查詢視窗中開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
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
    GO
    ```
  
    - 此函數是純量值函式，會傳回預先定義類型的單一資料值。
  
    - 它接受緯度和經度值作為輸入，並從車程的上車和下車位置取得這些值。 Haversine 公式會將這些位置轉換成弧度，然後使用這些值來計算這兩個位置之間的直線距離。

## <a name="generate-the-features-using-fnengineerfeatures"></a>產生使用的功能_fnEngineerFeatures_

若要新增的計算的值可用來定型模型的資料表，您將使用另一個函式， _fnEngineerFeatures_。 新的函式會呼叫先前建立的 T-SQL 函數_fnCalculateDistance_，以取得上車和下車位置之間的直線距離。 

1. 請花幾分鐘檢閱自訂 T-SQL 函數 _fnEngineerFeatures_的程式碼，在進行本逐步解說的準備工作時，應該已為您建立此函數。
  
    ```sql
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + 此資料表值函式會採用多個資料行做為輸入，並將輸出具有多個特徵資料行的資料表。

    + 此函式的目的是要建立新的功能，用於建立模型。

2.  若要確認此函式運作方式，使用它來計算這些車程，其中的計量付費的距離為 0，但上車和下車位置不同的地理距離。
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    如您所見，計量表回報的距離不一定會對應到地理距離。 這就是特徵工程之所以很重要的原因。 您可以使用這些改進的資料功能來定型機器學習模型，使用。

## <a name="next-lesson"></a>下一課

[第 3 課：訓練及儲存模型，使用 T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[第 1 課：瀏覽及視覺化資料使用 R 和預存程序](sqldev-explore-and-visualize-the-data.md)
