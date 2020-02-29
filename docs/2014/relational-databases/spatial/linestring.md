---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: e1bdfd447fdf61123615dad329b297490172b191
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176668"
---
# <a name="linestring"></a>LineString
  
  `LineString` 是代表一連串的點及連接這些點之線段的一維度物件。

## <a name="linestring-instances"></a>LineString 執行個體
 下圖顯示 `LineString` 執行個體的範例。

 ![幾何 LineString 執行個體的範例](../../database-engine/media/linestring.gif "幾何 LineString 執行個體的範例")

 如本圖所示：

-   圖 1 是簡單、非封閉的 `LineString` 執行個體。

-   圖 2 是非簡單、非封閉的 `LineString` 執行個體。

-   圖 3 是簡單、封閉的 `LineString` 執行個體，因此它是環形。

-   圖 4 是非簡單、封閉的 `LineString` 執行個體，因此它不是環形。

### <a name="accepted-instances"></a>已接受的執行個體
 您可以將已接受的 `LineString` 執行個體放入 geometry 變數中，但是它們可能不是有效的 `LineString` 執行個體。 若要讓系統接受 `LineString` 執行個體，就必須符合下列準則。 此執行個體至少必須由兩個點所組成，或者它必須是空的。 下面是已接受的 LineString 執行個體。

```
DECLARE @g1 geometry = 'LINESTRING EMPTY';
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';
```

 
  `@g3` 顯示 `LineString` 執行個體可被系統接受但卻無效。

 下面是無法接受的 `LineString` 執行個體。 它將擲回 `System.FormatException`。

```
DECLARE @g geometry = 'LINESTRING(1 1)';
```

### <a name="valid-instances"></a>有效的執行個體
 
  `LineString` 執行個體必須符合下列準則，才會是有效的。

1.  系統必須接受 `LineString` 執行個體。

2.  如果 `LineString` 執行個體不是空的，則它至少必須包含兩個相異點。

3.  
  `LineString` 執行個體本身不得在兩個或多個連續點的間隔上重疊。

 下面是有效的 `LineString` 執行個體。

```
DECLARE @g1 geometry= 'LINESTRING EMPTY';
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();

```

 下面是無效的 `LineString` 執行個體。

```
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';
SELECT @g1.STIsValid(), @g2.STIsValid();
```

> [!WARNING]
>  
  `LineString` 重疊的偵測是以浮點計算為基礎，但這些計算並不精確。

## <a name="examples"></a>範例
 下列範例示範如何建立具有三個點且 SRID 為 0 的 `geometry``LineString` 執行個體：

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);
```

 
  `LineString` 執行個體中的每個點都可包含 Z (高度) 和 M (測量) 值。 此範例會將 M 值加入到上述範例所建立的 `LineString` 執行個體。 M 和 Z 可以是 null 值。

```
DECLARE @g geometry;
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);
```

 下列範例會示範如何建立具有兩個相同點的 `geometry LineString` 執行個體。 
  `IsValid` 的呼叫表示 `LineString` 執行個體無效，而 `MakeValid` 的呼叫會將 `LineString` 執行個體轉換成 `Point`。

```sql
DECLARE @g geometry
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);
IF @g.STIsValid() = 1
  BEGIN
     SELECT @g.ToString() + ' is a valid LineString.';  
  END
ELSE
  BEGIN
     SELECT @g.ToString() + ' is not a valid LineString.';
     SET @g = @g.MakeValid();
     SELECT @g.ToString() + ' is a valid Point.';  
  END

```

 上述程式碼片段會傳回下列結果：

```
LINESTRING(1 3, 1 3) is not a valid LineString
POINT(1 3) is a valid Point.
```

## <a name="see-also"></a>另請參閱
 [STLength &#40;Geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type) [STStartPoint &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type) [STEndpoint &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type) [STPointN &#40;Geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type) [STNumPoints &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type) [STIsRing &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type) [STIsClosed &#40;geometry 資料類型](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)&#41;[STPointOnSurface &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type) [空間資料 &#40;SQL Server](../spatial/spatial-data-sql-server.md)&#41;


