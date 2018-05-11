---
title: CancelAssociated 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 97d8d3fbc5980d9e6ffab788af5c9a3cf61fcc15
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cancelassociated-element-xmla"></a>CancelAssociated 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指出 [Cancel](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) 父元素是否應該取消所有相關聯的命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[[取消]](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果您指定了這個元素並將它設定為 **True**，系統就會取消 **Cancel** 父命令中識別的每個對應連接、工作階段和命令。  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionID 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [SPID 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
