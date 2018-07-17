---
title: STGeometryType (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 29a6f63362f90102398cfaf1a3848fe2708181f7
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36258120"
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 **geography** 執行個體表示的開放地理空間協會 (Open Geospatial Consortium，OGC) 類型名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**nvarchar(4000)**  
  
 CLR 傳回類型：**SqlString**  
  
## <a name="remarks"></a>Remarks  
 `STGeometryType()` 可傳回的 OGC 類型名稱為 **Point**、**LineString**、**CircularString**、**CompoundCurve**、**Polygon**、**CurvePolygon**、**GeometryCollection**、**MultiPoint**、**MultiLineString** 和 **MultiPolygon**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Polygon` 執行個體，並使用 `STGeometryType()` 確認它是多邊形。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
