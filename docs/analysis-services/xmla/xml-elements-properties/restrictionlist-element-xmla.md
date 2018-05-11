---
title: RestrictionList 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71f6943f46178cab835bb6f43f976c460c9ce952
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 方法所使用之限制資料行和值的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[限制](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|子元素|限制資料行和值 (請參閱「備註」)。|  
  
## <a name="remarks"></a>備註  
 **RestrictionList** 元素包含可用來篩選 **Discover** 方法所傳回之資料的限制資料行集合。 **RestrictionList** 元素中的每個限制資料行都由不同的 XML 元素所定義。 限制資料行的值是 XML 元素所包含的資料，而限制資料行的名稱會對應至 XML 元素的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
