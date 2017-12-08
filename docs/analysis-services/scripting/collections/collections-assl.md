---
title: "集合 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68be246ab77c93a910a4d37b40808a42adecb8ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="collections-assl"></a>集合 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做集合之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，從開發人員的觀點來看，這一節所述的元素會對應至物件的集合，例如**維度**和**Cube**集合。  
  
 大部分元素的集合物件，在其中複數名詞會指定集合的集合 (如需範例， **Cube**)，而且集合包含單數形式之相同名詞所指定的項目 (例如， **Cube**)。  
  
 在某些情況中，此結構描述不會遵守這個一般規則。 例如， **ClassifiedColumns**集合包含**ClassifiedColumnID**項目。  
  
 在其他情況中，集合會包含對應至物件屬性而非物件本身的元素。 例如，**別名**集合包含**別名**屬性，其中每一個都是簡單字串值。  
  
|元素|Description|  
|-------------|-----------------|  
|[Accounts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)|包含集合中所定義的帳戶類型[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[Actions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)|包含的動作集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[AggregationDesigns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|包含可在資料庫中多個資料分割之間共用之彙總設計的集合。|  
|[AggregationInstances 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|包含集合中所定義的彙總執行個體[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目。|  
|[Aggregations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)|包含定義的彙總集合[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)項目。|  
|[AlgorithmParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|包含所使用之演算法的參數集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[Aliases 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aliases-element-assl.md)|包含集合[別名](../../../analysis-services/scripting/properties/alias-element-assl.md)與相關聯的項目[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)項目|  
|[AllMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)|包含集合[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)元素之 All 成員標題[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。|  
|[Annotations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/annotations-element-assl.md)|包含集合[註解](../../../analysis-services/scripting/objects/annotation-element-assl.md)元素與父元素相關聯。|  
|[Assemblies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)|包含集合[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)與相關聯的項目[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目或[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[AttributeAllMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)|包含維度之 All 成員標題的翻譯集合。|  
|[AttributePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|包含的個別屬性權限集合[角色](../../../analysis-services/scripting/objects/role-element-assl.md)之特定維度上的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[AttributeRelationships 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|包含集合[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)屬性的項目。|  
|[Attributes 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)|包含相關聯維度之屬性的集合。|  
|[Blocks 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)|包含代表的二進位內容的二進位資料區塊集合[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。|  
|[CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|包含集合[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)與相關聯的項目[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)項目。|  
|[Calculations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculations-element-assl.md)|包含集合[PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)與相關聯的項目[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[CellPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|包含在相關聯的資料格權限集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[ClassifiedColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)|包含相關的資料行所分類的集合[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)項目。|  
|[Columns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)|包含與父元素相關聯之資料行的集合。|  
|[Commands 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)|包含與 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 元素相關聯之 [Command](../../../analysis-services/scripting/objects/command-element-assl.md) 元素的集合。|  
|[CubePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|包含適用於權限集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[Cubes 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cubes-element-assl.md)|包含集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)與相關聯的項目[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[DatabasePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|包含集合[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)與相關聯的項目[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[Databases 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/databases-element-assl.md)|包含集合[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)與相關聯的項目[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。|  
|[DataSources 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasources-element-assl.md)|包含集合[DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)與相關聯的項目[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)資料型別。|  
|[DataSourcePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|包含集合[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)與相關聯的項目[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[DataSourceViews 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasourceviews-element-assl.md)|包含集合[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)與相關聯的項目[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[DimensionPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|包含適用於權限集合[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)項目或[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)項目。|  
|[Dimensions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/dimensions-element-assl.md)|包含與父元素相關聯之維度的集合。|  
|[Events 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)|定義要擷取的事件項目集合[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)。|  
|[Files 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)|包含集合[檔案](../../../analysis-services/scripting/objects/file-element-assl.md)構成項目[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)項目。|  
|[ForeignKeyColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/foreignkeycolumns-element-assl.md)|包含可識別關聯式資料來源父資料表之聯結的資料行集合。|  
|[Groups 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/groups-element-assl.md)|包含繫結至屬性之成員群組的集合。|  
|[Hierarchies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|包含集合[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素與父元素相關聯。|  
|[IncrementalProcessingNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/incrementalprocessingnotifications-element-assl.md)|包含集合[IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)項目提供資訊給[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷的進度所執行的查詢項目累加式處理。|  
|[KeyColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|包含集合[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)元素定義的父物件。|  
|[Kpis 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/kpis-element-assl.md)|包含集合[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)元素與父元素相關聯。|  
|[Levels 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/levels-element-assl.md)|包含集合[層級](../../../analysis-services/scripting/objects/level-element-assl.md)中的項目[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。|  
|[MdxScripts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)|包含集合[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)與相關聯的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[MeasureGroups 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|包含集合[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素與父元素相關聯。|  
|[Measures 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/measures-element-assl.md)|包含集合[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)元素與父元素相關聯。|  
|[Members 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/members-element-assl.md)|包含集合[成員](../../../analysis-services/scripting/objects/member-element-assl.md)父元素的元素。|  
|[MiningModelPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|包含的權限集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[MiningModels 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|包含集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)與相關聯的項目[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)。|  
|[MiningStructurePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|包含權限的集合上[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。|  
|[MiningStructures 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|包含集合[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)中的項目[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[ModelingFlags 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)|包含集合[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)元素中的資料行的[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)。|  
|[NamingTemplateTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)|提供當地語系化翻譯的集合[NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)父元素之[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)。|  
|[Partitions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/partitions-element-assl.md)|包含集合[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)元素所使用[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)項目或組成的行外的資料分割繫結的集合[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)項目。|  
|[Perspectives 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|包含集合[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)與相關聯的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[QueryNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/querynotifications-element-assl.md)|包含集合[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)項目提供資訊給[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷資料來源是否已經修改所執行之查詢的項目。|  
|[ReportFormatParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|包含集合[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)元素[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)項目。|  
|[ReportParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|包含集合[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)元素[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)項目。|  
|[Roles 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/roles-element-assl.md)|包含在父元素底下定義之 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 元素的集合。|  
|[ServerProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|包含集合[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)與相關聯的項目[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。|  
|[TableNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/tablenotifications-element-assl.md)|包含集合[TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)提供之資訊的項目[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)資料表或檢視資料來源中的修改過的項目。|  
|[Traces 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)|包含與 [Server](../../../analysis-services/scripting/objects/server-element-assl.md) 元素相關聯之 [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) 元素的集合。|  
|[Translations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/translations-element-assl.md)|包含集合[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)元素與父元素相關聯。|  
|[UnknownMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|包含標題的翻譯集合[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)維度的項目。|  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 指令碼語言 XML 元素階層 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
