---
title: Folders 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d225431c9426a9965014182bafa001f03df9dbc2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="folders-element-xmla"></a>Folders 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含在進行 [Restore](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) 或 [Synchronize](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 命令期間由 [Location](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 父元素所使用之 [Folder](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 元素的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location>  
   ...  
   <Folders>  
      <Folder>...</Folder>  
   </Folders>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|子元素|[資料夾](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Restore 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步處理項目 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
