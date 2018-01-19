---
title: "BufferWithCurves (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs: TSQL
helpviewer_keywords: BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 777f5d7a412cccc8b5757b2bf4f22404d12a9a77
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回**geography**表示集合的所有執行個體從呼叫點距離**geography**執行個體小於或等於*距離*參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 是**float**指出點形成緩衝區的最大距離可以與 geography 執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 下列準則會擲回**ArgumentException**。  
  
-   沒有參數傳遞至此方法，例如 `@g.BufferWithCurves()`  
  
-   非數值參數傳遞至此方法，例如 `@g.BufferWithCurves('a')`  
  
-   **NULL**傳遞至此方法，例如`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>備註  
 下表顯示針對不同距離值所傳回的結果。  
  
|distance 值|維度類型|傳回的空間類型|  
|--------------------|---------------------|---------------------------|  
|distance < 0|零或一維|空白**GeometryCollection**執行個體|  
|距離\<0|二維或以上|A **CurvePolygon**或**GeometryCollection**具有負數緩衝的執行個體。<br /><br /> 注意： 負數緩衝可能會建立空**GeometryCollection**|
|distance = 0|所有維度|叫用的複製**geography**執行個體|  
|distance > 0|所有維度|**CurvePolygon**或**GeometryCollection**執行個體|  
  
> [!NOTE]  
>  因為*距離*是**float**，非常小的值可等同於零的計算中。  當發生這種情況，然後呼叫副本**geography**會傳回執行個體。  
  
 如果**字串**參數傳遞至此方法，然後將轉換成**float**或將會擲回`ArgumentException`。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. 在一維地理位置執行個體上，以參數值 < 0 呼叫 BufferWithCurves()  
 下列範例會傳回空白 `GeometryCollection` 執行個體：  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. 在二維地理位置執行個體上，以參數值 < 0 呼叫 BufferWithCurves()  
 下列範例會傳回具有負數緩衝的 `CurvePolygon` 執行個體：  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. 以參數值 < 0 呼叫 BufferWithCurves()，傳回空的 GeometryCollection  
 下列範例會顯示發生什麼事時*距離*參數等於-2:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 這**選取**陳述式會傳回`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 以參數值 = 0 呼叫 BufferWithCurves()  
 下列範例會傳回一份呼叫**geography**執行個體：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 以極小的非零參數值呼叫 BufferWithCurves()  
 下列範例也會傳回一份呼叫**geography**執行個體：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. 以參數值 > 0 呼叫 BufferWithCurves()  
 下列範例會傳回 `CurvePolygon` 執行個體：  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. 傳遞有效的字串參數  
 下列範例會傳回與上述範例相同的 `CurvePolygon` 執行個體，但傳遞字串參數至方法：  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 傳遞無效的字串參數  
 下列範例會擲回錯誤：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 請注意，上述兩個範例傳遞字串常值至 `BufferWithCurves()` 方法。 第一個範例可行，因為字串常值可轉換為數值。 但是，第二個範例會擲回 `ArgumentException`。  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
