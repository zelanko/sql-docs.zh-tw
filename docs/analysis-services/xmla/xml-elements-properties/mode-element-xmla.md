---
title: "Mode 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57c3450e8928b24dc03e2d5915983f39330d0b0c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mode-element-xmla"></a>Mode 元素 (XMLA)
  識別要父系所使用的模式[鎖定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)項目指定的物件上建立鎖定時。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[鎖定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)，[解除鎖定](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 父代**鎖定**項目使用**模式**元素來決定要建立的物件上鎖定的類型。 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*CommitShared*|在指定的物件上建立共用鎖定。 您可以針對相同的物件建立其他共用鎖定。<br /><br /> 共用的鎖定會防止交易包含寫入作業，例如[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)執行方法呼叫[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令上指定的物件，從認可，直到移除共用的鎖定為止。 共用的鎖定無法防止交易包含讀取的作業，例如[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法呼叫或**Execute**執行方法呼叫[陳述式](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令，從正在認可。|  
|*執行 CommitExclusive*|在指定的物件上建立獨佔鎖定。 您無法針對相同的物件建立其他共用或獨佔鎖定。<br /><br /> 獨佔鎖定會防止認可在指定的物件上包含讀取或寫入作業的交易，直到移除獨佔鎖定為止。|  
  
## <a name="see-also"></a>另請參閱  
 [ID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Object 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

