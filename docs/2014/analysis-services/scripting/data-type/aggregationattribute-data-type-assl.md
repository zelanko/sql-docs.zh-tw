---
title: AggregationAttribute 資料類型 (ASSL) |Microsoft Docs
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
- AggregationAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationAttribute
helpviewer_keywords:
- AggregationAttribute data type
ms.assetid: 636827c7-938d-4b7d-9827-46da3bc60d9a
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71da4468ab4edece07744ae73a13243eefd1dfed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243418"
---
# <a name="aggregationattribute-data-type-assl"></a>AggregationAttribute 資料類型 (ASSL)
  定義代表之間的關聯的基本資料類型[彙總](../objects/aggregation-element-assl.md)元素和屬性。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AttributeID](../properties/id-element-assl.md)，[註解](../collections/annotations-element-assl.md)|  
|衍生的元素|[屬性](../objects/attribute-element-assl.md)([屬性](../collections/attributes-element-assl.md)的集合[AggregationDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中的對應類別是 <xref:Microsoft.AnalysisServices.AggregationAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Aggregation 元素&#40;ASSL&#41;](../objects/aggregation-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
