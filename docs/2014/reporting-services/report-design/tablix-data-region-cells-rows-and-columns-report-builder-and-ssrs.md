---
title: Tablix 資料區資料格、資料列及資料行 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10058"
- "10057"
- sql12.rtp.rptdesigner.deleterows.f1
- sql12.rtp.rptdesigner.deletecolumns.f1
ms.assetid: 70eef636-6d8c-495e-83fc-dc0fe9771658
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f55324123716289fec88b9d9bc531dccb22848d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720505"
---
# <a name="tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs"></a>Tablix 資料區資料格、資料列及資料行 (報表產生器及 SSRS)
  若要控制 Tablix 資料區域的資料列和資料行如何在報表中顯示資料，您必須了解如何指定詳細資料、群組資料以及標籤和總計的資料列與資料行。 在許多情況下，您可以使用資料表、矩陣或清單的預設結構來顯示您的資料。 如需詳細資訊，請參閱 <<c0> [ 資料表&#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)，[矩陣&#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)，或[列出&#40;報表產生器和SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。</c0>  
  
 Tablix 資料區域會顯示詳細資料列和詳細資料行的詳細資料，以及群組資料列和群組資料行的群組資料。 當您將資料列群組和資料行群組加入到 Tablix 資料區域時，便會自動加入顯示資料的資料列和資料行。 您可以手動加入及移除資料列和資料行來自訂 Tablix 資料區域，並控制您的資料顯示在報表中的方式。  
  
 為了解如何自訂 Tablix 資料區域，您應該先了解如何解譯您在設計介面上選取 Tablix 資料區域時所看到的視覺提示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-tablix-visual-cues"></a>了解 Tablix 視覺提示  
 Tablix 資料區域上的視覺提示可協助您使用 Tablix 資料區域顯示您想要的資料。  
  
### <a name="row-and-column-handles"></a>資料列和資料行控點  
 當您選取 Tablix 資料區域時，資料列和資料行控點圖形會指出每個資料列和資料行的用途。 控點表示群組內部或群組外部的資料列和資料行。 下表顯示各種控點顯示。  
  
|圖示|描述|  
|----------|-----------------|  
|![具有詳細資料列之三條平行線的資料列代碼](../media/rs-icontablix-detailsrow.gif "具有詳細資料列之三條平行線的資料列代碼")|只有資料列群組階層上的詳細資料群組|  
|![具有詳細資料列及一個外部群組的資料列代碼](../media/rs-icontablix-groupwithdetails.gif "具有詳細資料列及一個外部群組的資料列代碼")|一個外部群組和詳細資料子群組|  
|![兩個平行括號顯示巢狀群組](../media/rs-icontablix-nestedgroupnodetails.gif "兩個平行括號顯示巢狀群組")|一個外部群組、一個內部群組，沒有詳細資料群組|  
|![2 個括號 & 巢狀 & 詳細資料的 3 個堆疊線](../media/rs-icontablix-nestedgroupwithdetails.gif "2 個括號 & 巢狀 & 詳細資料的 3 個堆疊線")|一個外部群組、一個內部群組和詳細資料子群組|  
|![具有頁尾資料列和內部群組的一個外部群組、一個內部群組](../media/rs-icontablix-nestedgroupwithparentfooter.gif "具有頁尾資料列和內部群組的一個外部群組、一個內部群組")|包含詳細資料之頁尾資料列的一個外部群組，以及一個內部群組|  
|![外部群組括號、內部群組括號、詳細資料](../media/rs-icontablix-nestedgroupwithdetailsandtotals.gif "外部群組括號、內部群組括號、詳細資料")|包含詳細資料之頁尾資料列的一個外部群組、包含總計之頁尾資料列的一個內部群組，以及一個詳細資料列|  
|![父頁首和頁尾，以及子群組](../media/rs-icontablix-nestedgroupwithparentheaderandfooter.gif "父頁首和頁尾，以及子群組")|包含標籤頁首及總計頁尾的一個外部群組，以及一個內部群組，沒有詳細資料群組|  
  
### <a name="group-rows"></a>群組資料列  
 群組內部的資料列會針對每個唯一的群組值重複一次，而且通常用於彙總摘要。 群組外部的資料列會針對群組重複一次，而且用於標籤或小計。 當您選取 Tablix 資料格時，Tablix 資料區域內部的資料列和資料行控點以及方括號會顯示資料格所屬的群組。 此圖會顯示下列視覺提示：  
  
-   資料列和資料行控點，可表示群組關聯性。  
  
-   反白顯示的群組指標，可顯示所選資料格最內部的群組成員資格。  
  
-   的群組指標，可顯示所選資料格的所有群組成員資格。  
  
 ![具有詳細資料和巢狀資料列群組的資料表](../media/rs-tablixrowgroupvisualcues.gif "具有詳細資料和巢狀資料列群組的資料表")  
  
### <a name="total-rows"></a>總計資料列  
 加入資料列和資料行群組之後，您可以加入資料列來顯示資料行的總計，並加入資料行來顯示資料列的總計。 下圖顯示同時包含資料列和資料行群組，以及總計資料列和總計資料行的矩陣。  
  
 ![Tablix 資料區域](../media/rs-tablixparts.gif "Tablix 資料區域")  
  
### <a name="grouping-pane"></a>群組窗格  
 [群組] 窗格會針對目前在設計介面上選取的 Tablix 資料區域，顯示資料列和資料行群組。 下圖顯示此 Tablix 資料區域的 [群組] 窗格。  
  
 ![巢狀資料列和資料行群組的群組窗格](../media/rs-basictablixdesigngroupingpanedefaultview.gif "巢狀資料列和資料行群組的群組窗格")  
  
 [資料列群組] 窗格會顯示 Category 父群組和 Subcat 子群組。 [資料行群組] 窗格會顯示 Geography 父群組和 CountryRegion 子群組，同時顯示 Year 群組，為 Geography 群組的相鄰群組。 當您在 [資料列群組] 窗格中選取 Subcat 群組時，群組列會轉到較暗的橙色陰影，而對應的資料列群組成員資料格在設計介面上則會呈選取狀態。  
  
## <a name="displaying-data-on-rows-and-columns"></a>顯示資料列和資料行上的資料  
 資料列和資料列群組以及資料行和資料行群組擁有相同的關聯性。 以下討論描述如何加入資料列來顯示 Tablix 資料區域中資料列上的詳細資料與群組資料，但是加入資料行來顯示詳細資料和群組資料時，則適用相同的原則。  
  
 對於 Tablix 資料區域中的每個資料列而言，資料列位於每個資料列群組的內部或外部。 如果資料列位於資料列群組內部，該資料列會針對群組 (也就是所謂的 *「群組執行個體」*(Group Instance)) 的每個唯一值重複一次。 如果資料列位於資料列群組外部，則會針對該群組重複一次。 所有資料列群組外部的資料列都是靜態的，而且僅針對資料區域重複一次。 例如，資料表的頁首或頁尾資料列為靜態資料列。 根據至少一個群組重複的資料列是動態的。  
  
 當您擁有巢狀群組時，資料列可能會位於父群組內部，但位於子群組外部。 資料列會根據父群組中的每個群組值重複，但是僅針對子群組顯示一次。 若要顯示群組的標籤或總計，請加入群組外部的資料列。 若要顯示針對每個群組執行個體變更的資料，加入群組內部的資料列。  
  
 當您擁有詳細資料群組時，每個詳細資料列都位於詳細資料群組內部。 資料列會針對資料集查詢結果集中的每個值重複。  
  
 如需群組階層的詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)。  
  
 下圖顯示 Tablix 資料區域與巢狀資料列群組，以及詳細資料群組。  
  
 ![設計檢視，新增總資料列至群組和資料表](../media/rs-basictablegroupstotalscolordesign.gif "設計檢視，新增總資料列至群組和資料表")  
  
 若是顯示詳細資料的 Tablix 資料區域，詳細資料群組為最內部的子群組。 加入到詳細資料群組的資料列會針對連結到此 Tablix 資料區域之資料集查詢結果集中的每個資料列重複一次。 下圖顯示轉譯之報表的最後一頁。 在本圖中，您可以看到最後一個詳細資料列以及最後一個訂單的小計資料列。  
  
 ![預覽，具有群組總計的資料表、最後資料列](../media/rs-basictablegroupstotalscolorpreviewbottom.gif "預覽，具有群組總計的資料表、最後資料列")  
  
 對於 Tablix 資料區域中的每個資料行而言，則適用相同的原則。 例如，資料行位於每個資料行群組的內部或外部；若要顯示總計，請在群組外部加入資料行。  
  
 若要移除與某個群組相關聯的資料列和資料行，您可以刪除該群組。 當您刪除群組時，可以選擇僅刪除群組定義，或刪除群組及其所有關聯的資料列和資料行。 如果只刪除群組，您就可以保留資料區域上的資料列和資料行配置。 當您刪除群組及其相關的資料列和資料行時，您會刪除與該群組相關聯的所有靜態資料列和資料行 (群組首或群組尾) 以及動態資料列和資料行 (包括群組執行個體)。  
  
 如需新增或刪除資料列和資料行的逐步指示，請參閱[插入或刪除資料列 &#40;報表產生器及 SSRS&#41;](insert-or-delete-a-row-report-builder-and-ssrs.md) 和[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
## <a name="understanding-tablix-cells"></a>了解 Tablix 資料格  
 Tablix 資料格屬於下列其中一個 Tablix 區域：Tablix 主體、Tablix 資料列或 Tablix 資料行群組區域，或 Tablix 邊角。 雖然每個資料格都可能在資料集中顯示任何值，但是每個資料格的預設功能取決於其位置。 如需 Tablix 區域的詳細資訊，請參閱 [Tablix 資料區的區域 &#40;報表產生器及 SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
 根據預設，Tablix 資料列和資料行群組區域中的資料格代表群組成員。 群組成員在報表定義中會組織成多個樹狀結構。 資料列群組階層會以水平方式展開。 資料行群組階層則會以垂直方式展開。 這些資料格會在您建立群組，並在執行階段顯示群組的唯一值時自動加入。  
  
 Tablix 中的資料格則會在同時有資料列和資料行群組區域時建立。 您可以在這個區域中合併資料格，以建立標籤或嵌入其他的報表項目。  
  
 當資料格位於詳細資料列或資料行時，Tablix 主體區域中的資料格可以顯示詳細資料，而當資料格位於群組資料列或資料行時，則會顯示彙總群組資料。 資料格中的資料範圍是資料格所屬之最內部資料列群組及最內部資料行群組的交集。  
  
> [!NOTE]  
>  針對每個資料格顯示的實際資料是針對資料格所包含之報表項目 (這通常是文字方塊) 評估過的運算式。 在屬於詳細資料列或資料行的資料格中，此運算式預設為詳細資料 (例如， **[LineTotal]**)。 在不屬於詳細資料列或資料行的資料格中，此運算式預設為彙總函式 (例如， **Sum[LineTotal]**)。 如果即使在資料格屬於群組資料列或資料行時，運算式也沒有指定彙總函式，則會顯示群組中的第一個值。 如需彙總的詳細資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
### <a name="merging-and-splitting-cells"></a>合併與分割資料格  
 在 Tablix 區域內部，您可以將多個相鄰的資料格合併在一起。 例如，您可以針對跨越多個資料行或資料列的標籤建立資料格。  
  
 在 Tablix 邊角區域中，一次僅能以一個方向結合資料格：跨資料行以水平方式結合，或以垂直方式向資料列下方結合。 若要合併一組資料格，請先以水平方式合併資料格。 當所有資料格合併到每個資料列中的單一資料格之後，選取相鄰的資料格 (您可以選取資料行中的所有相鄰資料格) 並進行合併。  
  
 在 Tablix 主體區域中，僅能以水平方式合併資料格。 不支援以垂直方式合併資料格。  
  
 如需詳細資訊，請參閱[在資料區中合併資料格 &#40;報表產生器及 SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md)。  
  
 您可以分割先前合併的資料格。 您可以用水平方式跨資料行分割資料格，或以垂直方式向資料列下方合併資料格。 若要將某個資料格分割為一組資料格，請先以水平方式分割資料格，然後以垂直方式按照所需的次數分割。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)  
  
  
