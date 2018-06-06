---
title: return 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e8746fb9f8b397ef50b1a5c66a2132e5f0cf5c87
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576190"
---
# <a name="return-element-xmla"></a>return 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所傳回的資訊[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)元素為了回應[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法呼叫或[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)元素為了回應[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)， [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|子元素|請參閱下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)或[結果](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **傳回**元素包含所傳回的資料**探索**和**Execute**方法。 一般而言，**傳回**元素包含單一**根**包含成功所傳回的資料元素**探索**或**Execute**方法呼叫或 XML for Analysis (XMLA) 方法呼叫不成功所傳回的例外狀況。 如果**Execute**方法包含**批次**執行多項作業的命令**傳回**元素包含**結果**元素，其亦包含一個**根**每個命令執行成功或失敗的項目**批次**命令。  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
