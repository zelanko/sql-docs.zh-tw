---
title: "STCurveN (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d33b8e6752ac8aca3bc6846a4558af4830373081
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geography-data-type"></a>STCurveN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回從指定的曲線**geography**這個執行個體是**LineString**， **CircularString**，或**CompoundCurve**。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 是**int**介於 1 到中的曲線數目之間的運算式**geography**執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 如果 < n 1 則**ArgumentOutOfRangeException**就會擲回。  
  
## <a name="remarks"></a>備註  
 **NULL**時，會傳回下列準則，就會發生。  
  
-   **Geography**執行個體已宣告，但未具現化  
  
-   **Geography**是空的執行個體  
  
-   n 超過中的曲線數目**geography**執行個體 (請參閱[STNumCurves &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   維度**geography**執行個體不等於 (請參閱[STDimension &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. 在 CircularString 上使用 STCurveN()  
 下列範例會傳回中的第二個曲線**CircularString**執行個體：  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. 在 CompoundCurve 上使用 STCurveN()  
 下列範例會傳回中的第二個曲線**CompoundCurve**執行個體：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. 在包含三個 CircularStrings 的 CompoundCurve 上使用 STCurveN()  
 下列範例會使用**CompoundCurve**結合三個不同的執行個體**CircularString**放在同一個執行個體的曲線順序，與前一個範例：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 無論所使用的 Well-Known Text (WKT) 格式，`STCurveN()` 會傳回相同結果。  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. 在呼叫 STCurve() 之前測試有效性  
 下列範例示範如何確定 *n* 是否有效，才能呼叫 stcurven （） 方法：  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
