---
title: "STBuffer (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 87ad6ea01e471cf1ec407f0b8372300d07f0118f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回幾何物件，此物件表示聯集的所有點的距離**幾何**執行個體小於或等於指定的值。
  
## <a name="syntax"></a>語法  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *距離*  
 類型的值**float** (**double** .NET Framework 中) 指定從 geometry 執行個體的周圍計算緩衝的距離。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 `STBuffer()`計算緩衝，像是[BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)，並指定*容錯*= distance \* .001 和*相對* =  **false**。  
  
 當*距離*> 0，則**多邊形**或**MultiPolygon**會傳回執行個體。  
  
> [!NOTE]  
>  因為 distance 是**float**，非常小的值可等同於零的計算中。  當發生這種情況，一份呼叫**幾何**會傳回執行個體。  請參閱[float 和 real &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 當*距離*= 0，則呼叫副本**幾何**會傳回執行個體。  
  
 當*距離*< 0，則  
  
-   空白**GeometryCollection**當執行個體的維度是 0 或 1，則會傳回執行個體。  
  
-   當執行個體的維度是 2 或以上，則傳回負數緩衝。  
  
    > [!NOTE]  
    >  負數緩衝也可能會建立空**GeometryCollection**執行個體。  
  
 負數緩衝會移除幾何界限之給定距離內的所有點。  
  
 理論與計算的緩衝間的錯誤是最大值 (容錯，extents * 1.e-7) 其中容錯 = distance \* .001。 如需有關範圍的詳細資訊，請參閱[geometry 資料類型方法參考](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. 在一維幾何例項上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會傳回空白 `GeometryCollection` 執行個體：  
  
 `DECLARE @g geometry= 'LINESTRING(3 4, 8 11)';`  
  
 `SELECT @g.STBuffer(-1).ToString();`  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. 在 Polygon 執行個體上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會傳回具有負數緩衝的 `Polygon` 執行個體：  
  
 `DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))';`  
  
 `SELECT @g.STBuffer(-1).ToString();`  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. 在 CurvePolygon 執行個體上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會從 `Polygon` 執行個體傳回具有負數緩衝的 `CurvePolygon` 執行個體：  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))';`  
  
 `SELECT @g.STBuffer(-1).ToString();`  
  
> [!NOTE]  
>  傳回 `Polygon` 執行個體，而不是 `CurvePolygon` 執行個體。  要傳回`CurvePolygon`執行個體，請參閱[BufferWithCurves &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. 以負數參數值呼叫 STBuffer()，傳回空白執行個體  
 下列範例會顯示發生什麼事時*距離*參數等於-2 前, 一個範例。  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))';`  
  
 `SELECT @g.STBuffer(-2).ToString();`  
  
 這**選取**陳述式會傳回`GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. 以 parameter_value = 0 呼叫 STBuffer()  
 下列範例會傳回呼叫 `geometry` 執行個體的副本：  
  
 `DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';`  
  
 `SELECT @g.STBuffer(0).ToString();`  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. 以極小的非零參數值呼叫 STBuffer()  
 下列範例也會傳回呼叫 `geometry` 執行個體的副本：  
  
 `DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';`  
  
 `DECLARE @distance float = 1e-20;`  
  
 `SELECT @g.STBuffer(@distance).ToString();`  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. 以 parameter_value > 0 呼叫 STBuffer()  
 下列範例會傳回 `Polygon` 執行個體：  
  
 `DECLARE @g geometry= 'LINESTRING(3 4, 8 11)';`  
  
 `SELECT @g.STBuffer(2).ToString();`  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. 以字串參數值呼叫 STBuffer()  
 下列範例會傳回與上述範例相同的 `Polygon` 執行個體，但傳遞字串參數至方法：  
  
 `DECLARE @g geometry= 'LINESTRING(3 4, 8 11)';`  
  
 `SELECT @g.STBuffer('2').ToString();`  
  
 下列範例會擲回錯誤：  
  
 `DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';`  
  
 `SELECT @g.STBuffer('a').ToString();`  
  
> [!NOTE]  
>  上述兩個範例傳遞字串常值至 `STBuffer()`。  第一個範例可行，因為字串常值可轉換為數值。 但是，第二個範例會擲回 `ArgumentException`。  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. 在 MultiPoint 執行個體上呼叫 STBuffer()  
 下列範例會傳回兩個 `MultiPolygon` 執行個體和一個 `Polygon` 執行個體：  
  
 `DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))';`  
  
 `SELECT @g.STBuffer(1).ToString();`  
  
 `SELECT @g.STBuffer(1.5).ToString();`  
  
 `SELECT @g.STBuffer(1.6).ToString();`  
  
 前兩個**選取**陳述式會傳回`MultiPolygon`執行個體，因為參數*距離*小於或等於 1/2 的距離兩個點 (1 1) 和 (1 4)。 第三個**選取**陳述式會傳回`Polygon`執行個體，因為緩衝的執行個體的兩個點 (1 1) 和 (1 4) 重疊。  
  
## <a name="see-also"></a>另請參閱  
 [BufferWithTolerance &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


