---
title: GeometryCollection | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a5c21c01ab776a17d3e160fee51167c426dfa0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133911"
---
# <a name="geometrycollection"></a>GeometryCollection
  A`GeometryCollection`是零或多個集合`geometry`或`geography`執行個體。 A`GeometryCollection`可以是空的。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 執行個體  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 若要接受 `GeometryCollection` 執行個體，該執行個體必須是空的 `GeometryCollection` 執行個體，或者組成 `GeometryCollection` 執行個體的所有執行個體都必須是已接受的執行個體。 下列範例會顯示可接受的執行個體。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 下列範例會擲回`System.FormatException`因為`LinesString`執行個體中`GeometryCollection`不接受的執行個體。  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 當組成 `GeometryCollection` 執行個體的所有執行個體都有效時，`GeometryCollection` 執行個體是有效的。 下列範例示範三個有效`GeometryCollection`執行個體和一個無效的執行個體。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 無效，因為 `Polygon` 執行個體中的 `GeometryCollection` 執行個體無效。  
  
 如需可接受和有效執行個體的詳細資訊，請參閱＜ [Point](point.md)＞、＜ [MultiPoint](multipoint.md)＞、＜ [LineString](linestring.md)＞、＜ [MultiLineString](multilinestring.md)＞、＜ [Polygon](polygon.md)＞和＜ [MultiPolygon](multipolygon.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例會具現化 `geometry``GeometryCollection` ，其中包含 SRID 1 中具有 `Point` 執行個體和 `Polygon` 執行個體的 Z 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  