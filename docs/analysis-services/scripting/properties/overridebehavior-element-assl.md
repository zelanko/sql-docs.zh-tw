---
title: "OverrideBehavior 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: OverrideBehavior Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b1562dc4f32b5cf744c36274a7ce1c7cc5743ac2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="overridebehavior-element-assl"></a>OverrideBehavior 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]表示所描述之關聯性的覆寫行為[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*強式*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **OverrideBehavior**元素會決定相關屬性上的定位如何影響屬性上的定位  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*強式*|指出 AttributeRelationship 元素所描述之關聯性的覆寫行為。 決定一個屬性的定位如何影響其他位置。|  
|*無*|沒有影響。|  
  
 列舉型別對應至允許的值**OverrideBehavior**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.OverrideBehavior>。  
  
## <a name="see-also"></a>請參閱  
 [屬性和屬性階層](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
