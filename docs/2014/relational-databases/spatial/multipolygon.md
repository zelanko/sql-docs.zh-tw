---
title: MultiPolygon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f1d29c76541d87e950c973fd6dc7d57482c6d2b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023950"
---
# <a name="multipolygon"></a>MultiPolygon
  A`MultiPolygon`執行個體是零或多個集合`Polygon`執行個體。  
  
## <a name="polygon-instances"></a>多邊形執行個體  
 下圖顯示的範例`MultiPolygon`執行個體。  
  
 ![幾何 MultiPolygon 執行個體的範例](../../database-engine/media/multipolygon.gif "幾何 MultiPolygon 執行個體的範例")  
  
 如本圖所示：  
  
-   圖 1 是`MultiPolygon`具有兩個執行個體`Polygon`項目。 界限是由兩個外部環形和三個內部環形所定義。  
  
-   圖 2 是具有兩個 `MultiPolygon` 元素的 `Polygon` 執行個體。 界限是由兩個外部環形和三個內部環形所定義。 這兩個 `Polygon` 元素會在正切點相交。  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 A`MultiPolygon`還是可接受下列條件符合。  
  
-   它是空`MultiPolygon`執行個體。  
  
-   所有執行個體組成`MultiPolygon`執行個體所接受`Polygon`執行個體。 如需有關接受`Polygon`執行個體，請參閱[多邊形](../spatial/polygon.md)。  
  
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
  
 `@g2` 無效，因為這兩個`Polygon`執行個體只在正切點接觸。 `@g3` 不是有效因為兩個內部`Polygon`執行個體互相重疊。  
  
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
  
  
