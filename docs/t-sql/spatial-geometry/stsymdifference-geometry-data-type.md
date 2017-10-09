---
title: "STSymDifference (geometry 資料類型) |Microsoft 文件"
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
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b83e2ef917f76f615588327c8a3c2721f30e347a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回物件，表示所有點都會在某個**幾何**執行個體或另一個**幾何**執行個體，但不是在這兩個執行個體內的點。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**除了所在之執行個體的執行個體`STSymDistance()`叫用。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid)**幾何**例項不相符。 只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. 計算兩個 Polygon 執行個體的對稱差異  
 下列範例使用 `STSymDifference()` 來計算兩個 `Polygon` 執行個體之間的對稱差異。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. 計算 CurvePolygon 和 Polygon 執行個體之間的對稱差異  
 下列範例會傳回 `GeometryCollection`，代表 `CurvePolygon` 與 `Polygon` 之間的對稱差異。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. 在具有內切 Polygon 執行個體的 CurvePolygon 執行個體上使用 STSymDifference()  
 下列範例會傳回具有 `CurvePolygon` 內環的 `Polygon` 執行個體，代表兩個相比較執行個體之間的對稱差異。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

