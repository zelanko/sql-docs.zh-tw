---
title: EnvelopeAngle (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4a66a7995d4ad6a97ca7d90798038dc2fe372150
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836718"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 `EnvelopeCenter()` 所傳回的點與 **geography** 執行個體中的點之間的最大角度 (以度為單位)。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
 CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 這個方法會傳回 **geography** 執行個體中的點 (以度為單位)。 搭配 EnvelopeCenter() 使用時，`EnvelopeAngle()` 會傳回 **geography** 執行個體的週框圓形。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，這個方法已擴充到 **FullGlobe** 執行個體。  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中套用至 `EnvelopeAngle()` 的半球限制已遭到移除。 不過，對於角度大於 90 度的執行個體，則會傳回 180 度。 對於跨越超過一個半球的 **geography** 執行個體，`EnvelopeAngle()` 並不精確。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;geography 資料類型 &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
