---
title: "處理物件 (XMLA) |Microsoft 文件"
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
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dfc2fafb76d19ea986b697ec065abec738f4c05
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="processing-objects-xmla"></a>處理物件 (XMLA)
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 處理是在步驟或一系列的步驟將資料轉換成供商務分析資訊。 處理會因物件類型而異，但是處理永遠都是將資料轉換為資訊的一部分。  
  
 處理序[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件，您可以使用[程序](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令。 **程序**命令可以處理下列物件上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體：  
  
-   Cube  
  
-   資料庫  
  
-   維度  
  
-   量值群組  
  
-   採礦模型  
  
-   採礦結構  
  
-   資料分割  
  
 若要控制的物件，處理**程序**命令具有各種可以設定的屬性。 **程序**命令具有控制的屬性： 將完成多少處理、 將處理哪些物件、 是否要使用-單行繫結、 如何處理錯誤，以及如何管理回寫資料表。  
  
## <a name="specifying-processing-options"></a>指定處理選項  
 [類型](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md)屬性**程序**命令會指定處理物件時要使用的處理選項。 如需處理選項的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 下表列出的常數**類型**屬性和可使用每個常數處理的各種物件。  
  
|**型別**值|適用的物件|  
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
  
 如需有關處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件，請參閱[處理多維度模型 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>指定要處理的物件  
 [物件](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)屬性**程序**命令包含要處理之物件的物件識別碼。 中，可以指定只有一個物件**程序**命令，但是處理物件也會處理任何子物件。 例如，在 Cube 處理序中處理量值群組會處理該量值群組的所有資料分割，然而處理資料庫處理序則會處理資料庫包含的所有物件，包括 Cube、維度和採礦結構。  
  
 如果您設定**ProcessAffectedObjects**屬性**程序**命令為 true 時，任何相關的處理指定的物件所影響的物件也會處理。 例如，如果維度以累加方式更新使用*ProcessUpdate*處理中的選項**程序**命令時，其彙總都會變成無效，因為成員的任何磁碟分割正在加入或刪除也會處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如果**ProcessAffectedObjects**設為 true。 在這個情況下，單一**程序**命令可以處理多個物件上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，但[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]決定哪些物件中指定的單一物件除了**程序**也必須處理命令。  
  
 不過，您可以使用多個同時處理多個物件，例如維度、**程序**命令中**批次**命令。 批次作業進行更細微的層級控制的序列或平行處理的物件上提供[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]比使用的執行個體**ProcessAffectedObjects**屬性，並讓您調整您的處理方法更大[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 如需有關執行批次作業的詳細資訊，請參閱[執行批次作業 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>指定非正規繫結  
 如果**程序**命令未包含**批次**命令，您可以選擇性地指定-單行中的繫結[繫結](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)， [資料來源](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)，和[DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)屬性**程序**命令處理物件。 單行繫結就是資料來源、 資料來源檢視，以及繫結只會在執行期間的存在其他物件的參考**程序**命令，而且會覆寫任何現有的繫結相關聯正在處理的物件。 如果未指定非正規 (out-of-line) 繫結，會使用與要處理的物件目前關聯的繫結。  
  
 非正規 (out-of-line) 繫結用於在下列情況：  
  
-   以累加方式處理資料分割，其中必須指定替代的事實資料表或是在現有事實資料表上的篩選，以確定不會計數資料列兩次。  
  
-   使用資料流程工作中的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]處理維度、 採礦模型或資料分割時提供資料。  
  
 非正規繫結 (out-of-line) 是以 Analysis Services 指令碼語言 (ASSL) 的一部分來描述。 如需有關 ASSL 中-單行繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>以累加方式更新資料分割  
 以累加方式更新已經處理的資料分割通常需要非正規繫結 (out-of-line)，因為針對資料分割所指定的繫結，會參考已經在資料分割中彙總的事實資料表資料。 以累加方式更新已經處理的分割區使用時**程序**命令，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行下列動作：  
  
-   建立一個與要以累加方式更新的資料分割有相同結構的暫存資料分割。  
  
-   處理暫存資料分割，使用指定的-單行繫結**程序**命令。  
  
-   以現有選取的資料分割，合併暫存資料分割。  
  
 如需有關合併資料分割使用 XML for Analysis (XMLA) 的詳細資訊，請參閱[合併分割區 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>處理在處理時發生的錯誤  
 [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md)屬性**程序**命令可讓您指定如何處理在處理物件時發生錯誤。 例如，處理維度時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在索引鍵屬性的索引鍵資料行中遇到重複的值。 由於屬性索引鍵必須是唯一的，所以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會捨棄重複的記錄。 根據[KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md)屬性**ErrorConfiguration**，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]無法：  
  
-   忽略錯誤並繼續處理維度。  
  
-   傳回訊息以說明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遇到重複的索引鍵並繼續處理。  
  
 有許多類似的狀況**ErrorConfiguration**期間提供選項**程序**命令。  
  
## <a name="managing-writeback-tables"></a>管理回寫資料表  
 如果**程序**命令遇到可寫入分割區或這類的資料分割，尚未完全處理的 cube 或量值群組、 回寫資料表可能不存在該資料分割。 [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md)屬性**程序**命令會判斷是否[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]應該建立回寫資料表。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>Description  
 下列範例會完整處理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
### <a name="code"></a>程式碼  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 下列範例以累加方式處理**Internet_Sales_2004**資料分割中**Internet Sales**量值群組**Adventure Works DW** 中的cube[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 **程序**命令會將彙總加入訂單日期晚於 2006 年 12 月 31 日到分割區使用中的 out (out-of-line） 查詢繫結**繫結**屬性**程序**命令，以擷取事實資料表資料列，從而產生要加入資料分割的彙總。  
  
### <a name="code"></a>程式碼  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
  

