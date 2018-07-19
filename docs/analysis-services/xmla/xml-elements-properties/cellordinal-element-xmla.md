---
title: CellOrdinal 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e86dc93e6d7c2c4f8844f31d633fd95fdfa91463
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574344"
---
# <a name="cellordinal-element-xmla"></a>CellOrdinal 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含更新的資料格的 cube 中的序數位置[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cell>  
   ...  
   <CellOrdinal>...</CellOrdinal>  
   ...  
</Cell>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|長整數|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **CellOrdinal**元素會識別要更新之儲存格**UpdateCells**命令。  
  
 如需更新資料格的詳細資訊，請參閱[更新資料格 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另請參閱
 [值的項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)   
 [UpdateCells 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
