---
title: AttributeID 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52ab6f4ac9f1a2869b02b91334f6c2ca41d982d8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035749"
---
# <a name="attributeid-element-assl"></a>AttributeID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含與父元素相關聯之屬性的識別碼。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationAttribute> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <AttributeID>...</AttributeID>  
   ...  
</AggregationAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationAttribute](../../../analysis-services/scripting/data-type/aggregationattribute-data-type-assl.md)， [AggregationDesignAttribute](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)， [AggregationInstanceAttribute](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)， [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)， [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)， [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**AttributeID**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AggregationAttribute>， <xref:Microsoft.AnalysisServices.AggregationDesignAttribute>， <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>， <xref:Microsoft.AnalysisServices.AttributeBinding>， <xref:Microsoft.AnalysisServices.AttributePermission>， <xref:Microsoft.AnalysisServices.AttributeRelationship><xref:Microsoft.AnalysisServices.CubeAttribute>， <xref:Microsoft.AnalysisServices.CubeAttributeBinding>， <xref:Microsoft.AnalysisServices.PerspectiveAttribute>，和<xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
