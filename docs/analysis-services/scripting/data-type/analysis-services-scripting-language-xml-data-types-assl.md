---
title: "Analysis Services 指令碼語言 XML 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Analysis Services Scripting Language XML Data Types
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b15c0ffee8bc0217ec119d6d66ef446f7897c0e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>Analysis Services 指令碼語言 XML 資料類型 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做類型之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，從開發人員的觀點來看，這一節所述的元素對應至類型，例如**繫結**和**權限**，這是用來定義子項目和其他物件的屬性。  
  
 雖然類型元素 (例如物件元素) 絕對不是 ASSL 結構描述中的分葉層級元素，但是會具有對應至物件屬性的子元素和元素。  
  
 但是型別項目永遠不會顯示定義或描述的指令碼中的項目[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]物件。 而是它會顯示為其他物件元素，通常會以指定的型別**類型**屬性從 XML 結構描述執行個體結構描述使用**xsi: type**或**xs: type**。 例如， `<Assembly xsi:type="ClrAssembly">...</Assembly>`。  
  
 在部分情況中，某個類型會衍生自另一個類型。 例如， **CubeBinding**類型衍生自父代**繫結**型別。  
  
|元素|Description|  
|-------------|-----------------|  
|[Action 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|定義表示中的動作的抽象基本資料類型[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[AggregationAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationattribute-data-type-assl.md)|定義代表之間的關聯的基本資料類型[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)元素和屬性。|  
|[AggregationDesignAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)|定義代表屬性之間的關聯的基本資料類型和[AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)項目。|  
|[AggregationDesignDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)|定義代表 cube 維度之間的關聯性的基本資料類型和[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)項目。|  
|[AggregationDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)|定義代表維度之間的關聯性的基本資料類型和[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)項目。|  
|[AggregationInstanceAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)|定義代表彙總執行個體所使用之屬性相關資訊的基本資料類型。|  
|[AggregationInstanceCubeDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)|定義代表彙總執行個體所使用之 Cube 維度相關資訊的基本資料類型。|  
|[AggregationInstanceMeasure 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)|定義代表彙總執行個體所使用之量值相關資訊的基本資料類型。|  
|[Assembly 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/assembly-data-type-assl.md)|定義表示的抽象基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件或 COM 動態連結程式庫 (DLL) 相關聯[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)或[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[AttributeBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|定義衍生的資料類型表示的繫結[屬性](../../../analysis-services/scripting/objects/attribute-element-assl.md)項目。|  
|[AttributeTranslation 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|定義代表與相關聯之翻譯的衍生的資料類型[屬性](../../../analysis-services/scripting/objects/attribute-element-assl.md)項目|  
|[繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|定義代表兩個物件之間相依關聯性的抽象基本資料類型，其中某個物件的資料或中繼資料相依於繫結物件的資料或中繼資料。|  
|[ClrAssembly 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|定義衍生的資料類型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]與相關聯的組件[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)或[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目|  
|[ClrAssemblyFile 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|定義代表其中一個檔案組成的基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件 ([ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)項目)。|  
|[ColumnBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|定義代表資料來源檢視中的資料行的繫結的衍生的資料類型[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)項目。|  
|[ComAssembly 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|定義代表與相關聯之 COM 程式庫的衍生的資料類型[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)或[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[CubeAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)|定義代表屬性相關聯的基本資料類型[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[CubeAttributeBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|定義代表 Cube 維度中某個屬性與動作或採礦結構資料行之繫結的衍生資料類型。|  
|[CubeBinding 資料類型 &#40;-單行 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|定義表示之間的關聯性的基本資料型別[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目和[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)項目。|  
|[CubeDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|定義代表維度與 Cube 之間關聯性的基本資料類型。|  
|[CubeDimensionBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|定義衍生的資料類型表示的繫結[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)加入 cube 維度中的項目。|  
|[CubeDimensionPermission 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)|定義代表在 Cube 中特定維度上單一角色之權限的基本資料類型。|  
|[CubeHierarchy 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|定義代表的相關資訊的基本資料類型[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)中的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[DataBlock 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)|定義代表用來儲存的二進位內容資料區塊集合的基本資料類型[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。|  
|[DataItem 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|定義代表某個資料項目 (例如資料行或屬性) 之資料相關特性的基本資料類型。|  
|[DataMiningMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)|定義代表量值群組與資料採礦維度之間關聯性的衍生資料類型。|  
|[DataSource 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|定義表示中的資料來源的抽象基本資料類型[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[DataSourceViewBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|定義代表資料來源檢視與父元素之間繫結的衍生資料類型。|  
|[DegenerateMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)|定義代表變質維度 (亦即，事實維度) 與量值群組之間關聯性的衍生資料類型。|  
|[Dimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|定義代表資料庫維度的基本資料類型。|  
|[DimensionAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|定義代表維度中某個屬性的基本資料類型。|  
|[DimensionBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|定義代表資料來源之間的繫結的衍生的資料類型和[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)項目。|  
|[DimensionPermission 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)|定義代表指派給資料庫維度之權限的衍生資料類型。|  
|[DrillThroughAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|定義代表鑽研動作的衍生資料類型。|  
|[DSVTableBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md)|定義代表資料表之間的繫結的衍生的資料類型和[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)項目。|  
|[EventColumn 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|定義代表要針對擷取資訊的資料行的基本資料類型[事件](../../../analysis-services/scripting/objects/event-element-assl.md)一部分的項目[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目。|  
|[Hierarchy 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/hierarchy-data-type-assl.md)|定義代表維度中某個階層的基本資料類型。|  
|[ImpersonationInfo 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|定義代表用來模擬使用者之資訊的基本資料類型。|  
|[IncrementalProcessingNotification 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/incrementalprocessingnotification-data-type-assl.md)|定義衍生的資料類型代表資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷累加式處理進度所執行之查詢的項目。|  
|[InheritedBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|定義衍生的資料類型，以指出[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)元素會從屬性繼承其繫結。|  
|[ManyToManyMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)|定義代表多對多維度與量值群組之間關聯性的衍生資料類型。|  
|[MeasureBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|定義代表量值與父元素之繫結的衍生資料類型。|  
|[MeasureGroupAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|定義代表某個屬性與量值群組之間關聯性的基本資料類型。|  
|[MeasureGroupBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)項目。|  
|[MeasureGroupBinding 資料類型 &#40;-單行 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|定義代表量值群組之繫結的基本資料類型。|  
|[MeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|定義代表某個維度與量值群組之間關聯性的抽象基本資料類型。|  
|[MeasureGroupDimensionBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|定義代表維度與量值群組之間繫結的衍生資料類型。|  
|[MeasureGroupHierarchy 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)|定義代表量值群組中某個階層之相關資訊的基本資料類型。|  
|[MiningModelColumn 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|定義代表資料行中的相關資訊的基本資料類型[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[MiningModelingFlag 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningmodelingflag-data-type-assl.md)|定義表示之可用模型旗標的基本資料型別[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)項目。|  
|[MiningStructureColumn 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|定義代表資料行中的相關資訊的抽象基本資料類型[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。|  
|[OlapDataSource 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md)|定義代表多維度的衍生的資料類型[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)項目。|  
|[PartitionBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目。|  
|[Permission 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|定義代表個別權限之相關資訊的抽象基本資料類型。|  
|[PerspectiveAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|定義代表中動作的相關資訊的基本資料類型[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[PerspectiveAttribute 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|定義代表中屬性的相關資訊的基本資料類型[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)項目。|  
|[PerspectiveCalculation 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)|定義代表計算之間的關聯性的基本資料類型和[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[PerspectiveDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|定義代表檢視方塊中某個維度之相關資訊的基本資料類型。|  
|[PerspectiveHierarchy 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|定義代表某個階層中之相關資訊的基本資料類型[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)項目。|  
|[PerspectiveKpi 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|定義代表關鍵效能指標 (KPI) 的相關資訊的基本資料類型中[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[PerspectiveMeasure 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|定義代表量值中的相關資訊的基本資料類型[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)項目。|  
|[PerspectiveMeasureGroup 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|定義代表量值群組中的相關資訊的基本資料類型[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[ProactiveCachingBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關需要重建快取中的資料來源變更或重建處理序狀態的項目。|  
|[ProactiveCachingIncrementalProcessingBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關重建快取之處理序的狀態項目。|  
|[ProactiveCachingInheritedBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachinginheritedbinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關資料表與檢視透過需要重建快取的現有資料繫結中的資料來源變更的項目。|  
|[ProactiveCachingObjectNotificationBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關資料來源變更的項目，在指定的資料表和檢視表或資料表和檢視表中識別透過現有資料繫結需要重建快取。|  
|[ProactiveCachingQueryBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關資料表和檢視，透過指定的查詢需要重建快取的執行中的資料來源變更的項目。|  
|[ProactiveCachingTablesBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關指定之資料表和檢視表需要重建快取中的資料來源變更的項目。|  
|[PushedDataSource 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|定義代表資料來源的基本資料類型 (例如[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]封裝) 用於 「 推送 」 資料[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[QueryBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)|定義衍生的資料類型表示的關聯性[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)具有項目[QueryDefinition](../../../analysis-services/scripting/properties/querydefinition-element-assl.md)項目。|  
|[ReferenceMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|定義代表透過中繼維度與事實資料表間接相關之維度的衍生資料類型  (例如，Sales 量值群組可以參考透過 Customer 維度相關的 Geography 維度)。|  
|[RegularMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|定義代表維度與量值群組之間一般關聯性的衍生資料類型。|  
|[RelationalDataSource 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md)|定義衍生的資料類型，表示[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)關聯式資料來源為基礎的項目。|  
|[ReportAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|定義代表產生 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表之動作的衍生資料類型。|  
|[RowBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|定義代表資料表中的資料列繫結的衍生的資料類型[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)項目。|  
|[ScalarMiningStructureColumn 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|定義衍生的資料類型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含純量值，而不是巢狀資料表與相關聯的項目[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)包含巢狀的資料表的項目。|  
|[StandardAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|定義衍生的資料類型，它代表任何[動作](../../../analysis-services/scripting/objects/action-element-assl.md)以外的項目[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)項目或[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)項目。|  
|[TableBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|定義代表資料表之繫結的衍生資料類型。|  
|[TableMiningStructureColumn 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|定義衍生的資料類型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含巢狀的資料表，而不是與相關聯的純量值的項目[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)包含純量值的項目。|  
|[TabularBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|定義代表表格式項目 (例如資料表或 Cube 維度) 之繫結的抽象衍生資料類型。|  
|[TimeAttributeBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md)|定義衍生資料類型，它代表在伺服器時間維度中產生之資料項目 (例如屬性的索引鍵資料行) 的「預留位置」繫結。|  
|[TimeBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|定義代表時間週期之繫結的衍生資料類型。|  
|[Translation 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|定義代表當地語系化翻譯的基本資料類型。|  
|[UserDefinedGroupBinding 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|定義代表某個屬性之使用者定義群組的衍生資料類型。|  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 指令碼語言 XML 元素階層 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
