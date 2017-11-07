---
title: "Warning 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Warning Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords:
- Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5bd57e1ca9819f750f2538eba53b437aa8191a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="warning-element-xmla"></a>Warning 元素 (XMLA)
  包含的執行個體所傳回之警告的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
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
|子元素|無|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|說明|  
|---------------|-----------------|  
|ErrorCode|必要的 **UnsignedInt** 屬性。 包含警告的數值傳回碼。|  
|Severity|選擇性 **String** 屬性。 包含警告的嚴重性。|  
|說明|選擇性 **String** 屬性。 包含警告的描述性文字。|  
|Source|選擇性 **String** 屬性。 包含產生警告之元件的名稱。|  
|HelpFile|選擇性 **String** 屬性。 包含描述警告之說明檔或主題的路徑或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Error 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

