---
title: 訊息元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Messages Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Messages
- microsoft.xml.analysis.messages
- urn:schemas-microsoft-com:xml-analysis#Messages
helpviewer_keywords:
- Messages element
ms.assetid: 719d15ff-f18b-4c56-80ba-a9114c0b7d8a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4bb3d7e97332909864a7762291d39dbb4802b07e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103098"
---
# <a name="messages-element-xmla"></a>Messages 元素 (XMLA)
  包含的集合[訊息](message-element-xmla.md)執行個體中傳回的項目[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[探索](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[結果集](../xml-data-types/resultset-data-type-xmla.md)|  
|子元素|[Message](message-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 這個元素會用於 `Discover` 方法呼叫或 `Execute` 方法呼叫中的單一 XMLA 命令成功完成，但卻出現錯誤或警告的情況。 在此情況下，`Messages`項目加入至[根](root-element-xmla.md)之後其他所有元素，後者又包含一或多個項目`Message`項目。 每個`Message`項目代表單一所傳回的錯誤或警告的訊息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
