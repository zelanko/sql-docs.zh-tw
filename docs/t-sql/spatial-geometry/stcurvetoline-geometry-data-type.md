---
title: "STCurveToLine (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8da8776b690752e17b1cc25bb428190f2252d01d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回的多邊形近似值**幾何**包含圓弧線段的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 會傳回空白**GeometryCollection**空的執行個體**幾何**執行個體變數，並傳回**NULL**針對未初始化**幾何**變數。  
  
 方法會傳回的多邊形近似值取決於**幾何**您用來呼叫方法的執行個體：  
  
-   傳回**LineString**例項而言**CircularString**或**CompoundCurve**執行個體。  
  
-   傳回**多邊形**例項而言**CurvePolygon**執行個體。  
  
-   傳回一份**幾何**執行個體，如果該執行個體不是**CircularString**， **CompoundCurve**，或**CurvePolygon**執行個體. 例如，`STCurveToLine`方法會傳回**點**例項而言**幾何**這個執行個體是**點**執行個體。  
  
 與 SQL/MM 規格不同`STCurveToLine`方法未使用 z 座標值來計算多邊形近似值。 這個方法會忽略任何呼叫中存在的 z 座標值**幾何**執行個體。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 使用未初始化的幾何變數和空白執行個體  
 在下列範例中，第一個**選取**陳述式使用未初始化**幾何**執行個體來呼叫`STCurveToLine`方法，而且第二個**選取**陳述式會使用空**幾何**執行個體。 因此，此方法會傳回**NULL**第一個陳述式和**GeometryCollection**第二個陳述式的集合。  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. 使用 LineString 執行個體  
 **選取**陳述式在下列範例會使用**LineString**呼叫 STCurveToLine 方法的執行個體。 因此，此方法會傳回**LineString**執行個體。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. 使用 CircularString 執行個體  
 第一個**選取**陳述式在下列範例會使用**CircularString**呼叫 STCurveToLine 方法的執行個體。 因此，此方法會傳回**LineString**執行個體。 這**選取**陳述式也會比較兩個執行個體，也就是大約相同的長度。  最後，第二個**選取**陳述式會傳回每個執行個體的點數目。  它會傳回 5 點只針對**CircularString**執行個體，但 65 點**LineString**執行個體。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. 使用 CurvePolygon 執行個體  
 **選取**陳述式在下列範例會使用**CurvePolygon**呼叫 STCurveToLine 方法的執行個體。 因此，此方法會傳回**多邊形**執行個體。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>請參閱＜  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

