---
title: STCentroid (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STCentroid_TSQL
- STCentroid (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STCentroid (geometry Data Type)
ms.assetid: 4dc5a004-7a53-4cce-81dd-9f5e1dd0db78
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 406645a7e923ef429ca4b340f2daad5adf0718cb
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36249870"
---
# <a name="stcentroid-geometry-data-type"></a>STCentroid (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回由一個或多個多邊形組成之 **geometry** 執行個體的幾何中心點。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCentroid ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 開放地理空間協會 (OGC) 類型：**Point**  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 執行個體不是 **Polygon, CurvePolygon** 或 **MultiPolygon** 型別，`STCentroid()` 會傳回 null。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-centroid-of-a-polygon-instance"></a>A. 計算 Polygon 執行個體的距心  
 下列範例使用 `STCentroid()` 來計算 `polygon``geometry` 執行個體的距心：  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STCentroid().ToString();  
```  
  
### <a name="b-computing-the-centroid-of-a-curvepolygon-instance"></a>B. 計算 CurvePolygon 執行個體的距心  
 下列範例會計算 `CurvePolygon` 執行個體的距心：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))';  
 SELECT @g.STCentroid().ToString() AS Centroid
 ```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

