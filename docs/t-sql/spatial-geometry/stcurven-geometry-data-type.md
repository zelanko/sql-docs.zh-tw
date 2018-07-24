---
title: STCurveN (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f3ed32f720bc565fd50e230b9e209006ccc449ee
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041796"
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

從 **geometry** 執行個體傳回指定的 **LineString**、**CircularString**、**CompoundCurve**, 或 **MultiLineString** 曲線。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>引數  
 *curve_index*  
 這是 1 與 **geometry** 執行個體中曲線數目之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 如果 *curve_index* < 1，就會擲回 `ArgumentOutOfRangeException`。  
  
## <a name="remarks"></a>Remarks  
 當發生下列任何狀況時，會傳回 **NULL**：  
  
-   已宣告 **geometry** 執行個體，但未具現化  
  
-   **geometry** 執行個體是空的  
  
-   *curve_index* 超出 **geometry** 執行個體中的曲線數目  
  
-   **geometry** 執行個體是 **Point**、**MultiPoint**、**Polygon**、**CurvePolygon** 或 **MultiPolygon**  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用 STCurveN()  
 下列範例會傳回 `CircularString` 執行個體中的第二個曲線：  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 這個主題稍早的範例會傳回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. 在具有一個 CircularString 執行個體的 CompoundCurve 執行個體上使用 STCurveN()  
 下列範例會傳回 `CompoundCurve` 執行個體中的第二個曲線：  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 這個主題稍早的範例會傳回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. 在具有三個 CircularString 執行個體的 CompoundCurve 執行個體上使用 STCurveN()  
 下列範例使用 `CompoundCurve` 執行個體，這個執行個體將三個不同的 `CircularString` 執行個體組合成與前一個範例相同的曲線順序：  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 這個主題稍早的範例會傳回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 請注意，前三個範例的結果都相同。 無論使用何種 WKT (Well-known Text) 格式來輸入相同的曲線順序，使用 `STCurveN()` 執行個體時，`CompoundCurve` 所傳回的結果都相同。  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. 呼叫 STCurveN() 之前，先驗證參數  
 下列範例示範如何在呼叫 `STCurveN()`方法之前先確認 `@n` 有效：  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>另請參閱  
 [STNumCurves &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

