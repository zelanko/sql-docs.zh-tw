---
title: "Error 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Error Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords: Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e0d513dc324fe6f1efc857a03bf231d06481c10c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含有關錯誤的執行個體所傳回的資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
|特性|描述|  
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
|[資料格](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)，[資料列](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[描述](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md)， [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md)， [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md)，[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ErrorCode|需要**UnsignedInt**屬性 (只有當**訊息**是父項目。)包含錯誤的數值傳回碼。|  
|Severity|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的嚴重性。|  
|描述|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含錯誤的描述性文字。|  
|來源|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含產生錯誤之元件的名稱。|  
|HelpFile|選擇性**字串**屬性 (只有當**訊息**是父項目。)包含描述錯誤之說明檔或主題的路徑或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>請參閱  
 [Warning 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
