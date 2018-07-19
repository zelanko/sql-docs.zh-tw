---
title: DependsOnDimensionID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DependsOnDimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DependsOnDimensionID
helpviewer_keywords:
- DependsOnDimensionID element
ms.assetid: 66ec20dd-b475-4895-a92c-7ac0e7e1c675
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8bda178f067cb8bf1a3cfe4bf7341c6916659a65
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171399"
---
# <a name="dependsondimensionid-element-assl"></a>DependsOnDimensionID 元素 (ASSL)
  包含父維度所相依之另一個維度的識別碼 (ID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
      ...  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 相依的維度會使用 `DependsOnDimensionID` 元素來識別它所相依的維度。  
  
 對應至父系的元素`DependsOnDimensionID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
