---
description: Polygon
title: Polygon | Microsoft Docs
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46c16da6c20ae3dc99d437b114c36a15485ed216
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473189"
---
# <a name="polygon"></a>Polygon

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  **Polygon** 是儲存為一連串點的二維介面，這些點可定義一個外部週框環形以及零個或多個內部環形。  
  
## <a name="polygon-instances"></a>Polygon 執行個體  
 **Polygon** 執行個體可以從環形組成 (此環形至少有三個相異點)。 **Polygon** 執行個體也可以是空的。  
  
**Polygon** 的外部和任何內部環形定義了它的界限。 此環形內的空間定義了 **Polygon** 的內部。  
  
下圖顯示 **Polygon** 執行個體的範例。  
  
 ![幾何多邊形執行個體的範例](../../relational-databases/spatial/media/polygon.gif "幾何多邊形執行個體的範例")  
  
如本圖所示：  
  
1.  圖 1 是 **Polygon** 執行個體，其界限是由外部環形所定義。  
  
2.  圖 2 是 **Polygon** 執行個體，其界限是由一個外部環形和兩個內部環形所定義。 內部環形內的區域是 **Polygon** 執行個體外部的一部分。  
  
3.  圖 3 是有效的 **Polygon** 執行個體，因為它的內部環形會在單一正切點上相交。  

### <a name="accepted-instances"></a>已接受的執行個體  
 已接受的 **Polygon** 執行個體是指可儲存在 **geometry** 或 **geography** 變數中而不會擲回例外狀況的執行個體。 已接受的 **Polygon** 執行個體如下：  
  
-   空白的 **Polygon** 執行個體  
-   具有可接受之外環 (**LineString**) 以及零或多個可接受之內環 (**LineStrings**) 的 **Polygon** 執行個體。  
  
要讓環形成為可接受環 (**LineString**) 所需的條件如下。  
  
-   系統必須接受 **LineString** 執行個體。  
-   **LineString** 執行個體至少必須具有四個點。  
-   **LineString** 執行個體的開始和結束點必須相同。  
  
下列範例會顯示已接受的 **Polygon** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'POLYGON EMPTY';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';  
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';  
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';  
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
```  
  
如 `@g4` 和 `@g5` 所示，已接受的 **Polygon** 執行個體可能不是有效的 **Polygon** 執行個體。 `@g5` 也會顯示 Polygon 執行個體必須只包含具有任何四個點的環形才能被接受。  
  
下列範例會擲回 `System.FormatException` ，因為系統不接受 **Polygon** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';  
```  
  
`@g1` 不接受，因為外部環形的 **LineString** 執行個體未包含足夠的點。 `@g2` 不接受，因為外部環形 **LineString** 執行個體的起點與終點不相同。 下列範例具有可接受的外部環形，但是內部環形不是可接受的環形。 這也會擲回 `System.FormatException`。  
  
```sql  
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 **Polygon** 的內部環形可以在單一正切點上接觸其本身及彼此接觸，但是如果 **Polygon** 的內部環形相交，此執行個體就會無效。  
  
 下列範例會顯示有效的 **Polygon** 執行個體。  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g3` 有效，因為這兩個內部環形在單一點接觸，而且沒有彼此相交。 下列範例會顯示無效的 `Polygon` 執行個體。  
  
```sql   
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';  
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';  
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';  
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();  
```  
  
 `@g1` 無效，因為內部環形與外部環形有兩個接觸點。 `@g2` 無效，因為第二個內部環形位於第一個內部環形的內部。 `@g3` 無效，因為兩個內部環形有多個連續接觸點。 `@g4` 無效，因為兩個內部環形的內部互相重疊。 `@g5` 無效，因為內部環形不是第一個環形。 `@g6` 無效，因為環形並未包含至少三個不同的點。  
  
## <a name="examples"></a>範例  
### <a name="example-a"></a>範例 A。  
下列範例會建立包含間距及 SRID 10 的簡單 `geometry` `Polygon` 執行個體。
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STPolyFromText(
    'POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))',
    10);
```  
  

### <a name="example-b"></a>範例 B.   
可輸入無效的執行個體，並將它轉換成有效的 `geometry` 執行個體。 在下列 `Polygon`範例中，內部和外部環形會重疊，而且此執行個體無效。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse(
    'POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))'
    );  
```  
  
### <a name="example-c"></a>範例 C。  
在下列範例中，會使用 `MakeValid()`讓無效的執行個體變成有效。  
  
```sql  
SET @g = @g.MakeValid();  
SELECT @g.ToString();  
```  
  
上述範例傳回的 `geometry` 執行個體是 `MultiPolygon`。  
  
```sql  
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)),
              ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```  
  
### <a name="example-d"></a>範例 D.  
這是另一個將無效執行個體轉換成有效 geometry 執行個體的範例。 在下列範例中，我們已經使用三個完全相同的點來建立 `Polygon` 執行個體：  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');  
SET @g = @g.MakeValid();  
SELECT @g.ToString()  
```  
  
上述傳回的 geometry 執行個體是 `Point(1 3)`。  如果給定的 `Polygon` 為 `POLYGON((1 3, 1 5, 1 3, 1 3))` ，則 `MakeValid()` 就會傳回 `LINESTRING(1 3, 1 5)`。  
  
## <a name="see-also"></a>另請參閱  
 [STArea &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STExteriorRing &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)   
 [STNumInteriorRing &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)   
 [STInteriorRingN &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)   
 [STCentroid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [MultiPolygon](../../relational-databases/spatial/multipolygon.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [STIsValid &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STIsValid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
  
