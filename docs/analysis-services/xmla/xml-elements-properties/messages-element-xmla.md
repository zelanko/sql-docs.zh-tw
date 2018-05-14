---
title: 訊息元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90579f9204a263b4b2366e4b1eeab714676a4be7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="messages-element-xmla"></a>Messages 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含集合[訊息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)項目執行個體傳回的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
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
|父元素|[結果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|子元素|[訊息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 這個元素會用於 **Discover** 方法呼叫或 **Execute** 方法呼叫中的單一 XMLA 命令成功完成，但卻出現錯誤或警告的情況。 在這種情況下，**訊息**項目加入至[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)所有其他元素之後，該元素會包含一或多個項目**訊息**項目。 每個**訊息**元素代表單一訊息、 錯誤或警告，而傳回[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
