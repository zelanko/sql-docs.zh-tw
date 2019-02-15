---
title: 將資料新增至 Tablix 資料區 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 62c824c7192053655a928874877baea32dedc5cc
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292156"
---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>將資料加入至 Tablix 資料區 (報表產生器及 SSRS)
  若要在資料表或矩陣中顯示報表資料集的資料，請在每個資料格中，指定要顯示之資料集欄位的名稱。 您可以顯示詳細資料或群組資料。 如果您將群組加入到資料表或矩陣，則會自動加入群組值與群組資料的資料列和資料行。 接著，您可以加入資料的小計與總計。  
  
 資料區域中的所有資料至少都屬於一個群組。 詳細資料是詳細資料群組的成員。 如需詳細資料和群組資料的詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>加入詳細資料  
 詳細資料是將篩選套用到資料集、資料區域與詳細資料群組後，來自報表資料集的所有資料。 顯示在單一 Tablix 資料區域中的所有詳細資料都必須來自相同的報表資料集。  
  
 若要將詳細資料從報表資料集加入到 Tablix 資料區域，請將資料集欄位從 [報表資料] 窗格拖曳到詳細資料列中的每個資料格。 對於 Tablix 資料區域中的現有資料格，您可以使用每個資料格中的欄位選取器或將欄位從 [報表資料] 窗格拖曳到資料格，即可加入或編輯資料集欄位運算式。 若要建立額外的資料行，您可以從 [報表資料] 窗格拖曳欄位，並將其插入到現有的 Tablix 資料區域。  
  
 根據預設，在執行階段，詳細資料列中的資料格會顯示詳細資料，而群組資料列中的資料格會顯示彙總值。 如需 Tablix 資料列和資料行的詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 資料表範本和清單範本會提供詳細資料列。 矩陣範本則沒有詳細資料列。 如果您的 Tablix 資料區域沒有詳細資料列，您可以定義詳細資料群組來加入一個詳細資料列。 如需詳細資訊，請參閱[新增詳細資料群組 &#40;報表產生器及 SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md)。  
  
## <a name="adding-grouped-data"></a>加入群組資料  
 群組資料是將篩選套用到資料集、資料區域與群組後，由群組運算式指定的所有詳細資料。 若要在群組中組織詳細資料，將欄位從 [報表資料] 窗格拖曳到 [群組] 窗格。 當您加入群組時， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將相關的資料列或資料行自動加入群組資料顯示所在的 Tablix 資料區域。 這些資料列或資料行中的資料格與群組資料有關聯。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 根據預設，當您將代表數值資料的資料集欄位加入到群組資料列或資料行中的資料格時，資料格的值為資料格之最內部資料列和資料行群組成員資格範圍內的群組資料加總。 您可以將預設的彙總函式 Sum 變更為其他任何彙總函式，例如，Avg 或 Count。 您也可以變更彙總計算的預設範圍，以計算某個值佔資料列群組的百分比。 如需詳細資訊，請參閱 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 根據預設，所有群組資料都來自相同的報表資料集。 在 Tablix 資料區域中，您可以將資料集名稱指定為範圍，藉以加入來自其他資料集的彙總值。 您可以在單一的 Tablix 資料區域中，指定來自多個資料集的多個彙總值。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="adding-subtotals-and-totals"></a>加入小計和總計  
 若要加入群組的小計以及資料區域的總計，請在資料格或 [群組] 窗格中，使用快速鍵功能表上的 [加入總計] 功能。 系統會為您自動加入用於顯示總計的資料列和資料行。 小計與總計運算式預設使用 [Sum](report-builder-functions-sum-function.md) 彙總函式。 加入運算式之後，您可以變更預設函數。 如需詳細資訊，請參閱 [將總計新增到群組或 Tablix 資料區 &#40;報表產生器及 SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="adding-labels"></a>加入標籤  
 若要加入群組或資料區域的標籤，請在您要標示的群組外部，加入資料列或資料行。 標籤資料列和資料行類似您為顯示總計加入的資料列和資料行。 如需詳細資訊，請參閱[插入或刪除資料列 &#40;報表產生器及 SSRS&#41;](insert-or-delete-a-row-report-builder-and-ssrs.md) 或[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>從其他報表加入現有的 Tablix 資料區域  
 您可以從其他報表複製資料區域，並將其貼到新的或現有的報表中。 貼上資料區域之後，您必須確定資料區域所使用的資料集已定義，並確定資料集欄位的名稱和資料類型與原始報表中的名稱和資料類型相同。 您不能將一個報表中的資料集複製到另一個報表，但是如果您的報表使用共用資料來源，您可以快速複製另一個報表中的資料集。 此外，您也可以針對擷取資料集資料的查詢來匯入查詢文字，讓您輕鬆地複製報表中的查詢。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)   
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [新增、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [加入運算式 &#40;報表產生器及 SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)  
  
  
