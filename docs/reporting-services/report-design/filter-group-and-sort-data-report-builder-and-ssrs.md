---
title: "篩選、 分組和排序資料 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 422c3efc7f6514efafcfa552ed78658d002a2f42
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>篩選、分組和排序資料 (報表產生器及 SSRS)
  在報表中，運算式可用於協助您控制、組織和排序報表資料。 依預設，在您建立資料集與設計報表配置時，報表項目的屬性會依據資料集欄位、參數和 [報表資料] 窗格中出現的其他項目，自動設定為運算式。 您也可以將互動式排序按鈕加入至資料表或矩陣資料格，讓使用者以互動方式變更群組或群組內資料列的資料列排序順序。  
  
-   **篩選運算式** ：篩選運算式會依據您所指定的比較方式，測試包含或排除的資料。 在從資料連接擷取資料後，篩選便會套用到報表中的資料。 您可以將任何篩選組合加入到下列項目：報表伺服器上的共用資料集定義、報表中的共用資料集執行個體或內嵌資料集、資料區 (例如資料表或圖表) 或資料區群組 (例如資料表中的資料列群組或圖表中的類別目錄群組)。  
  
-   **群組運算式** ：群組運算式會依據資料集欄位或其他值來組織資料。 系統會在您建立報表配置時自動建立群組運算式。 將篩選套用到資料之後，以及在結合報表資料和資料區之時，報表處理器會評估群組運算式。 您可以在建立群組運算式之後加以自訂。  
  
-   **排序運算式** ：排序運算式會控制資料出現在資料區中的次序。 系統會在您建立報表配置時自動建立排序運算式。 根據預設，群組的排序運算式會設定為與群組運算式相同的值。 您可以在建立排序運算式之後加以自訂。  
  
-   **互動式排序** ：您可以將互動式排序按鈕加入到資料表或矩陣中的資料行標頭或群組首資料格，讓使用者排序資料行或反轉資料行的排序次序。  
  
 為協助使用者自訂篩選、群組或排序運算式，您可以變更運算式，以將參考加入至報表參數。 如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
 如需詳細資訊和範例，請參閱下列主題：  
  
-   [群組運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [報表產生器教學課程](../../reporting-services/report-builder-tutorials.md)  
  
-   [Reporting Services 教學課程 &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [報表範例 (報表產生器和 SSRS)](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> 篩選報表中的資料  
 篩選是報表的一部分，有助於控制從資料連接擷取的報表資料。 如果您無法在從外部資料來源擷取資料之前，變更資料集查詢來篩選資料，請使用篩選。  
  
 如果可能，請建立只會傳回需要顯示在報表中之資料的資料集查詢。 您可透過減少必須擷取和處理的資料量，協助增進報表效能。 如需詳細資訊，請參閱[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 從外部資料來源擷取資料之後，您可以將篩選加入至資料集、資料區和資料區群組，包括詳細資料群組。 篩選會在執行階段先套用至資料集、套用至資料區，然後套用至群組 (按照群組階層的由上而下順序)。 在資料表、矩陣或清單中，系統會針對資料列群組、資料行群組和相鄰群組獨立套用篩選。 在圖表中，系統會針對類別目錄群組和數列群組獨立套用篩選。 如需詳細資訊，請參閱 [加入資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
 針對每個篩選，您會指定一個 *「篩選方程式」*(Filter Equation)。 篩選方程式包含一個指定所要篩選之資料的資料集欄位或運算式、一個運算子和一個要比較的值。 在處理項目時，只會包含符合篩選條件的資料值。  
  
 您可以在篩選運算式中包含參數，讓使用者協助控制報表中的資料。 如需詳細資訊，請參閱[參數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)。  
  
 若要自訂每個使用者的檢視，您可以在篩選中包含內建欄位 UserID 的參考。 如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
  
##  <a name="Grouping"></a> 群組報表中的資料  
 群組可組織報表中的資料以供顯示或計算彙總值。 了解如何定義群組以及使用群組功能可協助您設計更精確的報表。  
  
 系統會在您執行下列作業時自動建立群組運算式：  
  
-   在資料表、矩陣或圖表精靈中排序資料集欄位，或是在地圖精靈中比對欄位。  
  
-   在資料表、矩陣或清單中，將欄位加入至 [群組] 窗格中的 [資料列群組] 或 [資料行群組] 區域。  
  
-   在圖表中，將欄位加入至 [圖表資料] 窗格中的 [類別目錄群組] 或 [數列群組] 區域。  
  
-   在地圖中，指定欄位，以比對地圖元素與 [圖層資料] 內容功能表項目中的分析資料。  
  
 群組是報表定義的一部分。 每個群組都有一個名稱。 依預設，群組名稱是其依據的資料集欄位。  
  
 在資料表或矩陣區域內，您可以建立多個資料列群組和資料行群組。 您可以透過組織巢狀群組、相鄰群組及遞迴階層群組 (例如組織圖)，以視覺階層顯示您的資料。  
  
 群組名稱會識別運算式範圍。 您可以將群組的名稱指定成下列作業的執行範圍：計算彙總、在向下鑽研報表中以階層方式組織資料並從父節點切換為子節點的顯示、在多個資料區中顯示相同資料的不同檢視，以及視覺化資料表、矩陣、圖表、量測計或地圖中的摘要資料。 如需詳細資訊，請參閱 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 若要在數個資料集欄位上分組，請將每個欄位加入到群組運算式集合。 您也可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]中，撰寫自己的群組運算式。 例如，您可以依據值的範圍分組，或者使用報表參數讓使用者選取在資料區中分組資料的方式藉以進行分組。 如需詳細資訊，請參閱 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)。  
  
 若要呈現報表，您可以在每個群組或每個群組執行個體的前後加入分頁符號，以減少每個頁面的資料量並協助您管理報表轉譯效能。 如需詳細資訊，請參閱[加入分頁符號 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md).  
  
 建立資料區群組是在報表中組織資料的一種方法。 另外還有其他幾種組織資料的方法，每一種都有其各自的優點。 如需詳細資訊，請參閱[鑽研、向下鑽研、子報表和巢狀資料區域 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
### <a name="defining-group-variables"></a>定義群組變數  
 當您定義群組時，可以建立群組變數，以便在以群組為範圍並可從巢狀群組存取的運算式中使用。 群組變數會針對每個群組執行個體計算一次，而且可以從子群組中的運算式存取。 例如，如果資料是依區域和子區域分組，您可以計算每個區域的稅額，並在子區域群組的計算中使用該稅額。  
  
 如需詳細資訊，請參閱 [報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) 和 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
### <a name="groups-and-scope-in-data-regions"></a>資料區中的群組和範圍  
 您可以為每個資料區指定相同的群組運算式，以提供相同資料集內資料的多個檢視。 例如，您可以顯示分類資料，以在資料表中顯示所有詳細資料，並在圖形圖中顯示彙總，同時協助您以相對於整個資料集的方式視覺化每個類別目錄。 如需詳細資訊，請參閱 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)。  
  
 當您在資料表、矩陣或清單的資料格中建立巢狀資料區時，您會自動將資料的範圍設定成該資料格的最內層群組成員資格。 例如，假設您將圖表加入到同時位於資料列群組和資料行群組的資料格中。 可用於該圖表的資料範圍在執行階段便為最內層的資料列群組執行個體與最內層的資料行群組執行個體。 如需詳細資訊，請參閱 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
  
##  <a name="Sorting"></a> 排序報表中的資料  
 若要控制報表中資料的排序次序，您可以在資料集查詢中排序資料，或針對資料區或群組定義排序運算式。 您也可以將互動式排序按鈕加入到資料表和矩陣，讓使用者變更資料列的排序次序。  
  
 三種類型的排序全都可以在相同的報表中結合。 依預設，排序次序是由資料集查詢傳回資料的順序來決定。 排序運算式會套用在資料區和資料區群組中。 互動式排序則是在排序運算式之後套用。  
  
 對於包含彙總函式的運算式，大部分的結果都不會受排序次序影響。 下列彙總函式的傳回值會受排序次序影響：First、Last 和 Previous。 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
### <a name="sorting-data-in-a-dataset-query"></a>排序資料集查詢中的資料  
 將資料集查詢中的排序次序加入到預先排序資料，然後再針對報表進行擷取。 透過排序查詢中的資料，排序工作將由資料來源而非報表處理器完成。  
  
 若是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源類型，您可以將 ORDER BY 子句加入到資料集查詢。 例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢會從 SalesOrders 資料表，以遞減的順序排序 Sales 和 Region by Sales 資料行： `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`。 如需詳細資訊，請參閱《 [SQL Server 線上叢書](http://go.microsoft.com/fwlink/?linkid=98335)》中的＜使用 ORDER BY 排序資料列＞。  
  
> [!NOTE]  
>  並非所有資料來源都支援在查詢中指定排序次序的能力。  
  
### <a name="sorting-data-with-sort-expressions"></a>利用排序運算式排序資料  
 若要在資料從資料來源擷取後排序報表中的資料，您可以針對 Tablix 資料區域或群組 (包括詳細資料群組) 設定排序運算式。 下列清單描述針對不同項目設定排序運算式的效果：  
  
-   **Tablix 資料區域：** 在執行階段套用資料集篩選和資料區域篩選之後，針對資料表、矩陣或清單資料區域設定排序運算式來控制資料在資料區域中的排序次序。  
  
-   **Tablix 資料區域群組：** 設定每個群組 (包括詳細資料群組) 的排序運算式來控制群組執行個體的排序次序。 例如，您可以針對詳細資料群組，控制詳細資料列的次序。 若是子群組，您可以針對父群組中的子群組，控制群組執行個體的次序。 根據預設，當您建立群組時，排序運算式會設定為群組運算式以及遞增順序。  
  
     如果您只有一個詳細資料群組，您可以在查詢中、資料區域上，或詳細資料群組上，將排序運算式定義為相同的效果。  
  
-   **圖表資料區域：** 設定類別目錄和數列群組的排序運算式來控制資料點的排序次序。 根據預設，資料點的次序也是色彩在圖表圖例中的次序。 如需詳細資訊，請參閱 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
-   **地圖報表項目：** 您通常不需要排序地圖資料區的資料，因為地圖會將要顯示在地圖元素上的資料分組。  
  
-   **量測計資料區：** 您通常不需要排序量測計資料區的資料，因為量測計會顯示相對於某個範圍的單一值。 如果您需要排序量測計中的資料，則必須先定義一個群組，然後設定該群組的排序運算式。  
  
#### <a name="sorting-by-a-different-value"></a>依其他值排序  
 您可以按照欄位值以外的其他值來排序資料區中的資料列。 例如，假設 [Size] 欄位包含對應於小、中、大和超大的文字值。 依預設，以 Size 為根據之資料列群組的排序運算式也是 [Size]。 若要更進一步控制資料排序的方式，您可以將欄位加入到定義所需排序次序的資料集查詢中。  
  
 或者，您也可以定義只包含大小的資料集，以及用來指定所需次序的值。 您可以將排序運算式變更為使用 Lookup 函數做為排序次序值。  
  
 例如，假設下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢定義一個名為 Sizes 的資料集。 此查詢會使用 CASE 陳述式，針對 Size 的每個值定義排序次序值 SizeSortOrder：  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 在具有以 `[Size]`做為根據之資料列群組的資料表中，您可以變更群組排序運算式，以使用 Lookup 函數來尋找對應於大小值的數值欄位。 這個運算式類似於下例：  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 如需詳細資訊，請參閱[在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md) 和 [Lookup 函數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)。  
  
###  <a name="Interactive"></a> 加入使用者的互動式排序  
 您可以將互動式排序按鈕加入到資料行標頭和群組首，讓使用者變更資料表或矩陣中報表資料的排序次序。 使用者可以按一下按鈕來切換排序次序。 系統以可讓使用者互動的轉譯格式支援互動式排序，例如 HTML。  
  
 您可以將互動式排序按鈕加入到 Tablix 資料區資料格裡的文字方塊中。 依預設，每個資料格都包含一個文字方塊。 在文字方塊屬性中，您可以指定要排序資料表或矩陣資料區的哪個部分 (父群組值、子群組值或詳細資料列)、排序的依據，以及是否要將排序運算式套用到具有對等關聯性的其他報表項目。 例如，如果在相同資料集中提供檢視的資料表和圖表都包含在矩形中，它們就是對等資料區域。 當使用者在資料表中切換排序次序時，圖表的排序次序也會切換。 如需詳細資訊，請參閱[篩互動式排序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 如何主題  
 [在報表中捲動時將標頭保持可見 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [將互動式排序加入至資料表或矩陣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [在資料區域中設定沒有資料的訊息 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [在圖表中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [將總計加入到群組或 Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> 本節內容  
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [加入資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> 相關章節  
 [了解群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [將包含多個資料範圍的數列顯示在圖表上 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>請參閱＜  
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [資料表、 矩陣和清單 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [對應 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [走勢圖和資料橫條 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [指標 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
