---
description: GeometryCollection
title: GeometryCollection | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c2c7be1815002208ffea6e08ea4b7200579a78e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455400"
---
# <a name="geometrycollection"></a>GeometryCollection
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  **GeometryCollection** 是零或多個 **geometry** 或 **geography** 執行個體的集合。 **GeometryCollection** 可以是空的。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 執行個體  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 若要接受 **GeometryCollection** 執行個體，該執行個體必須是空的 **GeometryCollection** 執行個體，或者組成 **GeometryCollection** 執行個體的所有執行個體都必須是已接受的執行個體。 下列範例會顯示可接受的執行個體。  
  
```sql  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 下列範例會擲回 `System.FormatException` ，因為不接受 **GeometryCollection** 執行個體中的 **LinesString** 執行個體。  
  
```sql  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有效的執行個體  
 當組成 **GeometryCollection** 執行個體的所有執行個體都有效時， **GeometryCollection** 執行個體是有效的。 下列範例示範三個有效的 **GeometryCollection** 執行個體和一個無效的執行個體。  
  
```sql  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 無效，因為 **GeometryCollection** 執行個體中的 **Polygon** 執行個體無效。  
  
 如需可接受和有效執行個體的詳細資訊，請參閱＜ [Point](../../relational-databases/spatial/point.md)＞、＜ [MultiPoint](../../relational-databases/spatial/multipoint.md)＞、＜ [LineString](../../relational-databases/spatial/linestring.md)＞、＜ [MultiLineString](../../relational-databases/spatial/multilinestring.md)＞、＜ [Polygon](../../relational-databases/spatial/polygon.md)＞和＜ [MultiPolygon](../../relational-databases/spatial/multipolygon.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例會具現化 `geometry``GeometryCollection` ，其中包含 SRID 1 中具有 `Point` 執行個體和 `Polygon` 執行個體的 Z 值。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
