---
title: R + T-SQL 教學課程：資料特徵
description: 此教學課程示範如何將計算新增至預存程序，以便在 R 機器學習模型中使用。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5b588f9cb94d39753040e3251d9a4b2e1f12d49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85670960"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>第 2 課：使用 R 和 T-SQL 建立資料特徵
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

本篇教學課程文章適用 SQL 開發人員，說明如何在 SQL Server 中使用 R。

在此步驟中，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，從原始資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

## <a name="about-feature-engineering"></a>關於特徵工程

瀏覽資料幾回合之後，您已從資料收集一些深入資訊，並準備好繼續進行「特徵工程」  。 這個程序從未經處理資料建立有意義特徵，是建立分析模型的重要步驟。

在此資料集中，距離值是以報告的計量表距離為基礎，不一定代表地理距離或實際的行駛距離。 因此，您必須使用來源紐約市計程車資料集中可用的座標，來計算上車和下車點之間的直線距離。 您可以使用自訂 [函數中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 公式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來執行這項運算。

您將會使用一個自訂 T-SQL 函數 _fnCalculateDistance_，透過 Haversine 公式來計算距離，並使用第二個自訂 T-SQL 函數 _fnEngineerFeatures_，建立包含所有特徵的資料表。

整體程序如下：

- 建立執行計算的 T-SQL 函數

- 呼叫該函數來產生特徵資料

- 將特徵資料儲存至資料表

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>使用 fnCalculateDistance 計算車程距離

在進行本教學課程的準備工作時，應已下載函數 _fnCalculateDistance_ 並向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊。 請花幾分鐘檢閱此程式碼。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依序展開 [可程式性]  、[函數]  和 [純量值函式]  。   

2. 以滑鼠右鍵按一下 [fnCalculateDistance]  ，然後選取 [修改]  ，在新的查詢視窗中開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。
  
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

## <a name="generate-the-features-using-_fnengineerfeatures_"></a>使用 _fnEngineerFeatures_ 產生特徵

若要將計算值加入可用於定型模型的資料表，您將使用另一個函數 _fnEngineerFeatures_。 這個新函數會呼叫先前建立的 T-SQL 函數 _fnCalculateDistance_，以取得上車與下車位置之間的直線距離。 

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

    + 此資料表值函數接受多個資料行作為輸入，然後輸出具有多個特徵資料行的資料表。

    + 此函數的目的是建立新特徵，以便用來建置模型。

2.  若要確認此函數運作正常，可以使用它來計算這些車程的地理距離，其中的計量付費距離為 0，但上車和下車位置不同。
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    如您所見，計量表回報的距離不一定會對應到地理距離。 這就是特徵工程之所以很重要的原因。 您可以使用這些已改善的資料特徵，透過 R 來定型機器學習模型。

## <a name="next-lesson"></a>下一課

[第 3 課：使用 T-SQL 定型及儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[第 1 課：使用 R 和預存程序探索及視覺化資料](sqldev-explore-and-visualize-the-data.md)
