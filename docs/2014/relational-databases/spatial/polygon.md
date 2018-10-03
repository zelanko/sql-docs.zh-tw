---
title: Polygon | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a78f615493ad531b8607abb0764891ffcb2805f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194478"
---
# <a name="polygon"></a>多邊形
  A`Polygon`是儲存為一連串點定義一個外部週框環形以及零或多個內部環形的二維介面。  
  
## <a name="polygon-instances"></a>Polygon 執行個體  
 A`Polygon`執行個體可以從環形組成有至少三個相異點。 A`Polygon`執行個體也可以是空白。  
  
 外部和任何內部環形`Polygon`定義它的界限。 此環形內的空間定義了 `Polygon` 的內部。  
  
 下圖顯示的範例`Polygon`執行個體。  
  
 ![幾何 Polygon 執行個體的範例](../../database-engine/media/polygon.gif "幾何 Polygon 執行個體的範例")  
  
 如本圖所示：  
  
1.  圖 1 是`Polygon`其界限由外部環形所定義的執行個體。  
  
2.  圖 2 是 `Polygon` 執行個體，其界限是由一個外部環形和兩個內部環形所定義。 內部環形內的區域是 `Polygon` 執行個體外部的一部分。  
  
3.  圖 3 是有效的 `Polygon` 執行個體，因為它的內部環形會在單一正切點上相交。  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 已接受的 `Polygon` 執行個體是指可儲存在 `geometry` 或 `geography` 變數中而不會擲回例外狀況的執行個體。 接受下列`Polygon`執行個體：  
  
-   空白`Polygon`執行個體  
  
-   具有可接受之外部環形以及零或多個可接受之內部環形的 `Polygon` 執行個體。  
  
 要讓環形成為可接受環形所需的準則如下。  
  
-   `LineString`必須接受的執行個體。  
  
-   `LineString` 執行個體至少必須具有四個點。  
  
-   `LineString` 執行個體的開始和結束點必須相同。  
  
 下列範例會顯示已接受`Polygon`執行個體。  
  
```  
DECLARE @g1 geometry = 'POLYGON EMPTY';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';  
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';  
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';  
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
```  
  
 如 `@g4` 和 `@g5` 所示，已接受的 `Polygon` 執行個體可能不是有效的 `Polygon` 執行個體。 `@g5` 也會顯示 Polygon 執行個體必須只包含具有任何四個點的環形才能被接受。  
  
 下列範例會擲回 `System.FormatException`，因為系統不接受 `Polygon` 執行個體。  
  
```  
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';  
```  
  
 不接受 `@g1`，因為外部環形的 `LineString` 執行個體未包含足夠的點。 不接受 `@g2`，因為外部環形 `LineString` 執行個體的起點與終點不相同。 下列範例具有可接受的外部環形，但是內部環形不是可接受的環形。 這也會擲回 `System.FormatException`。  
  
```  
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 內部環形`Polygon`接觸其本身及彼此在單一正切點，但是，如果內部環形的`Polygon`，跨執行個體無效。  
  
 下列範例示範有效`Polygon`執行個體。  
  
```  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g3` 有效，因為這兩個內部環形在單一點接觸，而且沒有彼此相交。 下列範例會顯示無效的 `Polygon` 執行個體。  
  
```  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';  
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';  
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';  
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();  
```  
  
 `@g1` 無效，因為內部環形與外部環形有兩個接觸點。 `@g2` 無效，因為第二個內部環形位於第一個內部環形的內部。 `@g3` 不是有效因為在多個連續點接觸，兩個內部環形。 `@g4` 無效，因為兩個內部環形的內部互相重疊。 `@g5` 無效，因為內部環形不是第一個環形。 `@g6` 無效，因為環形並未包含至少三個不同的點。  
  
## <a name="examples"></a>範例  
 下列範例會建立包含一個洞及 SRID 10 的簡單 `geometry``Polygon` 執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STPolyFromText('POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))', 10);  
```  
  
 可輸入無效的執行個體，並將它轉換成有效的 `geometry` 執行個體。 在下列 `Polygon`範例中，內部和外部環形會重疊，而且此執行個體無效。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))');  
```  
  
 在下列範例中，會使用 `MakeValid()`讓無效的執行個體變成有效。  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.ToString();  
```  
  
 上述範例傳回的 `geometry` 執行個體是 `MultiPolygon`。  
  
```  
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)), ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))  
```  
  
 下面是另一個將無效執行個體轉換成有效 geometry 執行個體的範例。 在下列範例中，我們已經使用三個完全相同的點來建立 `Polygon` 執行個體：  
  
```tsql  
DECLARE @g geometry  
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');  
SET @g = @g.MakeValid();  
SELECT @g.ToString()  
```  
  
 上述傳回的 geometry 執行個體是 `Point(1 3)`。  如果給定的 `Polygon` 為 `POLYGON((1 3, 1 5, 1 3, 1 3))` ，則 `MakeValid()` 就會傳回 `LINESTRING(1 3, 1 5)`。  
  
## <a name="see-also"></a>另請參閱  
 [STArea &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STExteriorRing &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)   
 [STNumInteriorRing &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)   
 [STInteriorRingN &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)   
 [STCentroid &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [MultiPolygon](../spatial/polygon.md)   
 [空間資料 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [STIsValid &#40;geography 資料類型&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)   
 [STIsValid &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
  
