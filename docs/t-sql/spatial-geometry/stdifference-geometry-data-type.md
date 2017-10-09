---
title: "STDifference (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geometry Data Type)
ms.assetid: 737f39bb-8750-4ffb-8594-23febc2f1075
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c6b79813c903e5c5541b2aab8d09ba1858f28f0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stdifference-geometry-data-type"></a>STDifference (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回物件，表示的點集合從一**幾何**不位於另一個的執行個體**幾何**執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.STDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**指出指向移除執行個體上的執行個體`STDifference()`叫用。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid)**幾何**例項不相符。   只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-difference-between-two-polygon-instances"></a>A. 計算兩個 Polygon 執行個體之間的差異  
 下列範例使用 `STDifference()` 來計算兩個多邊形之間的差異。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-invoking-stdifference-on-a-curvepolygon-instance"></a>B. 在 CurvePolygon 執行個體上叫用 STDifference()  
 下列範例會在 CurvePolygon 執行個體上使用 STDifference()。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 -- Note the different results returned by the two SELECT statements  
 SELECT @h.STDifference(@g).ToString(), @g.STDifference(@h).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


