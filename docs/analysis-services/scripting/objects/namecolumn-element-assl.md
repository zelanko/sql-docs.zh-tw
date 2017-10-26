---
title: "NameColumn 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NameColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NameColumn
helpviewer_keywords:
- NameColumn element
ms.assetid: 9ff79f2e-26d7-4ab9-a166-14c2c2d1fc07
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3d625f03339e5b17981db9d4e8105679fde40fb0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="namecolumn-element-assl"></a>NameColumn 元素 (ASSL)
  識別提供父元素名稱的資料行。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <NameColumn xsi:type="DataItem">...</NameColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|預設值|請參閱下表。|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
|上階或父系|預設值|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|非固定 (請參閱「備註」)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|無|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)集合**DimensionAttribute**包含單一[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)代表具有字串資料類型，相同的索引鍵資料行項目**DataItem**值做為預設值**NameColumn**項目。  
  
 如需有關**DataItem**型別，包括 Analysis Services 指令碼語言 (ASSL) 物件和屬性的資料表**DataItem**類型，請參閱[DataItem 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 對應至父系的項目**NameColumn**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

