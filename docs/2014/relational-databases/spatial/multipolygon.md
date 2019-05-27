---
title: MultiPolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ccb2689b24914a0a953c1b9f7325cd5aa9c75d0d
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014115"
---
# <a name="multipolygon"></a>MultiPolygon
  `MultiPolygon` 執行個體是零或多個 `Polygon` 執行個體的集合。  
  
## <a name="polygon-instances"></a>多邊形執行個體  
 下圖顯示 `MultiPolygon` 執行個體的範例。  
  
 ![幾何 MultiPolygon 執行個體的範例](../../database-engine/media/multipolygon.gif "幾何 MultiPolygon 執行個體的範例")  
  
 如本圖所示：  
  
-   圖 1 是具有兩個 `Polygon` 元素的 `MultiPolygon` 執行個體。 界限是由兩個外部環形和三個內部環形所定義。  
  
-   圖 2 是具有兩個 `MultiPolygon` 元素的 `Polygon` 執行個體。 界限是由兩個外部環形和三個內部環形所定義。 這兩個 `Polygon` 元素會在正切點相交。  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 如果下列其中一個條件成立，則接受 `MultiPolygon` 執行個體。  
  
-   它是空的 `MultiPolygon` 執行個體。  
  
-   組成 `MultiPolygon` 執行個體的所有執行個體都是可接受的 `Polygon` 執行個體。 如需有關已接受`Polygon`執行個體，請參閱[多邊形](../spatial/polygon.md)。  
  
 下列範例會顯示可接受的 `MultiPolygon` 執行個體。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 下列範例示範會擲出 `System.FormatException`的 MultiPolygon 執行個體。  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 MultiPolygon 中的第二個執行個體是 LineString 執行個體，不是可接受的 Polygon 執行個體。  
  
### <a name="valid-instances"></a>有效的執行個體  
 如果 `MultiPolygon` 執行個體是空的 `MultiPolygon` 執行個體或符合下列準則，則為有效的執行個體。  
  
1.  組成 `MultiPolygon` 執行個體的所有執行個體都是有效的 `Polygon` 執行個體。 有效`Polygon`執行個體，請參閱[多邊形](../spatial/polygon.md)。  
  
2.  組成 `Polygon` 執行個體的所有 `MultiPolygon` 執行個體彼此不會重疊。  
  
 下列範例示範兩個有效的 `MultiPolygon` 執行個體和一個無效的 `MultiPolygon` 執行個體。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` 有效，因為這兩個 `Polygon` 執行個體只在一個相切點接觸。 `@g3` 無效，因為這兩個 `Polygon` 執行個體的內部互相重疊。  
  
## <a name="examples"></a>範例  
 下列範例示範 `geometry``MultiPolygon` 執行個體的建立作業，並傳回第二個元件的 Well-Known Text (WKT)。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 此範例會具現化空的 `MultiPolygon` 執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>另請參閱  
 [Polygon](../spatial/polygon.md)   
 [STArea &#40;geometry Data Type&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STCentroid &#40;geometry Data Type&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;geometry Data Type&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [空間資料 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
