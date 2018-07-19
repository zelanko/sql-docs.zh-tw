---
title: AttributeHierarchyVisible 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81762d27a57b4c4d2aa4c9bed829059cc3664c0c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032559"
---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定用戶端應用程式是否可看到屬性階層。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|**True**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **AttributeHierarchyVisible**元素會決定是否可看到用戶端應用程式與屬性相關聯屬性階層。 如果這個項目設定為**False**，屬性階層仍可用於建立使用者定義階層，而且可以由多維度運算式 (MDX) 陳述式中參考。  
  
 對應至父系的項目**AttributeHierarchyVisible**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CubeAttribute>， <xref:Microsoft.AnalysisServices.DimensionAttribute>，和<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [AttributeHierarchyEnabled 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
