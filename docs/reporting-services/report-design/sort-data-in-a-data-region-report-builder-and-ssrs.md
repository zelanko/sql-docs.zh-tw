---
title: 在資料區中排序資料 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 642d8f6d08c21daa478bbc159b2fe71461ba0391
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>在資料區中排序資料 (報表產生器及 SSRS)
  若要在資料區域中變更報表第一次執行時資料的排序次序，您必須針對資料區域或群組設定排序運算式。 根據預設，群組的排序運算式會自動設定為與群組運算式相同的值。  
  
-   在 Tablix 資料區域中，設定資料區域或每個群組 (包括詳細資料群組) 的排序運算式。 如果您在 Tablix 資料區域中只有一個詳細資料群組，您可以在查詢中、資料區域上，或詳細資料群組上，定義排序運算式，而且它們都有相同的效果。  
  
-   在圖表資料區域中，設定 [類別目錄] 和 [數列] 群組的排序運算式來控制每個群組的排序次序。 在圖表圖例中，色彩的次序取決於 [類別目錄] 群組中資料點的排序運算式。  
  
-   在量測計資料區域中，您通常不需要排序資料，因為量測計會顯示一個相對於範圍的單一值。 如果您需要排序量測計中的資料，則必須先定義一個群組，然後設定該群組的排序運算式。  
  
 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
 若是 Tablix 資料區域，您也可以將互動式排序按鈕加入到資料行標頭的頂端，以提供使用者變更群組或詳細資料列之排序次序的能力。 如需詳細資訊，請參閱[互動式排序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>在 Tablix 資料區域中排序資料  
  
1.  以滑鼠右鍵按一下設計介面上的資料列控制代碼，然後按一下 [Tablix 屬性]。  
  
2.  按一下 **[排序]**。  
  
3.  針對每個排序運算式，請依照下列步驟執行：  
  
    1.  按一下 **[加入]**。  
  
    2.  輸入或選取排序資料所依據的運算式。  
  
    3.  從 **Order** 資料行下拉式清單中，選擇每個運算式的排序方向。 **A-Z** 會以遞增順序排序運算式。 **Z-A** 會以遞減順序排序運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>針對 Tablix 排序群組 (包括詳細資料群組) 中的值  
  
1.  在設計介面上，按一下 Tablix 資料區域來選取它。 [群組] 窗格會顯示 Tablix 資料區域的資料列群組和資料行群組。  
  
2.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下群組名稱，然後按一下 [編輯群組]。  
  
3.  在 **[Tablix 群組]** 對話方塊中，按一下 **[排序]**。  
  
4.  針對每個排序運算式，請依照下列步驟執行：  
  
    1.  按一下 **[加入]**。  
  
    2.  輸入或選取排序資料所依據的運算式。  
  
    3.  從 **Order** 資料行下拉式清單中，選擇每個運算式的排序方向。 **A-Z** 會以遞增順序排序運算式。 **Z-A** 會以遞減順序排序運算式。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>在圖表上按照字母順序排序 x 軸標籤  
  
1.  在 [類別目錄欄位] 放置區中的欄位上按一下滑鼠右鍵，然後按一下 [類別目錄群組屬性]。  
  
2.  在 **[類別目錄群組屬性]** 對話方塊中，按一下 **[排序]**。  
  
3.  針對每個排序運算式，請依照下列步驟執行：  
  
    1.  按一下 **[加入]**。  
  
    2.  選取符合您群組欄位的運算式。 您可以按一下 **[群組]** 來驗證群組欄位的運算式。  
  
    3.  從 **Order** 資料行下拉式清單中，選擇每個運算式的排序方向。 [A-Z] 會以字母的遞增順序排序運算式。 [Z-A] 會以字母的遞減順序排序運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>在圖表上，以遞增或遞減的順序排序資料點  
  
1.  在 [類別目錄欄位] 放置區中的欄位上按一下滑鼠右鍵，然後按一下 [類別目錄群組屬性]。  
  
2.  在 **[類別目錄群組屬性]** 對話方塊中，按一下 **[排序]**。  
  
3.  針對每個排序運算式，請依照下列步驟執行：  
  
    1.  按一下 **[加入]**。  
  
    2.  選取符合您資料欄位的運算式。 在大部分的情況下，這是彙總值，例如 `=Sum(Fields!Quantity.Value)`。  
  
    3.  從 **Order** 資料行下拉式清單中，選擇每個運算式的排序方向。 **A-Z** 會以遞增順序排序運算式。 **Z-A** 會以遞減順序排序運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>在量測計上，以遞增或遞減的順序排序要顯示的資料  
  
1.  以滑鼠右鍵按一下量測計，然後按一下 [新增資料群組]。  
  
2.  必要時，在 [量測計面板群組屬性] 對話方塊中，按一下 [一般]。  
  
3.  在 **[群組運算式]** 中，按一下 **[加入]**。  
  
4.  在 **[群組對象]** 中，輸入或選取用來分組資料的運算式。  
  
5.  重複步驟 3 和 4，直到加入您要使用的所有群組運算式為止。  
  
6.  按一下 **[排序]**。  
  
7.  針對每個排序運算式，請依照下列步驟執行：  
  
    1.  按一下 **[加入]**。  
  
    2.  選取符合您群組欄位的運算式。 您可以按一下 **[群組]** 來驗證群組欄位的運算式。  
  
    3.  從 **Order** 資料行下拉式清單中，選擇每個運算式的排序方向。 **A-Z** 會以遞增順序排序運算式。 **Z-A** 會以遞減順序排序運算式。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 如需如何在量測計中群組資料的詳細資訊，請參閱[量測計 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和精靈的報表產生器說明](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [跨多個形狀圖指定一致的色彩 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  
