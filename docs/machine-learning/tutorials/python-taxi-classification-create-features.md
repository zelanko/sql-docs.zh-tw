---
title: Python 教學課程：建立資料特徵
titleSuffix: SQL machine learning
description: 在這五部分教學課程系列的第三部分中，您會將計算新增至預存程序，以用於 SQL 機器學習的 Python 機器學習模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: db28a38415d62abe9bab3540c47567a92df25104
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470349"
---
# <a name="python-tutorial-create-data-features-using-t-sql"></a>Python 教學課程：使用 T-SQL 建立資料特徵
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

在這個五部分教學課程系列的第三部分中，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式，從未經處理的資料建立特徵。 接著，您將從 SQL 預存程序呼叫該函式，以建立包含特徵值的資料表。

*特徵工程* 的程序 (從未經處理資料建立特徵)，會是建立進階分析模型的重要步驟。

在本文中，您將：

> [!div class="checklist"]
> + 修改自訂函式以計算路程距離
> + 使用另一個自訂函式儲存特徵

在[第一部分](python-taxi-classification-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](python-taxi-classification-explore-data.md)中，您已探索範例資料並產生一些繪圖。

在[第四部分](python-taxi-classification-train-model.md)中，您將載入模組，並呼叫所需的函式，以使用 SQL Server 預存程序來建立和定型模型。

在[第五部分](python-taxi-classification-deploy-model.md)中，您將了解如何運作您在第四部分中定型並儲存的模型。

## <a name="define-the-function"></a>定義函數

原始資料中報告的距離值是以報告的計量表距離為基礎，不一定代表地理距離或行車距離。 因此，您必須使用來源紐約市計程車資料集中可用的座標，來計算上車和下車點之間的直線距離。 您可以使用自訂 [函數中的](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 公式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來執行這項運算。

您將會使用一個自訂 T-SQL 函數 _fnCalculateDistance_，透過 Haversine 公式來計算距離，並使用第二個自訂 T-SQL 函數 _fnEngineerFeatures_，建立包含所有特徵的資料表。

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>使用 fnCalculateDistance 計算車程距離

1. 函式 _fnCalculateDistance_ 包含在範例資料庫中。 請花幾分鐘檢閱此程式碼。
  
2. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，依序展開 [可程式性]、[函數] 和 [純量值函式]。
   以滑鼠右鍵按一下 [fnCalculateDistance]，然後選取 [修改]，在新的查詢視窗中開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。
  
   ```sql
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

+ 此函數是純量值函式，會傳回預先定義類型的單一資料值。
+ 它接受緯度和經度值作為輸入，並從車程的上車和下車位置取得這些值。 Haversine 公式會將這些位置轉換成弧度，然後使用這些值來計算這兩個位置之間的直線距離。

若要將計算值加入可用於定型模型的資料表，您將使用另一個函數 _fnEngineerFeatures_。

### <a name="save-the-features-using-_fnengineerfeatures_"></a>使用 _fnEngineerFeatures_ 儲存特徵

1. 請花幾分鐘的時間檢閱包含在範例資料庫中的自訂 T-SQL 函式 _fnEngineerFeatures_ 的程式碼。
  
   此函數是資料表值函式，接受多個資料行作為輸入，然後輸出具有多個特徵資料行的資料表。  此函數的目的是建立特徵集，以用於建立模型。 _fnEngineerFeatures_ 函數會呼叫先前建立的 T-SQL 函數 _fnCalculateDistance_，以取得上車與下車位置之間的直線距離。
  
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
  
2. 若要確認此函數運作正常，您可以使用它來計算這些車程的地理距離，其中的計量付費距離為 0，但上車和下車位置不同。
  
   ```sql
       SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
       trip_distance, pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
       FROM nyctaxi_sample
       WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
       ORDER BY trip_time_in_secs DESC
   ```
  
   如您所見，計量表回報的距離不一定會對應到地理距離。 這就是特徵工程之所以重要的原因。

在下一個部分中，您將了解如何使用這些資料特徵，透過 Python 建立和定型機器學習模型。

## <a name="next-steps"></a>後續步驟

在本文章中，您將：

> [!div class="checklist"]
> + 已修改自訂函式以計算路程距離
> + 已使用另一個自訂函式儲存特徵

> [!div class="nextstepaction"]
> [Python 教學課程：使用 T-SQL 定型及儲存 Python 模型](python-taxi-classification-train-model.md)