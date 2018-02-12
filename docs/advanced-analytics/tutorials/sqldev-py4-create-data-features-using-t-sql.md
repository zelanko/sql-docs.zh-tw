---
title: "步驟 4︰使用 T-SQL 建立資料特徵 | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 3adcfd4a53da9f0e61c7ae62d1367cff48194782
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="step-4-create-data-features-using-t-sql"></a>步驟 4︰使用 T-SQL 建立資料特徵
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料探索之後, 您已經從資料收集一些深入資訊後，即可移至*功能工程*。 這個程序的功能建立從原始資料可以是進階的分析模型的重要步驟。

這篇文章的教學課程中，屬於[SQL 開發人員的資料庫中的 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數，從原始資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

## <a name="define-the-function"></a>定義函數

原始資料中報告的距離值是以報告的計量表距離為基礎，不一定代表地理距離或行車距離。 因此，您必須使用來源紐約市計程車資料集中可用的座標，來計算上車和下車點之間的直線距離。 您可以使用自訂 [函數中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 公式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來執行這項運算。

您將會使用一個自訂 T-SQL 函數 _fnCalculateDistance_，透過 Haversine 公式來計算距離，並使用第二個自訂 T-SQL 函數 _fnEngineerFeatures_，建立包含所有特徵的資料表。

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>計算使用 fnCalculateDistance 的旅行距離

1.  在進行本逐步解說的準備工作時，已下載並向 _註冊函數_ fnCalculateDistance [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 花點時間檢閱程式碼。
  
    在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依序展開 [可程式性]、[函數] 和 [純量值函式]。
    以滑鼠右鍵按一下 [fnCalculateDistance]，然後選取 [修改]，在新的查詢視窗中開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。
  
    ```SQL
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function that calculates the direct distance between two geographical coordinates
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
**注意：**

- 此函數是純量值函式，會傳回預先定義類型的單一資料值。
- 它接受緯度和經度值作為輸入，並從車程的上車和下車位置取得這些值。 Haversine 公式會將這些位置轉換成弧度，然後使用這些值來計算這兩個位置之間的直線距離。

若要將計算值加入可用於定型模型的資料表，您將使用另一個函數 _fnEngineerFeatures_。

### <a name="save-the-features-using-fnengineerfeatures"></a>儲存使用的功能_fnEngineerFeatures_

1.  請花幾分鐘檢閱自訂 T-SQL 函數 _fnEngineerFeatures_的程式碼，在進行本逐步解說的準備工作時，應該已為您建立此函數。
  
    此函數是資料表值函式，接受多個資料行作為輸入，然後輸出具有多個特徵資料行的資料表。  此函數的目的是建立特徵集，以用於建立模型。 _fnEngineerFeatures_ 函數會呼叫先前建立的 T-SQL 函數 _fnCalculateDistance_，以取得上車與下車位置之間的直線距離。
  
    ```
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
  
2. 若要確認此函數運作正常，您可以使用它來計算這些車程的地理距離，其中的計量付費距離為 0，但上車和下車位置不同。
  
    ```
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    如您所見，計量表回報的距離不一定會對應到地理距離。 這就是為什麼特徵設計很重要。

在下一個步驟中，您將學習如何使用這些資料功能來建立及定型使用 Python 的機器學習模型。

## <a name="next-step"></a>下一步

[步驟 5： 訓練並儲存使用 T-SQL Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一個步驟

[步驟 3：瀏覽及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)


