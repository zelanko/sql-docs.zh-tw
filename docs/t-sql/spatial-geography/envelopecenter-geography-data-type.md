---
title: "EnvelopeCenter (geography 資料類型) |Microsoft 文件"
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0638e8793c75ad78aafa12bec1d1f8a3061022c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回可用的週框圓形中心的點**geography**執行個體。  
  
 為了決定週框圓形，該執行個體中的每個點都會描述為從地球中心到地球表面點的向量。 週框圓形的中心點是由所有向量的平均值來計算。 封閉迴圈，有兩種**多邊形**執行個體或**linestring**執行個體，第一個和最後一個點只有使用一次。  
  
 這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 這個方法會傳回**點**。 當搭配`EnvelopeAngle()`，`EnvelopeCenter()`傳回的週框圓形**geography**執行個體。  
  
> [!NOTE]  
>  `EnvelopeCenter()`傳回的週框圓形**geography**執行個體，但結果不保證能夠產生最小週框圓形。 相反地，**幾何**資料類型方法`STEnvelope()`保證會傳回最小週框方塊，當套用至**幾何**執行個體。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本中，傳回表示這個執行個體之信封的圓形中心的**點**。 根據 `EnvelopeAngle()` = 180 所定義，對所有大型物件來說，`EnvelopeCenter()` 會傳回 (90,0)。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
