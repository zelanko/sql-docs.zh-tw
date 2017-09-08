---
title: "物件 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 749c363a814590705b61d0821f1fee44ea93d488
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="objects-assl"></a>物件 (ASSL)
  這個參考章節包含在「Analysis Services 指令碼語言」(ASSL) 結構描述中當做物件之每個元素的語法和使用方式資訊。  
  
 雖然 ASSL 結構描述僅包含 XML 元素，從開發人員的觀點來看，這一節所述的元素對應至物件，例如**資料庫**， **Cube**，和**維度**的執行個體所包含的物件階層中的物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 雖然物件絕對不是 ASSL 結構描述中的分葉層級元素，但是會具有對應至物件屬性的子元素和元素。  
  
 在少數情況下，結構描述中可能會顯示成屬性的分葉層級元素會分類成物件，因為元素的類型是物件類型。 例如，**來源**的**維度**物件屬於類型**DimensionBinding**。  
  
## <a name="in-this-section"></a>本節內容  
  
|元素|Description|  
|-------------|-----------------|  
|[Account 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|包含內部帳戶類型的詳細[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[Action 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|包含中可用動作的相關資訊[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[Aggregation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|定義單一彙總[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目。|  
|[AggregationDesign 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|定義可在資料庫中多個分割區之間共用之彙總定義的集合。|  
|[AggregationInstance 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|定義資料分割的彙總執行個體。|  
|[AlgorithmParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|定義所使用之演算法參數[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[AllMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|包含之 All 成員標題的翻譯[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。|  
|[註釋項目 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|包含用來擴充 ASSL 結構描述的元素。|  
|[組件元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|代表[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件或 COM 動態連結程式庫 (DLL) 相關聯[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目或[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[Attribute 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|包含屬性的描述。|  
|[AttributeAllMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|包含之 All 成員標題的翻譯[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)項目。|  
|[AttributePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|定義的權限的成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素中個別維度屬性上有[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[AttributeRelationship 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|提供有關兩個屬性之間關聯性的詳細資料。|  
|[Block 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|包含所有或部分二進位內容的[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。|  
|[Calculation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|將計算與[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[CalculationProperty 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|包含的使用者介面中使用之計算的屬性集合[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)項目。|  
|[CaptionColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|定義可提供屬性標題的資料行。|  
|[CellPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|描述的權限的成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素內部個別資料格有[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[Column 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|描述與父元素相關聯之資料行集合中的資料行。|  
|[Command 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|定義可在 Commands 集合之父元素內容內部使用的命令。|  
|[Cube 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|定義中的一般、 虛擬或連結 cube [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[CubePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|定義特定成員的權限[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素中特殊[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[CustomRollupColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|定義提供自訂積存公式之資料行的詳細資料。|  
|[CustomRollupPropertiesColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|定義提供自訂積存公式屬性之資料行的詳細資料。|  
|[資料元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|包含 (子系的集合中**區塊**項目) 的二進位內容[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。|  
|[Database 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|定義 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫。|  
|[DatabasePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|定義中的預設權限[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)特定的項目[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。|  
|[DataSource 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|定義中的資料來源[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[DataSourcePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|定義中的預設權限[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)特定的資料型別[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。|  
|[DataSourceView 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|定義所使用的資料來源檢視[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。|  
|[Dimension 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|定義維度。|  
|[DimensionPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|定義屬於特定的權限[角色](../../../analysis-services/scripting/objects/role-element-assl.md)特定資料庫維度或 cube 維度的項目。|  
|[ErrorConfiguration 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|指定在處理父元素時可能會發生之錯誤的處理設定。|  
|[Event 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|定義事件擷取成一部分[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目。|  
|[File 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|撰寫的檔案會定義[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)項目。|  
|[ForeignKeyColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|識別關聯式資料來源之父資料表的聯結。|  
|[Group 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|定義繫結至屬性的成員群組。|  
|[Hierarchy 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|定義維度中的階層。|  
|[IncrementalProcessingNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|包含的資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷累加式處理進度所執行之查詢的項目。|  
|[KeyColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|包含屬於屬性索引鍵或其中一部分之資料行的定義。|  
|[Kpi 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|定義關鍵效能指標 (KPI) 內[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。|  
|[Level 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|定義中的層級[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。|  
|[MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|包含相關聯的多維度運算式 (MDX) 指令碼的相關資訊[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[Measure 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|定義量值。|  
|[MeasureGroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|定義位於相同資料粒度層級的一組量值。|  
|[Member 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|包含的成員名稱[群組](../../../analysis-services/scripting/objects/group-element-assl.md)項目或[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。|  
|[MiningModel 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|定義單一資料採礦模型。|  
|[MiningModelPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|定義的權限成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)針對個別的項目有[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。|  
|[MiningStructure 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|定義一組採礦模型的結構。|  
|[MiningStructurePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|定義的權限的成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)針對個別的項目有[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。|  
|[ModelingFlag 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|包含採礦結構或採礦模型中某個資料行的模型旗標。|  
|[NameColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|識別提供父元素名稱的資料行。|  
|[NamingTemplateTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|提供當地語系化的翻譯的**NamingTemplate**父項目[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)資料型別。|  
|[Partition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|定義的資料分割[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)項目或資料分割繫結中的行外[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)項目。|  
|[Perspective 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|定義檢視方塊的詳細資料[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。|  
|[ProactiveCaching 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|定義父元素的主動式快取設定。|  
|[QueryNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|包含的資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷資料來源是否已經修改所執行之查詢的項目。|  
|[ReportFormatParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|包含名稱和值的參數來指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]格式化報表在執行階段。|  
|[ReportParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|包含在執行階段傳遞給 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表之參數的名稱和值。|  
|[Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|包含有關安全性角色的資訊。|  
|[Server 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。|  
|[ServerProperty 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|定義相關聯的伺服器屬性[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。|  
|[SkippedLevelsColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|提供儲存每個成員與其父系之間略過 (空白) 之層級數目的資料行詳細資料。|  
|[SourceMeasureGroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|識別當做採礦結構資料行之資料來源的量值群組。|  
|[TableNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|包含的資訊[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關的資料表或檢視已經修改資料來源中的項目。|  
|[Trace 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|定義可查詢的追蹤。|  
|[Translation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|提供當地語系化的翻譯給父代[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)集合。|  
|[UnaryOperatorColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|定義提供一元運算子之資料行的詳細資料。|  
|[UnknownMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|包含標題的翻譯[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)元素[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)項目。|  
|[ValueColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|識別提供父元素之值的資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 元素階層 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
