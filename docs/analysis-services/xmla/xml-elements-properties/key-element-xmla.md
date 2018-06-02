---
title: 索引鍵元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bea00c5b5fdff010d667db19ef3af28284ce3ed9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575780"
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
  
|特性|描述|  
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
 [屬性項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [AttributeName 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Drop 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [更新項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [其中的項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
