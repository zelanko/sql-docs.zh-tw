---
title: TableNotifications 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1125b70b4c6dcc2ff9c089f30722ebd8162a16f7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="tablenotifications-element-xmla"></a>TableNotifications 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含集合[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)元素所使用[NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<NotifyTableChange >  
   ...  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
   </TableNotifications>  
   ...  
</NotifyTableChange>  
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
|父元素|[NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|  
|子元素|[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
