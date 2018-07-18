---
title: Member 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c962452675a0c1c91a3573546f0763060dfb44e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994640"
---
# <a name="member-element-xmla"></a>Member 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示父代中的單一成員[成員](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)或是[Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)項目。  
  
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
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[成員](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)， [Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
|子元素|[Caption](../../../analysis-services/xmla/xml-elements-properties/caption-element-xmla.md)， [DisplayInfo](../../../analysis-services/xmla/xml-elements-properties/displayinfo-element-xmla.md)， [LName](../../../analysis-services/xmla/xml-elements-properties/lname-element-xmla.md)， [LNum](../../../analysis-services/xmla/xml-elements-properties/lnum-element-xmla.md)， [UName](../../../analysis-services/xmla/xml-elements-properties/uname-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|階層|所需**字串**屬性 (父**Tuple**只有項目)。 代表由之成員的階層名稱**成員**所屬項目。|  
  
## <a name="remarks"></a>備註  
 **成員**項目包含找出並顯示指定的階層內的成員所需的資訊。 父**成員**項目，藉由已指定階層**階層**父項目的屬性。 父**Tuple**項目，使用指定的階層**階層**屬性**成員**項目。  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
