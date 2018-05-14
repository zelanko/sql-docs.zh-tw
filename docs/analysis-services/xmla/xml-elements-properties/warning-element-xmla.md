---
title: Warning 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ab17dd225e84061549eab6854d220782456f727f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="warning-element-xmla"></a>Warning 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|Description|選擇性 **String** 屬性。 包含警告的描述性文字。|  
|Source|選擇性 **String** 屬性。 包含產生警告之元件的名稱。|  
|HelpFile|選擇性 **String** 屬性。 包含描述警告之說明檔或主題的路徑或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Error 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
