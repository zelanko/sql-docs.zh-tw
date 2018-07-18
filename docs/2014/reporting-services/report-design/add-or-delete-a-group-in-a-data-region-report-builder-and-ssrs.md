---
title: 在資料區中新增或刪除群組 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4f65bacaaa25568b9dd1b30cfec7767beecd6f1e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194804"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>在資料區中加入或刪除群組 (報表產生器及 SSRS)
  當您想要針對顯示和計算，依特定值或特定一組運算式組織資料時，將群組加入至資料區。 每個群組都有一個名稱和一個運算式，識別資料集中的哪個資料屬於群組。 如需群組的詳細資訊，請參閱 [了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)。  
  
 在 Tablix 資料區中，按一下資料表、矩陣或清單來顯示 [群組] 窗格。 將資料集欄位拖曳到 [資料列群組] 和 [資料行群組] 窗格以建立父群組或子群組。 以滑鼠右鍵按一下現有的群組即可加入相鄰的群組。 根據定義，詳細資料群組是最內部的群組，而且僅能當做子群組加入。 以滑鼠右鍵按一下現有的群組即可刪除該群組。 系統會為您自動加入用於顯示群組值的資料列和資料行。 如需詳細資訊，請參閱 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
 在 [圖表] 資料區域中，按一下圖表來顯示放置區。 將資料集欄位拖曳到類別目錄和數列放置區，藉以建立群組。 若要加入巢狀群組，將多個欄位加入至放置區。  
  
 依預設，在量測計中不會定義群組。 量測計的預設行為是將指定之欄位中的所有值彙總為量測計上顯示的一個值。 如需詳細資訊，請參閱 [量測計 &#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>若要將父或子資料列或資料行群組加入到 Tablix 資料區  
  
1.  將欄位從 **[報表資料]** 窗格拖曳到 **[資料列群組]** 窗格或 **[資料行群組]** 窗格。  
  
    > [!NOTE]  
    >  如果沒有看到 [群組] 窗格，請按一下 [檢視] 索引標籤上的 [群組]。  
  
2.  使用導覽列將欄位放在群組階層之上或之下，以便將群組當做父群組或子群組放到現有的群組中。  
  
     此群組會使用預設名稱、群組運算式以及以欄位名稱為基礎的排序運算式加入。  
  
### <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>若要將相鄰的資料列或資料行群組加入到 Tablix 資料區  
  
1.  在 [群組] 窗格中，以滑鼠右鍵按一下與您想要加入之群組對等的群組。 按一下 **[加入群組]**，然後按一下 **[前方相鄰]** 或 **[後方相鄰]** 來指定要加入群組的位置。 **[Tablix 群組]** 對話方塊隨即開啟。  
  
2.  在 **[名稱]** 中，輸入群組的名稱。  
  
3.  在 [群組運算式] 中鍵入運算式，或按一下運算式按鈕 (**fx**) 建立運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     此時會將新群組加入到 [群組] 窗格中，並將在其中顯示群組值的資料列或資料行加入到設計介面的 Tablix 資料區中。  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>將詳細資料群組加入到 Tablix 資料區域  
  
1.  在 [群組] 窗格中，以滑鼠右鍵按一下屬於最內部子群組的群組，而不是 [詳細資料] 群組。 按一下 **[加入群組]**，然後按一下 **[子群組]**。 **[Tablix 群組]** 對話方塊隨即開啟。  
  
2.  在 **[群組運算式]** 中，將運算式保留空白。 詳細資料群組沒有運算式。  
  
3.  選取 **[顯示詳細資料]**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     此時新的詳細資料群組會當做子群組加入到 [群組] 窗格中，而且您在步驟 1 中選取之群組的資料列控制代碼會顯示詳細資料群組圖示。 如需控制代碼的詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
### <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>若要在 Tablix 資料區中編輯資料列或資料行群組  
  
1.  在報表設計介面上，按一下 Tablix 資料區中的任意位置來選取它。 [群組] 窗格會顯示資料列和資料行群組。  
  
2.  以滑鼠右鍵按一下群組，然後按一下 [群組屬性]。  
  
3.  在 **[名稱]** 中，輸入群組的名稱。  
  
4.  在 [群組運算式] 中鍵入或選取簡單運算式，或是按一下 [運算式]\(**fx**) 按鈕來建立群組運算式。  
  
5.  按一下 **[加入]** 來建立其他運算式。 您指定的所有運算式都會使用邏輯 AND 結合在一起以指定此群組的資料。  
  
6.  (選擇性) 按一下 [分頁符號] 來設定分頁符號選項。  
  
7.  (選擇性) 按一下 [排序] 來選取或鍵入運算式，以指定群組中值的排序次序。  
  
8.  (選擇性) 按一下 [可見度] 來選取項目的可見度選項。  
  
9. (選擇性) 按一下 [篩選] 來設定此群組的篩選條件。  
  
10. (選擇性) 按一下 [變數] 來定義此群組範圍內、可從任何子群組存取的變數。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-group-from-a-tablix-data-region"></a>若要從 Tablix 資料區刪除群組  
  
1.  在 [群組] 窗格中，以滑鼠右鍵按一下群組，然後按一下 [刪除群組]。  
  
2.  在 **[刪除群組]** 對話方塊中，選取下列其中一個選項：  
  
    -   **刪除群組及相關資料列和資料行** ：選擇此選項來刪除群組定義與顯示群組資料的所有相關資料列。 對於詳細資料群組而言，如果相同的資料列同時屬於詳細資料與群組資料，則只會刪除詳細資料資料列。  
  
    -   **只刪除群組** ：選擇此選項，讓 Tablix 資料區的結構保持相同，並僅刪除群組定義。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>若要從 Tablix 資料區刪除詳細資料群組  
  
1.  在 [群組] 窗格中，以滑鼠右鍵按一下詳細資料群組，然後按一下 [刪除群組]。  
  
2.  在 **[刪除群組]** 對話方塊中，選取下列其中一個選項：  
  
    -   **刪除群組及相關資料列和資料行** ：選擇此選項來刪除群組定義與顯示群組資料的所有相關資料列。 對於詳細資料群組而言，如果相同的資料列同時屬於詳細資料與群組資料，則只會刪除詳細資料資料列。  
  
    -   **只刪除群組** ：選擇此選項，讓 Tablix 資料區的結構保持相同，並僅刪除群組定義。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     已刪除詳細資料群組。  
  
    > [!NOTE]  
    >  確認移除詳細資料資料列之後，每個資料格中的運算式都會在適當時指定彙總運算式。 如有必要，編輯運算式以指定所需的彙總函式。  
  
## <a name="see-also"></a>另請參閱  
 [報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)   
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器和 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
