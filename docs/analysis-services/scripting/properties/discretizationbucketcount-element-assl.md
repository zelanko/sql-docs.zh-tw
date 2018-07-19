---
title: DiscretizationBucketCount 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 389719df8815321ab5b2860425e4724b6b622770
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035869"
---
# <a name="discretizationbucketcount-element-assl"></a>DiscretizationBucketCount 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含要進行離散化的值區數目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**DiscretizationBucketCount**元素會決定多少群組或"buckets"時，會建立值**DimensionAttribute**或**ScalarMiningStructureColumn**是離散化或組織成特定群組集合。 如果未指定此元素，或指定項目的值為零[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]建立適當的群組，根據離散化方法數目。 如需有關離散化方法的詳細資訊，請參閱[離散化方法&#40;資料採礦&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 對應至父系的項目**DiscretizationBucketCount**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [DiscretizationMethod 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
