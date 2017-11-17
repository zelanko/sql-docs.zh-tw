---
title: "STGeometryType (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9ce316d900f057e8c1907b8e731f1080a84fb5dc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回所表示的開放式地理空間協會 (OGC) 類型名稱**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （4000)**  
  
 CLR 傳回類型： **SqlString**  
  
## <a name="remarks"></a>備註  
 可傳回的 OGC 類型名稱`STGeometryType()`是**點**， **LineString**， **CircularString**， **CompoundCurve**，**多邊形**， **CurvePolygon**， **GeometryCollection**， **MultiPoint**， **MultiLineString**，和**MultiPolygon**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Polygon` 執行個體，並使用 `STGeometryType()` 確認它是多邊形。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

