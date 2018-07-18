---
title: Exception 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d3e542534b85d0f87b689b196001e9a00fe49b15
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036766"
---
# <a name="exception-element-xmla"></a>Exception 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示已從中傳回例外狀況[Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md)或是[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間** `http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|父元素|[根目錄](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果在執行期間發生錯誤**Discover**方法呼叫或單一 XMLA 命令中**Execute**方法呼叫，以防止方法或命令完成後，**根**該方法或命令的項目包含**例外狀況**項目並**訊息**項目。 **例外狀況**項目表示，就會發生錯誤，導致方法或命令無法順利執行，而**訊息**元素包含錯誤或警告訊息的清單與錯誤相關。  
  
## <a name="see-also"></a>另請參閱
 [訊息項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
