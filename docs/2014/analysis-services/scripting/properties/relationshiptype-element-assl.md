---
title: RelationshipType 元素 (ASSL) |Microsoft 文件
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
- RelationshipType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a2e5b5ec9e9591a45a80f099397ed6568a986313
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145239"
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 元素 (ASSL)
  指出是否成員關聯性[AttributeRelationship](../objects/attributerelationship-element-assl.md)可以變更。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*彈性*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*固定*|屬性與相關屬性之間的成員關聯性無法變更。|  
|*彈性*|屬性與相關屬性之間的成員關聯性可以變更。|  
  
 例如，如果`ZipCode`無法從一個變更`City`之間的關聯性`ZipCode`至`City`標示為*固定*。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `RelationshipType` 允許值的列舉是 <xref:Microsoft.AnalysisServices.RelationshipType>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  