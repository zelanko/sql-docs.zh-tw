---
title: Description 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e0f31d44e908362b0416f7e02bacc204d976ca3d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="description-element-assl"></a>Description 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含父元素的描述。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)，[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)，[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)， [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)， [CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[層級](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)， [資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)，[角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)， [追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)，[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**描述**項目具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 如果值包含開頭或尾端空格**描述**項目，這些空格會隱含地移除[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   此值不得包含控制字元。 如果中的值包含控制字元**描述**項目，這些字元將會隱含地移除[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [名稱元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
