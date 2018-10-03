---
title: 屬性 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6371a751cdd5a4d647b781373ab74629103e0c44
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061398"
---
# <a name="properties-assl"></a>屬性 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做物件屬性之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，但是從開發人員的觀點而言，本節中描述的元素會對應至描述物件的屬性。  
  
 屬性是 ASSL 結構描述中的分葉層級元素，而且沒有對應至本身屬性的子元素和元素。  
  
 在少數情況下，結構描述中可能會顯示成屬性的分葉層級元素會分類成物件，因為元素的類型是物件類型。 例如，`Source` 物件的 `Dimension` 屬於 `DimensionBinding` 類型。  
  
## <a name="in-this-section"></a>本節內容  
  
|元素|描述|  
|-------------|-----------------|  
|[存取項目&#40;ASSL&#41;](access-element-assl.md)|表示層級的存取權提供給[CellPermission](../objects/cellpermission-element-assl.md)項目。|  
|[帳戶項目&#40;ImpersonationInfo&#41; &#40;ASSL&#41;](account-element-impersonationinfo-assl.md)|包含的使用者帳戶名稱[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)資料型別。|  
|[AccountType 元素&#40;ASSL&#41;](accounttype-element-assl.md)|包含名稱中所定義之帳戶類型的[資料庫](../objects/database-element-assl.md)項目。|  
|[ActionID 元素&#40;ASSL&#41;](id-element-assl.md)|包含名稱的[動作](../objects/action-element-assl.md)上定義的項目[Cube](../objects/cube-element-assl.md)項目可在其[觀點來看](../objects/perspective-element-assl.md)項目做為[PerspectiveAction](../data-type/action-data-type-assl.md)項目。|  
|[Administer 元素&#40;ASSL&#41;](administer-element-assl.md)|指出相關聯的權限是否包含管理 `Database` 元素的權限。|  
|[AggregateFunction 元素&#40;ASSL&#41;](aggregatefunction-element-assl.md)|定義所使用的彙總函式的型別[量值](../objects/measure-element-assl.md)項目。|  
|[AggregationDesignID 元素&#40;ASSL&#41;](aggregationdesignid-element-assl.md)|識別[AggregationDesign](../objects/aggregationdesign-element-assl.md)相關聯的項目[分割區](../objects/partition-element-assl.md)項目。|  
|[AggregationFunction 元素&#40;ASSL&#41;](aggregationfunction-element-assl.md)|包含要用於帳戶類型的彙總函式。|  
|[AggregationID 元素&#40;ASSL&#41;](aggregationid-element-assl.md)|識別用來建立彙總執行個體之 `AggregationDesign` 元素的彙總定義。|  
|[AggregationInstanceSource 元素&#40;ASSL&#41;](aggregationinstancesource-element-assl.md)|識別繫結至 `Partition` 元素之使用者定義彙總執行個體的資料來源。|  
|[AggregationPrefix 元素&#40;ASSL&#41;](aggregationprefix-element-assl.md)|定義要在整個相關聯父元素中用於彙總名稱的一般前置詞。|  
|[AggregationStorage 元素&#40;ASSL&#41;](aggregationstorage-element-assl.md)|識別彙總的儲存方法。|  
|[AggregationType 元素&#40;ASSL&#41;](aggregationtype-element-assl.md)|定義 `Partition` 元素所儲存的彙總類型。|  
|[AggregationUsage 元素&#40;ASSL&#41;](aggregationusage-element-assl.md)|控制項如何在彙總設計師[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]設計彙總。|  
|[Algorithm 元素&#40;ASSL&#41;](algorithm-element-assl.md)|定義所使用的演算法[MiningModel](../objects/miningmodel-element-assl.md)項目。|  
|[Alias 元素&#40;ASSL&#41;](alias-element-assl.md)|定義的別名[帳戶](../objects/account-element-assl.md)項目。|  
|[AllMemberAggregationUsage 元素&#40;ASSL&#41;](allmemberaggregationusage-element-assl.md)|控制 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的彙總設計師如何設計彙總。|  
|[AllMemberName 元素&#40;ASSL&#41;](name-element-assl.md)|包含 「 全部 」 成員的預設語言的標題[階層](../objects/hierarchy-element-assl.md)項目。|  
|[AllowBrowsing 元素&#40;ASSL&#41;](allowbrowsing-element-assl.md)|定義是否隸屬[角色](../objects/role-element-assl.md)元素擁有瀏覽權限`MiningModel`項目。|  
|[AllowDrillThrough 元素&#40;ASSL&#41;](allowdrillthrough-element-assl.md)|決定是否允許針對父元素進行鑽研。|  
|[AllowDuplicateNames 元素&#40;ASSL&#41;](allowduplicatenames-element-assl.md)|決定 `Hierarchy` 元素中是否允許重複名稱。|  
|[AllowedSet 元素&#40;ASSL&#41;](allowedset-element-assl.md)|包含針對屬性之 `Role` 元素定義允許權限集合的集合運算式。|  
|[應用程式項目&#40;ASSL&#41;](application-element-assl.md)|識別與 `Action` 元素相關聯的應用程式。|  
|[AssociatedMeasureGroupID 元素&#40;ASSL&#41;](measuregroupid-element-assl.md)|包含的識別碼 (ID) [MeasureGroup](../objects/group-element-assl.md)相關聯的項目[CalculationProperty](../objects/calculationproperty-element-assl.md)項目或有[Kpi](../objects/kpi-element-assl.md)項目。|  
|[AttributeAllMemberName 元素&#40;ASSL&#41;](attributeallmembername-element-assl.md)|包含維度之 All 成員的標題，而這個標題會以預設語言顯示。|  
|[AttributeHierarchyDisplayFolder 元素&#40;ASSL&#41;](displayfolder-element-assl.md)|識別要在其中顯示相關聯屬性階層的資料夾。|  
|[AttributeHierarchyEnabled 元素&#40;ASSL&#41;](enabled-element-assl.md)|決定是否針對此屬性啟用屬性階層。|  
|[AttributeHierarchyOptimizedState 元素&#40;ASSL&#41;](state-element-assl.md)|決定套用至屬性階層的最佳化層級。|  
|[AttributeHierarchyOrdered 元素&#40;ASSL&#41;](attributehierarchyordered-element-assl.md)|決定是否排序相關聯的屬性階層。|  
|[AttributeHierarchyVisible 元素&#40;ASSL&#41;](visible-element-assl.md)|決定用戶端應用程式是否可看到屬性階層。|  
|[AttributeID 元素&#40;ASSL&#41;](attributeid-element-assl.md)|包含與父元素相關聯之屬性的識別碼。|  
|[稽核項目&#40;ASSL&#41;](audit-element-assl.md)|指定[追蹤](../objects/trace-element-assl.md)元素無法卸除任何事件，即使這樣造成伺服器效能降低。|  
|[AutoRestart 元素&#40;ASSL&#41;](autorestart-element-assl.md)|決定如果 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服務停止並重新啟動，`Trace` 元素是否應該自動重新啟動。|  
|[BackColor 元素&#40;ASSL&#41;](backcolor-element-assl.md)|描述父元素的色彩相關顯示特性。|  
|[CacheMode 元素&#40;ASSL&#41;](cachemode-element-assl.md)|決定用於培訓在處理採礦結構時擷取之資料的快取機制。|  
|[CalculationReference 元素&#40;ASSL&#41;](calculationreference-element-assl.md)|包含 `CalculationProperty` 元素所參考之命名集或導出資料格的名稱。|  
|[CalculationType 元素&#40;ASSL&#41;](calculationtype-element-assl.md)|描述相關聯 `CalculationProperty` 元素中定義的計算類型。|  
|[CalendarEndDate 元素&#40;ASSL&#41;](calendarenddate-element-assl.md)|定義之日曆週期的結束日期[TimeBinding](../data-type/binding-data-type-assl.md)項目。|  
|[CalendarLanguage 元素&#40;ASSL&#41;](language-element-assl.md)|定義用於 `TimeBinding` 元素的日曆語言。|  
|[CalendarStartDate 元素&#40;ASSL&#41;](calendarstartdate-element-assl.md)|定義 `TimeBinding` 元素之日曆週期的開始日期。|  
|[標題項目&#40;ASSL&#41;](caption-element-assl.md)|包含相關聯父元素的標題。|  
|[CaptionIsMdx 元素&#40;ASSL&#41;](captionismdx-element-assl.md)|定義 `Action` 元素的標題是否為多維度運算式 (MDX) 運算式。|  
|[Cardinality 元素&#40;ASSL&#41;](cardinality-element-assl.md)|表示所描述之關聯性的基數[AttributeRelationship](../objects/attributerelationship-element-assl.md)或是[RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)。|  
|[CaseCubeDimensionID 元素&#40;ASSL&#41;](dimensionid-element-assl.md)|包含將資料採礦維度關聯至量值群組之 Cube 維度的識別碼。|  
|[ClassifiedColumnID 元素&#40;ASSL&#41;](classifiedcolumnid-element-assl.md)|包含所分類之相關資料行的識別碼[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)項目。|  
|[定序項目&#40;ASSL&#41;](collation-element-assl.md)|決定父元素所使用的定序。|  
|[ColumnID 元素&#40;ColumnBinding&#41; &#40;ASSL&#41;](columnid-element-columnbinding-assl.md)|包含資料表中資料項目所繫結之資料行的識別碼。|  
|[ColumnID 元素&#40;EventColumn&#41; &#40;ASSL&#41;](columnid-element-eventcolumn-assl.md)|包含要針對某個事件擷取成 `Trace` 元素一部分之資訊資料行的識別碼。|  
|[Condition 項目&#40;ASSL&#41;](condition-element-assl.md)|包含 MDX 運算式，決定是否`Action`父項目套用至目標。|  
|[ConnectionString 元素&#40;ASSL&#41;](connectionstring-element-assl.md)|包含加密的連接字串[DataSource](../objects/datasource-element-assl.md)項目。|  
|[ConnectionStringSecurity 元素&#40;ASSL&#41;](connectionstringsecurity-element-assl.md)|指定是否要針對安全性目的從資料來源連接字串中移除使用者密碼。|  
|[內容項目&#40;ASSL&#41;](content-element-assl.md)|說明中的資料行的內容[MiningStructure](../objects/miningstructure-element-assl.md)項目。|  
|[CreatedTimestamp 元素&#40;ASSL&#41;](createdtimestamp-element-assl.md)|包含父元素的唯讀建立時間戳記。|  
|[CubeDimensionID 元素&#40;ASSL&#41;](cubedimensionid-element-assl.md)|識別[CubeDimension](../data-type/cubedimension-data-type-assl.md)與父元素相關聯的項目。|  
|[CubeID 元素&#40;ASSL&#41;](cubeid-element-assl.md)|識別`Cube`元素相關聯[繫結](../data-type/binding-data-type-assl.md)項目。|  
|[CurrentStorageMode 元素&#40;ASSL&#41;](storagemode-element-assl.md)|決定父元素的目前儲存模式。|  
|[CurrentTimeMember 元素&#40;ASSL&#41;](../objects/member-element-assl.md)|定義與 `Kpi` 元素相關聯之時間維度的目前成員。|  
|[DataAggregation 元素&#40;ASSL&#41;](../objects/aggregation-element-assl.md)|決定此執行個體是否可彙總 `MeasureGroup` 的保存資料或快取資料。|  
|[DatabaseID 元素&#40;ASSL&#41;](databaseid-element-assl.md)|識別與非正規 (out-of-line) `Database` 元素相關聯的 `Binding` 元素。|  
|[DataSize 元素&#40;ASSL&#41;](datasize-element-assl.md)|包含以位元組為單位的大小[DataItem](../data-type/dataitem-data-type-assl.md)項目。|  
|[DataSourceID 元素&#40;ASSL&#41;](datasourceid-element-assl.md)|識別與父元素相關聯的 `DataSource` 元素。|  
|[DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)|包含在連接至 `Database` 元素的資料來源時，用來決定模擬行為的資訊。|  
|[DataSourceViewID 元素&#40;ASSL&#41;](datasourceviewid-element-assl.md)|識別[DataSourceView](../objects/datasourceview-element-assl.md)相關聯的項目`Binding`父項目。|  
|[DataType 元素&#40;ASSL&#41;](datatype-element-assl.md)|定義相關聯元素的資料類型。|  
|[DbSchemaName 元素&#40;ASSL&#41;](dbschemaname-element-assl.md)|包含父元素所識別之資料表中所使用的結構描述名稱[DbTableName](dbtablename-element-assl.md)項目。|  
|[DbTableName 元素&#40;ASSL&#41;](dbtablename-element-assl.md)|包含父元素所繫結之資料表的名稱。|  
|[預設項目&#40;ASSL&#41;](default-element-assl.md)|決定 `DrillThroughAction` 是否為預設的鑽研動作。|  
|[DefaultMeasure 元素&#40;ASSL&#41;](defaultmeasure-element-assl.md)|包含定義 `Cube` 或 `Perspective` 元素之預設量值的 MDX 語言運算式。|  
|[DefaultMember 元素&#40;ASSL&#41;](defaultmember-element-assl.md)|包含可識別父元素之預設成員的 MDX 運算式。|  
|[DefaultScript 元素&#40;ASSL&#41;](defaultscript-element-assl.md)|識別預設[MdxScript](../objects/mdxscript-element-assl.md)中的項目[MdxScripts](../collections/mdxscripts-element-assl.md)集合。|  
|[DefaultValue 元素&#40;ASSL&#41;](value-element-assl.md)|包含相關聯的唯讀預設值[ServerProperty](../objects/serverproperty-element-assl.md)項目。|  
|[DeniedSet 元素&#40;ASSL&#41;](deniedset-element-assl.md)|包含定義在相關聯屬性上遭拒之權限清單的集合運算式。|  
|[DependsOnDimensionID 元素&#40;ASSL&#41;](dependsondimensionid-element-assl.md)|包含父維度所相依之其他維度的識別碼。|  
|[Description 項目&#40;ASSL&#41;](description-element-assl.md)|包含父元素的描述。|  
|[DimensionID 元素&#40;ASSL&#41;](dimensionid-element-assl.md)|包含維度的識別碼。|  
|[DiscretizationBucketCount 元素&#40;ASSL&#41;](discretizationbucketcount-element-assl.md)|包含要進行離散化的值區數目。|  
|[DiscretizationMethod 元素&#40;ASSL&#41;](discretizationmethod-element-assl.md)|定義用於進行離散化的方法。|  
|[DisplayFlag 元素&#40;ASSL&#41;](displayflag-element-assl.md)|包含指出使用者介面元件是否應該顯示相關聯 `ServerProperty` 元素的唯讀提示。|  
|[DisplayFolder 元素&#40;ASSL&#41;](displayfolder-element-assl.md)|指定要在其中列出父元素的資料夾。 開發人員和系統管理員的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 應用程式可能會支援使用顯示資料夾以視覺化方式分類多個元素。|  
|[Distribution 元素&#40;ASSL&#41;](distribution-element-assl.md)|包含描述純量值如何在 `MiningStructure` 元素之資料行內部散發的提供者專用值。|  
|[Edition 元素&#40;ASSL&#41;](edition-element-assl.md)|包含執行個體的唯讀版本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[Server](../objects/server-element-assl.md)項目。|  
|[啟用項目&#40;ASSL&#41;](enabled-element-assl.md)|指出是否已啟用父元素。|  
|[EndOfData 元素&#40;ASSL&#41;](../objects/data-element-assl.md)|表示從收到的資料結尾[PushedDataSource](../data-type/datasource-data-type-assl.md)項目。|  
|[EstimatedCount 元素&#40;ASSL&#41;](estimatedcount-element-assl.md)|包含屬性之成員的估計數目。|  
|[EstimatedPerformanceGain 元素&#40;ASSL&#41;](estimatedperformancegain-element-assl.md)|包含資料分割之估計效能改善的唯讀百分比。|  
|[EstimatedRows 元素&#40;ASSL&#41;](estimatedrows-element-assl.md)|包含父元素所代表之估計的資料列數目。|  
|[EstimatedSize 元素&#40;ASSL&#41;](estimatedsize-element-assl.md)|包含父元素的維度估計大小 (以位元組為單位)。|  
|[EventID 元素&#40;ASSL&#41;](eventid-element-assl.md)|可唯一識別[事件](../objects/event-element-assl.md)要擷取做為一部分的項目`Trace`項目。|  
|[Expression 元素&#40;ASSL&#41;](expression-element-assl.md)|包含定義父元素之內容的 MDX 運算式。|  
|[篩選項目&#40;繫結&#41; &#40;ASSL&#41;](filter-element-binding-assl.md)|包含篩選父元素之內容的 MDX 運算式。|  
|[篩選項目&#40;追蹤&#41; &#40;ASSL&#41;](filter-element-trace-assl.md)|包含描述 `Trace` 篩選的 XML 文件片段。|  
|[FirstDayOfWeek 元素&#40;ASSL&#41;](firstdayofweek-element-assl.md)|定義 `TimeBinding` 元素之當週的第一天。|  
|[FiscalFirstDayOfMonth 元素&#40;ASSL&#41;](fiscalfirstdayofmonth-element-assl.md)|定義 `TimeBinding` 元素之會計月份的第一天。|  
|[FiscalFirstMonth 元素&#40;ASSL&#41;](fiscalfirstmonth-element-assl.md)|定義 `TimeBinding` 元素之會計週期的第一個月。|  
|[FiscalYearName 元素&#40;ASSL&#41;](fiscalyearname-element-assl.md)|定義 `TimeBinding` 元素之會計年度名稱的命名慣例。|  
|[FontFlags 元素&#40;ASSL&#41;](fontflags-element-assl.md)|描述 `CalculationProperty` 或 `Measure` 父元素的字型相關顯示特性。|  
|[FontName 元素&#40;ASSL&#41;](fontname-element-assl.md)|描述 `CalculationProperty` 或 `Measure` 父元素的字型相關顯示特性。|  
|[FontSize 元素&#40;ASSL&#41;](fontsize-element-assl.md)|描述 `CalculationProperty` 或 `Measure` 父元素的字型相關顯示特性。|  
|[ForceRebuildInterval 元素&#40;ASSL&#41;](forcerebuildinterval-element-assl.md)|決定多維度 OLAP (MOLAP) 影像處理無條件開始所經過的時間量 (從全新 MOLAP 影像可用開始計算)。|  
|[ForeColor 元素&#40;ASSL&#41;](forecolor-element-assl.md)|描述 `CalculationProperty` 或 `Measure` 父元素的色彩相關顯示特性。|  
|[格式項目&#40;ASSL&#41;](format-element-assl.md)|包含 `DataItem` 元素的必要格式。|  
|[FormatString 元素&#40;ASSL&#41;](formatstring-element-assl.md)|描述 `CalculationProperty` 元素或 `Measure` 元素的顯示格式。|  
|[Goal 元素&#40;ASSL&#41;](goal-element-assl.md)|識別 `Kpi` 元素中的所需目標。|  
|[GranularityAttributeID 元素&#40;ASSL&#41;](granularityattributeid-element-assl.md)|包含與父代相關聯之屬性的識別碼[MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)資料型別。|  
|[HideMemberIf 元素&#40;ASSL&#41;](hidememberif-element-assl.md)|指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。|  
|[HierarchyID 元素&#40;ASSL&#41;](hierarchyid-element-assl.md)|包含的識別碼[CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)項目。|  
|[HierarchyUniqueNameStyle 元素&#40;ASSL&#41;](hierarchyuniquenamestyle-element-assl.md)|決定如何為 `CubeDimension` 內所包含的階層產生唯一名稱。|  
|[ID 項目&#40;ASSL&#41;](id-element-assl.md)|包含父元素的唯一識別碼。|  
|[IgnoreUnrelatedDimensions 元素&#40;ASSL&#41;](../collections/dimensions-element-assl.md)|決定當查詢中包含與量值群組不相關的維度成員時，是否將不相關的維度強制在其最上層。|  
|[ImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)|包含在存取或執行組件時，用來決定模擬行為的資訊。|  
|[ImpersonationInfoSecurity 元素&#40;ASSL&#41;](impersonationinfosecurity-element-assl.md)|包含唯讀的值，指出是否已對 `ImpersonationInfo` 資料類型中提供的安全性認證進行任何變更。|  
|[ImpersonationMode 元素&#40;ASSL&#41;](impersonationmode-element-assl.md)|包含一個值，表示衍生自 `ImpersonationInfo` 資料類型之元素的模擬方法。|  
|[InstanceSelection 元素&#40;ASSL&#41;](instanceselection-element-assl.md)|提供一個提示給用戶端應用程式，以便根據清單中的預期項目數目來建議應該如何顯示項目清單。|  
|[IntermediateCubeDimensionID 元素&#40;ASSL&#41;](intermediatecubedimensionid-element-assl.md)|包含將參考維度關聯至量值群組之維度的識別碼。|  
|[IntermediateGranularityAttributeID 元素&#40;ASSL&#41;](intermediategranularityattributeid-element-assl.md)|包含中繼 Cube 維度中用來將參考維度關聯至中繼維度之資料粒度屬性的識別碼。|  
|[InvalidXmlCharacters 元素&#40;ASSL&#41;](invalidxmlcharacters-element-assl.md)|指定來源資料中無效 XML 字元的處理方法。|  
|[Invocation 元素&#40;ASSL&#41;](invocation-element-assl.md)|指定應該如何叫用 `Action`。|  
|[IsAggregatable 元素&#40;ASSL&#41;](isaggregatable-element-assl.md)|指定是否的值[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)元素可彙總。|  
|[IsKey 元素&#40;ASSL&#41;](iskey-element-assl.md)|指出此資料行是否會針對 `MiningStructure` 元素中的案例提供索引鍵。|  
|[Isolation 元素&#40;ASSL&#41;](isolation-element-assl.md)|指出衍生自元素的隔離等級[DataSource](../data-type/datasource-data-type-assl.md)資料型別。|  
|[KeyDuplicate 元素&#40;ASSL&#41;](keyduplicate-element-assl.md)|決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何處理在處理期間遇到的重複索引鍵錯誤。|  
|[KeyErrorAction 元素&#40;ASSL&#41;](keyerroraction-element-assl.md)|指定在索引鍵發生錯誤時要讓 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 採取的動作。|  
|[KeyErrorLimit 元素&#40;ASSL&#41;](keyerrorlimit-element-assl.md)|包含處理期間可接受的錯誤數目。|  
|[KeyErrorLimitAction 元素&#40;ASSL&#41;](keyerrorlimitaction-element-assl.md)|指定的動作所[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定的索引鍵錯誤計數時[KeyErrorLimit](keyerrorlimit-element-assl.md)項目出現為止。|  
|[KeyErrorLogFile 元素&#40;ASSL&#41;](../objects/file-element-assl.md)|包含記錄處理錯誤的檔案名稱。|  
|[KeyNotFound 元素&#40;ASSL&#41;](keynotfound-element-assl.md)|指定當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遇到參考完整性錯誤時如何回應。|  
|[KeyUniquenessGuarantee 元素&#40;ASSL&#41;](keyuniquenessguarantee-element-assl.md)|指出屬性索引鍵與其名稱之間的關聯性以及相關屬性的關聯性是否保證有效。|  
|[KpiID 元素&#40;ASSL&#41;](kpiid-element-assl.md)|包含將 `Kpi` 元素與 `Perspective` 元素產生關聯的識別碼。|  
|[語言項目&#40;ASSL&#41;](language-element-assl.md)|包含父元素的語言識別碼。|  
|[LastProcessed 元素&#40;ASSL&#41;](lastprocessed-element-assl.md)|包含唯讀的時間戳記，指出上次處理包含父元素之資料庫的時間。|  
|[LastSchemaUpdate 元素&#40;ASSL&#41;](lastschemaupdate-element-assl.md)|包含父元素的唯讀中繼資料更新時間戳記。|  
|[LastUpdate 元素&#40;ASSL&#41;](lastupdate-element-assl.md)|包含唯讀的時間戳記，指出上次相關聯 `Database` 或資料庫包含之任何主要物件遭變更的時間。|  
|[Latency 元素&#40;ASSL&#41;](latency-element-assl.md)|定義最早通知與終結 MOLAP 影像之間的「寬限期」。|  
|[LogFileAppend 元素&#40;ASSL&#41;](logfileappend-element-assl.md)|決定 `Trace` 元素會將其記錄輸出附加至現有的記錄檔，還是覆寫記錄檔。|  
|[LogFileName 元素&#40;ASSL&#41;](logfilename-element-assl.md)|包含 `Trace` 元素之記錄檔的檔案名稱。|  
|[LogFileRollover 元素&#40;ASSL&#41;](logfilerollover-element-assl.md)|指定的記錄`Trace`輸出應該換到新的檔案，或應該在中指定的最大記錄檔大小的停止[LogFileSize](logfilesize-element-assl.md)為止。|  
|[LogFileSize 元素&#40;ASSL&#41;](logfilesize-element-assl.md)|指定最大記錄檔大小 (以 MB 為單位)。|  
|[ManagedProvider 元素&#40;ASSL&#41;](managedprovider-element-assl.md)|包含衍生自 `DataSource` 資料類型之元素所使用的 Managed 提供者名稱。|  
|[ManufacturingExtraMonthQuarter 元素&#40;ASSL&#41;](manufacturingextramonthquarter-element-assl.md)|定義要針對 `TimeBinding` 元素指派延長月份之製造週期的月份。|  
|[ManufacturingFirstMonth 元素&#40;ASSL&#41;](manufacturingfirstmonth-element-assl.md)|定義 `TimeBinding` 元素的第一個製造月份。|  
|[ManufacturingFirstWeekOfMonth 元素&#40;ASSL&#41;](manufacturingfirstweekofmonth-element-assl.md)|定義 `TimeBinding` 元素之製造月份的第一週。|  
|[MasterDatasourceID 元素&#40;ASSL&#41;](masterdatasourceid-element-assl.md)|包含 `Database` 元素的主要資料來源識別碼。|  
|[Materialization 元素&#40;ASSL&#41;](materialization-element-assl.md)|指出量值群組與參考維度之間關聯性的類型。|  
|[MaxActiveConnections 元素&#40;ASSL&#41;](maxactiveconnections-element-assl.md)|包含衍生自 `DataSource` 資料類型之元素所允許的最大並行連接數目。|  
|[MdxMissingMemberMode 元素&#40;ASSL&#41;](mdxmissingmembermode-element-assl.md)|決定如何處理 MDX 陳述式的遺漏成員。|  
|[MeasureExpression 元素&#40;ASSL&#41;](measureexpression-element-assl.md)|包含定義量值的 MDX 運算式。|  
|[MeasureGroupID 元素&#40;ASSL&#41;](measuregroupid-element-assl.md)|將 `MeasureGroup` 與父元素、繫結或非正規 (out-of-line) 繫結產生關聯。|  
|[MeasureID 元素&#40;ASSL&#41;](measureid-element-assl.md)|將 `Measure` 元素與父元素產生關聯。|  
|[MeasureQualificaton 元素&#40;ASSL&#41;](measurequalificaton-element-assl.md)|決定前置詞是否會套用至 `MeasureGroup` 中的量值。|  
|[MemberNamesUnique 元素&#40;ASSL&#41;](membernamesunique-element-assl.md)|決定父元素底下的成員名稱是否必須是唯一的。|  
|[MemberUniqueNameStyle 元素&#40;ASSL&#41;](memberuniquenamestyle-element-assl.md)|決定如何為 `CubeDimension` 元素內所包含的階層成員產生唯一名稱。|  
|[MembersWithData 元素&#40;ASSL&#41;](memberswithdata-element-assl.md)|決定是否要在父屬性中顯示非分葉成員的資料成員。|  
|[MembersWithDataCaption 元素&#40;ASSL&#41;](memberswithdatacaption-element-assl.md)|提供範本字串，該字串會用來建立系統所產生之資料成員的標題。|  
|[MimeType 元素&#40;ASSL&#41;](mimetype-element-assl.md)|包含 `DataItem` 父元素所代表之資料的多用途網際網路郵件延伸標準 (MIME) 類型 (如果適用的話)。|  
|[MiningModelID 元素&#40;ASSL&#41;](miningmodelid-element-assl.md)|將採礦模型與資料採礦維度產生關聯。|  
|[名稱項目&#40;ASSL&#41;](name-element-assl.md)|包含父元素的名稱。|  
|[NamingTemplate 元素&#40;ASSL&#41;](namingtemplate-element-assl.md)|定義在從 `DimensionAttribute` 父元素建構的父子式階層中如何命名層級。|  
|[NonEmptyBehavior 元素&#40;ASSL&#41;](nonemptybehavior-element-assl.md)|決定與 `CalculationProperty` 元素之父系相關聯的非空白行為。|  
|[NotificationTechnique 元素&#40;ASSL&#41;](notificationtechnique-element-assl.md)|指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部的用戶端應用程式會處理通知。|  
|[NullKeyConvertedToUnknown 元素&#40;ASSL&#41;](nullkeyconvertedtounknown-element-assl.md)|指定遇到 Null 轉換錯誤時要採取的動作。|  
|[NullKeyNotAllowed 元素&#40;ASSL&#41;](nullkeynotallowed-element-assl.md)|決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 處理引擎如何處理在處理期間遇到的 Null 索引鍵錯誤。|  
|[NullProcessing 元素&#40;ASSL&#41;](nullprocessing-element-assl.md)|定義 Null 值的處理方式。|  
|[OnlineMode 元素&#40;ASSL&#41;](onlinemode-element-assl.md)|指定資料庫會在起始快取的重建作業時立即返回線上狀態，還是只有在快取的重建作業完成時才返回線上狀態。|  
|[OptimizedState 元素&#40;ASSL&#41;](state-element-assl.md)|決定套用至階層的最佳化層級。|  
|[Optionality 元素&#40;ASSL&#41;](optionality-element-assl.md)|指出 `AttributeRelationship` 元素之成員的選擇性。|  
|[OrderBy 元素&#40;ASSL&#41;](orderby-element-assl.md)|描述如何排序屬性中包含的成員。|  
|[OrderByAttributeID 元素&#40;ASSL&#41;](orderbyattributeid-element-assl.md)|識別排序的成員所依據的另一個屬性[維度](../data-type/dimensionattribute-data-type-assl.md)屬性。|  
|[Ordinal 元素&#40;ASSL&#41;](ordinal-element-assl.md)|指出索引鍵和翻譯等集合中要繫結的目標序號。|  
|[OverrideBehavior 元素&#40;ASSL&#41;](overridebehavior-element-assl.md)|指出 `AttributeRelationship` 元素所描述之關聯性的覆寫行為。|  
|[PartitionID 元素&#40;ASSL&#41;](partitionid-element-assl.md)|將 `Partition` 元素與父元素、繫結或非正規 (out-of-line) 繫結產生關聯。|  
|[Password 元素&#40;ASSL&#41;](password-element-assl.md)|包含 `ImpersonationInfo` 元素之使用者帳戶的密碼。|  
|[路徑項目&#40;ASSL&#41;](path-element-assl.md)|所提供的執行個體所包含的路徑[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，所使用之報表的[ReportAction](../data-type/reportaction-data-type-assl.md)項目。|  
|[PendingValue 元素&#40;ASSL&#41;](pendingvalue-element-assl.md)|包含相關聯 `ServerProperty` 元素的唯讀暫止值。|  
|[PermissionSet 元素&#40;ASSL&#41;](permissionset-element-assl.md)|識別與相關聯的權限集合[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。|  
|[Persistence 元素&#40;ASSL&#41;](persistence-element-assl.md)|繫結的來源資料中哪些部分是動態的而且會檢查是否有更新使用所指定的頻率會決定[RefreshPolicy](refreshpolicy-element-assl.md)項目。|  
|[處理項目&#40;ASSL&#41;](process-element-assl.md)|決定使用者是否可以處理父元素的擁有者。|  
|[ProcessingMode 元素&#40;ASSL&#41;](processingmode-element-assl.md)|指出此執行個體應該在處理期間或處理之後進行索引和彙總。|  
|[ProcessingPriority 元素&#40;ASSL&#41;](processingpriority-element-assl.md)|決定背景作業期間父物件的處理優先權 (例如，延遲彙總、索引或叢集)。|  
|[ProcessingQuery 元素&#40;ASSL&#41;](query-element-assl.md)|包含要針對累加式處理狀態通知執行之查詢的參數化文字。|  
|[ProductName 元素&#40;ASSL&#41;](productname-element-assl.md)|包含與 `Server` 元素相關聯之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的唯讀產品名稱。|  
|[查詢項目&#40;ASSL&#41;](query-element-assl.md)|包含要針對通知執行之查詢的文字。|  
|[QueryDefinition 元素&#40;ASSL&#41;](querydefinition-element-assl.md)|包含與相關聯之查詢的不透明運算式`DataSource`中的項目[QueryBinding](../data-type/querybinding-data-type-assl.md)項目。|  
|[讀取項目&#40;ASSL&#41;](read-element-assl.md)|判斷是否可讀取資料或中繼資料的給定[CubeDimensionPermission](../data-type/permission-data-type-assl.md)或是[權限](../data-type/permission-data-type-assl.md)項目。|  
|[ReadDefinition 元素&#40;ASSL&#41;](readdefinition-element-assl.md)|決定成員是否可以讀取資料庫的定義或資料庫中物件的定義。|  
|[ReadSourceData 元素&#40;ASSL&#41;](readsourcedata-element-assl.md)|決定如何為 `CubePermission` 內所包含的階層產生唯一名稱。|  
|[RefreshInterval 元素&#40;ASSL&#41;](refreshinterval-element-assl.md)|指定重新整理與父元素相關聯之繫結資料的間隔。|  
|[RefreshPolicy 元素&#40;ASSL&#41;](refreshpolicy-element-assl.md)|決定多久維度或量值群組之動態部分 (依照[持續性](persistence-element-assl.md)項目) 會檢查變更。|  
|[RelationshipType 元素&#40;ASSL&#41;](relationshiptype-element-assl.md)|指出 `AttributeRelationship` 的成員關聯性是否可變更。|  
|[RemoteDatasourceID 元素&#40;ASSL&#41;](remotedatasourceid-element-assl.md)|指定指向儲存遠端資料分割之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的 OLAP 資料來源的識別碼。|  
|[ReportingFirstMonth 元素&#40;ASSL&#41;](reportingfirstmonth-element-assl.md)|定義 `TimeBinding` 元素的第一個報表月份。|  
|[ReportingFirstWeekOfMonth 元素&#40;ASSL&#41;](reportingfirstweekofmonth-element-assl.md)|定義 `TimeBinding` 元素之報表月份的第一週。|  
|[ReportingWeekToMonthPattern 元素&#40;ASSL&#41;](reportingweektomonthpattern-element-assl.md)|定義 `TimeBinding` 元素的報表週至月份模式。|  
|[ReportServer 元素&#40;ASSL&#41;](reportserver-element-assl.md)|包含 `ReportAction` 所使用之 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 執行個體的名稱。|  
|[RequiresRestart 元素&#40;ASSL&#41;](requiresrestart-element-assl.md)|包含與 `ServerProperty` 元素相關聯的唯讀值，可決定變更伺服器屬性的值是否需要重新啟動執行個體才能讓變更生效。|  
|[RoleID 元素&#40;ASSL&#41;](roleid-element-assl.md)|識別要定義權限的角色。|  
|[根項目&#40;ASSL&#41;](root-element-assl.md)|包含資料來源的資料 (資料列集)。|  
|[RootMemberIf 元素&#40;ASSL&#41;](rootmemberif-element-assl.md)|決定如何識別父屬性的根成員。|  
|[結構描述項目&#40;ASSL&#41;](schema-element-assl.md)|包含資料來源檢視的結構描述。|  
|[ScriptCacheProcessingMode 元素&#40;ASSL&#41;](scriptcacheprocessingmode-element-assl.md)|指出伺服器應該在處理期間或處理之後建立指令碼快取。|  
|[SilenceInterval 元素&#40;ASSL&#41;](silenceinterval-element-assl.md)|定義在啟動 MOLAP 影像處理處理序之前，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體暫停的最小時間量。|  
|[SilenceOverrideInterval 元素&#40;ASSL&#41;](silenceoverrideinterval-element-assl.md)|定義在收到初始通知之後和 MOLAP 影像處理無條件開始之前必須經過的時間量。|  
|[配量項目&#40;ASSL&#41;](slice-element-assl.md)|包含定義資料分割中包含之配量的 MDX 運算式。|  
|[SolveOrder 元素&#40;ASSL&#41;](solveorder-element-assl.md)|指出 `CalculationProperty` 元素套用至導出成員或導出資料格定義的求解順序。|  
|[Source 元素&#40;繫結&#41; &#40;ASSL&#41;](source-element-binding-assl.md)|識別父元素所繫結的資料來源。|  
|[Source 元素&#40;ComAssembly&#41; &#40;ASSL&#41;](source-element-comassembly-assl.md)|包含元件物件模型 (COM) 元件的檔案名稱或程式設計識別碼 (ProgID)。|  
|[Source 元素&#40;量值&#41; &#40;ASSL&#41;](source-element-measure-assl.md)|包含具有 `Measure` 元素值之來源的詳細資料。|  
|[SourceAttributeID 元素&#40;ASSL&#41;](sourceattributeid-element-assl.md)|包含來源屬性的識別碼[層級](../objects/level-element-assl.md)項目為基礎。|  
|[SourceColumnID 元素&#40;ASSL&#41;](sourcecolumnid-element-assl.md)|包含 `MiningStructure` 上階元素中來源採礦結構資料行的識別碼。|  
|[狀態項目&#40;ASSL&#41;](state-element-assl.md)|包含描述父元素之目前處理狀態的唯讀值。|  
|[狀態項目&#40;ASSL&#41;](status-element-assl.md)|包含傳回 `Kpi` 元素之狀態指標的 MDX 運算式。|  
|[StatusGraphic 元素&#40;ASSL&#41;](statusgraphic-element-assl.md)|包含 `Kpi` 元素之狀態的建議圖形表示。|  
|[StopTime 元素&#40;ASSL&#41;](stoptime-element-assl.md)|指定 `Trace` 元素應該停止的日期和時間。|  
|[StorageLocation 元素&#40;ASSL&#41;](storagelocation-element-assl.md)|包含父元素之內容的檔案系統儲存位置。|  
|[StorageMode 元素&#40;ASSL&#41;](storagemode-element-assl.md)|決定父元素的儲存模式。|  
|[TableID 元素&#40;ASSL&#41;](tableid-element-assl.md)|包含與父元素相關聯之資料表 (來自 `DataSourceView` 元素) 的識別碼。|  
|[Target 項目&#40;ASSL&#41;](target-element-assl.md)|識別 `Action` 元素的目標。|  
|[TargetType 元素&#40;ASSL&#41;](targettype-element-assl.md)|識別項目類型中所識別之項目的[目標](target-element-assl.md)項目。|  
|[文字項目&#40;ASSL&#41;](text-element-assl.md)|包含的文字[命令](../objects/command-element-assl.md)項目。|  
|[Timeout 元素&#40;ASSL&#41;](timeout-element-assl.md)|指定一段時間 (以秒為單位)，經過這段時間之後，嘗試擷取資料的行為就會回報逾時。|  
|[Trend 元素&#40;ASSL&#41;](trend-element-assl.md)|包含傳回 `Kpi` 元素之趨勢指標的 MDX 運算式。|  
|[TrendGraphic 元素&#40;ASSL&#41;](trendgraphic-element-assl.md)|包含 `Kpi` 元素之趨勢的建議圖形表示。|  
|[Trimming 元素&#40;ASSL&#41;](trimming-element-assl.md)|指定如何修剪資料來源的資料。|  
|[輸入項目&#40;動作&#41; &#40;ASSL&#41;](type-element-action-assl.md)|包含 `Action` 元素的類型。|  
|[輸入項目&#40;繫結&#41; &#40;ASSL&#41;](type-element-binding-assl.md)|包含屬性繫結的類型。|  
|[輸入項目&#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](type-element-clrassemblyfile-assl.md)|指定的其中一個屬於.NET Framework 組件檔案的檔案類型。|  
|[輸入項目&#40;維度&#41; &#40;ASSL&#41;](type-element-dimension-assl.md)|提供有關維度內容的資訊。|  
|[輸入項目&#40;DimensionAttribute&#41; &#40;ASSL&#41;](type-element-dimensionattribute-assl.md)|包含屬性的類型。|  
|[輸入項目&#40;MeasureGroup&#41; &#40;ASSL&#41;](type-element-measuregroup-assl.md)|指定 `MeasureGroup` 的類型。|  
|[輸入項目&#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](type-element-measuregroupattribute-assl.md)|包含的型別[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)項目。|  
|[輸入項目&#40;MiningStructureColumn&#41; &#40;ASSL&#41;](type-element-miningstructurecolumn-assl.md)|包含的型別[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)項目。|  
|[輸入項目&#40;資料分割&#41; &#40;ASSL&#41;](type-element-partition-assl.md)|包含 `Partition` 元素的類型。|  
|[輸入項目&#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](type-element-perspectivecalculation-assl.md)|表示的型別[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)項目。|  
|[UnknownMember 元素&#40;ASSL&#41;](unknownmember-element-assl.md)|指出未知的成員是否可見。|  
|[UnknownMemberName 元素&#40;ASSL&#41;](unknownmembername-element-assl.md)|包含維度之未知成員的標題，而這個標題會以維度的預設語言顯示。|  
|[Usage 元素&#40;DimensionAttribute&#41; &#40;ASSL&#41;](usage-element-dimensionattribute-assl.md)|描述如何使用屬性。|  
|[Usage 元素&#40;MiningModelColumn&#41; &#40;ASSL&#41;](usage-element-miningmodelcolumn-assl.md)|描述父 `MiningStructure` 中相關聯資料行的使用方式。|  
|[值項目&#40;ASSL&#41;](value-element-assl.md)|包含父元素的值。|  
|[Version 項目&#40;ASSL&#41;](version-element-assl.md)|包含由 `Server` 元素代表之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的唯讀版本號碼。|  
|[Visibility 元素&#40;ASSL&#41;](visibility-element-assl.md)|定義的可視性[註釋](../objects/annotation-element-assl.md)項目。|  
|[Visible 元素&#40;ASSL&#41;](visible-element-assl.md)|決定父元素的可見性。|  
|[VisualTotals 元素&#40;ASSL&#41;](visualtotals-element-assl.md)|包含決定是否要針對這個屬性之成員顯示視覺化總計的 MDX 運算式。|  
|[寫入項目&#40;ASSL&#41;](write-element-assl.md)|決定是否可以針對給定的 `CubeDimensionPermission` 或 `Permission` 元素寫入資料或中繼資料。|  
|[WriteEnabled 元素&#40;ASSL&#41;](writeenabled-element-assl.md)|指出是否可以使用維度回寫 (受限於安全性權限)。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 元素階層&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
