---
title: Error 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f223bff2dced01c2b3f954ca14242b1a35c93813
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036646"
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含 Analysis services 執行個體所傳回之錯誤的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
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
|父元素|[Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|子元素|請參閱下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|無|  
|[儲存格](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)，[資料列](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[描述](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md)， [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md)， [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md)，[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ErrorCode|所需**UnsignedInt**屬性 (只有當**訊息**是父項目。)包含錯誤的數值傳回碼。|  
|Severity|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的嚴重性。|  
|描述|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的描述性文字。|  
|來源|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含產生錯誤之元件的名稱。|  
|HelpFile|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含描述錯誤之說明檔或主題的路徑或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱
 [Warning 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
