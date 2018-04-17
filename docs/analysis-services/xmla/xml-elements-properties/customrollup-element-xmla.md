---
title: CustomRollup 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CustomRollup Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#CustomRollup
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollup
- microsoft.xml.analysis.customrollup
helpviewer_keywords:
- CustomRollup element
ms.assetid: b266ac8b-1ae7-461c-9127-3c5642f829f5
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 152ccc8fa7194676d65bdf03239969b7a8201c86
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="customrollup-element-xmla"></a>CustomRollup 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含父代所代表之屬性成員的自訂積存公式[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollup>...</CustomRollup>  
   ...  
</Attribute>  
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
|父元素|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **CustomRollup**元素包含定義父代所定義之屬性成員的彙總行為的多維度運算式 (MDX) 運算式**屬性**項目。  
  
 如需有關 MDX 運算式的詳細資訊，請參閱[運算式 &#40;MDX &#41;](../../../mdx/expressions-mdx.md).  
  
## <a name="see-also"></a>請參閱  
 [插入項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
