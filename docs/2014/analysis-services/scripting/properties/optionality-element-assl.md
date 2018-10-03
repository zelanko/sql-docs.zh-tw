---
title: Optionality 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Optionality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Optionality element
ms.assetid: 6cd2ef0a-6fbe-4462-ab27-4cdfeb33f8ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d59b04dad688d438ca2f4777b404dcc4fe8976b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099168"
---
# <a name="optionality-element-assl"></a>Optionality 元素 (ASSL)
  表示之成員的選擇性[AttributeRelationship](../objects/attributerelationship-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <Optionality>...</OPtionality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*必要項目*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*必要項目*|相關屬性中的每個成員至少必須與屬性中擁有 `AttributeRelationship` 元素的一個成員產生關聯。|  
|*選擇性*|相關屬性中的每個成員不一定要與屬性中擁有 `AttributeRelationship` 元素的一個成員產生關聯。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Cardinality` 允許值的列舉是 <xref:Microsoft.AnalysisServices.Optionality>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
