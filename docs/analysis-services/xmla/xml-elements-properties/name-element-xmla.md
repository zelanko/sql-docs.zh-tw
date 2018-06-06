---
title: Name 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c0686dfbb5949c9b2fe3a20e34824e731369b266
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575810"
---
# <a name="name-element-xmla"></a>Name 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父代之屬性成員名稱[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)或[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|請參閱下表。|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)，[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**屬性**項目，**名稱**元素包含要插入或更新期間，分別更新屬性成員的名稱**插入**或**更新**命令。  
  
 如**轉譯**項目，**名稱**項目包含標題中所指定的語言的屬性成員的**語言**之父代的項目**轉譯**物件。 如果**名稱**項目未指定，或包含空字串，值**名稱**元素**屬性**包含項目**轉譯**使用項目。  
  
## <a name="see-also"></a>另請參閱
 [插入項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [語言項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
