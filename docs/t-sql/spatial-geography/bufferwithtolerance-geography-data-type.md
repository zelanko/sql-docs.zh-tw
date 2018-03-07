---
title: "BufferWithTolerance (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb70f24c521fd5f0325ecbb718e7d76aa43f935d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回幾何物件，代表所有點的聯集的值從距離**geography**執行個體小於或等於指定值，允許指定的容錯。  
  
 這個 geography 資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 是**float**運算式指定從距離**geography**執行個體的周圍計算緩衝。  
  
 緩衝區的最大距離不能超過 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周) 或完整的地球。  
  
 *tolerance*  
 是**float**運算式，指定緩衝距離的容錯。  
  
 *容錯*值指的是傳回之線性近似值之理想緩衝距離的最大變異。  
  
 例如，點的理想緩衝距離是圓形，但是這必須由多邊形來模擬。 當容錯越小時，多邊形就會有越多的點，這樣會增加結果的複雜度，但是會減少錯誤。  
  
 最小限制為 0.1% 的距離，而且小於該值的和任何容錯將會四捨五入至最小限制。  
  
 *relative*  
 是**元**指定是否*容錯*值是相對或絕對。 如果 'TRUE' 或 1，容錯為相對值，而且會計算的產品為*容錯*參數與角度\*橢圓體半徑的橢圓體。 如果 'FALSE' 或 0，容錯為絕對值，*容錯*值是傳回之線性近似值之理想緩衝距離的最大絕對變異。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**ArgumentException**如果*距離*不是數字 (NAN)，或如果*距離*是正數或負的無限大。  這個方法也會擲回**ArgumentException**如果*容錯*零 (0)，而不是數字 (NaN)，負數或正數或負的無限大。  
  
 `STBuffer()`會傳回**FullGlobe**在某些情況下，執行個體，例如`STBuffer()`傳回**FullGlobe**當緩衝距離至赤道距離大於兩極上的執行個體兩極。  
  
 這個方法會擲回**ArgumentException**中**FullGlobe**緩衝距離超過下列限制：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周)  
  
 理論與計算的緩衝間的錯誤是最大值 (tolerance，範圍\*1.e-7) 容限是值的其中*容錯*參數。 如需有關範圍的詳細資訊，請參閱[geography 資料類型方法參考](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Point` 執行個體，並使用 `BufferWithTolerance()` 來取得其周圍的約略緩衝。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STBuffer &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
