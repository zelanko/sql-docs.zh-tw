---
title: "屬性 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fee88a17655823ed00bbcb864dabcf1980663724
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="properties-assl"></a>屬性 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做物件屬性之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，但是從開發人員的觀點而言，本節中描述的元素會對應至描述物件的屬性。  
  
 屬性是 ASSL 結構描述中的分葉層級元素，而且沒有對應至本身屬性的子元素和元素。  
  
 在少數情況下，結構描述中可能會顯示成屬性的分葉層級元素會分類成物件，因為元素的類型是物件類型。 例如，**來源**的**維度**物件屬於類型**DimensionBinding**。  
  
## <a name="in-this-section"></a>本節內容  
  
|元素|Description|  
|-------------|-----------------|  
|[Access 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/access-element-assl.md)|表示層級的存取權提供給[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)項目。|  
|[Account 元素 &#40; ImpersonationInfo &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md)|包含的使用者帳戶名稱[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)資料型別。|  
|[AccountType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)|包含名稱中所定義之帳戶類型的[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[ActionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/actionid-element-assl.md)|包含名稱的[動作](../../../analysis-services/scripting/objects/action-element-assl.md)上定義的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)元素可在其[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目做為[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)項目。|  
|[管理項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/administer-element-assl.md)|指出相關聯的權限是否包含管理權**資料庫**項目。|  
|[AggregateFunction 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)|定義所使用的彙總函式的型別[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)項目。|  
|[AggregationDesignID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)|識別[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素相關聯[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目。|  
|[AggregationFunction 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md)|包含要用於帳戶類型的彙總函式。|  
|[AggregationID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationid-element-assl.md)|識別彙總定義**AggregationDesign**用來建立彙總執行個體的項目。|  
|[AggregationInstanceSource 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)|識別的使用者定義彙總執行個體繫結至資料來源**分割**項目。|  
|[AggregationPrefix 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)|定義要在整個相關聯父元素中用於彙總名稱的一般前置詞。|  
|[AggregationStorage 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md)|識別彙總的儲存方法。|  
|[AggregationType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md)|定義所儲存的彙總類型**分割**項目。|  
|[AggregationUsage 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)|控制項如何在彙總設計師[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]設計彙總。|  
|[Algorithm 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)|定義所使用的演算法[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[Alias 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/alias-element-assl.md)|定義的別名[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)項目。|  
|[AllMemberAggregationUsage 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md)|控制 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的彙總設計師如何設計彙總。|  
|[AllMemberName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allmembername-element-assl.md)|包含的所有成員的預設語言的標題[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。|  
|[AllowBrowsing 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md)|定義是否屬於[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素擁有瀏覽權限**MiningModel**項目。|  
|[AllowDrillThrough 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|決定是否允許針對父元素進行鑽研。|  
|[AllowDuplicateNames 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allowduplicatenames-element-assl.md)|決定是否允許重複的名稱，以在**階層**項目。|  
|[AllowedSet 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allowedset-element-assl.md)|包含定義允許權限集集合運算式**角色**屬性上的項目。|  
|[應用程式項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/application-element-assl.md)|識別應用程式相關聯**動作**項目。|  
|[AssociatedMeasureGroupID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)|包含的識別碼 (ID) [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素相關聯[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)項目或[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)項目。|  
|[AttributeAllMemberName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md)|包含維度之 All 成員的標題，而這個標題會以預設語言顯示。|  
|[AttributeHierarchyDisplayFolder 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md)|識別要在其中顯示相關聯屬性階層的資料夾。|  
|[AttributeHierarchyEnabled 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)|決定是否針對此屬性啟用屬性階層。|  
|[AttributeHierarchyOptimizedState 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)|決定套用至屬性階層的最佳化層級。|  
|[AttributeHierarchyOrdered 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md)|決定是否排序相關聯的屬性階層。|  
|[AttributeHierarchyVisible 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)|決定用戶端應用程式是否可看到屬性階層。|  
|[AttributeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|包含與父元素相關聯之屬性的識別碼。|  
|[Audit 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/audit-element-assl.md)|指定[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)元素無法卸除任何事件，即使這樣造成伺服器效能降低。|  
|[AutoRestart 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/autorestart-element-assl.md)|決定是否**追蹤**項目應該自動重新啟動[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服務停止並重新啟動。|  
|[BackColor 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/backcolor-element-assl.md)|描述父元素的色彩相關顯示特性。|  
|[CacheMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/cachemode-element-assl.md)|決定用於培訓在處理採礦結構時擷取之資料的快取機制。|  
|[CalculationReference 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/calculationreference-element-assl.md)|包含命名的集或導出資料格所參考的名稱**CalculationProperty**項目。|  
|[CalculationType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)|描述中相關聯定義的計算類型**CalculationProperty**項目。|  
|[CalendarEndDate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/calendarenddate-element-assl.md)|定義的之日曆週期的結束日期[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)項目。|  
|[CalendarLanguage 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/calendarlanguage-element-assl.md)|定義所使用的日曆語言**TimeBinding**項目。|  
|[CalendarStartDate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/calendarstartdate-element-assl.md)|定義的之日曆週期的開始日期**TimeBinding**項目。|  
|[Caption 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/caption-element-assl.md)|包含相關聯父元素的標題。|  
|[CaptionIsMdx 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/captionismdx-element-assl.md)|定義是否的標題**動作**項目是多維度運算式 (MDX) 運算式。|  
|[Cardinality 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/cardinality-element-assl.md)|表示所描述之關聯性基數[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)或[RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)。|  
|[CaseCubeDimensionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/casecubedimensionid-element-assl.md)|包含將資料採礦維度關聯至量值群組之 Cube 維度的識別碼。|  
|[ClassifiedColumnID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/classifiedcolumnid-element-assl.md)|包含所分類之相關資料行的識別碼[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)項目。|  
|[Collation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/collation-element-assl.md)|決定父元素所使用的定序。|  
|[ColumnID 元素 &#40;ColumnBinding &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/columnid-element-columnbinding-assl.md)|包含資料表中資料項目所繫結之資料行的識別碼。|  
|[ColumnID 元素 &#40;EventColumn &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|包含要做為的一部分，針對某個事件擷取資訊的資料行的識別碼**追蹤**項目。|  
|[Condition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/condition-element-assl.md)|包含 MDX 運算式以判斷是否**動作**父項目套用至目標。|  
|[ConnectionString 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/connectionstring-element-assl.md)|包含加密的連接字串[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)項目。|  
|[ConnectionStringSecurity 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md)|指定是否要針對安全性目的從資料來源連接字串中移除使用者密碼。|  
|[內容項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/content-element-assl.md)|說明內容中的資料行的[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。|  
|[CreatedTimestamp 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)|包含父元素的唯讀建立時間戳記。|  
|[CubeDimensionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|識別[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)與父元素相關聯的項目。|  
|[CubeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/cubeid-element-assl.md)|識別**Cube**元素相關聯[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)項目。|  
|[CurrentStorageMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)|決定父元素的目前儲存模式。|  
|[CurrentTimeMember 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/currenttimemember-element-assl.md)|定義的時間維度相關聯的目前成員**Kpi**項目。|  
|[DataAggregation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/dataaggregation-element-assl.md)|決定執行個體是否可彙總保存的資料或快取的資料**MeasureGroup**。|  
|[DatabaseID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/databaseid-element-assl.md)|識別**資料庫**元素相關聯的行外**繫結**項目。|  
|[DataSize 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasize-element-assl.md)|包含以位元組為單位的大小[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)項目。|  
|[DataSourceID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)|識別**DataSource**與父元素相關聯的項目。|  
|[DataSourceImpersonationInfo 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)|包含用來連接到資料來源時，決定模擬行為的資訊**資料庫**項目。|  
|[DataSourceViewID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md)|識別[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)元素相關聯**繫結**父項目。|  
|[DataType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datatype-element-assl.md)|定義相關聯元素的資料類型。|  
|[DbSchemaName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md)|包含父元素所識別之資料表中所使用的結構描述名稱[DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)項目。|  
|[DbTableName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|包含父元素所繫結之資料表的名稱。|  
|[預設項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/default-element-assl.md)|決定是否**DrillThroughAction**為預設鑽研動作。|  
|[DefaultMeasure 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)|包含定義的預設量值的 MDX 語言運算式**Cube**或**觀點來看**項目。|  
|[DefaultMember 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)|包含可識別父元素之預設成員的 MDX 運算式。|  
|[DefaultScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/defaultscript-element-assl.md)|識別預設[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)中的項目[MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)集合。|  
|[DefaultValue 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/defaultvalue-element-assl.md)|包含相關聯的唯讀預設值[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)項目。|  
|[DeniedSet 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/deniedset-element-assl.md)|包含定義在相關聯屬性上遭拒之權限清單的集合運算式。|  
|[DependsOnDimensionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md)|包含父維度所相依之其他維度的識別碼。|  
|[Description 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/description-element-assl.md)|包含父元素的描述。|  
|[DimensionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)|包含維度的識別碼。|  
|[DiscretizationBucketCount 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)|包含要進行離散化的值區數目。|  
|[DiscretizationMethod 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)|定義用於進行離散化的方法。|  
|[DisplayFlag 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/displayflag-element-assl.md)|包含指出使用者介面元件是否應該顯示相關聯的唯讀提示**ServerProperty**項目。|  
|[DisplayFolder 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)|指定要在其中列出父元素的資料夾。 開發人員和系統管理員的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 應用程式可能會支援使用顯示資料夾以視覺化方式分類多個元素。|  
|[Distribution 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/distribution-element-assl.md)|包含描述純量值如何提供者特定值的資料行內部散發**MiningStructure**項目。|  
|[Edition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/edition-element-assl.md)|包含執行個體的唯讀版本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。|  
|[Enabled 的元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/enabled-element-assl.md)|指出是否已啟用父元素。|  
|[EndOfData 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/endofdata-element-assl.md)|表示從收到的資料結尾[PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)項目。|  
|[EstimatedCount 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)|包含屬性之成員的估計數目。|  
|[EstimatedPerformanceGain 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md)|包含資料分割之估計效能改善的唯讀百分比。|  
|[EstimatedRows 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)|包含父元素所代表之估計的資料列數目。|  
|[EstimatedSize 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md)|包含父元素的維度估計大小 (以位元組為單位)。|  
|[EventID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/eventid-element-assl.md)|可唯一識別[事件](../../../analysis-services/scripting/objects/event-element-assl.md)要擷取的一部分的項目**追蹤**項目。|  
|[Expression 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/expression-element-assl.md)|包含定義父元素之內容的 MDX 運算式。|  
|[篩選條件項目 &#40;繫結 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/filter-element-binding-assl.md)|包含篩選父元素之內容的 MDX 運算式。|  
|[篩選條件項目 &#40;追蹤 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)|包含描述的 XML 文件片段**追蹤**篩選器。|  
|[FirstDayOfWeek 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/firstdayofweek-element-assl.md)|定義之當週的第一天**TimeBinding**項目。|  
|[FiscalFirstDayOfMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fiscalfirstdayofmonth-element-assl.md)|定義之會計月份的第一天**TimeBinding**項目。|  
|[FiscalFirstMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fiscalfirstmonth-element-assl.md)|定義之會計週期的第一個月**TimeBinding**項目。|  
|[FiscalYearName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fiscalyearname-element-assl.md)|定義用於會計年度名稱的命名慣例**TimeBinding**項目。|  
|[FontFlags 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fontflags-element-assl.md)|描述字型相關顯示特性**CalculationProperty**或**量值**父項目。|  
|[FontName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fontname-element-assl.md)|描述字型相關顯示特性**CalculationProperty**或**量值**父項目。|  
|[FontSize 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/fontsize-element-assl.md)|描述字型相關顯示特性**CalculationProperty**或**量值**父項目。|  
|[ForceRebuildInterval 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md)|決定多維度 OLAP (MOLAP) 影像處理無條件開始所經過的時間量 (從全新 MOLAP 影像可用開始計算)。|  
|[ForeColor 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/forecolor-element-assl.md)|描述的色彩相關顯示特性**CalculationProperty**或**量值**父項目。|  
|[Format 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/format-element-assl.md)|包含所需的格式**DataItem**項目。|  
|[FormatString 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/formatstring-element-assl.md)|說明的顯示格式**CalculationProperty**項目或**量值**項目。|  
|[Goal 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/goal-element-assl.md)|識別所需的目標中**Kpi**項目。|  
|[GranularityAttributeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/granularityattributeid-element-assl.md)|包含與父代相關聯之屬性的識別碼[MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)資料型別。|  
|[HideMemberIf 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/hidememberif-element-assl.md)|指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。|  
|[HierarchyID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)|包含識別碼[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)項目。|  
|[HierarchyUniqueNameStyle 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md)|決定如何唯一名稱的內所包含的階層產生**CubeDimension**。|  
|[ID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)|包含父元素的唯一識別碼。|  
|[IgnoreUnrelatedDimensions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/ignoreunrelateddimensions-element-assl.md)|決定當查詢中包含與量值群組不相關的維度成員時，是否將不相關的維度強制在其最上層。|  
|[ImpersonationInfo 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)|包含在存取或執行組件時，用來決定模擬行為的資訊。|  
|[ImpersonationInfoSecurity 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/impersonationinfosecurity-element-assl.md)|包含唯讀的值，指出是否已中提供的安全性認證進行任何變更**ImpersonationInfo**資料型別。|  
|[ImpersonationMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)|包含值，指出衍生自的元素的模擬方法**ImpersonationInfo**資料型別。|  
|[InstanceSelection 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/instanceselection-element-assl.md)|提供一個提示給用戶端應用程式，以便根據清單中的預期項目數目來建議應該如何顯示項目清單。|  
|[IntermediateCubeDimensionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/intermediatecubedimensionid-element-assl.md)|包含將參考維度關聯至量值群組之維度的識別碼。|  
|[IntermediateGranularityAttributeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/intermediategranularityattributeid-element-assl.md)|包含中繼 Cube 維度中用來將參考維度關聯至中繼維度之資料粒度屬性的識別碼。|  
|[InvalidXmlCharacters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md)|指定來源資料中無效 XML 字元的處理方法。|  
|[Invocation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/invocation-element-assl.md)|指定如何**動作**應叫用。|  
|[IsAggregatable 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md)|指定是否值[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)項目可以彙總。|  
|[IsKey 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/iskey-element-assl.md)|指出資料行是否提供的案例中的索引鍵**MiningStructure**項目。|  
|[Isolation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/isolation-element-assl.md)|表示衍生自元素的隔離層級[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)資料型別。|  
|[KeyDuplicate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md)|決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何處理在處理期間遇到的重複索引鍵錯誤。|  
|[KeyErrorAction 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md)|指定在索引鍵發生錯誤時要讓 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 採取的動作。|  
|[KeyErrorLimit 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)|包含處理期間可接受的錯誤數目。|  
|[KeyErrorLimitAction 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md)|指定的動作，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定的索引鍵錯誤計數時[KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)到達項目。|  
|[KeyErrorLogFile 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md)|包含記錄處理錯誤的檔案名稱。|  
|[KeyNotFound 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keynotfound-element-assl.md)|指定當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遇到參考完整性錯誤時如何回應。|  
|[KeyUniquenessGuarantee 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md)|指出屬性索引鍵與其名稱之間的關聯性以及相關屬性的關聯性是否保證有效。|  
|[KpiID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/kpiid-element-assl.md)|包含產生關聯的識別碼**Kpi**具有項目**觀點來看**項目。|  
|[語言項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/language-element-assl.md)|包含父元素的語言識別碼。|  
|[LastProcessed 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)|包含唯讀的時間戳記，指出上次處理包含父元素之資料庫的時間。|  
|[LastSchemaUpdate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)|包含父元素的唯讀中繼資料更新時間戳記。|  
|[LastUpdate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/lastupdate-element-assl.md)|包含唯讀時間時間戳記，指出上次相關聯**資料庫**或任何資料庫所包含的主要物件遭變更。|  
|[Latency 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/latency-element-assl.md)|定義最早通知與終結 MOLAP 影像之間的「寬限期」。|  
|[LogFileAppend 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/logfileappend-element-assl.md)|決定是否**追蹤**元素將其記錄輸出附加至現有的記錄檔，還是覆寫它。|  
|[LogFileName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/logfilename-element-assl.md)|包含的記錄檔的檔案名稱**追蹤**項目。|  
|[LogFileRollover 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md)|指定是否記錄**追蹤**輸出應該換用新檔案，或停止時的最大記錄檔大小應該指定[LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)為止。|  
|[LogFileSize 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)|指定最大記錄檔大小 (以 MB 為單位)。|  
|[ManagedProvider 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/managedprovider-element-assl.md)|包含衍生自項目所使用的 managed 提供者名稱**DataSource**資料型別。|  
|[ManufacturingExtraMonthQuarter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/manufacturingextramonthquarter-element-assl.md)|定義要指派延長月份的月份之製造週期**TimeBinding**項目。|  
|[ManufacturingFirstMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/manufacturingfirstmonth-element-assl.md)|定義的第一個製造月份**TimeBinding**項目。|  
|[ManufacturingFirstWeekOfMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/manufacturingfirstweekofmonth-element-assl.md)|定義之製造月份的第一週**TimeBinding**項目。|  
|[MasterDatasourceID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/masterdatasourceid-element-assl.md)|包含主要資料來源識別碼**資料庫**項目。|  
|[Materialization 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/materialization-element-assl.md)|指出量值群組與參考維度之間關聯性的類型。|  
|[MaxActiveConnections 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md)|包含衍生自項目所允許的同時連線數目上限**DataSource**資料型別。|  
|[MdxMissingMemberMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md)|決定如何處理 MDX 陳述式的遺漏成員。|  
|[MeasureExpression 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/measureexpression-element-assl.md)|包含定義量值的 MDX 運算式。|  
|[MeasureGroupID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md)|將**MeasureGroup**與父元素、 繫結或超出的非正規繫結。|  
|[MeasureID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/measureid-element-assl.md)|將**量值**元素與父元素。|  
|[MeasureQualificaton 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/measurequalificaton-element-assl.md)|決定前置詞是否會套用至中量值**MeasureGroup**。|  
|[MemberNamesUnique 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)|決定父元素底下的成員名稱是否必須是唯一的。|  
|[MemberUniqueNameStyle 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md)|決定如何唯一名稱內所包含的階層成員產生**CubeDimension**項目。|  
|[MembersWithData 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)|決定是否要在父屬性中顯示非分葉成員的資料成員。|  
|[MembersWithDataCaption 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)|提供範本字串，該字串會用來建立系統所產生之資料成員的標題。|  
|[MimeType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/mimetype-element-assl.md)|包含的多用途網際網路郵件延伸標準 (MIME) 類型，如果適用的話，父代所代表之資料的**DataItem**項目。|  
|[MiningModelID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md)|將採礦模型與資料採礦維度產生關聯。|  
|[Name 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)|包含父元素的名稱。|  
|[NamingTemplate 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)|定義從建構的父子式階層中如何命名層級**DimensionAttribute**父項目。|  
|[NonEmptyBehavior 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md)|決定父代相關聯的非空白行為**CalculationProperty**項目。|  
|[NotificationTechnique 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/notificationtechnique-element-assl.md)|指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部用戶端應用程式會處理通知。|  
|[NullKeyConvertedToUnknown 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)|指定遇到 Null 轉換錯誤時要採取的動作。|  
|[NullKeyNotAllowed 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 處理引擎如何處理在處理期間遇到的 Null 索引鍵錯誤。|  
|[NullProcessing 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)|定義 Null 值的處理方式。|  
|[OnlineMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/onlinemode-element-assl.md)|指定資料庫會在起始快取的重建作業時立即返回線上狀態，還是只有在快取的重建作業完成時才返回線上狀態。|  
|[OptimizedState 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)|決定套用至階層的最佳化層級。|  
|[Optionality 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/optionality-element-assl.md)|表示之成員的選擇性**AttributeRelationship**項目。|  
|[OrderBy 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/orderby-element-assl.md)|描述如何排序屬性中包含的成員。|  
|[OrderByAttributeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)|識別用來排序成員的另一個屬性[維度](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)屬性。|  
|[Ordinal 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/ordinal-element-assl.md)|指出索引鍵和翻譯等集合中要繫結的目標序號。|  
|[OverrideBehavior 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/overridebehavior-element-assl.md)|表示所描述之關聯性的覆寫行為**AttributeRelationship**項目。|  
|[PartitionID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/partitionid-element-assl.md)|將**分割**元素與父元素、 繫結或超出的非正規繫結。|  
|[Password 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/password-element-assl.md)|包含的使用者帳戶的密碼**ImpersonationInfo**項目。|  
|[路徑項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/path-element-assl.md)|包含所提供的執行個體的路徑， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，所使用之報表的[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)項目。|  
|[PendingValue 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/pendingvalue-element-assl.md)|包含的唯讀暫止值相關聯的**ServerProperty**項目。|  
|[PermissionSet 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|識別相關聯的權限集合[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。|  
|[Persistence 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)|決定繫結的來源資料中哪些部分是動態的而且會檢查是否有使用所指定的頻率更新[RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)項目。|  
|[Process 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/process-element-assl.md)|決定使用者是否可以處理父元素的擁有者。|  
|[ProcessingMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/processingmode-element-assl.md)|指出此執行個體應該在處理期間或處理之後進行索引和彙總。|  
|[ProcessingPriority 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)|決定背景作業期間父物件的處理優先權 (例如，延遲彙總、索引或叢集)。|  
|[ProcessingQuery 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/processingquery-element-assl.md)|包含要針對累加式處理狀態通知執行之查詢的參數化文字。|  
|[ProductName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/productname-element-assl.md)|包含執行個體的唯讀產品名稱[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]相關聯**伺服器**項目。|  
|[Query 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/query-element-assl.md)|包含要針對通知執行之查詢的文字。|  
|[QueryDefinition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/querydefinition-element-assl.md)|包含與相關聯之查詢的不透明運算式**DataSource**中的項目[QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)項目。|  
|[Read 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/read-element-assl.md)|判斷是否可讀取資料或中繼資料的指定[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)或[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)項目。|  
|[ReadDefinition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/readdefinition-element-assl.md)|決定成員是否可以讀取資料庫的定義或資料庫中物件的定義。|  
|[ReadSourceData 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/readsourcedata-element-assl.md)|決定如何唯一名稱的內所包含的階層產生**CubePermission**。|  
|[RefreshInterval 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)|指定重新整理與父元素相關聯之繫結資料的間隔。|  
|[RefreshPolicy 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)|決定多久維度或量值群組之動態部分 (依指定[持續性](../../../analysis-services/scripting/properties/persistence-element-assl.md)項目) 會檢查是否有變更。|  
|[RelationshipType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/relationshiptype-element-assl.md)|指出是否成員關聯性**AttributeRelationship**可以變更。|  
|[RemoteDatasourceID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)|指定指向儲存遠端資料分割之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的 OLAP 資料來源的識別碼。|  
|[ReportingFirstMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/reportingfirstmonth-element-assl.md)|定義的第一個報表月份**TimeBinding**項目。|  
|[ReportingFirstWeekOfMonth 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/reportingfirstweekofmonth-element-assl.md)|定義之報表月份的第一週**TimeBinding**項目。|  
|[ReportingWeekToMonthPattern 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/reportingweektomonthpattern-element-assl.md)|定義的報表週至月份模式**TimeBinding**項目。|  
|[ReportServer 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|包含名稱的[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]所使用的執行個體**ReportAction**。|  
|[RequiresRestart 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/requiresrestart-element-assl.md)|包含相關聯的唯讀值**ServerProperty**項目可決定是否變更伺服器屬性的值需要執行個體，重新啟動，變更才會生效。|  
|[RoleID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/roleid-element-assl.md)|識別要定義權限的角色。|  
|[根項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/root-element-assl.md)|包含資料來源的資料 (資料列集)。|  
|[RootMemberIf 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md)|決定如何識別父屬性的根成員。|  
|[Schema 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/schema-element-assl.md)|包含資料來源檢視的結構描述。|  
|[ScriptCacheProcessingMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md)|指出伺服器應該在處理期間或處理之後建立指令碼快取。|  
|[SilenceInterval 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md)|定義在啟動 MOLAP 影像處理處理序之前，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體暫停的最小時間量。|  
|[SilenceOverrideInterval 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md)|定義在收到初始通知之後和 MOLAP 影像處理無條件開始之前必須經過的時間量。|  
|[Slice 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/slice-element-assl.md)|包含定義資料分割中包含之配量的 MDX 運算式。|  
|[SolveOrder 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/solveorder-element-assl.md)|指出求解順序**CalculationProperty**元素套用至導出的成員或導出資料格定義。|  
|[Source 元素 &#40;繫結 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|識別父元素所繫結的資料來源。|  
|[Source 元素 &#40;ComAssembly &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|包含元件物件模型 (COM) 元件的檔案名稱或程式設計識別碼 (ProgID)。|  
|[Source 元素 &#40;量值 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/source-element-measure-assl.md)|包含詳細資料包含的值之來源的**量值**項目。|  
|[SourceAttributeID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/sourceattributeid-element-assl.md)|包含在其上之來源屬性識別碼[層級](../../../analysis-services/scripting/objects/level-element-assl.md)項目為基礎。|  
|[SourceColumnID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/sourcecolumnid-element-assl.md)|包含 ID 的來源採礦結構資料行中的上階**MiningStructure**項目。|  
|[State 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/state-element-assl.md)|包含描述父元素之目前處理狀態的唯讀值。|  
|[Status 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/status-element-assl.md)|包含傳回之狀態指標的 MDX 運算式**Kpi**項目。|  
|[StatusGraphic 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/statusgraphic-element-assl.md)|包含狀態的建議圖形表示**Kpi**項目。|  
|[StopTime 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|指定的日期和時間**追蹤**元素應該停止。|  
|[StorageLocation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)|包含父元素之內容的檔案系統儲存位置。|  
|[StorageMode 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/storagemode-element-assl.md)|決定父元素的儲存模式。|  
|[TableID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/tableid-element-assl.md)|包含資料表的識別碼 (從**DataSourceView**項目) 與父元素相關聯。|  
|[目標項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/target-element-assl.md)|識別的目標**動作**項目。|  
|[TargetType 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/targettype-element-assl.md)|識別項目類型中所識別的項目[目標](../../../analysis-services/scripting/properties/target-element-assl.md)項目。|  
|[文字元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/text-element-assl.md)|包含文字的[命令](../../../analysis-services/scripting/objects/command-element-assl.md)項目。|  
|[Timeout 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/timeout-element-assl.md)|指定一段時間 (以秒為單位)，經過這段時間之後，嘗試擷取資料的行為就會回報逾時。|  
|[Trend 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)|包含傳回之趨勢指標的 MDX 運算式**Kpi**項目。|  
|[TrendGraphic 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/trendgraphic-element-assl.md)|包含之趨勢的建議圖形表示**Kpi**項目。|  
|[Trimming 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/trimming-element-assl.md)|指定如何修剪資料來源的資料。|  
|[Type 元素 &#40;動作 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-action-assl.md)|包含的型別**動作**項目。|  
|[Type 元素 &#40;繫結 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|包含屬性繫結的類型。|  
|[Type 元素 &#40;ClrAssemblyFile &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-clrassemblyfile-assl.md)|指定的其中一個屬於.NET Framework 組件檔案的檔案類型。|  
|[Type 元素 &#40; 維度 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)|提供有關維度內容的資訊。|  
|[Type 元素 &#40; DimensionAttribute &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md)|包含屬性的類型。|  
|[Type 元素 &#40;MeasureGroup &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-measuregroup-assl.md)|指定的型別**MeasureGroup**。|  
|[Type 元素 &#40;MeasureGroupAttribute &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-measuregroupattribute-assl.md)|包含的型別[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)項目。|  
|[Type 元素 &#40;MiningStructureColumn &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-miningstructurecolumn-assl.md)|包含的型別[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)項目。|  
|[Type 元素 &#40;分割區 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|包含的型別**分割**項目。|  
|[Type 元素 &#40;PerspectiveCalculation &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/type-element-perspectivecalculation-assl.md)|表示的類型[PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)項目。|  
|[UnknownMember 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)|指出未知的成員是否可見。|  
|[UnknownMemberName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)|包含維度之未知成員的標題，而這個標題會以維度的預設語言顯示。|  
|[Usage 元素 &#40; DimensionAttribute &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)|描述如何使用屬性。|  
|[Usage 元素 &#40;MiningModelColumn &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/properties/usage-element-miningmodelcolumn-assl.md)|描述如何與父系相關聯的資料行**MiningStructure**用。|  
|[Value 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/value-element-assl.md)|包含父元素的值。|  
|[Version 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/version-element-assl.md)|包含執行個體的唯讀版本號碼[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由**伺服器**項目。|  
|[Visibility 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/visibility-element-assl.md)|定義的可視性[註解](../../../analysis-services/scripting/objects/annotation-element-assl.md)項目。|  
|[Visible 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/visible-element-assl.md)|決定父元素的可見性。|  
|[VisualTotals 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|包含決定是否要針對這個屬性之成員顯示視覺化總計的 MDX 運算式。|  
|[寫入項目 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/write-element-assl.md)|判斷是否可寫入資料或中繼資料的指定**CubeDimensionPermission**或**權限**項目。|  
|[WriteEnabled 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|指出是否可以使用維度回寫 (受限於安全性權限)。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 元素階層 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  

