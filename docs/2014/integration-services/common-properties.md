---
title: 通用屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- external metadata column properties [Integration Services]
- output properties [Integration Services]
- data types [Integration Services], properties
- input properties [Integration Services]
- component properties [Integration Services]
ms.assetid: 51973502-5cc6-4125-9fce-e60fa1b7b796
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ab92e158fe5da6312959cc0797ff48e1c44e0080
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835210"
---
# <a name="common-properties"></a>通用屬性
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中的資料流程物件具有元件層級、輸入和輸出層級，以及輸入資料行和輸出資料行層級上的通用屬性和自訂屬性。 許多屬性都有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
 本主題將列出及描述資料流程物件的通用屬性。  
  
-   [Components](#components)  
  
-   [輸入](#inputs)  
  
-   [輸入資料行](#inputcolumns)  
  
-   [輸出](#outputs)  
  
-   [輸出資料行](#outputcolumns)  
  
 如需有關客戶屬性的詳細資訊，請參閱下列主題  
  
-   [ADO NET 自訂屬性](data-flow/ado-net-custom-properties.md)  
  
-   [CDC 控制工作自訂屬性](control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC 來源自訂屬性](data-flow/cdc-source-custom-properties.md)  
  
-   [資料採礦模型定型目的地自訂屬性](data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [資料讀取元目的地自訂屬性](data-flow/datareader-destination-custom-properties.md)  
  
-   [維度處理目的地自訂屬性](data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel 自訂屬性](data-flow/excel-custom-properties.md)  
  
-   [一般檔案自訂屬性](data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 目的地自訂屬性](data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC 來源自訂屬性](data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB 自訂屬性](data-flow/ole-db-custom-properties.md)OLE DB 自訂屬性  
  
-   [分割區處理目的地自訂屬性](data-flow/partition-processing-destination-custom-properties.md)  
  
-   [原始檔案自訂屬性](data-flow/raw-file-custom-properties.md)  
  
-   [資料錄集目的地自訂屬性](data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 目的地自訂屬性](data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 目的地自訂屬性](data-flow/sql-server-destination-custom-properties.md)  
  
-   [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 來源自訂屬性](data-flow/xml-source-custom-properties.md)  
  
##  <a name="components"></a> 元件屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，資料流程中的元件會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面。  
  
 下表將描述資料流程中的元件屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|元件的 CLSID。|  
|ContactInfo|String|元件開發人員的連絡資訊。|  
|描述|String|資料流程元件的描述。 這個屬性的預設值為資料流程元件的名稱。|  
|ID|Integer|可唯一識別這個元件執行個體的值。|  
|IdentificationString|String|識別此元件。|  
|IsDefaultLocale|布林|指示元件是否使用其所屬之資料流程工作的地區設定。|  
|LocaleID|Integer|當封裝執行時，資料流程元件所使用的地區設定。 所有的 Windows 地區設定都可用於資料流程元件。|  
|名稱|String|資料流程元件的名稱。|  
|PipelineVersion|Integer|專門用來執行元件的資料流程工作版本。|  
|UsesDispositions|布林|指示元件是否有錯誤輸出。|  
|ValidateExternalMetadata|布林|指示是否會驗證外部資料行的中繼資料。 此屬性的預設值為 `True`。|  
|版本|Integer|元件的版本。|  
  
##  <a name="inputs"></a> 輸入的屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，轉換和目的地都有輸入。 資料流程中元件的輸入會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 介面。  
  
 下表將描述資料流程中元件輸入的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|描述|String|輸入的描述。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
|HasSideEffects|布林|指出是否移除從資料流程的執行計畫的元件以及它將不會附加到下游元件時`RunInOptimizedMode`是`true`。|  
|ID|Integer|可唯一識別輸入的值。|  
|IdentificationString|String|識別輸入的字串。|  
|IsSorted|布林|指示是否要排序輸入中的資料。|  
|名稱|String|輸入的名稱。|  
|SourceLocale|Integer|輸入資料的地區設定識別碼 (LCID)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 . 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
  
 目的地和某些轉換不支援錯誤輸出，而且這些元件的 ErrorRowDisposition 和 TruncationRowDisposition 屬性是唯讀的。  
  
###  <a name="inputcolumns"></a> 輸入資料行屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，輸入包含輸入資料行的集合。 資料流程中元件的輸入資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> 介面。  
  
 下表將描述資料流程中元件輸入資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|指定具有字元資料類型之資料行比較的一組旗標。 如需詳細資訊，請參閱 [Comparing String Data](data-flow/comparing-string-data.md)。|  
|描述|String|描述輸入資料行。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|指派給輸入資料行之外部中繼資料行的識別碼。|  
|ID|Integer|可唯一識別輸入資料行的值。|  
|IdentificationString|String|識別輸入資料行的字串。|  
|LineageID|Integer|上游資料行的識別碼。|  
|名稱|String|輸入資料行的名稱。|  
|SortKeyPosition|Integer|指示是否排序資料行、其排序次序以及排序多個資料行之順序的值。 值為 **0** 時，指出資料行並未排序。  如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
|UpstreamComponentName|String|上游元件的名稱。|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|決定元件如何使用輸入資料行的值。|  
  
 輸入資料行也具有資料類型屬性 (如「資料類型屬性」底下所述)。  
  
##  <a name="outputs"></a> 輸出屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，來源和轉換都有輸出。 資料流程中元件的輸出會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 介面。  
  
 下表將描述資料流程中元件輸出的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|布林|決定當從路徑中卸離輸出時，資料流程引擎是否要刪除輸出的值。|  
|描述|String|描述輸出。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
|ExclusionGroup|Integer|識別一組互斥輸出的值。|  
|HasSideEffects|布林|指示當元件未附加到上游元件以及當 `RunInOptimizedMode` 為 `true` 時，是否可以從資料流程的執行計畫中移除此元件的值‧|  
|ID|Integer|可唯一識別輸出的值。|  
|IdentificationString|String|識別輸出的字串。|  
|IsErrorOut|布林|指示輸出是否為錯誤輸出。|  
|IsSorted|布林|指示是否要排序輸出。 預設值是 `False`。<br /><br /> **\*\* 重要\* \*** 的值設定`IsSorted`屬性設`True`不會排序資料。 此屬性僅針對資料先前已經過排序的下游元件提供提示。 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|名稱|String|輸出的名稱。|  
|SynchronousInputID|Integer|與輸出同步之輸入的識別碼。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。|  
  
###  <a name="outputcolumns"></a> 輸出資料行屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，輸出包含輸出資料行的集合。 資料流程中元件的輸出資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> 介面。  
  
 下表將描述資料流程中元件輸出資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|指定具有字元資料類型之資料行比較的一組旗標。 如需詳細資訊，請參閱 [Comparing String Data](data-flow/comparing-string-data.md)。|  
|描述|String|描述輸出資料行。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。 預設值是 `Fail component`。|  
|ExternalMetadataColumnID|Integer|指派給輸入資料行之外部中繼資料行的識別碼。|  
|ID|Integer|可唯一識別輸出資料行的值。|  
|IdentificationString|String|識別輸出資料行的字串。|  
|LineageID|Integer|輸出資料行的識別碼。 下游元件會使用這個值來參考此資料行。|  
|名稱|String|輸出資料行的名稱。|  
|SortKeyPosition|Integer|指示是否排序資料行、其排序次序以及排序多個資料行之順序的值。 值為 **0** 時，指出資料行並未排序。 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|SpecialFlags|Integer|包含輸出資料行之特殊旗標的值。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值為 `Fail component`、`Ignore failure` 和 `Redirect row`。 預設值是 `Fail component`。|  
  
 輸出資料行也包含一組資料類型屬性。  
  
## <a name="external-metadata-column-properties"></a>外部中繼資料行屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，輸入和輸出都可以包含外部中繼資料行的集合。 資料流程中元件的外部中繼資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 介面。  
  
 下表將描述資料流程中元件之外部中繼資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|描述|String|描述外部資料行。|  
|ID|Integer|可唯一識別此資料行的值。|  
|IdentificationString|String|識別此資料行的字串。|  
|名稱|String|外部資料行的名稱。|  
  
 外部中繼資料行也包含一組資料類型屬性。  
  
## <a name="data-type-properties"></a>資料類型屬性  
 輸出資料行和外部中繼資料行也包含一組資料類型屬性。 根據此資料行的資料類型而定，屬性可以是可讀寫或唯讀。  
  
 下表將描述輸出資料行和外部中繼資料行的資料類型屬性。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|CodePage|Integer|指定字串資料的字碼頁不是 Unicode。|  
|DataType|整數 (列舉)|資料行的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。|  
|長度|Integer|資料行的長度 (以字元為測量單位)。|  
|有效位數|Integer|數值資料行的有效位數。|  
|小數位數|Integer|數值資料行的小數位數。|  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](data-flow/data-flow.md)   
 [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)   
 [路徑屬性](../../2014/integration-services/path-properties.md)   
 [可以使用運算式設定的資料流程屬性](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
