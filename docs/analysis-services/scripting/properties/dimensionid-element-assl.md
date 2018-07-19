---
title: DimensionID 元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 340225d519cb119daaae4628033e67a9f007d830
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052706"
---
# <a name="dimensionid-element-assl"></a>DimensionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含維度的識別碼 (ID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension> <!-- or DimensionBinding, DimensionAttributeBinding -- >  
   ...  
   <DimensionID>...</DimensionID>  
      ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素**DimensionID**在 「 分析管理物件 (AMO) 物件模型會<xref:Microsoft.AnalysisServices.CubeDimension>和<xref:Microsoft.AnalysisServices.DimensionBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
