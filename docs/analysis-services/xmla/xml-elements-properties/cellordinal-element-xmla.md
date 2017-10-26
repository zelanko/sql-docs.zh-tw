---
title: "CellOrdinal 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CellOrdinal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellordinal
- urn:schemas-microsoft-com:xml-analysis#CellOrdinal
- http://schemas.microsoft.com/analysisservices/2003/engine#CellOrdinal
helpviewer_keywords:
- CellOrdinal element
ms.assetid: 1808c498-e3b4-4e5c-9e22-7f8662d32874
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49094babe0ca84d60015c56112d7103340a909ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cellordinal-element-xmla"></a>CellOrdinal 元素 (XMLA)
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
  
|特性|說明|  
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
 [Value 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)   
 [UpdateCells 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

