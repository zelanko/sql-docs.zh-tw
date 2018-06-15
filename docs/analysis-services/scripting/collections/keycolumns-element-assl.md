---
title: KeyColumns 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cb3bbbb05ddaaf77de7f384bcfb4614fd67d9db0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030389"
---
# <a name="keycolumns-element-assl"></a>KeyColumns 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含集合[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)元素定義的父物件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or AggregationInstanceAttribute, AggregationInstanceCubeDimension, MeasureGroupAttribute, ScalarMiningStructureColumn -->  
   ...  
   <KeyColumns>  
      <KeyColumn xsi:type="DataItem"...</KeyColumn>  
   </KeyColumns>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstanceAttribute](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)， [AggregationInstanceCubeDimension](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)型別的[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 **KeyColumns**集合可以包含多個**KeyColumn**之多部分的項目索引鍵屬性或採礦結構資料行。  
  
## <a name="see-also"></a>另請參閱  
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
