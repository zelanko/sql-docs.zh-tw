---
title: 在矩陣和圖表上顯示相同的資料 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3c062c241a6949921b550460488316861e54e8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106011"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>在矩陣和圖表上顯示相同的資料 (報表產生器)
  當您想要在矩陣和圖表中顯示相同的資料時，必須針對兩個資料區設定屬性來指定相同的資料集，也必須針對篩選、群組、排序和資料設定相同的運算式。  
  
 資料 (報表資料集) 的兩個資料區都有相同的上階，因此您可以將互動式排序按鈕加入到矩陣中，讓使用者在按一下該按鈕時，可同時針對矩陣和圖表變更排序次序。 如需詳細資訊，請參閱 [將互動式排序加入至資料表或矩陣 &#40;報表產生器及 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
 若要使用矩陣資料行群組值做為圖表的圖例，您必須在圖表上指定數列資料的色彩，然後使用相同的色彩做為矩陣資料格中，顯示群組值之文字方塊的背景填滿色彩。 如需詳細資訊，請參閱[跨多個形狀圖指定一致的色彩 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
 如果您的群組定義有太多群組值，您的群組在執行階段可能有點混亂。 您可能需要篩選值、結合群組，或調整圖表的臨界值來為您結合群組。 如需詳細資訊，請參閱 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>若要加入矩陣和圖表來顯示相同的資料  
  
1.  在設計檢視中，開啟報表。  
  
2.  在 **[插入]** 索引標籤的 **[資料區域]** 群組中，按一下 **[矩陣]** ，然後按一下報表主體或報表主體中的矩形。 如此矩陣就會加入至報表。  
  
3.  在 **[插入]** 索引標籤的 **[資料區域]** 群組中，按一下 **[圖表]** ，然後選取圖表類型。 如此圖表就會加入至報表。  
  
4.  (選擇性) 在 [插入]  索引標籤的 [報表項目]  群組中，按一下 [矩形]  ，然後按一下報表。 如此矩形就會加入至報表。 將步驟 2 和 3 的矩陣與圖表拖曳至矩形中。  
  
     透過將多個資料區域放在矩形容器中，您可以協助控制檢視報表時，矩陣和圖表的呈現方式。  
  
     在接下來的幾個步驟中，您將選擇相同的資料集欄位以便顯示在矩陣和圖表中。  
  
5.  將數值資料集欄位從 [報表資料] 窗格拖曳到矩陣的 [資料] 資料格中。  
  
     依預設，彙總函式 Sum 用於計算群組值。 如果您變更矩陣中的彙總函式，也必須變更圖表中的彙總函式。  
  
6.  在矩陣中，以滑鼠右鍵按一下包含資料的資料格，再按一下 [文字方塊屬性]  ，然後按一下 [數字]  。 為資料集欄位值選擇適當的格式。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  將您在步驟 3 所選擇的相同資料集欄位拖曳到圖表上的 **[值]** 區域。  
  
9. 在圖表中，以滑鼠右鍵按一下 Y 軸，按一下 [軸屬性]  ，然後按一下 [數字]  。 為您在步驟 4 中選擇的資料選擇相同的格式。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在接下來的幾個步驟中，您會將矩陣資料列群組和圖表數列群組設定為相同的運算式，同時也設定圖表數列群組的排序次序。  
  
11. 從 [報表資料] 窗格中，將您要依矩陣資料列分組的資料集欄位拖曳到 [資料列群組] 窗格。  
  
     根據預設，矩陣資料列群組會加入與群組運算式相同的排序運算式。  
  
12. 將您在步驟 9 中所使用的相同資料集欄位拖曳到圖表的 **[數列群組]** 區域。  
  
13. 以滑鼠右鍵按一下 [數列群組]  區域中的群組，然後按一下 [數列群組屬性]  。  
  
14. 按一下 **[排序]** 。  
  
15. 按一下 **[加入]** 。 新的資料列會出現在排序運算式方格中。  
  
16. 在 [排序依據]  的下拉式清單中，選擇您在步驟 9 中選為分組依據的資料集欄位。  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在接下來的幾個步驟中，您會將矩陣資料行群組和圖表類別目錄群組設定為相同的運算式，同時也設定圖表類別目錄群組的排序次序。  
  
18. 從 [報表資料] 窗格中，將您要依矩陣資料行分組的資料集欄位拖曳到 [資料行群組] 窗格。  
  
     根據預設，矩陣資料行群組會加入與群組運算式相同的排序運算式。  
  
19. 將您在步驟 16 中所使用的相同資料集欄位拖曳到圖表的 **[類別目錄群組]** 區域。  
  
20. 以滑鼠右鍵按一下 [類別目錄群組]  區域中的群組，然後按一下 [類別目錄群組屬性]  。  
  
21. 按一下 **[排序]** 。  
  
22. 按一下 **[加入]** 。 新的資料列會出現在排序運算式方格中。  
  
23. 在 [排序依據]  的下拉式清單中，選擇您在步驟 16 中選為分組依據的資料集欄位。  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. 預覽結果。 矩陣資料列和資料行群組會顯示與圖表數列和類別目錄群組相同的資料。  
  
## <a name="see-also"></a>另請參閱  
 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
