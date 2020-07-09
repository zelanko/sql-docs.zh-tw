---
title: STCurveToLine (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1b0dff24ff83cd577bfdb572a16582bbdc6b6863
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748683"
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

傳回包含圓弧線段之 **geometry** 執行個體的多邊形近似值。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>備註  
 針對空的 **geometry** 執行個體變數，會傳回空的**GeometryCollection** 執行個體，而針對未初始化的 **geometry** 變數，則會傳回 **NULL**。  
  
 此方法所傳回的多邊形近似值取決於您用來呼叫方法的 **geometry** 執行個體：  
  
-   傳回 **CircularString** 或 **CompoundCurve** 執行個體的 **LineString** 執行個體。  
  
-   傳回 **CurvePolygon** 執行個體的 **Polygon** 執行個體。  
  
-   如果 **geometry** 執行個體不是 **CircularString**、**CompoundCurve**, 或 **CurvePolygon** 執行個體，便傳回其複本。 例如，`STCurveToLine` 方法會針對本身是 **Point** 執行個體的 **geometry** 執行個體，傳回 **Point** 執行個體。  
  
 與 SQL/MM 規格不同，`STCurveToLine` 方法並不使用 z 座標值來計算多邊形近似值。 此方法會忽略呼叫端 **geometry** 執行個體中已有的任何 z 座標值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 使用未初始化的幾何變數和空白執行個體  
 在下列範例中，第一個 **SELECT** 陳述式使用未初始化的 **geometry** 執行個體來呼叫 `STCurveToLine` 方法，第二個 **SELECT** 陳述式使用空的 **geometry** 執行個體。 因此，此方法會對第一個陳述式傳回 **NULL**，對第二個陳述式則傳回 **GeometryCollection** 集合。  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. 使用 LineString 執行個體  
 在下列範例中，**SELECT** 陳述式使用 **LineString** 執行個體來呼叫 STCurveToLine 方法。 因此，此方法會傳回 **LineString** 執行個體。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. 使用 CircularString 執行個體  
 在下列範例中，第一個 **SELECT** 陳述式使用 **CircularString** 執行個體來呼叫 STCurveToLine 方法。 因此，此方法會傳回 **LineString** 執行個體。 這個 **SELECT** 陳述式也會比較兩個執行個體的長度，它們的長度大致相同。  最後，第二個 **SELECT** 陳述式會傳回每個執行個體的點數。  針對 **CircularString** 執行個體，只會傳回 5 點，但針對 **LineString** 執行個體則會傳回 65 點。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. 使用 CurvePolygon 執行個體  
 在下列範例中，**SELECT** 陳述式使用 **CurvePolygon** 執行個體來呼叫 STCurveToLine 方法。 因此，此方法會傳回 **Polygon**執行個體。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

