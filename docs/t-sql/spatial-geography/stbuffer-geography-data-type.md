---
title: STBuffer (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7a09c5653fe89528c49ade19e044066acfb34cd
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403703"
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 geography 物件，表示與 **geography** 執行個體之間的距離小於或等於指定值之所有點的聯集。  
  
 這個 geography 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 這是 **float** 類型 (.NET Framework 中的 **double**) 的值，可指定與 **geography** 執行個體之間的距離 (將會從此執行個體的周圍計算緩衝)。  
  
 緩衝的最大距離不能超過 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周) 或完整的地球。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 STBuffer() 會使用與 [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md) 相同的方式計算緩衝，指定 *tolerance* = abs(distance) \* .001 且 *relative* = **false**。  
  
 負數的緩衝會移除 **geography** 執行個體界限之給定距離內的所有點。  
  
 在某些情況下，`STBuffer()` 會傳回 **FullGlobe** 執行個體，例如，當緩衝距離大於兩極至赤道距離時，`STBuffer()` 會傳回 **FullGlobe** 執行個體。 緩衝不能超過完整地球。  
  
 針對緩衝區距離超過下列限制的位置，這個方法將擲回 **FullGlobe** 執行個體中的 **ArgumentException**：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 的地球圓周)  
  
 最大距離限制允許緩衝建構盡可能有彈性。  
  
 理論與計算所得之緩衝間的誤差為 max(tolerance, extents * 1.E-7)，其中 tolerance = distance \* .001。 如需有關範圍的詳細資訊，請參閱 [geography 資料類型方法參考](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString``geography` 執行個體。 然後它會使用 `STBuffer()`，傳回此例項之 1 公尺內的區域。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [BufferWithTolerance &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
