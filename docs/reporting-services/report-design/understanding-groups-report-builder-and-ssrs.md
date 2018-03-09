---
title: "了解群組 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10056"
- "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 6972387a10c596256f0eef54e14054ae5adc9b38
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="understanding-groups-report-builder-and-ssrs"></a>了解群組 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，群組是一組來自繫結至資料區域之報表資料集的具名資料。 基本上，一個群組會組織一個報表資料集的檢視。 資料區域中的所有群組會指定相同報表資料集的不同檢視。  
  
 為協助視覺化群組所代表的意義，請參閱下圖，其中顯示預覽中的 Tablix 資料區域。 在此圖中，資料列群組會依產品類型為資料集分類，而資料行群組則依地理區域和年份為資料集分類。  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 下列章節描述各種層面的群組。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="what-makes-a-group"></a>構成群組的要素為何？  
 一個群組擁有一個您指定的名稱以及一組群組運算式。 這組群組運算式可以是單一的資料集欄位參考，也可以是多個運算式的組合。 在執行階段，群組運算式會結合 (如果群組具有多個運算式的話)，並且套用至群組中的資料。 例如，您所擁有的群組會使用日期欄位來組織資料區域中的資料。 在執行階段，資料會先依日期組織，然後顯示並加總每個日期的其他資料集值。  
  
## <a name="when-do-i-create-groups"></a>何時建立群組？  
 在大部分情況下，報表產生器和報表設計師會在您設計資料區域時，自動為您建立一個群組。 若是資料表、矩陣或清單，當您將欄位放到 [群組] 窗格時，就會建立群組。 若是圖表，則當您將欄位放在圖表放置區時，建立群組。 若是量測計，您必須使用量測計屬性對話方塊。 若是資料表、矩陣或清單，您也可以手動建立群組。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。 如需如何在建立資料表時新增群組的範例，請參閱[教學課程︰建立基本資料表報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md) 或[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)。  
  
## <a name="how-can-i-modify-a-group"></a>如何修改群組？  
 建立群組之後，您可以設定資料區域專屬的屬性 (例如，篩選和排序運算式、分頁符號與群組變數) 來保存範圍專屬的資料。 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
 若要修改現有的群組，請開啟適當的群組屬性對話方塊。 您可以變更群組的名稱。 同時，您可以根據單一欄位或多個欄位，或者根據在執行階段指定值的報表參數，指定群組運算式。 您也可以根據一組運算式建立群組，例如，指定人口統計資料之年齡範圍的一組運算式。 如需詳細資訊，請參閱 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  如果您要變更群組的名稱，必須手動更新參照群組舊名稱的所有群組運算式。  
  
## <a name="how-are-groups-organized"></a>如何組織群組？  
 了解群組組織可以協助您透過指定相同的群組運算式，設計可顯示相同資料之不同檢視的資料區域。  
  
 系統會針對每個資料區域，在內部將群組組織為一或多個階層的成員。 群組階層擁有巢狀的父/子群組，而且可以擁有相鄰的群組。  
  
 如果您將父/子群組視為樹狀結構，每個群組階層都是樹狀結構的樹系。 Tablix 資料區域包含資料列群組階層和資料行群組階層。 與資料列群組成員相關聯的資料會以水平的方式跨頁面展開，而與資料行群組成員相關聯的資料會以垂直的方式向頁面下方展開。 [群組] 窗格會針對目前在設計介面上選取的 Tablix 資料區域，顯示資料列群組和資料行群組成員。 如需詳細資訊，請參閱[群組窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)。  
  
 圖表資料區域包含類別目錄群組階層和數列群組階層。 類別目錄群組成員會顯示在類別目錄軸上，而數列群組成員會顯示在數列軸上。  
  
 雖然量測計資料區域通常不需要，但是群組還是會讓您指定如何為資料分組以便針對量測計進行彙總。  
  
## <a name="what-types-of-groups-are-available-per-data-region"></a>每個資料區域提供哪些類型的群組？  
 展開為方格的資料區域支援的群組與以視覺方式顯示摘要資料的資料區域不同。 因此，Tablix 資料區域，以及以 Tablix 資料區域為基礎的資料表、清單與矩陣支援的群組與圖表或量測計不同。 下列章節討論在每個資料區域類型中分組的類型和用途。  
  
> [!NOTE]  
>  雖然群組在不同的資料區域中有不同的名稱，但是建立與使用群組之方式背後的原則是相同的。 當您針對資料區域建立群組時，會指定一種方式，從連結到資料區域的資料集組織詳細資料。 每個資料區域都支援一個用於顯示群組資料的群組結構。  
  
### <a name="groups-in-a-tablix-data-region-details-row-and-column-groups"></a>Tablix 資料區域中的群組：詳細資料、資料列與資料行群組  
 如本主題稍早所述，Tablix 資料區域可讓您依資料列或資料行，將資料組織到群組中。 不過，資料列和資料行群組不是 Tablix 資料區域中提供的唯一群組。 此資料區域可能有下列類型的群組：  
  
-   **詳細資料群組** ：[詳細資料] 群組包含報表產生器或報表設計師套用資料集與資料區域篩選後，來自報表資料集的所有資料。 因此，詳細資料群組是唯一沒有群組運算式的群組。  
  
     基本上，詳細資料群組會指定您在查詢設計工具中執行資料集查詢時所看到的資料。 例如，您所擁有的查詢會從銷售訂單資料表擷取所有資料行。 因此，此詳細資料群組中的資料在資料表中包含所有資料行之每個資料列的所有值。 此詳細資料群組中的資料也包含您已建立之所有導出資料集欄位的值。  
  
    > [!NOTE]  
    >  詳細資料群組中的資料也可以包含伺服器彙總，這些是在資料來源上導出，並在查詢中擷取的彙總。 依預設，除非您的報表包含使用彙總函式的運算式，否則報表產生器和報表設計師會將伺服器彙總視為詳細資料。 如需詳細資訊，請參閱＜ [彙總](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)＞。  
  
     根據預設，當您將資料表或清單加入到報表時，報表產生器和報表設計師會為您自動建立 [詳細資料] 群組，並加入資料列來顯示詳細資料。 根據預設，當您將資料集欄位加入到此資料列中的資料格時，您會看到欄位的簡單運算式，例如 [Sales]。 當您檢視資料區域時，詳細資料列會針對結果集中的每個值重複一次。  
  
-   **資料列群組和資料行群組** ：您可以依資料列或資料行將資料組織到群組中。 資料列群組會以垂直方式，在頁面上展開。 資料行群組則會以水平方式，在頁面上展開。 群組可以是巢狀的，例如，先依 [Year] 分組，再依 [Quarter] 分組，然後依 [Month] 分組。 群組也可以是相鄰的，例如，針對 [Territory] 分組，另外依 [ProductCategory] 分組。  
  
     當您建立資料區域的群組時，報表產生器和報表設計師會將資料列或資料行自動加入資料區域，然後使用這些資料列或資料行顯示群組資料。  
  
-   **遞迴階層群組** ：遞迴階層群組會從單一的報表資料集，組織包含多個層級的資料。 例如，遞迴階層群組可以顯示組織階層，例如，回報給 [Employee] 的 [Employee]。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供群組屬性和內建函數，讓您針對此種報表資料建立群組。 如需詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
 下列清單摘要說明您針對每個資料區域使用群組的方式：  
  
-   **資料表** ：定義巢狀資料列群組、相鄰資料列群組及遞迴階層資料列群組 (例如針對組織圖)。 根據預設，資料表包含詳細資料群組。 將資料集欄位拖曳到所選資料表的 [群組] 窗格來加入群組。  
  
-   **矩陣** ：定義巢狀資料列和資料行群組，以及相鄰資料列和資料行群組。 將資料集欄位拖曳到所選矩陣的 [群組] 窗格來加入群組。  
  
-   **清單** ：根據預設，支援詳細資料群組。 一般用途為支援群組的一個層級。 將資料集欄位拖曳到所選清單的 [群組] 窗格來加入群組。  
  
 加入群組之後，資料區域的資料列和資料行控點會變更以反映群組成員資格。 當您刪除群組時，可以選擇僅刪除群組定義，或刪除群組及其所有關聯的資料列和資料行。 如需詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 若要將資料限制為在詳細資料或群組資料的計算中顯示或使用，請針對群組設定篩選。 如需詳細資訊，請參閱 [加入資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
 根據預設，當您建立群組時，群組的排序運算式與群組運算式相同。 若要變更排序次序，請變更排序運算式。 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
#### <a name="understanding-group-membership-for-tablix-cells"></a>了解 Tablix 資料格的群組成員資格  
 Tablix 資料區域之資料列或資料行中的資料格可以屬於多個資料列和資料行群組。 當您在資料格的文字方塊中定義使用彙總函式 (例如 `=Sum(Fields!FieldName.Value`) 的運算式時，資料格的預設群組範圍是其所屬的最內部子群組。 當資料格同時屬於資料列和資料行群組時，其範圍是兩個最內部的群組。 您也可以撰寫運算式，計算某個群組相對於另一組資料之範圍的彙總小計。 例如，您可以計算某個群組相對於資料行群組，或相對於資料區域之所有資料的百分比 (例如 `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`)。 如需詳細資訊，請參閱 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [將總計新增至群組或 Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [向下鑽研動作 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
