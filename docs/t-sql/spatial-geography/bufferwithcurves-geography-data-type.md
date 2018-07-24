---
title: BufferWithCurves (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 45510220511ae8d487c8f2f961ab47274bb4fd26
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049086"
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 **geography** 執行個體，表示與呼叫 **geography** 執行個體相距的距離小於或等於 *distance* 參數的所有點的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 這是 **float**，指出形成緩衝之點與 geography 執行個體相距的最大可能距離。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 下列準則會擲回 **ArgumentException**。  
  
-   沒有參數傳遞至此方法，例如 `@g.BufferWithCurves()`  
  
-   非數值參數傳遞至此方法，例如 `@g.BufferWithCurves('a')`  
  
-   將 **NULL** 傳遞至此方法，例如 `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Remarks  
 下表顯示針對不同距離值所傳回的結果。  
  
|distance 值|維度類型|傳回的空間類型|  
|--------------------|---------------------|---------------------------|  
|distance < 0|零或一維|空的 **GeometryCollection** 執行個體|  
|distance \< 0|二維或以上|具有負數緩衝的 **CurvePolygon** 或 **GeometryCollection** 執行個體。<br /><br /> 注意：負數緩衝可能會建立空白 **GeometryCollection**|
|distance = 0|所有維度|叫用 **geography** 執行個體的副本|  
|distance > 0|所有維度|**CurvePolygon** 或 **GeometryCollection** 執行個體|  
  
> [!NOTE]  
>  因為 *distance* 是 **float**，所以非常小的值在計算中可等同於零。  發生這種狀況時，會傳回呼叫 **geography** 執行個體的副本。  
  
 如果將 **string** 參數傳遞給此方法，它就會轉換成 **float** 或擲回 `ArgumentException`。  
  
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
 下列範例示範當 *distance* 參數等於 -2 時會發生何種狀況：  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 這個 **SELECT** 陳述式會傳回 `GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 以參數值 = 0 呼叫 BufferWithCurves()  
 下列範例會傳回呼叫 **geography** 執行個體的副本：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 以極小的非零參數值呼叫 BufferWithCurves()  
 下列範例也會傳回呼叫 **geography** 執行個體的副本：  

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
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
