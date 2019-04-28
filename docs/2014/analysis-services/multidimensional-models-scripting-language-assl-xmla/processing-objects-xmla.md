---
title: 處理物件 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab38ea9b58e891d813a3ca73f43d20a364275da0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727594"
---
# <a name="processing-objects-xmla"></a>處理物件 (XMLA)
  在  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 處理是在步驟或一系列的步驟轉換資料成供商務分析的資訊。 處理會因物件類型而異，但是處理永遠都是將資料轉換為資訊的一部分。  
  
 程序[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件，您可以使用[程序](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)命令。 `Process` 命令可以處理在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的下列物件：  
  
-   Cube  
  
-   資料庫  
  
-   維度  
  
-   量值群組  
  
-   採礦模型  
  
-   採礦結構  
  
-   資料分割  
  
 若要控制物件的處理，`Process` 命令具有各種可以設定的屬性。 `Process` 命令具有可控制以下動作的屬性：將完成多少處理、將處理哪些物件、是否使用非正規的繫結、如何處理錯誤以及如何管理回寫資料表。  
  
## <a name="specifying-processing-options"></a>指定處理選項  
 [型別](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)屬性`Process`命令會指定處理物件時要使用的處理選項。 如需處理選項的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 下表列出 `Type` 屬性的常數，以及各種可使用每個常數處理的物件。  
  
|`Type` 值|適用的物件|  
|--------------------|------------------------|  
|*ProcessFull*|Cube、資料庫、維度、量值群組、採礦模型、採礦結構、資料分割|  
|*ProcessAdd*|維度、資料分割|  
|*ProcessUpdate*|維度|  
|*ProcessIndexes*|維度、Cube、量值群組，磁碟分割|  
|*ProcessData*|維度、Cube、量值群組，磁碟分割|  
|*ProcessDefault*|Cube、資料庫、維度、量值群組、採礦模型、採礦結構、資料分割|  
|*ProcessClear*|Cube、資料庫、維度、量值群組、採礦模型、採礦結構、資料分割|  
|*ProcessStructure*|Cube、採礦結構|  
|*ProcessClearStructureOnly*|採礦結構|  
|*ProcessScriptCache*|Cube|  
  
 如需有關處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件，請參閱[多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
## <a name="specifying-objects-to-be-processed"></a>指定要處理的物件  
 [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性`Process`命令中包含要處理之物件的物件識別碼。 在 `Process` 命令中只能指定一個物件，但是處理物件也會處理任何子系物件。 例如，在 Cube 處理序中處理量值群組會處理該量值群組的所有資料分割，然而處理資料庫處理序則會處理資料庫包含的所有物件，包括 Cube、維度和採礦結構。  
  
 如果您將 `ProcessAffectedObjects` 命令的 `Process` 屬性設定為 True，則也會處理指定物件所影響的任何相關物件。 例如，如果使用以累加方式更新的維度*ProcessUpdate*處理中的選項`Process`命令時，也是其彙總都會變成無效，因為加入或刪除成員的任何磁碟分割由處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如果`ProcessAffectedObjects`設為 true。 在這種情況下，單一 `Process` 命令可以處理在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的多個物件，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會決定除了在 `Process` 命令中指定的單一物件之外，還必須處理哪些物件。  
  
 不過，您可以使用 `Process` 命令中的 `Batch` 命令來同時處理多個物件 (例如維度)。 相較於使用 `ProcessAffectedObjects` 屬性，批次作業在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上依序或平行處理物件時，提供更細的控制層級，而且可讓您為較大的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫調整您的處理方法。 如需有關執行批次作業的詳細資訊，請參閱 <<c0> [ 執行批次運算&#40;XMLA&#41;](performing-batch-operations-xmla.md)。</c0>  
  
## <a name="specifying-out-of-line-bindings"></a>指定非正規繫結  
 如果`Process`命令未包含之`Batch`命令，您可以選擇性地指定中的程式碼外部繫結[繫結](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)， [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)，和[DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)屬性的`Process`命令要處理的物件。 非正規 (out-of-line) 繫結是資料來源、資料來源檢視以及其他物件的參考，其中繫結只會在 `Process` 命令執行期間存在，而且會覆寫任何與要處理的物件關聯的現有繫結。 如果未指定非正規 (out-of-line) 繫結，會使用與要處理的物件目前關聯的繫結。  
  
 非正規 (out-of-line) 繫結用於在下列情況：  
  
-   以累加方式處理資料分割，其中必須指定替代的事實資料表或是在現有事實資料表上的篩選，以確定不會計數資料列兩次。  
  
-   使用中的資料流程工作[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]來處理維度、 採礦模型或資料分割時提供資料。  
  
 非正規繫結 (out-of-line) 是以 Analysis Services 指令碼語言 (ASSL) 的一部分來描述。 如需有關 ASSL 中非正規 out-of-line 繫結的詳細資訊，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
### <a name="incrementally-updating-partitions"></a>以累加方式更新資料分割  
 以累加方式更新已經處理的資料分割通常需要非正規繫結 (out-of-line)，因為針對資料分割所指定的繫結，會參考已經在資料分割中彙總的事實資料表資料。 當使用 `Process` 命令時，以累加方式更新已經處理的資料分割時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會執行下列動作：  
  
-   建立一個與要以累加方式更新的資料分割有相同結構的暫存資料分割。  
  
-   使用在 `Process` 命令中指定的非正規繫結 (out-of-line) 來處理暫存資料分割。  
  
-   以現有選取的資料分割，合併暫存資料分割。  
  
 如需有關合併資料分割使用 XML for Analysis (XMLA) 的詳細資訊，請參閱[合併的分割區&#40;XMLA&#41;](merging-partitions-xmla.md)。  
  
## <a name="handling-processing-errors"></a>處理在處理時發生的錯誤  
 [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)屬性`Process`命令可讓您指定如何處理在處理物件時發生錯誤。 例如，處理維度時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在索引鍵屬性的索引鍵資料行中遇到重複的值。 由於屬性索引鍵必須是唯一的，所以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會捨棄重複的記錄。 根據[KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl)屬性`ErrorConfiguration`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]無法：  
  
-   忽略錯誤並繼續處理維度。  
  
-   傳回訊息以說明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遇到重複的索引鍵並繼續處理。  
  
 當 `ErrorConfiguration` 在 `Process` 命令期間提供選項時，有許多類似的狀況。  
  
## <a name="managing-writeback-tables"></a>管理回寫資料表  
 如果 `Process` 命令遇到可寫入的資料分割，或是這類資料分割尚未完全處理的 Cube 或是量值群組，該資料分割可能不會有已經存在的回寫資料表。 [WritebackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla)屬性`Process`命令會判斷是否[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]應該建立回寫資料表。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會完整處理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
### <a name="code"></a>程式碼  
  
```  
<Process xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>描述  
 下列範例以累加方式處理**Internet_Sales_2004**分割區**Internet Sales**量值群組**Adventure Works DW** 中的cube[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 `Process`命令會將彙總加入訂單日期晚於 2006 年 12 月 31 日到分割區使用中的程式碼外部查詢繫結`Bindings`屬性`Process`命令來擷取要用於產生的事實資料表資料列若要加入資料分割的彙總。  
  
### <a name="code"></a>程式碼  
  
```  
<Process ProcessAffectedObjects="true" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
