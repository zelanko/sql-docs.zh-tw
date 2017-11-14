---
title: "其中元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Where Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords:
- Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b559e82af0840067e9448e83056a3f1e96937b39
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="where-element-xmla"></a>Where 元素 (XMLA)
  定義 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 或 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) 父命令所使用的篩選條件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|子元素|[屬性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 若為 **Drop** 命令，與 **DeleteWithDescendants** 元素結合的 [Where](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) 元素會識別要卸除之屬性成員的範圍。  
  
 若為 **Update** 命令， **Where** 元素會識別要更新之屬性成員的範圍。 您可以使用 **Attributes** 父命令之 **Update** 集合和 **Attributes** 元素之 **Where** 集合中包含的屬性組合來更新多個屬性成員。  
  
 如需刪除和更新屬性成員的詳細資訊，請參閱[插入、更新和卸除成員 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

