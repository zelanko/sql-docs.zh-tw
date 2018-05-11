---
title: BufferWithTolerance (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0aa4291944b92dd83f2ce1d5d39704c171d8c76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 geometric 物件，此物件表示與 **geography** 執行個體之間的距離小於或等於指定值 (允許有指定的容錯) 之所有點值的聯集。  
  
 這個 geography 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 這是指定與 **geography** 執行個體之間距離的 **float** 運算式，將會從此執行個體的周圍計算緩衝。  
  
 緩衝的最大距離不能超過 0.999 \* *π*  * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周) 或完整的地球。  
  
 *tolerance*  
 這是 **float** 運算式，用來指定緩衝距離的容錯。  
  
 *tolerance* 值指的是傳回之線性近似值之理想緩衝距離的最大變異。  
  
 例如，點的理想緩衝距離是圓形，但是這必須由多邊形來模擬。 當容錯越小時，多邊形就會有越多的點，這樣會增加結果的複雜度，但是會減少錯誤。  
  
 最小限制為 0.1% 的距離，而且小於該值的和任何容錯將會四捨五入至最小限制。  
  
 *relative*  
 這是 **bit**，用來指定 *tolerance* 值是相對的還是絕對的。 如果為 'TRUE' 或 1，則 tolerance 為相對值，而且會計算為 *tolerance* 參數與角度 \* 橢圓體半徑的乘積。 如果為 'FALSE' 或 0，tolerance 就是絕對值，而 *tolerance* 值會是所傳回線性近似值之理想緩衝距離的最大變異絕對值。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 如果 *distance* 不是數字 (NAN)，或如果 *distance* 是正的或負的無限值，這個方法將會擲回 **ArgumentException**。  如果 *tolerance* 是零 (0) 而不是數字 (NaN) 或正的或負的無限值，這個方法也將擲回 **ArgumentException**。  
  
 在某些情況下，`STBuffer()` 會傳回 **FullGlobe** 執行個體，例如，當緩衝距離大於兩極至赤道距離時，`STBuffer()` 會在兩極傳回 **FullGlobe** 執行個體。  
  
 針對緩衝區距離超過下列限制的位置，這個方法將擲回 **FullGlobe** 執行個體中的 **ArgumentException**：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周)  
  
 理論與計算所得之緩衝間的誤差為 max(tolerance, extents \* 1.E-7)，其中 tolerance 是 *tolerance* 參數的值。 如需有關範圍的詳細資訊，請參閱 [geography 資料類型方法參考](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
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
  
  
