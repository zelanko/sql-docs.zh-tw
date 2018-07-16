---
title: Cardinality 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cardinality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Cardinality element
ms.assetid: 60ac8a26-7c8b-4011-9b9b-a29863779428
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7446923efc15a2fe05f3e8bf8c86a2e9f429a2c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325078"
---
# <a name="cardinality-element-assl"></a>Cardinality 元素 (ASSL)
  表示所描述之關聯性的基數[AttributeRelationship](../objects/attributerelationship-element-assl.md)或是[RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship> <!-- or RegularMeasureGroupDimension -->  
   ...  
   <Cardinality>...</Cardinality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*許多*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../objects/attributerelationship-element-assl.md)， [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*許多*|多對一關聯性|  
|*其中一個*|一對一關聯性|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Cardinality` 允許值的列舉是 <xref:Microsoft.AnalysisServices.Cardinality>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
