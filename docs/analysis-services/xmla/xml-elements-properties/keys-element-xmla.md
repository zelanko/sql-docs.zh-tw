---
title: 索引鍵元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8ad15ae719e3d0bd31dccda3271ffccdbeacbfd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050525"
---
# <a name="keys-element-xmla"></a>Keys 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含的集合[金鑰](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md)用來識別父元素所代表之屬性成員的成員索引鍵的項目[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute>  
   ...  
   <Keys>  
      <Key>...</Key>  
   </Keys>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|子元素|[索引鍵](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱
 [卸除項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
