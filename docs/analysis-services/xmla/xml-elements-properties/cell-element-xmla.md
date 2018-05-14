---
title: 資料格元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 014f46219ece054c292ff3a3b7a11d98c07c1547
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cell-element-xmla"></a>Cell 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含要由 [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) 命令更新之資料格的資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<UpdateCells>  
   ...  
   <Cell CellOrdinal="Long">  
      <Value>...</Value>  
   </Cell>  
   ...  
</UpdateCells>  
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
|父元素|[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|子元素|[值](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|說明|  
|---------------|-----------------|  
|CellOrdinal|必要的 **Long** 屬性。 包含要更新之資料格的以零為基底序數位置。|  
  
## <a name="remarks"></a>備註  
 如需更新資料格的詳細資訊，請參閱[更新資料格 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
