---
title: RelationshipType 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d740a3bed4b9fe8d9aa3bf259a9b83a59af26f5a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指出是否成員關聯性[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)可以變更。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*彈性*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*固定*|屬性與相關屬性之間的成員關聯性無法變更。|  
|*彈性*|屬性與相關屬性之間的成員關聯性可以變更。|  
  
 例如，如果**ZipCode**無法變更從一個**縣 （市)** 之間的關聯性**ZipCode**至**縣 （市)** 標示為*固定*。  
  
 列舉型別對應至允許的值**RelationshipType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.RelationshipType>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
