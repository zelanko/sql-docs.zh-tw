---
title: Description 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Description Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19a041d81646361d1f6eefb96604829ec1928032
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126128"
---
# <a name="description-element-assl"></a>Description 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)，[彙總](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)，[組件](../objects/assembly-element-assl.md)， [AttributePermission](../objects/attributepermission-element-assl.md)， [CalculationProperty](../objects/calculationproperty-element-assl.md)， [CellPermission](../objects/cellpermission-element-assl.md)， [Cube](../objects/cube-element-assl.md)， [CubeDimensionPermission](../data-type/permission-data-type-assl.md)，[資料庫](../objects/database-element-assl.md)[DataSource](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[階層](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[層級](../objects/level-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)，[量值](../objects/measure-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)， [資料分割](../objects/partition-element-assl.md)，[權限](../data-type/permission-data-type-assl.md)，[觀點來看](../objects/perspective-element-assl.md)，[角色](../objects/role-element-assl.md)， [Server](../objects/server-element-assl.md)， [追蹤](../objects/trace-element-assl.md)，[轉譯](../objects/translation-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Description` 元素的值具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 如果中的值包含開頭或尾端空格`Description`項目，移除這些空格會被隱含地[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   此值不得包含控制字元。 如果 `Description` 元素的值包含控制字元，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會隱含地移除這些字元。  
  
## <a name="see-also"></a>另請參閱  
 [名稱項目&#40;ASSL&#41;](name-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
