---
title: KeyColumn 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- KeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e27744d2c8e2d54d44318ceac7b79dc4e4e10e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247758"
---
# <a name="keycolumn-element-assl"></a>KeyColumn 元素 (ASSL)
  包含屬於屬性索引鍵或其中一部分之資料行的定義。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[KeyColumns](../collections/columns-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`DataItem`型別，包括 Analysis Services 指令碼語言 (ASSL) 物件和屬性的資料表`DataItem`類型，請參閱[DataItem 資料類型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `KeyColumns` 集合父系的元素是 <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>、<xref:Microsoft.AnalysisServices.DimensionAttribute>、<xref:Microsoft.AnalysisServices.MeasureGroupAttribute> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [AggregationInstanceAttribute 資料類型&#40;ASSL&#41;](../data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension 資料類型&#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [DimensionAttribute 資料類型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [MeasureGroupAttribute 資料類型&#40;ASSL&#41;](../data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn 資料類型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
