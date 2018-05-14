---
title: ReportParameter 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f69cea98c9a6e0147dc1659f8397116d4e4ca14a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="reportparameter-element---assl"></a>ReportParameter 元素-ASSL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含名稱和值的參數，傳遞至[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表在執行階段。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReportParameters>  
      <ReportParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportParameter>  
</ReportParameters>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|  
|子元素|[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **值**元素必須包含多維度運算式 (MDX) 運算式。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ReportParameter>。  
  
## <a name="see-also"></a>另請參閱  
 [ReportAction 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Action 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
