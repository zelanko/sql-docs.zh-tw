---
title: "其中元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Where Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords: Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e5958155b5209ec613df35b3cc94ad693ce00a88
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="where-element-xmla"></a>Where 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]定義父代所使用的篩選條件[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)或[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)命令。  
  
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
  
|特性|描述|  
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
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
