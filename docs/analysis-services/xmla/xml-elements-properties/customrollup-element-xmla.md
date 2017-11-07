---
title: "CustomRollup 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8f9ddeaa48de1d3864239acd722a516cbd4dd69d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="customrollup-element-xmla"></a>CustomRollup 元素 (XMLA)
  包含父代所代表之屬性成員的自訂積存公式[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollup>...</CustomRollup>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
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
  
## <a name="see-also"></a>另請參閱  
 [插入項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

