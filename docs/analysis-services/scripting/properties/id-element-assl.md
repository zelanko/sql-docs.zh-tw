---
title: "ID 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ID
helpviewer_keywords: ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 16b2e7db5b7cd20f9addfeb1965c175b1aeff541
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="id-element-assl"></a>ID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含父元素的唯一識別碼 (ID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (最多 100 個字元)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)，[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)，[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)， [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[層級](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)，[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)，[角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)，[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在每個主要物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]具有**識別碼**元素當做屬性。 值**識別碼**項目具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]將會隱含地移除開頭或尾端空格的值從**識別碼**項目。  
  
-   此值不得包含控制字元。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]將會隱含地移除控制字元的值從**識別碼**項目。  
  
-   下列保留的值不可使用：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9 (COM1、COM2、COM3 等等)  
  
    -   CON  
  
    -   LPT1 到 LPT9 (LPT1、LPT2、LPT3 等等)  
  
    -   NUL  
  
    -   PRN  
  
 下表列出的值之中不能使用的其他字元**識別碼**項目，並根據父項目。  
  
|父元素|字元|  
|--------------------|----------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|此值必須依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 電腦名稱的規則 (IP 位址無效)。|  
|[資料來源](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[層級](../../../analysis-services/scripting/objects/level-element-assl.md)，[屬性項目](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|所有其他的父元素。|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>請參閱  
 [Name 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
