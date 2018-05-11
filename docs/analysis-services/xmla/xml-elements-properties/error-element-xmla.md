---
title: Error 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9903e86d5931d92222aec00f3896a2db78732f5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體所傳回之錯誤的相關資訊。  
  
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
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[訊息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|子元素|請參閱下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[訊息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|無|  
|[Cell](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)、 [row](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Description](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md)、 [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md)、 [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md)、 [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|說明|  
|---------------|-----------------|  
|ErrorCode|需要**UnsignedInt**屬性 (只有當**訊息**是父項目。)包含錯誤的數值傳回碼。|  
|Severity|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的嚴重性。|  
|Description|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的描述性文字。|  
|Source|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含產生錯誤之元件的名稱。|  
|HelpFile|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含描述錯誤之說明檔或主題的路徑或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Warning 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
