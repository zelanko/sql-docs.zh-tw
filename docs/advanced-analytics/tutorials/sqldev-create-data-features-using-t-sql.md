---
title: 課程 4 請建立資料功能使用 T-SQL 函式 （SQL Server 機器學習） |Microsoft 文件
description: 教學課程顯示如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 98182e8e602b8bba8ca7d7fd58cf23f3fcaaa435
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249541"
---
# <a name="lesson-4-create-data-features-using-r-and-t-sql"></a>第 4 課： 建立使用 R 和 T-SQL 資料功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，從原始資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

## <a name="about-feature-engineering"></a>關於特徵設計

瀏覽資料幾回合之後，您已從資料收集一些深入資訊，並準備好繼續進行「特徵工程」。 這個程序的建立有意義的功能，從原始資料是在建立分析模型的重要步驟。

這個資料集，距離值為基礎的報告計量表距離，並不必然表示地理距離或旅行的實際距離。 因此，您必須使用來源紐約市計程車資料集中可用的座標，來計算上車和下車點之間的直線距離。 您可以使用自訂 [函數中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 公式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來執行這項運算。

您將會使用一個自訂 T-SQL 函數 _fnCalculateDistance_，透過 Haversine 公式來計算距離，並使用第二個自訂 T-SQL 函數 _fnEngineerFeatures_，建立包含所有特徵的資料表。

整個程序如下所示：

- 建立執行計算的 T-SQL 函式

- 呼叫產生功能資料函式

- 儲存功能資料的資料表

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>計算使用 fnCalculateDistance 的旅行距離

此函式_fnCalculateDistance_應該下載並註冊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的準備工作，在此教學課程的一部分。 花點時間檢閱程式碼。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依序展開 [可程式性]、[函數] 和 [純量值函式]。   

2. 以滑鼠右鍵按一下 [fnCalculateDistance]，然後選取 [修改]，在新的查詢視窗中開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。
  
    ```SQL
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

若要將計算的值加入至資料表可以用來定型模型，您將使用另一個函式， _fnEngineerFeatures_。 新的函式會呼叫先前建立的 T-SQL 函式， _fnCalculateDistance_，以取得收取和下車位置之間的直接距離。 

1. 請花幾分鐘檢閱自訂 T-SQL 函數 _fnEngineerFeatures_的程式碼，在進行本逐步解說的準備工作時，應該已為您建立此函數。
  
    ```SQL
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

    + 這個資料表值函式會使用多個資料行做為輸入，並輸出包含多個特徵資料行的資料表。

    + 此函式的目的是建立新功能，用於建立模型。

2.  若要確認此函式運作方式，使用它來計算這些往返的計量付費的距離為 0，但收取和下車位置是不同之地理距離。
  
    ```SQL
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    如您所見，計量表回報的距離不一定會對應到地理距離。 這就是特徵工程之所以很重要的原因。 您可以使用這些提升的資料的功能來定型使用 r 的機器學習模型

## <a name="next-lesson"></a>下一課

[第 5 課： 定型和儲存模型，使用 T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[第 3 課： 探索和視覺化的資料，使用 R 和預存程序](../tutorials/sqldev-explore-and-visualize-the-data.md)
