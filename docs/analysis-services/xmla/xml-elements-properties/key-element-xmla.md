---
title: 索引鍵元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd43ad594acb118be0e7fb8d39cb34f2ae3e6ef6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="key-element-xmla"></a>Key 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含屬性成員的成員索引鍵值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[索引鍵](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素所使用的資料類型應該與指定屬性之適當索引鍵資料行的資料類型相符。 如果**金鑰**項目未指定父**屬性**項目， **AttributeName**和**名稱**中指定項目父**屬性**項目會用來識別要修改之屬性成員。  
  
## <a name="see-also"></a>另請參閱  
 [Attribute 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [AttributeName 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [卸除元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入項目 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Update 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [其中元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
