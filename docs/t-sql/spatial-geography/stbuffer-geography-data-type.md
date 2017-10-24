---
title: "STBuffer (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fa06f270ad653e9c8e43a5ec5456257e785670e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stbuffer-geography-data-type"></a>STBuffer (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 geography 物件，表示聯集之所有點的距離**geography**執行個體小於或等於指定的值。  
  
 這個 geography 資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *距離*  
 類型的值**float** (**double** .NET Framework 中) 指定的距離**geography**執行個體的周圍計算緩衝。  
  
 緩衝區的最大距離不能超過 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周) 或完整的地球。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 Stbuffer （） 以相同方式計算緩衝[BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)，並指定*容錯*= abs （distance） \* .001 和*相對* = **false**。  
  
 負數緩衝會移除界限之給定距離內的所有點**geography**執行個體。  
  
 `STBuffer()`會傳回**FullGlobe**在某些情況下，執行個體，例如`STBuffer()`傳回**FullGlobe**當緩衝距離大於兩極至赤道距離時，執行個體。 緩衝不能超過完整地球。  
  
 這個方法會擲回**ArgumentException**中**FullGlobe**緩衝距離超過下列限制：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周)  
  
 最大距離限制允許緩衝建構盡可能有彈性。  
  
 理論與計算的緩衝間的錯誤是最大值 (容錯，extents * 1.e-7) 其中容錯 = distance \* .001。 如需有關範圍的詳細資訊，請參閱[geography 資料類型方法參考](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
## <a name="examples"></a>範例  
 下列範例會建立`LineString``geography`執行個體。 然後它會使用 `STBuffer()`，傳回此例項之 1 公尺內的區域。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [BufferWithTolerance &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

