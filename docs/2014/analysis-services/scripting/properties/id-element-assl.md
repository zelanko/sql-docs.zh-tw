---
title: ID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c323bd71865d0dd09bf724373ece03d83e7608ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209938"
---
# <a name="id-element-assl"></a>ID 元素 (ASSL)
  包含父元素的唯一識別碼 (ID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (最多 100 個字元)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)，[彙總](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)，[組件](../objects/assembly-element-assl.md)， [Cube](../objects/cube-element-assl.md)， [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)，[資料庫](../objects/database-element-assl.md)， [DataSource](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[階層](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[層級](../objects/level-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)，[量值](../objects/measure-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)，[分割](../objects/partition-element-assl.md)，[權限](../data-type/permission-data-type-assl.md)，[觀點來看](../objects/perspective-element-assl.md)，[角色](../objects/role-element-assl.md)，[伺服器](../objects/server-element-assl.md)，[追蹤](../objects/trace-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在每個主要物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]具有`ID`元素當做屬性。 `ID` 元素的值具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將從 `ID` 元素的值中隱含地移除開頭或尾端空格。  
  
-   此值不得包含控制字元。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將從 `ID` 元素的值中隱含地移除控制字元。  
  
-   下列保留的值不可使用：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9 (COM1、COM2、COM3 等等)  
  
    -   CON  
  
    -   LPT1 到 LPT9 (LPT1、LPT2、LPT3 等等)  
  
    -   NUL  
  
    -   PRN  
  
 下表將列出無法在 `ID` 元素值內部使用的其他字元，端視父元素而定。  
  
|父元素|字元|  
|--------------------|----------------|  
|[Server](../objects/server-element-assl.md)|此值必須依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 電腦名稱的規則 (IP 位址無效)。|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?"（) []{}<>|  
|[層級](../objects/level-element-assl.md)，[屬性項目](../objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"& %$！ + = []{}<>|  
|所有其他的父元素。|.,;'`:/\\*&#124;?"& %$！ + = （) []{}<>|  
  
## <a name="see-also"></a>另請參閱  
 [名稱項目&#40;ASSL&#41;](name-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
