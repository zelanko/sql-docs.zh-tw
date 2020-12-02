---
description: STIntersection (geography 資料類型)
title: STIntersection (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection method
ms.assetid: 7e09468f-499f-4a38-ba4b-bb30b8821e3b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 26df98e23bc24c0f1c112ffa2a07600cc753cb1d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467465"
---
# <a name="stintersection-geography-data-type"></a>STIntersection (geography 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  傳回物件，表示 **geography** 執行個體與另一個 **geography** 執行個體相交的點。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIntersection ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geography*  
 這是要與叫用 STIntersection() 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
 傳回兩個 geography 執行個體的交集。  
  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，STIntersection() 一律會傳回 Null。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援大於半球的空間執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在伺服器上傳回的可能結果集中，可能包含 **FullGlobe** 執行個體。  
  
 只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-intersection-of-a-polygon-and-a-linestring"></a>A. 計算 Polygon 和 LineString 的交集  
 下列範例使用 `STIntersection()` 來計算 `Polygon` 和 `LineString` 的交集。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-computing-the-intersection-of-a-polygon-and-a-curvepolygon"></a>B. 計算 Polygon 和 CurvePolygon 的交集  
 下列範例會傳回包含圓弧線段的執行個體。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="c-computing-the-symmetric-difference-with-fullglobe"></a>C. 計算與 FullGlobe 的對稱差異  
 下列範例會計算 `Polygon` 與 `FullGlobe` 之間的對稱差異。  
  
```  
DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
SELECT @g.STIntersection('FULLGLOBE').ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理位置例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
