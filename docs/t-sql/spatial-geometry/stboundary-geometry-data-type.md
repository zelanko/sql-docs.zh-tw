---
title: "STBoundary (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a582d1c730fa8e11b6ddd684494588b69a01bf64
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stboundary-geometry-data-type"></a>STBoundary (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的界限**幾何**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 `STBoundary()`會傳回空白**GeometryCollection**時的端點**LineString**， **CircularString**，或**CompoundCurve**執行個體都相同。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>A. 在具有不同端點的 LineString 執行個體上使用 STBoundary()  
 下列範例會建立`LineString``geometry`執行個體。 `STBoundary()`傳回的界限`LineString`。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>B. 在具有相同端點的 LineString 執行個體上使用 STBoundary()  
 下列範例會建立具有相同端點的有效 `LineString` 執行個體。 `STBoundary()` 會傳回空的 `GeometryCollection`。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>C. 在 CurvePolygon 執行個體上使用 STBoundary()  
 下列範例會在 `STBoundary()` 執行個體上使用 `CurvePolygon`。 `STBoundary()` 會傳回 `CircularString` 執行個體。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

