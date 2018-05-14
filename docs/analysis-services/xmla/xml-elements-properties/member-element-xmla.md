---
title: Member 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ef62ab60f54f8bb9f4590ca6bbe2d1a7893399e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="member-element-xmla"></a>Member 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示父系中的單一成員[成員](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)或[Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[成員](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)， [Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
|子元素|[Caption](../../../analysis-services/xmla/xml-elements-properties/caption-element-xmla.md), [DisplayInfo](../../../analysis-services/xmla/xml-elements-properties/displayinfo-element-xmla.md), [LName](../../../analysis-services/xmla/xml-elements-properties/lname-element-xmla.md), [LNum](../../../analysis-services/xmla/xml-elements-properties/lnum-element-xmla.md), [UName](../../../analysis-services/xmla/xml-elements-properties/uname-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|階層|需要**字串**屬性 (父**Tuple**僅元素)。 代表由之成員的階層名稱**成員**所屬項目。|  
  
## <a name="remarks"></a>備註  
 **成員**元素包含找出並顯示指定的階層內的成員所需的資訊。 父**成員**項目，由已指定階層**階層**父項目的屬性。 父**Tuple**項目，使用指定的階層**階層**屬性**成員**項目。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
