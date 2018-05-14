---
title: CubeID 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf4e9b2446689039e70e1b74fcf7e9462fae1670
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cubeid-element-xmla"></a>CubeID 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  識別父元素中包含物件參考的 Cube。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeID>...</CubeID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|請參閱下表。|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|1-1：只出現一次的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)、[ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)、[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)、[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
