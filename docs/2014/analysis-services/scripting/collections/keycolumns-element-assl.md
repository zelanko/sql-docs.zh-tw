---
title: KeyColumns 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KeyColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyColumns
helpviewer_keywords:
- KeyColumns element
ms.assetid: 03f3ad21-25cb-4afd-9287-cbf942ac1ad9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a5c699f95d91cdb48d780875d8f9190114d4b7a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152630"
---
# <a name="keycolumns-element-assl"></a>KeyColumns 元素 (ASSL)
  包含的集合[KeyColumn](../objects/column-element-assl.md)元素定義的父物件。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstanceAttribute](../data-type/aggregationinstanceattribute-data-type-assl.md)， [AggregationInstanceCubeDimension](../data-type/dimension-data-type-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|[KeyColumn](../objects/column-element-assl.md)型別的[DataItem](../data-type/dataitem-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 `KeyColumns` 集合可以包含屬性或採礦結構資料行之多部分索引鍵的多個 `KeyColumn` 元素。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
