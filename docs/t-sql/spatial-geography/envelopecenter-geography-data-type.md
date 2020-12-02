---
description: EnvelopeCenter (geography 資料類型)
title: EnvelopeCenter (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c6e7173111dd48e54c85410b89d5a450adfe1169
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124376"
---
# <a name="envelopecenter-geography-data-type"></a>EnvelopeCenter (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回可作為 **geography** 執行個體週框圓形中心的點。  
  
該執行個體中的每個點都會描述為向量。 為了找出週框圓形，向量會從地球中心延伸到地球表面上的點。 週框圓形的中心點是由所有向量的平均值來計算。 如果是封閉式迴圈 (不論是 **Polygon** 執行個體還是 **LineString** 執行個體)，第一個和最後一個點都只會使用一次。  
  
這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
EnvelopeCenter( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
這個方法會傳回 **point**。 搭配 `EnvelopeAngle()` 使用時，`EnvelopeCenter()` 會傳回 **geography** 執行個體的週框圓形。  
  
> [!NOTE]  
>  `EnvelopeCenter()` 會傳回 **geography** 執行個體的週框圓形，但結果並不保證能夠產生最小週框圓形。 相反地，**geometry** 資料類型方法 `STEnvelope()` 套用到 **geometry** 執行個體時，則保證會傳回最小週框方塊。  
  
在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本中，會傳回使用 **point** 表示這個執行個體之信封的圓形中心。 根據 `EnvelopeAngle()` = 180 所定義，對所有大型物件來說，`EnvelopeCenter()` 會傳回 (90,0)。  
  
這個方法並不精確。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
[地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
[EnvelopeAngle &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
