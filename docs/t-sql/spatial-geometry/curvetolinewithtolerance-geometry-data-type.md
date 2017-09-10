---
title: "CurveToLineWithTolerance (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5120f9c27e6157fd2f19c598ad984e1a3543db94
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回的多邊形近似值**幾何**包含圓弧線段的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>引數  
 *容錯*  
 是**double**運算式，定義介於原始圓弧線段及其線性近似值之間的最大錯誤。  
  
 *相對*  
 是**bool**運算式，指出是否要使用偏差的相對最大。 如果 relative 設為 false (0)，則會設定線性近似值的偏差絕對最大值。 如果 relative 設為 true (1)，則會以容錯參數與空間物件週框方塊之直徑的乘積來計算容錯。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 如果容錯設為 <= 0，則會擲回 `ArgumentOutOfRange` 例外狀況。  
  
## <a name="remarks"></a>備註  
 這個方法可以指定容錯量結果**LineString**。  
  
 下表顯示 `CurveToLineWithTolerance()` 為各種不同類型所傳回的執行個體類型。  
  
|叫用執行個體類型|傳回的空間類型|  
|----------------------------|---------------------------|  
|空白 geometry 執行個體|空白**GeometryCollection**執行個體|  
|**點**和**MultiPoint**|**點**執行個體|  
|**MultiPoint**|**點**或**MultiPoint**執行個體|  
|**CircularString**， **CompoundCurve**，或**LineString**|**LineString**執行個體|  
|**MultiLineString**|**LineString**或**MultiLineString**執行個體|  
|**CurvePolygon**和**多邊形**|**多邊形**執行個體|  
|**MultiPolygon**|**多邊形**或**MultiPolygon**執行個體|  
|**GeometryCollection**未包含圓弧線段是單一執行個體|執行個體中包含**GeometryCollection**判斷傳回的執行個體的類型。|  
|**GeometryCollection**具有一維圓弧線段執行個體 (**CircularString**， **CompoundCurve**)|**LineString**執行個體|  
|**GeometryCollection**具有一個二維圓弧線段執行個體 (**CurvePolygon**)|**多邊形**執行個體|  
|**GeometryCollection**多個一維執行個體|**MultiLineString**執行個體|  
|**GeometryCollection**具有多個二維執行個體|**MultiPolygon**執行個體|  
|**GeometryCollection**不同維度的多重執行個體|**GeometryCollection**執行個體|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用不同的容錯值  
 下列範例示範如何設定容錯影響`LineString`從傳回的執行個體`CircularString`執行個體：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();`  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 在包含一個 LineString 的 MultiLineString 執行個體上使用此方法  
 下列範例示範從只包含一個 `MultiLineString` 執行個體的 `LineString` 執行個體傳回的資料：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();`  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 在包含多個 LineString 的 MultiLineString 執行個體上使用此方法  
 下列範例示範從包含多個 `MultiLineString` 執行個體的 `LineString` 執行個體傳回的資料：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();`  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 為叫用 CurvePolygon 執行個體，將 relative 設為 true  
 下列範例會使用`CurvePolygon`執行個體來呼叫`CurveToLineWithTolerance()`與*相對*設為 true:  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))';`  
  
 `SELECT @g.CurveToLineWithTolerance(.5,1).ToString();`  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. 在 GeometryCollection 執行個體上使用此方法  
 下列範例會在包含二維 `CurveToLineWithTolerance()` 執行個體和一維 `GeometryCollection` 執行個體的 `CurvePolygon` 上呼叫 `CircularString`。 `CurveToLineWithTolerance()` 會將這兩種圓弧線段類型轉換成線段類型，並以 `GeometryCollection` 類型傳回它們。  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();`  
  
## <a name="see-also"></a>另請參閱  
 [CurveToLineWithTolerance &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  


