---
title: 值元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa5a552bc756abee0e8755ebd7b4c107da4ea7c0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-xmla"></a>Value 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所需的值的[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)要新增的項目[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)命令，或[儲存格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)更新的項目[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)，[資料格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**屬性**項目，**值**項目包含的成員之後，應該包含所需的值**插入**命令就會認可。 如需有關插入成員的詳細資訊，請參閱[插入、 更新和卸除成員&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
 如**儲存格**項目，**值**項目包含的資料格之後，應該包含所需的值**UpdateCells**命令就會認可。 針對該資料格儲存於回寫資料表中的實際值就是資料格之原始值與資料格之所需值之間的差異。  
  
 這個元素所使用的資料類型應該與要更新之資料格的資料類型相符。  
  
 如需更新資料格的詳細資訊，請參閱[更新資料格 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CellOrdinal 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [插入項目 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
