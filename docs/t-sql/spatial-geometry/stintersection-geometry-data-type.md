---
title: STIntersection (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f556697457ba8baa649458f7a7c46b02e4682d4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759666"
---
# <a name="stintersection-geometry-data-type"></a>STIntersection (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回物件，表示 **geometry** 執行個體與另一個 **geometry** 執行個體相交的點。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與 `STIntersection()` 叫用所在之執行個體相比較的另一個 **geometry** 執行個體，以判斷兩者相交的地方。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 執行個體的空間參考識別碼 (SRID) 不相符，`STIntersection()` 一定會傳回 Null。 只有當輸入執行個體包含圓弧線段，結果才能包含圓弧線段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>A. 在 Polygon 執行個體上使用 STIntersection()  
 下列範例使用 `STIntersection()` 來計算兩個多邊形的交集。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. 在 CurvePolygon 執行個體上使用 STIntersection()  
 下列範例會傳回包含圓弧線段的執行個體。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STIntersection(@g).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

