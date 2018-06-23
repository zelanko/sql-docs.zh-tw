---
title: Analysis Services 指令碼語言 XML 資料類型階層 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Analysis Services Scripting Language XML Data Type Hierarchy
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
ms.assetid: f143c9f8-225d-495d-ac8e-ac2d2a7b4c07
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2ebea80cfdecc82a3db5bb1c6cc4b10dcf40b06c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036480"
---
# <a name="analysis-services-scripting-language-xml-data-type-hierarchy-assl"></a>Analysis Services 指令碼語言 XML 資料類型階層 (ASSL)
  下表顯示「Analysis Services 指令碼語言」(ASSL) 中資料類型的繼承階層。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
Action  
DrillThroughAction  
ReportAction  
StandardAction  
AggregationAttribute  
AggregationDesignAttribute  
AggregationDesignDimension  
AggregationDimension  
Assembly  
ClrAssembly  
ComAssembly  
AttributeTranslation  
Binding  
AttributeBinding  
ColumnBinding  
CubeAttributeBinding  
CubeDimensionBinding  
DataSourceViewBinding  
DimensionBinding  
InheritedBinding  
MeasureBinding  
MeasureGroupBinding  
MeasureGroupDimensionBinding  
PartitionBinding  
ProactiveCachingBinding  
ProactiveCachingIncrementalProcessingBinding  
ProactiveCachingObjectNotificationBinding  
ProactiveCachingInheritedBinding  
ProactiveCachingTablesBinding  
ProactiveCachingQueryBinding  
RowBinding  
TabularBinding  
DSVTableBinding  
QueryBinding  
TableBinding  
TimeAttributeBinding  
TimeBinding  
UserDefinedGroupBinding  
ClrAssemblyFile  
CubeAttribute  
CubeBinding (out-of-line)  
CubeDimension  
CubeDimensionPermission  
CubeHierarchy  
DataBlock  
DataItem  
DataMiningMeasureGroupDimension  
DegenerateMeasureGroupDimension  
DimensionAttribute  
EventColumn  
ManyToManyMeasureGroupDimension  
MeasureGroupAttribute  
MeasureGroupBinding (out-of-line)  
MeasureGroupDimension  
MeasureGroupHierarchy  
MiningModelColumn  
MiningModelingFlag  
MiningStructureColumn  
OlapDataSource  
Permission  
PerspectiveAction  
PerspectiveAttribute  
PerspectiveCalculation  
PerspectiveDimension  
PerspectiveHierarchy  
PerspectiveKpi  
PerspectiveMeasure  
PerspectiveMeasureGroup  
PushedDataSource  
ReferenceMeasureGroupDimension  
RegularMeasureGroupDimension  
RelationalDataSource  
ScalarMiningStructureColumn  
TableMiningStructureColumn  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](data-type/analysis-services-scripting-language-xml-data-types-assl.md)   
 [Analysis Services 指令碼語言 XML 元素階層&#40;ASSL&#41;](analysis-services-scripting-language-xml-element-hierarchy-assl.md)   
 [Analysis Services 指令碼語言&#40;ASSL&#41;參考](analysis-services-scripting-language-assl-for-xmla.md)  
  
  