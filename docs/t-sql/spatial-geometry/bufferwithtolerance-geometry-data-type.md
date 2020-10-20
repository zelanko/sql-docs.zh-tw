---
description: BufferWithTolerance (geometry 資料類型)
title: BufferWithTolerance (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a039118dc0abe85b065d74b96f551c2991820333
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037061"
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回幾何物件，此物件代表與 **geometry** 執行個體相距的距離小於或等於指定值 (允許有指定的容錯) 之所有點值的聯集。
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *distance*  
 這是一個 **float** 運算式，用來指定與 **geometry** 執行個體相距的距離 (將會從此執行個體的周圍計算緩衝)。  
  
 *tolerance*  
 這是 **float** 運算式，用來指定緩衝距離的容錯。  
  
 「容錯」** 係指所傳回線性近似值之理想緩衝距離的最大變異。  
  
 例如，點的理想緩衝距離是圓形，但是這必須由多邊形來模擬。 當容錯越小時，多邊形就會有越多的點，這樣會增加結果的複雜度，但是會減少錯誤。  
  
 *relative*  
 這是 **bit**，用來指定 *tolerance* 值是相對的還是絕對的。 如果為 'TRUE' 或 1，tolerance 就是相對值，會計算為 *tolerance* 參數與執行個體週框方塊之直徑的乘積。 如果為 'FALSE' 或 0，tolerance 就是絕對值，而 *tolerance* 值會是所傳回線性近似值之理想緩衝距離的最大變異絕對值。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 *tolerance* 參數必須大於零。 如果 *tolerance* <= 0，則會擲回 `System.ArgumentOutOfRangeException`。  
  
> [!NOTE]  
>  由於 *tolerance* 是 **float** 類型，因此如果指定的容錯值非常小，就可能因為浮點類型的捨入問題而擲回 `System.Runtime.InteropServices.COMException`。  
  
## <a name="remarks"></a>備註  
 當 *distance* > 0 時，會傳回 **Polygon** 或 **MultiPolygon** 執行個體。  
  
> [!NOTE]  
>  由於 distance 是 **float**，因此極小的值在計算中可能會等於零。 發生這種情況時，會傳回呼叫端 **geometry** 執行個體的複本。 請參閱 [float 和 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)。  
  
 當 *distance* = 0 時，會傳回呼叫端 **geometry** 執行個體的複本。  
  
 當 *distance* < 0 時，則  
  
-   如果執行個體的維度是 0 或 1，就會傳回空的 **GeometryCollection** 執行個體。  
  
-   當執行個體的維度是 2 或以上，則傳回負數緩衝。  
  
    > [!NOTE]  
    >  負數緩衝也可能會建立空的 **GeometryCollection** 執行個體。  
  
 負數緩衝會移除 **geometry** 執行個體邊界之指定距離內的所有點。  
  
 理論與計算所得之緩衝區間的誤差為 max(tolerance, extents \* 1.E-7)，其中 tolerance 是 *tolerance* 參數的值。 如需有關範圍的詳細資訊，請參閱 [geometry 資料類型方法參考](./spatial-types-geometry-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Point` 執行個體，並使用 `BufferWithTolerance()` 來取得其周圍的約略緩衝。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STBuffer &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
