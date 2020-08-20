---
description: EnvelopeAngle (geography 資料類型)
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c72459ec22208dfebbe234430ba49a4e94cb06a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479369"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回 `EnvelopeCenter()` 所傳回的點與 **geography** 執行個體中的點之間的最大角度 (以度為單位)。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
EnvelopeAngle( )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
 CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
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
  
  
