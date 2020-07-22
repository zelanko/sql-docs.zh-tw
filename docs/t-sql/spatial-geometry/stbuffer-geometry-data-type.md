---
title: STBuffer (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b461b711ba7e91e4c29a362523b3ebb4a1228004
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552802"
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回幾何物件，此物件代表與 **geometry** 執行個體相距的距離小於或等於指定值之所有點的聯集。
  
## <a name="syntax"></a>語法  
  
```  
  
.STBuffer ( distance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *distance*  
 這是 **float** 類型 (.NET Framework 中的 **double**) 的值，用來指定與 geometry 執行個體相距的距離 (將會從此執行個體的周圍計算緩衝)。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>備註  
 `STBuffer()` 會指定 *tolerance* = distance \* .001 且 *relative* = **false** 來計算緩衝，此計算方式與 [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md) 類似。  
  
 當 *distance* > 0 時，會傳回 **Polygon** 或 **MultiPolygon** 執行個體。  
  
> [!NOTE]  
>  因為 distance 是 **float**，所以非常小的值在計算中可等同於零。  發生這種情況時，會傳回呼叫端 **geometry** 執行個體的複本。  請參閱 [float 和 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 當 *distance* = 0 時，會傳回呼叫端 **geometry** 執行個體的複本。  
  
 當 *distance* < 0 時，則  
  
-   如果執行個體的維度是 0 或 1，就會傳回空的 **GeometryCollection** 執行個體。  
  
-   當執行個體的維度是 2 或以上，則傳回負數緩衝。  
  
    > [!NOTE]  
    >  負數緩衝也可能會建立空的 **GeometryCollection** 執行個體。  
  
 負數緩衝會移除幾何界限之給定距離內的所有點。  
  
 理論與計算所得之緩衝區間的誤差為 max(tolerance, extents * 1.E-7)，其中 tolerance = distance \* .001。 如需有關範圍的詳細資訊，請參閱 [geometry 資料類型方法參考](https://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-stbuffer-with-parameter_value--0-on-one-dimensional-geometry-instance"></a>A. 在一維地理位置執行個體上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會傳回空白 `GeometryCollection` 執行個體：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parameter_value--0-on-a-polygon-instance"></a>B. 在 Polygon 執行個體上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會傳回具有負數緩衝的 `Polygon` 執行個體：  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parameter_value--0-on-a-curvepolygon-instance"></a>C. 在 CurvePolygon 執行個體上，以 parameter_value < 0 呼叫 STBuffer()  
 下列範例會從 `Polygon` 執行個體傳回具有負數緩衝的 `CurvePolygon` 執行個體：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  傳回 `Polygon` 執行個體，而不是 `CurvePolygon` 執行個體。  若要傳回 `CurvePolygon` 執行個體，請參閱 [BufferWithCurves &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. 以負數參數值呼叫 STBuffer()，傳回空白執行個體  
 下列範例示範當上一個範例的 *distance* 參數等於 -2 時會發生何種狀況。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 這個 **SELECT** 陳述式會傳回 `GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parameter_value--0"></a>E. 以 parameter_value = 0 呼叫 STBuffer()  
 下列範例會傳回呼叫 `geometry` 執行個體的副本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. 以極小的非零參數值呼叫 STBuffer()  
 下列範例也會傳回呼叫 `geometry` 執行個體的副本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parameter_value--0"></a>G. 以 parameter_value > 0 呼叫 STBuffer()  
 下列範例會傳回 `Polygon` 執行個體：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. 以字串參數值呼叫 STBuffer()  
 下列範例會傳回與上述範例相同的 `Polygon` 執行個體，但傳遞字串參數至方法：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 下列範例會擲回錯誤：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  上述兩個範例傳遞字串常值至 `STBuffer()`。  第一個範例可行，因為字串常值可轉換為數值。 但是，第二個範例會擲回 `ArgumentException`。  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. 在 MultiPoint 執行個體上呼叫 STBuffer()  
 下列範例會傳回兩個 `MultiPolygon` 執行個體和一個 `Polygon` 執行個體：  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 前兩個 **SELECT** 陳述式會傳回 `MultiPolygon` 執行個體，因為參數 *distance* 小於或等於 (1 1) 和 (1 4) 兩點之間距離的 1/2。 第三個 **SELECT** 陳述式會傳回 `Polygon` 執行個體，因為 (1 1) 和 (1 4) 兩點的緩衝執行個體重疊。  
  
## <a name="see-also"></a>另請參閱  
 [BufferWithTolerance &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

