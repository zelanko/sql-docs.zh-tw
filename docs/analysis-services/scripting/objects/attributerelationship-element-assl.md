---
title: AttributeRelationship 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AttributeRelationship Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MemberProperty
helpviewer_keywords:
- AttributeRelationship element
ms.assetid: 2e786109-b8bf-4295-b0fe-9c1997349993
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 24beade45688ceab3c291a1e4671dfe37501feac
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="attributerelationship-element-assl"></a>AttributeRelationship 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供兩個屬性之間的關聯性的詳細資料。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationships>  
      <AttributeRelationship>  
      <AttributeID>...</AttributeID>  
            <RelationshipType>...</RelationshipType>  
      <Cardinality>...</Cardinality>  
      <Optionality >...</Optionality>  
      <OverrideBehavior >...</OverrideBehavior>  
            <Annotations>...</Annotations>  
      <Name>...</Name>  
      <Visible>...</Visible>  
      <Translations>...</Translations>  
   </AttributeRelationship>  
</AttributeRelationships>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)，[基數](../../../analysis-services/scripting/properties/cardinality-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [Optionality](../../../analysis-services/scripting/properties/optionality-element-assl.md)， [OverrideBehavior](../../../analysis-services/scripting/properties/overridebehavior-element-assl.md)， [RelationshipType](../../../analysis-services/scripting/properties/relationshiptype-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[可見](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AttributeRelationship>。  
  
## <a name="see-also"></a>請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
