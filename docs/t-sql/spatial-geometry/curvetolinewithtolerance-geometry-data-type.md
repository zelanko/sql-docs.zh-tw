---
description: CurveToLineWithTolerance (geometry 資料類型)
title: CurveToLineWithTolerance (geometry 資料類型) | Microsoft Docs
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
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4a717b5b83be8d381a91ff1ab1055d24ae8c59ed
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96115969"
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

傳回包含圓弧線段之 **geometry** 執行個體的多邊形近似值。
  
## <a name="syntax"></a>語法  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *tolerance*  
 這是 **double** 運算式，用來定義原始圓弧線段與其線性近似值之間的最大誤差。  
  
 *relative*  
 這是一個 **bool** 運算式，用來指出是否要使用偏差的相對最大值。 如果 relative 設為 false (0)，則會設定線性近似值的偏差絕對最大值。 如果 relative 設為 true (1)，則會以容錯參數與空間物件週框方塊之直徑的乘積來計算容錯。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 如果容錯設為 <= 0，則會擲回 `ArgumentOutOfRange` 例外狀況。  
  
## <a name="remarks"></a>備註  
 此方法可以指定結果 **LineString** 的誤差容許範圍。  
  
 下表顯示 `CurveToLineWithTolerance()` 為各種不同類型所傳回的執行個體類型。  
  
|叫用執行個體類型|傳回的空間類型|  
|----------------------------|---------------------------|  
|空白 geometry 執行個體|空的 **GeometryCollection** 執行個體|  
|**Point** 和 **MultiPoint**|**Point** 執行個體|  
|**MultiPoint**|**Point** 或 **MultiPoint** 執行個體|  
|**CircularString****CompoundCurve** 或 **LineString**|**LineString** 執行個體|  
|**MultiLineString**|**LineString** 或 **MultiLineString** 執行個體|  
|**CurvePolygon** 和 **Polygon**|**Polygon** 執行個體|  
|**MultiPolygon**|**Polygon** 或 **MultiPolygon** 執行個體|  
|具有不含圓弧線段之單一執行個體的 **GeometryCollection**|**GeometryCollection** 中包含的執行個體會決定所傳回的執行個體類型。|  
|具有單一一維圓弧線段執行個體 (**CircularString**、**CompoundCurve**) 的 **GeometryCollection**|**LineString** 執行個體|  
|具有單一二維圓弧線段執行個體 (**CurvePolygon**) 的 **GeometryCollection**|**Polygon** 執行個體|  
|具有多個一維執行個體的 **GeometryCollection**|**MultiLineString** 執行個體|  
|具有多個二維執行個體的 **GeometryCollection**|**MultiPolygon** 執行個體|  
|具有多個不同維度之執行個體的 **GeometryCollection**|**GeometryCollection** 執行個體|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用不同的容錯值  
 下列範例示範設定容錯如何影響從 `CircularString` 執行個體傳回的 `LineString` 執行個體：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 在包含一個 LineString 的 MultiLineString 執行個體上使用此方法  
 下列範例示範從只包含一個 `MultiLineString` 執行個體的 `LineString` 執行個體傳回的資料：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 在包含多個 LineString 的 MultiLineString 執行個體上使用此方法  
 下列範例示範從包含多個 `MultiLineString` 執行個體的 `LineString` 執行個體傳回的資料：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 為叫用 CurvePolygon 執行個體，將 relative 設為 true  
 下列範例使用 `CurvePolygon` 執行個體，在 *relative* 設為 true 時呼叫 `CurveToLineWithTolerance()`：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. 在 GeometryCollection 執行個體上使用此方法  
 下列範例會在包含二維 `CurveToLineWithTolerance()` 執行個體和一維 `GeometryCollection` 執行個體的 `CurvePolygon` 上呼叫 `CircularString`。 `CurveToLineWithTolerance()` 會將這兩種圓弧線段類型轉換成線段類型，並以 `GeometryCollection` 類型傳回它們。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [CurveToLineWithTolerance &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

