---
title: ID 元素 (ASSL) |Microsoft 文件
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0a1ad98b6b9609cf50d16816c8ae5328083a63ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144813"
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
|父元素|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [Cube](../objects/cube-element-assl.md), [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding](../data-type/binding-data-type-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [Trace](../objects/trace-element-assl.md)|  
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
 [名稱元素&#40;ASSL&#41;](name-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  