---
description: 設定資料流程元件的屬性
title: 設定資料流程元件的屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c7799b5d2f5f541b6713821dccbec820697371ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88348944"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>設定資料流程元件的屬性

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  若要設定資料流程元件的屬性 (包括來源、目的地和轉換)，請使用下列其中一個功能：  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的元件編輯器。 這些編輯器僅包括每個資料流程元件的自訂屬性。  
  
-   [屬性]**** 視窗會列出每個元素的元件層級自訂屬性，以及所有資料流程元素通用的屬性。  
  
-   [進階編輯器]**** 對話方塊可讓您存取每一個元件的自訂屬性。 [進階編輯器] 對話方塊也可讓您存取所有資料流程元件的屬性，也就是輸入、輸出、錯誤輸出、資料行和外部資料行的屬性。  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>使用元件編輯器設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程]**** 索引標籤，然後按兩下包含資料流程 (具有您要檢視及修改其屬性之元件) 的「資料流程」工作。  
  
4.  按兩下資料流程元件。  
  
5.  在元件編輯器中，檢視或修改屬性值，然後關閉編輯器。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>在屬性視窗中設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程]**** 索引標籤，然後按兩下包含您要檢視及修改其屬性之元件的「資料流程」工作。  
  
4.  以滑鼠右鍵按一下資料流程元件，然後按一下 [屬性]****。  
  
5.  檢視或修改屬性值，然後關閉 [屬性]**** 視窗。  
  
    > [!NOTE]  
    >  許多屬性都是唯讀的，因此無法修改。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>使用進階編輯器設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程]**** 索引標籤，然後按兩下包含您要檢視或修改之元件的「資料流程」工作。  
  
4.  在資料流程設計師中，以滑鼠右鍵按一下資料流程元件，然後按一下 [顯示進階編輯器]****。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，支援多個輸入的資料流程元件無法使用 [進階編輯器]****。  
  
5.  在 [進階編輯器]**** 對話方塊中，執行下列任何一個步驟：  
  
    -   若要檢視及指定此元件所使用的連接，請按一下 [連線管理員]**** 索引標籤。  
  
        > [!NOTE]  
        >  [連線管理員]**** 索引標籤只可用於使用連線管理員連接到資料來源 (例如檔案和資料庫) 的資料流程元件  
  
    -   若要檢視和修改元件層級屬性，請按一下 [元件屬性]**** 索引標籤。  
  
    -   若要檢視和修改外部資料行與可用輸出之間的對應，請按一下 [資料行對應]**** 索引標籤。  
  
        > [!NOTE]  
        >  [資料行對應]**** 索引標籤只能在檢視或編輯來源或目的地時使用。  
  
    -   若要檢視可用輸入資料行的清單並更新輸出資料行的名稱，請按一下 [輸入資料行]**** 索引標籤。  
  
        > [!NOTE]  
        >  [輸入資料行] 索引標籤僅在使用轉換或目的地時可用。 如需詳細資訊，請參閱 [Integration Services 轉換](../../integration-services/data-flow/transformations/integration-services-transformations.md)。  
  
    -   若要檢視和修改輸入、輸出及錯誤輸出的屬性，以及檢視和修改其包含之資料行的屬性，請按一下 [輸入與輸出屬性]**** 索引標籤。  
  
        > [!NOTE]  
        >  來源沒有輸入。 除了選擇性的錯誤輸出之外，目的地沒有輸出。  
  
6.  檢視或修改屬性值。  
  
7.  按一下 [確定]  。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  

## <a name="common-properties-of-data-flow-components"></a>資料流程元件的通用屬性
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中的資料流程物件具有元件層級、輸入和輸出層級，以及輸入資料行和輸出資料行層級上的通用屬性和自訂屬性。 許多屬性都有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
 本主題將列出及描述資料流程物件的通用屬性。  
  
-   [Components](#components)  
  
-   [輸入](#inputs)  
  
-   [輸入資料行](#inputcolumns)  
  
-   [輸出](#outputs)  
  
-   [輸出資料行](#outputcolumns)  
  
 
###  <a name="component-properties"></a><a name="components"></a> 元件屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，資料流程中的元件會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面。  
  
 下表將描述資料流程中的元件屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|元件的 CLSID。|  
|ContactInfo|String|元件開發人員的連絡資訊。|  
|描述|String|資料流程元件的描述。 這個屬性的預設值為資料流程元件的名稱。|  
|ID|整數|可唯一識別這個元件執行個體的值。|  
|IdentificationString|String|識別此元件。|  
|IsDefaultLocale|布林值|指示元件是否使用其所屬之資料流程工作的地區設定。|  
|LocaleID|整數|當封裝執行時，資料流程元件所使用的地區設定。 所有的 Windows 地區設定都可用於資料流程元件。|  
|Name|String|資料流程元件的名稱。|  
|PipelineVersion|整數|專門用來執行元件的資料流程工作版本。|  
|UsesDispositions|布林值|指示元件是否有錯誤輸出。|  
|ValidateExternalMetadata|Boolean|指示是否會驗證外部資料行的中繼資料。 這個屬性的預設值為 **True**。|  
|版本|整數|元件的版本。|  
  
###  <a name="input-properties"></a><a name="inputs"></a> 輸入屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，轉換和目的地都有輸入。 資料流程中元件的輸入會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 介面。  
  
 下表將描述資料流程中元件輸入的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|描述|String|輸入的描述。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
|HasSideEffects|布林值|指示當元件未附加到下游元件以及當 **RunInOptimizedMode** 為 **true**時，是否可以從資料流程的執行計畫中移除此元件。|  
|ID|整數|可唯一識別輸入的值。|  
|IdentificationString|String|識別輸入的字串。|  
|IsSorted|布林值|指示是否要排序輸入中的資料。|  
|Name|String|輸入的名稱。|  
|SourceLocale|整數|輸入資料的地區設定識別碼 (LCID)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 . 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
  
 目的地和某些轉換不支援錯誤輸出，而且這些元件的 ErrorRowDisposition 和 TruncationRowDisposition 屬性是唯讀的。  
  
###  <a name="input-column-properties"></a><a name="inputcolumns"></a> 輸入資料行屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，輸入包含輸入資料行的集合。 資料流程中元件的輸入資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> 介面。  
  
 下表將描述資料流程中元件輸入資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComparisonFlags|整數|指定具有字元資料類型之資料行比較的一組旗標。 如需詳細資訊，請參閱 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)。|  
|描述|String|描述輸入資料行。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|指派給輸入資料行之外部中繼資料行的識別碼。|  
|ID|整數|可唯一識別輸入資料行的值。|  
|IdentificationString|String|識別輸入資料行的字串。|  
|LineageID|整數|上游資料行的識別碼。|  
|LineageIdentificationString|String|包含上游資料行名稱的識別字串。|  
|Name|String|輸入資料行的名稱。|  
|SortKeyPosition|整數|指示是否排序資料行、其排序次序以及排序多個資料行之順序的值。 值為 **0** 時，指出資料行並未排序。  如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
|UpstreamComponentName|String|上游元件的名稱。|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|決定元件如何使用輸入資料行的值。|  
  
 輸入資料行也具有資料類型屬性 (如「資料類型屬性」底下所述)。  
  
###  <a name="output-properties"></a><a name="outputs"></a> 輸出屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，來源和轉換都有輸出。 資料流程中元件的輸出會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 介面。  
  
 下表將描述資料流程中元件輸出的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|布林值|決定當從路徑中卸離輸出時，資料流程引擎是否要刪除輸出的值。|  
|描述|String|描述輸出。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
|ExclusionGroup|整數|識別一組互斥輸出的值。|  
|HasSideEffects|布林值|指示當元件未附加到上游元件以及當 **RunInOptimizedMode** 為 **true**時，是否可以從資料流程的執行計畫中移除此元件的值。|  
|ID|整數|可唯一識別輸出的值。|  
|IdentificationString|String|識別輸出的字串。|  
|IsErrorOut|布林值|指示輸出是否為錯誤輸出。|  
|IsSorted|布林值|指示是否要排序輸出。 預設值為 **[False]** 。<br /><br /> **\*\* 重要事項 \*\*** 將 **IsSorted** 屬性的值設定為 **True** 時，不會排序資料。 此屬性僅針對資料先前已經過排序的下游元件提供提示。 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|Name|String|輸出的名稱。|  
|SynchronousInputID|整數|與輸出同步之輸入的識別碼。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。|  
  
###  <a name="output-column-properties"></a><a name="outputcolumns"></a> 輸出資料行屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，輸出包含輸出資料行的集合。 資料流程中元件的輸出資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> 介面。  
  
 下表將描述資料流程中元件輸出資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ComparisonFlags|整數|指定具有字元資料類型之資料行比較的一組旗標。 如需詳細資訊，請參閱 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)。|  
|描述|String|描述輸出資料行。|  
|ErrorOrTruncationOperation|String|指定處理資料列時發生之錯誤或截斷類型的選擇性字串。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|指定錯誤處理的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。 預設值為 [失敗元件]****。|  
|ExternalMetadataColumnID|整數|指派給輸入資料行之外部中繼資料行的識別碼。|  
|ID|整數|可唯一識別輸出資料行的值。|  
|IdentificationString|String|識別輸出資料行的字串。|  
|LineageID|整數|輸出資料行的識別碼。 下游元件會使用這個值來參考此資料行。|  
|LineageIdentificationString|String|包含資料行名稱的識別字串。|  
|Name|String|輸出資料行的名稱。|  
|SortKeyPosition|整數|指示是否排序資料行、其排序次序以及排序多個資料行之順序的值。 值為 **0** 時，指出資料行並未排序。 如需詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。|  
|SpecialFlags|整數|包含輸出資料行之特殊旗標的值。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|決定元件如何處理當處理資料列時發生之截斷的值。 這些值包括 [失敗元件]****、[忽略失敗]**** 和 [重新導向資料列]****。 預設值為 [失敗元件]****。|  
  
 輸出資料行也包含一組資料類型屬性。  
  
### <a name="external-metadata-column-properties"></a>外部中繼資料行屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，輸入和輸出都可以包含外部中繼資料行的集合。 資料流程中元件的外部中繼資料行會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 介面。  
  
 下表將描述資料流程中元件之外部中繼資料行的屬性。 某些屬性具有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|描述|String|描述外部資料行。|  
|ID|整數|可唯一識別此資料行的值。|  
|IdentificationString|String|識別此資料行的字串。|  
|Name|String|外部資料行的名稱。|  
  
 外部中繼資料行也包含一組資料類型屬性。  
  
### <a name="data-type-properties"></a>資料類型屬性  
 輸出資料行和外部中繼資料行也包含一組資料類型屬性。 根據此資料行的資料類型而定，屬性可以是可讀寫或唯讀。  
  
 下表將描述輸出資料行和外部中繼資料行的資料類型屬性。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|CodePage|整數|指定字串資料的字碼頁不是 Unicode。|  
|DataType|整數 (列舉)|資料行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|長度|整數|資料行的長度 (以字元為測量單位)。|  
|精確度|整數|數值資料行的有效位數。|  
|調整|整數|數值資料行的小數位數。|  

## <a name="custom-properties-of-data-flow-components"></a>資料流程元件的自訂屬性
如需自訂屬性的資訊，請參閱下列主題  
  
-   [ADO NET 自訂屬性](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [CDC 控制工作自訂屬性](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC 來源自訂屬性](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [資料採礦模型定型目的地自訂屬性](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [DataReader 目的地自訂屬性](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [維度處理目的地自訂屬性](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel 自訂屬性](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 目的地自訂屬性](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB 自訂屬性](../../integration-services/data-flow/ole-db-custom-properties.md)OLE DB 自訂屬性  
  
-   [資料分割處理目的地自訂屬性](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [原始檔案自訂屬性](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [資料錄集目的地自訂屬性](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 目的地自訂屬性](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 目的地自訂屬性](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [轉換自訂屬性](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 來源自訂屬性](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>在資料流程元件中使用運算式
此程序描述如何將運算式加入「條件式分割」轉換或「衍生的資料行」轉換。 「條件式分割」轉換會使用運算式，定義將資料列導向轉換輸出的條件，而「衍生的資料行」轉換則使用運算式，定義指派給資料行的值。  
  
 若要在轉換中實作運算式，封裝必須至少包括一個「資料流程」工作和一個來源。 
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，按一下 [控制流程]**** 索引標籤，然後再按包含要在其中實作運算式之資料流程的「資料流程」工作。  
  
4.  按一下 [資料流程]**** 索引標籤，然後將「條件式分割」或「衍生的資料行」轉換，從 [工具箱]**** 拖曳至設計介面。  
  
5.  將綠色連接子從來源或轉換拖曳至「條件式分割」或「衍生的資料行」轉換。  
  
6.  按兩下轉換，以開啟其對話方塊。  
  
7.  在左窗格中，展開 [變數]****，以顯示系統變數和使用者自訂變數，並展開 [資料行]****，以顯示轉換輸入資料行。  
  
8.  在右窗格中，展開 [數學函數]****、[字串函數]****、[日期/時間函數]****、[NULL 函數]****、[類型轉換]**** 和 [運算子]****，以存取運算式文法所提供的函數、轉換和運算子。  
  
9. 因轉換的不同，請執行下列其中之一，以建立運算式：  
  
    -   在 [條件式分割轉換編輯器]**** 對話方塊中，將變數、資料行、函數、運算子和轉換拖曳至 [條件]**** 資料行。 您也可以在 [條件]**** 資料行中直接鍵入運算式。  
  
    -   在 [衍生的資料行轉換編輯器]**** 對話方塊中，將變數、資料行、函數、運算子和轉換拖曳至 [運算式]**** 資料行。 您也可以在 [運算式]**** 資料行中直接鍵入運算式。  
  
        > [!NOTE]  
        >  從 [條件]**** 資料行或 [運算式]**** 資料行移除焦點時，運算式文字可能會反白顯示，指示運算式語法不正確。  
  
10. 按一下 **[確定]**，結束對話方塊。  
  
    > [!NOTE]  
    >  如果運算式無效，則會出現警示，描述運算式中的語法錯誤。  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>您可以使用運算式設定的資料流程屬性
可使用「資料流程」工作容器上提供的屬性運算式，以指定資料流程物件的某些屬性值。  
  
 如需使用屬性運算式的資訊，請參閱 [在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
 您可以使用屬性運算式來為封裝之每個部署的執行個體自訂組態。 您也可以使用屬性運算式來指定封裝的執行階段條件約束，其方法是搭配 **dtexec** 命令提示字元公用程式使用 **/set** 選項。 例如，您可以約束「排序」轉換所使用的 **MaximumThreads** ，或是「模糊群組」和「模糊查閱」轉換所使用的 **MaxMemoryUsage** 。 如果未受到約束，這些轉換可能會在記憶體中快取大量的資料。  
  
 若要針對本主題所列的其中一個資料流程物件屬性指定屬性運算式，請顯示資料流程工作的 [屬性]**** 視窗，其方式是在設計工具的 [控制流程]**** 介面上選取資料流程工作，或是選取設計工具的 [資料流程]**** 索引標籤，而不需選取任何個別的元件或路徑。 選取 [運算式]**** 屬性，然後按一下省略符號 (...)，顯示 [屬性運算式編輯器]**** 對話方塊。 下拉 [屬性]**** 清單來選取屬性，然後在 [運算式]**** 文字方塊中輸入運算式，或是按一下省略符號 (...) 以顯示 [運算式產生器]**** 對話方塊。  
  
 [屬性]**** 清單只會針對您已經放在設計工具之 [資料流程]**** 介面上的那些資料流程物件來顯示可用的屬性。 因此，您無法使用 [屬性]**** 清單來檢視支援屬性運算式之資料流程物件的所有可能屬性。 例如，如果您已經在設計工具介面上放置 ADO NET 來源，則 [屬性]**** 清單會包含 **[ADO NET Source].[SqlCommand]** 屬性的項目。 此清單也會顯示資料流程工作本身的許多屬性。  
 
 可以使用屬性運算式來指定下列清單中的屬性值。  
  
### <a name="data-flow-sources"></a>資料流程來源  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|ADO NET 來源|TableOrViewName 屬性<br /><br /> SqlCommand 屬性|  
|XML 來源|XMLData 屬性<br /><br /> XMLSchemaDefinition 屬性|  
  
### <a name="data-flow-transformations"></a>資料流程轉換  
 如需這些自訂屬性的詳細資訊，請參閱 [轉換自訂屬性](../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|條件式分割轉換|FriendlyExpression 屬性|  
|衍生的資料行轉換|FriendlyExpression 屬性|  
|模糊群組轉換|MaxMemoryUsage 屬性|  
|模糊查閱轉換|MaxMemoryUsage 屬性|  
|查閱轉換|SqlCommand 屬性<br /><br /> SqlCommandParam 屬性|  
|OLE DB 命令轉換|SqlCommand 屬性|  
|百分比取樣轉換|SamplingValue 屬性|  
|樞紐轉換|PivotKeyValue 屬性|  
|資料列取樣轉換|SamplingValue 屬性|  
|排序轉換|MaximumThreads 屬性|  
|取消樞紐轉換|PivotKeyValue 屬性|  
  
### <a name="data-flow-destinations"></a>資料流程目的地  
  
|資料流程物件|屬性|  
|----------------------|--------------|  
|ADO NET 目的地|TableOrViewName 屬性<br /><br /> BatchSize 屬性<br /><br /> CommandTimeout 屬性|  
|一般檔案目的地|Header 屬性|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地|TableName 屬性|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地|BulkInsertTableName 屬性<br /><br /> BulkInsertFirstRow 屬性<br /><br /> BulkInsertLastRow 屬性<br /><br /> BulkInsertOrder 屬性<br /><br /> Timeout 屬性|  

