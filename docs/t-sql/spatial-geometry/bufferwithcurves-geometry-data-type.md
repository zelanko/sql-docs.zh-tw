---
title: BufferWithCurves (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 45f265bee2ef910313bc8280cb753e1209a86a0a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38030427"
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  傳回 **geometry** 執行個體，此執行個體代表與呼叫端 **geometry** 執行個體相距的距離小於或等於 *distance* 參數之所有點的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 這是一個 **float**，指出形成緩衝的點與 **geometry** 執行個體相距的最大可能距離。  
  
## <a name="return-types"></a>傳回類型  
SQL Server 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 下列準則會擲回 **ArgumentException**。  
  
-   沒有參數傳遞至此方法，例如 `@g.BufferWithCurves()`  
  
-   非數值參數傳遞至此方法，例如 `@g.BufferWithCurves('a')`  
  
-   將 **NULL** 傳遞至此方法，例如 `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Remarks  
 下圖顯示由這個方法傳回的 geometry 執行個體範例。  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 下表顯示針對不同距離值所傳回的結果。  
  
|distance 值|維度類型|傳回的空間類型|  
|--------------------|---------------------|---------------------------|  
|distance < 0|零或一維|空的 **GeometryCollection** 執行個體|  
|distance < 0|二維或以上|具有負數緩衝的 **CurvePolygon** 或 **GeometryCollection** 執行個體。 **注意：** 負數緩衝可能會建立空的 **GeometryCollection**|  
|distance = 0|所有維度|叫用端 **geometry** 執行個體的複本|  
|distance > 0|所有維度|**CurvePolygon** 或 **GeometryCollection** 執行個體|  
  
> [!NOTE]  
>  因為 *distance* 是 **float**，所以非常小的值在計算中可等同於零。 發生這種情況時，會傳回呼叫端 **geometry** 執行個體的複本。 請參閱 [float 和 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)。  
  
 負數緩衝會移除幾何界限之給定距離內的所有點。 下圖中，負數緩衝顯示為圓形淺色陰影區域。 點線是原始多邊形的界限，實線是結果多邊形的界限。  
  
 如果將 **string** 參數傳遞給此方法，它就會轉換成 **float** 或擲回 `ArgumentException`。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. 在一維幾何例項上，以參數值 < 0 呼叫 BufferWithCurves()  
 下列範例會傳回空白 `GeometryCollection` 執行個體：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. 在二維幾何例項上，以參數值 < 0 呼叫 BufferWithCurves()  
 下列範例會傳回具有負數緩衝的 `CurvePolygon` 執行個體：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. 以參數值 < 0 呼叫 BufferWithCurves()，傳回空的 GeometryCollection  
 下列範例示範當 *distance* 參數等於 -2 時會發生何種狀況：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 這個 **SELECT** 陳述式會傳回 `GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 以參數值 = 0 呼叫 BufferWithCurves()  
 下列範例會傳回呼叫端 **geometry** 執行個體的複本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 以極小的非零參數值呼叫 BufferWithCurves()  
 下列範例也會傳回呼叫端 **geometry** 執行個體的複本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. 以參數值 > 0 呼叫 BufferWithCurves()  
 下列範例會傳回 `CurvePolygon` 執行個體：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. 傳遞有效的字串參數  
 下列範例會傳回與上述範例相同的 `CurvePolygon` 執行個體，但傳遞字串參數至方法：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 傳遞無效的字串參數  
 下列範例會擲回錯誤：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 請注意，上述兩個範例傳遞字串常值至 `BufferWithCurves()` 方法。 第一個範例可行，因為字串常值可轉換為數值。 但是，第二個範例會擲回 `ArgumentException`。  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. 在 MultiPoint 執行個體上呼叫 BufferWithCurves()  
 下列範例會傳回兩個 `GeometryCollection` 執行個體和一個 `CurvePolygon` 執行個體：  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 前兩個 **SELECT** 陳述式會傳回 `GeometryCollection` 執行個體，因為參數 *distance* 小於或等於 (1 1) 和 (1 4) 兩點之間距離的 1/2。 第三個 **SELECT** 陳述式會傳回 `CurvePolygon` 執行個體，因為 (1 1) 和 (1 4) 兩點的緩衝執行個體重疊。  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
