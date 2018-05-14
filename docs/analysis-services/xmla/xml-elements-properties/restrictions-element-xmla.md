---
title: Restrictions 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78c69d2e3a53e2e0ad3561e09feffdf9dfabdcfb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="restrictions-element-xmla"></a>Restrictions 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  限制資料行和使用的資料包含[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Discover>  
...  
   <Restrictions>  
      <RestrictionList>...</RestrictionList>  
   </Restrictions>  
...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|子元素|[RestrictionList](../../../analysis-services/xmla/xml-elements-properties/restrictionlist-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **限制**元素代表限制資料行以及用來限制所擷取之資訊資料**探索**方法。  
  
## <a name="example"></a>範例  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_PROPERTIES</RequestType>  
   <Restrictions>  
      <RestrictionList xmlns="urn:schemas-microsoft-com:xml-analysis">  
         <PropertyName>Catalog</PropertyName>  
      </RestrictionList>  
   </Restrictions>  
   <Properties />  
</Discover>  
```  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
