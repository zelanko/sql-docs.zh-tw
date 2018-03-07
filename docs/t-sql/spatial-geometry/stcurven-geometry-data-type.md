---
title: "STCurveN (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 496934186af543eb5a7263245c90ce7309112d10
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回從指定的曲線**幾何**這個執行個體是**LineString**， **CircularString**， **CompoundCurve**，或**MultiLineString**。
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>引數  
 *curve_index*  
 是**int**介於 1 到中的曲線數目之間的運算式**幾何**執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 如果*curve_index* < 1 則`ArgumentOutOfRangeException`就會擲回。  
  
## <a name="remarks"></a>備註  
 **NULL**時，會傳回下列任一項，就會發生：  
  
-   **幾何**執行個體已宣告，但未具現化  
  
-   **幾何**是空的執行個體  
  
-   *curve_index*超過中的曲線數目**幾何**執行個體  
  
-   **幾何**執行個體是**點**， **MultiPoint**，**多邊形**， **CurvePolygon**，或**MultiPolygon**  
  
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
 下列範例示範如何確定`@n`是否有效，才能呼叫`STCurveN()`方法：  
  
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
 [STNumCurves &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

