---
title: Column 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Column Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Column
helpviewer_keywords:
- Column element
ms.assetid: 10dc6d5e-c690-4415-adbb-eaeebaa29cb4
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 474e094335c22ca1a715b48715e968c7dd13f515
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312428"
---
# <a name="column-element-assl"></a>Column 元素 (ASSL)
  描述與父元素相關聯之資料行集合中的資料行。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Columns>  
   <Column xsi:type="MeasureBinding">...</Column> <!-- parent of collection: DrillThroughAction -->  
   <!-- or -->  
   <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent of collection: DrillThroughAction -->  
   <!-- or -->  
   <Column xsi:type="EventColumn">...</Column> <!-- parent of collection: Event -->  
   <!-- or -->  
   <Column xsi:type="MiningModelColumn">...</Column> <!-- parent of collection: MiningModel or MiningModelColumn -->  
   <!-- or -->  
   <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent of collection: MiningStructure or TableMiningStructureColumn -->  
</Columns>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度||  
|預設值|無|  
|基數||  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md)， [CubeAttributeBinding](../data-type/attributebinding-data-type-assl.md)|  
|[事件](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](miningstructure-element-assl.md)， [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[事件](event-element-assl.md)|1-n：出現一次以上的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料行](../collections/columns-element-assl.md)|  
|子元素|無|  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
