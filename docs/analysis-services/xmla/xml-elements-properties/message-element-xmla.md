---
title: "訊息元素 (XMLA) |Microsoft 文件"
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
- Message Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords:
- Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 513b0b4be9666d667bd33221552fd792e92e3790
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="message-element-xmla"></a>Message 元素 (XMLA)
  包含的執行個體所傳回的訊息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Messages>  
   ...  
   <Message>  
      <Error>...</Error>  
      <!-- or -->  
      <Warning>...</Warning>  
   </Message>  
   ...  
</Messages>  
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
|父元素|[訊息](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|子元素|[錯誤](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)，[警告](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 這個元素會用於 **Discover** 方法呼叫或 **Execute** 方法呼叫中的單一 XMLA 命令成功完成，但卻出現錯誤或警告的情況。 在這種情況下，**訊息**元素會加入至根項目之後的所有其他項目，其中包含一或多個**訊息**項目。 每個**訊息**元素代表單一訊息、 錯誤或警告，而傳回[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

