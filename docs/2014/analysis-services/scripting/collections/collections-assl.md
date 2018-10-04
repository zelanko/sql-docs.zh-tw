---
title: 集合 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f549a8d84f356b9315cdf3ec03ee41234e4dd0d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48199708"
---
# <a name="collections-assl"></a>集合 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做集合之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，但是從開發人員的觀點而言，本節中描述的元素會對應至物件的集合，例如 `Dimensions` 和 `Cubes` 集合。  
  
 集合大部分是物件元素的集合，其中複數名詞會指定集合 (例如，`Cubes`)，而且集合包含單數形式之相同名詞所指定的元素 (例如，`Cube`)。  
  
 在某些情況中，此結構描述不會遵守這個一般規則。 例如，`ClassifiedColumns` 集合包含 `ClassifiedColumnID` 元素。  
  
 在其他情況中，集合會包含對應至物件屬性而非物件本身的元素。 例如，`Aliases` 集合便包含 `Alias` 屬性，其中每個屬性都是單一字串值。  
  
|元素|描述|  
|-------------|-----------------|  
|[帳戶項目&#40;ASSL&#41;](accounts-element-assl.md)|包含帳戶類型中所定義的集合[資料庫](../objects/database-element-assl.md)項目。|  
|[動作項目&#40;ASSL&#41;](actions-element-assl.md)|包含動作的集合[Cube](../objects/cube-element-assl.md)或是[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[AggregationDesigns 元素&#40;ASSL&#41;](aggregationdesigns-element-assl.md)|包含可在資料庫中多個資料分割之間共用之彙總設計的集合。|  
|[AggregationInstances 元素&#40;ASSL&#41;](aggregationinstances-element-assl.md)|包含彙總執行個體中所定義的集合[分割區](../objects/partition-element-assl.md)項目。|  
|[Aggregations 元素&#40;ASSL&#41;](aggregations-element-assl.md)|包含定義的彙總的集合[AggregationDesign](../objects/aggregationdesign-element-assl.md)項目。|  
|[AlgorithmParameters 元素&#40;ASSL&#41;](algorithmparameters-element-assl.md)|包含所使用之演算法參數的集合[MiningModel](../objects/miningmodel-element-assl.md)項目。|  
|[Aliases 元素&#40;ASSL&#41;](aliases-element-assl.md)|包含的集合[別名](../properties/alias-element-assl.md)相關聯的項目[帳戶](../objects/account-element-assl.md)項目|  
|[AllMemberTranslations 元素&#40;ASSL&#41;](translations-element-assl.md)|包含的集合[翻譯](../objects/translation-element-assl.md)元素之 All 成員標題[階層](../objects/hierarchy-element-assl.md)項目。|  
|[Annotations 元素&#40;ASSL&#41;](annotations-element-assl.md)|包含的集合[註釋](../objects/annotation-element-assl.md)元素與父元素相關聯。|  
|[Assemblies 元素&#40;ASSL&#41;](assemblies-element-assl.md)|包含的集合[組件](../objects/assembly-element-assl.md)相關聯的項目[伺服器](../objects/server-element-assl.md)項目或有[資料庫](../objects/database-element-assl.md)項目。|  
|[AttributeAllMemberTranslations 元素&#40;ASSL&#41;](attributeallmembertranslations-element-assl.md)|包含維度之 All 成員標題的翻譯集合。|  
|[AttributePermissions 元素&#40;ASSL&#41;](attributepermissions-element-assl.md)|包含個別的屬性權限的集合[角色](../objects/role-element-assl.md)特定維度上的項目[Cube](../objects/cube-element-assl.md)項目。|  
|[AttributeRelationships 元素&#40;ASSL&#41;](relationships-element-assl.md)|包含的集合[AttributeRelationship](../objects/attributerelationship-element-assl.md)屬性的項目。|  
|[Attributes 項目&#40;ASSL&#41;](attributes-element-assl.md)|包含相關聯維度之屬性的集合。|  
|[封鎖項目&#40;ASSL&#41;](blocks-element-assl.md)|包含的二進位表示的二進位內容的資料區塊集合[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)項目。|  
|[CalculationProperties 元素&#40;ASSL&#41;](calculationproperties-element-assl.md)|包含的集合[CalculationProperty](../objects/calculationproperty-element-assl.md)相關聯的項目[MdxScript](../objects/mdxscript-element-assl.md)項目。|  
|[Calculations 元素&#40;ASSL&#41;](calculations-element-assl.md)|包含的集合[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)相關聯的項目[觀點來看](../objects/perspective-element-assl.md)項目。|  
|[CellPermissions 元素&#40;ASSL&#41;](cellpermissions-element-assl.md)|包含在相關聯的資料格權限的集合[Cube](../objects/cube-element-assl.md)項目。|  
|[ClassifiedColumns 元素&#40;ASSL&#41;](columns-element-assl.md)|包含相關的資料行所分類的集合[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)項目。|  
|[資料行的項目&#40;ASSL&#41;](columns-element-assl.md)|包含與父元素相關聯之資料行的集合。|  
|[命令項目&#40;ASSL&#41;](commands-element-assl.md)|包含與 [MdxScript](../objects/mdxscript-element-assl.md) 元素相關聯之 [Command](../objects/command-element-assl.md) 元素的集合。|  
|[CubePermissions 元素&#40;ASSL&#41;](cubepermissions-element-assl.md)|包含適用於權限的集合[Cube](../objects/cube-element-assl.md)項目。|  
|[Cube 元素&#40;ASSL&#41;](cubes-element-assl.md)|包含的集合[Cube](../objects/cube-element-assl.md)相關聯的項目[資料庫](../objects/database-element-assl.md)項目。|  
|[DatabasePermissions 元素&#40;ASSL&#41;](databasepermissions-element-assl.md)|包含的集合[DatabasePermission](../objects/databasepermission-element-assl.md)相關聯的項目[資料庫](../objects/database-element-assl.md)項目。|  
|[資料庫項目&#40;ASSL&#41;](databases-element-assl.md)|包含的集合[資料庫](../objects/database-element-assl.md)相關聯的項目[Server](../objects/server-element-assl.md)項目。|  
|[DataSources 元素&#40;ASSL&#41;](datasources-element-assl.md)|包含的集合[DataSourcePermission](../objects/datasourcepermission-element-assl.md)相關聯的項目[DataSource](../data-type/datasource-data-type-assl.md)資料型別。|  
|[DataSourcePermissions 元素&#40;ASSL&#41;](datasourcepermissions-element-assl.md)|包含的集合[DataSource](../objects/datasource-element-assl.md)相關聯的項目[資料庫](../objects/database-element-assl.md)項目。|  
|[DataSourceViews 元素&#40;ASSL&#41;](datasourceviews-element-assl.md)|包含的集合[DataSourceView](../objects/datasourceview-element-assl.md)相關聯的項目[資料庫](../objects/database-element-assl.md)項目。|  
|[DimensionPermissions 元素&#40;ASSL&#41;](dimensionpermissions-element-assl.md)|包含適用於權限的集合[維度](../objects/dimension-element-assl.md)項目或有[CubePermission](../objects/cubepermission-element-assl.md)項目。|  
|[Dimensions 元素&#40;ASSL&#41;](dimensions-element-assl.md)|包含與父元素相關聯之維度的集合。|  
|[Events 元素&#40;ASSL&#41;](events-element-assl.md)|定義所要擷取的事件項目的集合[追蹤](../objects/trace-element-assl.md)。|  
|[檔案項目&#40;ASSL&#41;](files-element-assl.md)|包含的集合[檔案](../objects/file-element-assl.md)構成項目[ClrAssembly](../data-type/assembly-data-type-assl.md)項目。|  
|[ForeignKeyColumns 元素&#40;ASSL&#41;](keycolumns-element-assl.md)|包含可識別關聯式資料來源父資料表之聯結的資料行集合。|  
|[群組項目&#40;ASSL&#41;](groups-element-assl.md)|包含繫結至屬性之成員群組的集合。|  
|[Hierarchies 元素&#40;ASSL&#41;](hierarchies-element-assl.md)|包含的集合[階層](../objects/hierarchy-element-assl.md)元素與父元素相關聯。|  
|[IncrementalProcessingNotifications 元素&#40;ASSL&#41;](incrementalprocessingnotifications-element-assl.md)|包含的集合[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)項目提供資訊給[ProactiveCaching](../objects/proactivecaching-element-assl.md)判斷的進度所執行之查詢的項目累加式處理。|  
|[KeyColumns 元素&#40;ASSL&#41;](keycolumns-element-assl.md)|包含的集合[KeyColumn](../objects/column-element-assl.md)元素定義的父物件。|  
|[Kpis 元素&#40;ASSL&#41;](kpis-element-assl.md)|包含的集合[Kpi](../objects/kpi-element-assl.md)元素與父元素相關聯。|  
|[層級項目&#40;ASSL&#41;](levels-element-assl.md)|包含的集合[層級](../objects/level-element-assl.md)中的項目[階層](../objects/hierarchy-element-assl.md)項目。|  
|[MdxScripts 元素&#40;ASSL&#41;](mdxscripts-element-assl.md)|包含的集合[MdxScript](../objects/mdxscript-element-assl.md)相關聯的項目[Cube](../objects/cube-element-assl.md)項目。|  
|[MeasureGroups 元素&#40;ASSL&#41;](measuregroups-element-assl.md)|包含的集合[MeasureGroup](../objects/group-element-assl.md)元素與父元素相關聯。|  
|[測量項目&#40;ASSL&#41;](measures-element-assl.md)|包含的集合[量值](../objects/measure-element-assl.md)元素與父元素相關聯。|  
|[Members 元素&#40;ASSL&#41;](members-element-assl.md)|包含的集合[成員](../objects/member-element-assl.md)父項目的項目。|  
|[MiningModelPermissions 元素&#40;ASSL&#41;](miningmodelpermissions-element-assl.md)|包含的權限集合[MiningModel](../objects/miningmodel-element-assl.md)項目。|  
|[MiningModels 元素&#40;ASSL&#41;](miningmodels-element-assl.md)|包含的集合[MiningModel](../objects/miningmodel-element-assl.md)相關聯的項目[MiningStructure](../objects/miningstructure-element-assl.md)。|  
|[MiningStructurePermissions 元素&#40;ASSL&#41;](miningstructurepermissions-element-assl.md)|包含權限的集合上[MiningStructure](../objects/miningstructure-element-assl.md)項目。|  
|[MiningStructures 元素&#40;ASSL&#41;](miningstructures-element-assl.md)|包含的集合[MiningStructure](../objects/miningstructure-element-assl.md)中的項目[資料庫](../objects/database-element-assl.md)項目。|  
|[ModelingFlags 元素&#40;ASSL&#41;](modelingflags-element-assl.md)|包含的集合[ModelingFlag](../objects/modelingflag-element-assl.md)中的資料行的項目[MiningStructure](../objects/miningstructure-element-assl.md)或是[MiningModel](../objects/miningmodel-element-assl.md)。|  
|[NamingTemplateTranslations 元素&#40;ASSL&#41;](namingtemplatetranslations-element-assl.md)|提供當地語系化翻譯的集合[NamingTemplate](../properties/namingtemplate-element-assl.md)項目之父代[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)。|  
|[分割項目&#40;ASSL&#41;](partitions-element-assl.md)|包含的集合[資料分割](../objects/partition-element-assl.md)所使用的項目[MeasureGroup](../objects/group-element-assl.md)項目或組成的列外的資料分割繫結的集合[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)項目。|  
|[Perspectives 元素&#40;ASSL&#41;](perspectives-element-assl.md)|包含的集合[觀點來看](../objects/perspective-element-assl.md)相關聯的項目[Cube](../objects/cube-element-assl.md)項目。|  
|[QueryNotifications 元素&#40;ASSL&#41;](querynotifications-element-assl.md)|包含的集合[QueryNotification](../objects/querynotification-element-assl.md)項目提供資訊給[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關判斷資料來源是否已經修改所執行之查詢的項目。|  
|[ReportFormatParameters 元素&#40;ASSL&#41;](reportformatparameters-element-assl.md)|包含的集合[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)項目[ReportAction](../data-type/action-data-type-assl.md)項目。|  
|[ReportParameters 元素&#40;ASSL&#41;](reportparameters-element-assl.md)|包含的集合[ReportParameter](../objects/reportparameter-element-assl.md)項目[ReportAction](../data-type/action-data-type-assl.md)項目。|  
|[Roles 元素&#40;ASSL&#41;](roles-element-assl.md)|包含在父元素底下定義之 [Role](../objects/role-element-assl.md) 元素的集合。|  
|[ServerProperties 元素&#40;ASSL&#41;](serverproperties-element-assl.md)|包含的集合[ServerProperty](../objects/serverproperty-element-assl.md)相關聯的項目[Server](../objects/server-element-assl.md)項目。|  
|[TableNotifications 元素&#40;ASSL&#41;](tablenotifications-element-assl.md)|包含的集合[TableNotification](../objects/tablenotification-element-assl.md)提供資訊的項目[ProactiveCaching](../objects/proactivecaching-element-assl.md)之資料表或檢視資料來源中的修改過的項目。|  
|[追蹤項目&#40;ASSL&#41;](traces-element-assl.md)|包含與 [Server](../objects/server-element-assl.md) 元素相關聯之 [Trace](../objects/trace-element-assl.md) 元素的集合。|  
|[Translations 元素&#40;ASSL&#41;](translations-element-assl.md)|包含的集合[翻譯](../objects/translation-element-assl.md)元素與父元素相關聯。|  
|[UnknownMemberTranslations 元素&#40;ASSL&#41;](unknownmembertranslations-element-assl.md)|包含標題的翻譯集合[UnknownMember](../properties/unknownmember-element-assl.md)維度的項目。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 元素階層&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
