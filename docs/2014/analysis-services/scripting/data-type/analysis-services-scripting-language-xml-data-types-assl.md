---
title: Analysis Services 指令碼語言 XML 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Analysis Services Scripting Language XML Data Types
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5ff2f0989aa2c88a69351d698c847ca6e835285
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179248"
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>Analysis Services 指令碼語言 XML 資料類型 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做類型之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，但是從開發人員的觀點而言，本節中描述的元素會對應至用來定義其他物件之子元素和屬性的類型，例如 `Binding` 和 `Permission`。  
  
 雖然類型元素 (例如物件元素) 絕對不是 ASSL 結構描述中的分葉層級元素，但是會具有對應至物件屬性的子元素和元素。  
  
 不過，類型元素絕不會顯示為定義或描述的指令碼中的項目[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]物件。 反而，它會顯示成其他物件元素的類型，而這種類型通常是使用 `type` 或 `xsi:type` 以「XML 結構描述執行個體」結構描述的 `xs:type` 屬性指定。 例如， `<Assembly xsi:type="ClrAssembly">...</Assembly>` 。  
  
 在部分情況中，某個類型會衍生自另一個類型。 例如，`CubeBinding` 類型便衍生自 `Binding` 父類型。  
  
|元素|描述|  
|-------------|-----------------|  
|[Action 資料類型&#40;ASSL&#41;](action-data-type-assl.md)|定義表示中的動作的抽象基本資料類型[Cube](../objects/cube-element-assl.md)項目或有[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[AggregationAttribute 資料類型&#40;ASSL&#41;](aggregationattribute-data-type-assl.md)|定義代表之間的關聯的基本資料類型[彙總](../objects/aggregation-element-assl.md)元素和屬性。|  
|[AggregationDesignAttribute 資料類型&#40;ASSL&#41;](aggregationdesignattribute-data-type-assl.md)|定義代表屬性之間的關聯的基本資料類型和[AggregationDesignDimension](dimension-data-type-assl.md)項目。|  
|[AggregationDesignDimension 資料類型&#40;ASSL&#41;](dimension-data-type-assl.md)|定義代表 cube 維度之間的關聯性的基本資料類型和[AggregationDesign](../objects/aggregationdesign-element-assl.md)項目。|  
|[AggregationDimension 資料類型&#40;ASSL&#41;](aggregationdimension-data-type-assl.md)|定義代表維度之間的關聯性的基本資料類型和[彙總](../objects/aggregation-element-assl.md)項目。|  
|[AggregationInstanceAttribute 資料類型&#40;ASSL&#41;](aggregationinstanceattribute-data-type-assl.md)|定義代表彙總執行個體所使用之屬性相關資訊的基本資料類型。|  
|[AggregationInstanceCubeDimension 資料類型&#40;ASSL&#41;](cubedimension-data-type-assl.md)|定義代表彙總執行個體所使用之 Cube 維度相關資訊的基本資料類型。|  
|[AggregationInstanceMeasure 資料類型&#40;ASSL&#41;](aggregationinstancemeasure-data-type-assl.md)|定義代表彙總執行個體所使用之量值相關資訊的基本資料類型。|  
|[Assembly 資料類型&#40;ASSL&#41;](assembly-data-type-assl.md)|定義表示的抽象基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件或 COM 動態連結程式庫 (DLL) 與相關聯[伺服器](../objects/server-element-assl.md)或是[資料庫](../objects/database-element-assl.md)項目。|  
|[AttributeBinding 資料類型&#40;ASSL&#41;](binding-data-type-assl.md)|定義衍生的資料類型表示的繫結[屬性](../objects/attribute-element-assl.md)項目。|  
|[AttributeTranslation 資料類型&#40;ASSL&#41;](translation-data-type-assl.md)|定義代表與相關聯之翻譯的衍生的資料類型[屬性](../objects/attribute-element-assl.md)項目|  
|[繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)|定義代表兩個物件之間相依關聯性的抽象基本資料類型，其中某個物件的資料或中繼資料相依於繫結物件的資料或中繼資料。|  
|[ClrAssembly 資料類型&#40;ASSL&#41;](clrassembly-data-type-assl.md)|定義衍生的資料類型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]相關聯的組件[資料庫](../objects/database-element-assl.md)或是[Server](../objects/server-element-assl.md)項目|  
|[ClrAssemblyFile 資料類型&#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)|定義代表其中一個 compose 檔案的基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件 ([ClrAssembly](clrassembly-data-type-assl.md)項目)。|  
|[ColumnBinding 資料類型&#40;ASSL&#41;](columnbinding-data-type-assl.md)|定義代表資料來源檢視中的資料行的繫結的衍生的資料類型[DataItem](dataitem-data-type-assl.md)項目。|  
|[ComAssembly 資料類型&#40;ASSL&#41;](comassembly-data-type-assl.md)|定義代表與相關聯之 COM 程式庫的衍生的資料類型[伺服器](../objects/server-element-assl.md)或是[資料庫](../objects/database-element-assl.md)項目。|  
|[CubeAttribute 資料類型&#40;ASSL&#41;](cubeattribute-data-type-assl.md)|定義代表屬性與相關聯的基本資料類型[Cube](../objects/cube-element-assl.md)項目。|  
|[CubeAttributeBinding 資料類型&#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|定義代表 Cube 維度中某個屬性與動作或採礦結構資料行之繫結的衍生資料類型。|  
|[CubeBinding 資料類型&#40;程式碼外部&#41; &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|定義表示之間的關聯性的基本資料型別[Cube](../objects/cube-element-assl.md)項目並[DataSource](../objects/datasource-element-assl.md)項目。|  
|[CubeDimension 資料類型&#40;ASSL&#41;](cubedimension-data-type-assl.md)|定義代表維度與 Cube 之間關聯性的基本資料類型。|  
|[CubeDimensionBinding 資料類型&#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|定義衍生的資料類型表示的繫結[維度](../objects/dimension-element-assl.md)，[量值](../objects/measure-element-assl.md)，或[MiningModel](../objects/miningmodel-element-assl.md)的 cube 維度的項目。|  
|[CubeDimensionPermission 資料類型&#40;ASSL&#41;](permission-data-type-assl.md)|定義代表在 Cube 中特定維度上單一角色之權限的基本資料類型。|  
|[CubeHierarchy 資料類型&#40;ASSL&#41;](hierarchy-data-type-assl.md)|表示有關的資訊的基本資料類型會定義[階層](../objects/hierarchy-element-assl.md)中的項目[Cube](../objects/cube-element-assl.md)項目。|  
|[DataBlock 資料類型&#40;ASSL&#41;](datablock-data-type-assl.md)|定義代表用來儲存的二進位內容的資料區塊集合的基本資料類型[ClrAssemblyFile](clrassemblyfile-data-type-assl.md)項目。|  
|[DataItem 資料類型&#40;ASSL&#41;](dataitem-data-type-assl.md)|定義代表某個資料項目 (例如資料行或屬性) 之資料相關特性的基本資料類型。|  
|[DataMiningMeasureGroupDimension 資料類型&#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|定義代表量值群組與資料採礦維度之間關聯性的衍生資料類型。|  
|[DataSource 資料類型&#40;ASSL&#41;](datasource-data-type-assl.md)|定義表示中的資料來源的抽象基本資料類型[資料庫](../objects/database-element-assl.md)項目。|  
|[DataSourceViewBinding 資料類型&#40;ASSL&#41;](datasourceviewbinding-data-type-assl.md)|定義代表資料來源檢視與父元素之間繫結的衍生資料類型。|  
|[DegenerateMeasureGroupDimension 資料類型&#40;ASSL&#41;](degeneratemeasuregroupdimension-data-type-assl.md)|定義代表變質維度 (亦即，事實維度) 與量值群組之間關聯性的衍生資料類型。|  
|[維度的資料類型&#40;ASSL&#41;](dimension-data-type-assl.md)|定義代表資料庫維度的基本資料類型。|  
|[DimensionAttribute 資料類型&#40;ASSL&#41;](dimensionattribute-data-type-assl.md)|定義代表維度中某個屬性的基本資料類型。|  
|[DimensionBinding 資料類型&#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|定義代表資料來源之間的繫結的衍生的資料類型和[維度](../objects/dimension-element-assl.md)項目。|  
|[DimensionPermission 資料類型&#40;ASSL&#41;](permission-data-type-assl.md)|定義代表指派給資料庫維度之權限的衍生資料類型。|  
|[DrillThroughAction 資料類型&#40;ASSL&#41;](drillthroughaction-data-type-assl.md)|定義代表鑽研動作的衍生資料類型。|  
|[DSVTableBinding 資料類型&#40;ASSL&#41;](tablebinding-data-type-assl.md)|定義代表資料表之間的繫結的衍生的資料類型和[DataSourceView](../objects/datasourceview-element-assl.md)項目。|  
|[EventColumn 資料類型&#40;ASSL&#41;](eventcolumn-data-type-assl.md)|定義代表要針對擷取資訊的資料行的基本資料類型[事件](../objects/event-element-assl.md)一部分的項目[追蹤](../objects/trace-element-assl.md)項目。|  
|[Hierarchy 資料類型&#40;ASSL&#41;](hierarchy-data-type-assl.md)|定義代表維度中某個階層的基本資料類型。|  
|[ImpersonationInfo 資料類型&#40;ASSL&#41;](impersonationinfo-data-type-assl.md)|定義代表用來模擬使用者之資訊的基本資料類型。|  
|[IncrementalProcessingNotification 資料類型&#40;ASSL&#41;](incrementalprocessingnotification-data-type-assl.md)|定義衍生的資料類型表示的資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關判斷累加式處理進度所執行之查詢的項目。|  
|[InheritedBinding 資料類型&#40;ASSL&#41;](inheritedbinding-data-type-assl.md)|定義衍生的資料類型，表示[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)元素會從屬性繼承其繫結。|  
|[ManyToManyMeasureGroupDimension 資料類型&#40;ASSL&#41;](manytomanymeasuregroupdimension-data-type-assl.md)|定義代表多對多維度與量值群組之間關聯性的衍生資料類型。|  
|[MeasureBinding 資料類型&#40;ASSL&#41;](measurebinding-data-type-assl.md)|定義代表量值與父元素之繫結的衍生資料類型。|  
|[MeasureGroupAttribute 資料類型&#40;ASSL&#41;](measuregroupattribute-data-type-assl.md)|定義代表某個屬性與量值群組之間關聯性的基本資料類型。|  
|[MeasureGroupBinding 資料類型&#40;ASSL&#41;](measuregroupbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[MeasureGroup](../objects/group-element-assl.md)項目。|  
|[MeasureGroupBinding 資料類型&#40;程式碼外部&#41; &#40;ASSL&#41;](measuregroupbinding-data-type-out-of-line-assl.md)|定義代表量值群組之繫結的基本資料類型。|  
|[MeasureGroupDimension 資料類型&#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|定義代表某個維度與量值群組之間關聯性的抽象基本資料類型。|  
|[MeasureGroupDimensionBinding 資料類型&#40;ASSL&#41;](measuregroupdimensionbinding-data-type-assl.md)|定義代表維度與量值群組之間繫結的衍生資料類型。|  
|[MeasureGroupHierarchy 資料類型&#40;ASSL&#41;](measuregrouphierarchy-data-type-assl.md)|定義代表量值群組中某個階層之相關資訊的基本資料類型。|  
|[MiningModelColumn 資料類型&#40;ASSL&#41;](miningmodelcolumn-data-type-assl.md)|定義代表資料行中的相關資訊的基本資料類型[MiningModel](../objects/miningmodel-element-assl.md)項目。|  
|[MiningModelingFlag 資料類型&#40;ASSL&#41;](miningmodelingflag-data-type-assl.md)|定義表示之可用模型旗標的基本資料型別[ModelingFlag](../objects/modelingflag-element-assl.md)項目。|  
|[MiningStructureColumn 資料類型&#40;ASSL&#41;](miningstructurecolumn-data-type-assl.md)|定義代表資料行中的相關資訊的抽象基本資料類型[MiningStructure](../objects/miningstructure-element-assl.md)項目。|  
|[OlapDataSource 資料類型&#40;ASSL&#41;](olapdatasource-data-type-assl.md)|定義代表多維度的衍生的資料類型[DataSource](../objects/datasource-element-assl.md)項目。|  
|[PartitionBinding 資料類型&#40;ASSL&#41;](partitionbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[分割區](../objects/partition-element-assl.md)項目。|  
|[Permission 資料類型&#40;ASSL&#41;](permission-data-type-assl.md)|定義代表個別權限之相關資訊的抽象基本資料類型。|  
|[PerspectiveAction 資料類型&#40;ASSL&#41;](perspectiveaction-data-type-assl.md)|定義代表中動作的相關資訊的基本資料類型[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[PerspectiveAttribute 資料類型&#40;ASSL&#41;](perspectiveattribute-data-type-assl.md)|定義代表屬性中的相關資訊的基本資料類型[PerspectiveDimension](perspectivedimension-data-type-assl.md)項目。|  
|[PerspectiveCalculation 資料類型&#40;ASSL&#41;](perspectivecalculation-data-type-assl.md)|定義代表計算之間的關聯性的基本資料類型和[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[PerspectiveDimension 資料類型&#40;ASSL&#41;](perspectivedimension-data-type-assl.md)|定義代表檢視方塊中某個維度之相關資訊的基本資料類型。|  
|[PerspectiveHierarchy 資料類型&#40;ASSL&#41;](perspectivehierarchy-data-type-assl.md)|定義代表某個階層中之相關資訊的基本資料類型[PerspectiveDimension](perspectivedimension-data-type-assl.md)項目。|  
|[PerspectiveKpi 資料類型&#40;ASSL&#41;](perspectivekpi-data-type-assl.md)|定義代表關鍵效能指標 (KPI) 的相關資訊的基本資料類型中[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[PerspectiveMeasure 資料類型&#40;ASSL&#41;](perspectivemeasure-data-type-assl.md)|定義代表量值中的相關資訊的基本資料類型[PerspectiveMeasureGroup](perspectivemeasuregroup-data-type-assl.md)項目。|  
|[PerspectiveMeasureGroup 資料類型&#40;ASSL&#41;](perspectivemeasuregroup-data-type-assl.md)|定義代表量值群組中的相關資訊的基本資料類型[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[ProactiveCachingBinding 資料類型&#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)|定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關需要重建快取中的資料來源變更或重建處理序狀態的項目。|  
|[ProactiveCachingIncrementalProcessingBinding 資料類型&#40;ASSL&#41;](proactivecachingincrementalprocessingbinding-data-type-assl.md)|定義代表繫結的衍生的資料類型[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關重建快取之處理序狀態的項目。|  
|[ProactiveCachingInheritedBinding 資料類型&#40;ASSL&#41;](proactivecachinginheritedbinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料表和檢視透過需要重建快取的現有資料繫結所識別的資料來源變更的項目。|  
|[ProactiveCachingObjectNotificationBinding 資料類型&#40;ASSL&#41;](proactivecachingobjectnotificationbinding-data-type-assl.md)|定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料來源變更，在指定的資料表和檢視表或資料表和檢視透過現有資料繫結所識別的項目需要重建快取。|  
|[ProactiveCachingQueryBinding 資料類型&#40;ASSL&#41;](querybinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料表和檢視，識別執行指定之查詢所需要重建快取中的資料來源變更的項目。|  
|[ProactiveCachingTablesBinding 資料類型&#40;ASSL&#41;](proactivecachingtablesbinding-data-type-assl.md)|定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關指定之資料表和檢視表需要重建快取中的資料來源變更的項目。|  
|[PushedDataSource 資料類型&#40;ASSL&#41;](pusheddatasource-data-type-assl.md)|定義代表資料來源的基本資料類型 (例如[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]封裝) 用於 「 推送 」 資料載入[Cube](../objects/cube-element-assl.md)項目。|  
|[QueryBinding 資料類型&#40;ASSL&#41;](querybinding-data-type-assl.md)|定義衍生的資料類型表示的關聯[DataSource](../objects/datasource-element-assl.md)項目[QueryDefinition](../properties/querydefinition-element-assl.md)項目。|  
|[ReferenceMeasureGroupDimension 資料類型&#40;ASSL&#41;](referencemeasuregroupdimension-data-type-assl.md)|定義代表透過中繼維度與事實資料表間接相關之維度的衍生資料類型  (例如，Sales 量值群組可以參考透過 Customer 維度相關的 Geography 維度)。|  
|[RegularMeasureGroupDimension 資料類型&#40;ASSL&#41;](regularmeasuregroupdimension-data-type-assl.md)|定義代表維度與量值群組之間一般關聯性的衍生資料類型。|  
|[RelationalDataSource 資料類型&#40;ASSL&#41;](relationaldatasource-data-type-assl.md)|定義衍生的資料類型，表示[DataSource](../objects/datasource-element-assl.md)關聯式資料來源為基礎的項目。|  
|[ReportAction 資料類型&#40;ASSL&#41;](reportaction-data-type-assl.md)|定義代表產生 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表之動作的衍生資料類型。|  
|[RowBinding 資料類型&#40;ASSL&#41;](rowbinding-data-type-assl.md)|定義代表資料表中的資料列繫結的衍生的資料類型[DataSourceView](../objects/datasourceview-element-assl.md)項目。|  
|[ScalarMiningStructureColumn 資料類型&#40;ASSL&#41;](scalarminingstructurecolumn-data-type-assl.md)|定義衍生的資料類型，表示[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)包含純量值，而不是巢狀資料表與相關聯的項目[TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)項目包含巢狀的資料表。|  
|[StandardAction 資料類型&#40;ASSL&#41;](standardaction-data-type-assl.md)|定義代表任何的衍生的資料類型[動作](../objects/action-element-assl.md)以外的項目[DrillThroughAction](drillthroughaction-data-type-assl.md)項目或有[ReportAction](reportaction-data-type-assl.md)項目。|  
|[TableBinding 資料類型&#40;ASSL&#41;](tablebinding-data-type-assl.md)|定義代表資料表之繫結的衍生資料類型。|  
|[TableMiningStructureColumn 資料類型&#40;ASSL&#41;](tableminingstructurecolumn-data-type-assl.md)|定義衍生的資料類型，表示[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)包含巢狀的資料表，而不是與相關聯的純量值的項目[ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md)項目包含純量值。|  
|[TabularBinding 資料類型&#40;ASSL&#41;](tabularbinding-data-type-assl.md)|定義代表表格式項目 (例如資料表或 Cube 維度) 之繫結的抽象衍生資料類型。|  
|[TimeAttributeBinding 資料類型&#40;ASSL&#41;](timebinding-data-type-assl.md)|定義衍生資料類型，它代表在伺服器時間維度中產生之資料項目 (例如屬性的索引鍵資料行) 的「預留位置」繫結。|  
|[TimeBinding 資料類型&#40;ASSL&#41;](timebinding-data-type-assl.md)|定義代表時間週期之繫結的衍生資料類型。|  
|[Translation 資料類型&#40;ASSL&#41;](translation-data-type-assl.md)|定義代表當地語系化翻譯的基本資料類型。|  
|[UserDefinedGroupBinding 資料類型&#40;ASSL&#41;](userdefinedgroupbinding-data-type-assl.md)|定義代表某個屬性之使用者定義群組的衍生資料類型。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 元素階層&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
