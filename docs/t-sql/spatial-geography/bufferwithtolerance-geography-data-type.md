---
description: BufferWithTolerance (geography 資料類型)
title: BufferWithTolerance (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 50c8e19dd3ed6782a7a8fe8532ab0edb61cceb34
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88360404"
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回 geometric 物件，此物件表示與 **geography** 執行個體之間的距離小於或等於指定值 (允許有指定的容錯) 之所有點值的聯集。  
  
這個 geography 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
_distance_  
這是指定與 **geography** 執行個體之間距離的 **float** 運算式，將會從此執行個體的周圍計算緩衝。  
  
緩衝區最大距離不能超過 0.999 \* _π_  * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周) 或完整地球。  
  
_tolerance_  
這是 **float** 運算式，用來指定緩衝距離的容錯。  
  
_tolerance_ 值是傳回之線性近似值的理想緩衝距離最大變異值。  
  
例如，點的理想緩衝距離是圓形，但此距離必須由多邊形來模擬。 當 tolerance 越小時，多邊形就會有越多的點。 這樣會增加結果的複雜度，但可減少錯誤。  
  
最小限制為 0.1% 的距離，而且小於該值的和任何容錯將會四捨五入至最小限制。  
  
_relative_  
這是 **bit**，用來指定 _tolerance_ 值是相對的還是絕對的。 如果值為 'TRUE' 或 1，則 tolerance 為相對值。 此值為 _tolerance_ 參數與角度範圍 \* 橢圓體赤道半徑的乘積。 如果值為 'FALSE' 或 0，則 tolerance 為絕對值。 此 _tolerance_ 值是傳回之線性近似值的理想緩衝距離絕對最大變異值。  
  
## <a name="return-types"></a>傳回型別  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
如果 _distance_ 不是數字 (NAN)，或如果 _distance_ 是正或負的無限值，則這個方法會擲回 **ArgumentException**。  如果 _tolerance_ 是零 (0) 而不是數字 (NaN) 或正的或負的無限值，則這個方法也會擲回 **ArgumentException**。  
  
在某些情況下，`STBuffer()` 會傳回 **FullGlobe** 執行個體，例如，當緩衝距離大於兩極至赤道距離時，`STBuffer()` 會在兩極傳回 **FullGlobe** 執行個體。  
  
針對緩衝區距離超過下列限制的位置，這個方法將擲回 **FullGlobe** 執行個體中的 **ArgumentException**：  
  
0.999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周)  
  
理論與計算所得之緩衝區間的誤差為 max(tolerance, extents \* 1.E-7)，其中 tolerance 是 _tolerance_ 參數的值。 如需有關範圍的詳細資訊，請參閱 [geography 資料類型方法參考](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
這個方法並不精確。  
  
## <a name="examples"></a>範例  
下列範例會建立 `Point` 執行個體，並使用 `BufferWithTolerance()` 來取得其周圍的約略緩衝。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
[STBuffer &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
[地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
