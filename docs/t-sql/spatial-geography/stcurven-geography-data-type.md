---
description: STCurveN (geography 資料類型)
title: STCurveN (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 18d3a992b3f3d5eeecb09a16ce3fb6d582ee2fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479338"
---
# <a name="stcurven-geography-data-type"></a>STCurveN (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回從 **geography** 執行個體指定的曲線，可能是 **LineString**、**CircularString** 或 **CompoundCurve**。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveN( n )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *n*  
 這是介於 1 和 **geography** 執行個體中曲線數目之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 如果 n < 1，則會擲回 **ArgumentOutOfRangeException**。  
  
## <a name="remarks"></a>備註  
 當發生下列準則時，會傳回 **NULL**。  
  
-   **geography** 執行個體已宣告，但未具現化  
  
-   **geography** 執行個體為空白  
  
-   n 超過 **geography** 執行個體中的曲線數目 (請參閱 [STNumCurves &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   **geography** 執行個體的該維度不相等 (請參閱 [STDimension &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. 在 CircularString 上使用 STCurveN()  
 下列範例會傳回 **CircularString** 執行個體中的第二個曲線：  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. 在 CompoundCurve 上使用 STCurveN()  
 下列範例會傳回 **CompoundCurve** 執行個體中的第二個曲線：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. 在包含三個 CircularStrings 的 CompoundCurve 上使用 STCurveN()  
 下列範例使用 **CompoundCurve** 執行個體，這個執行個體將三個不同的 **CircularString** 執行個體組合成與前一個範例相同的曲線順序：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 範例會傳回。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 無論所使用的 Well-Known Text (WKT) 格式，`STCurveN()` 會傳回相同結果。  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. 在呼叫 STCurve() 之前測試有效性  
 下列範例示範如何在呼叫 STCurveN() 方法之前確認 *n* 有效：  
  
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
 [地理位置例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
