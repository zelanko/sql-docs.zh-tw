---
title: "加入篩選 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10ae54e7-0e8a-4dff-995d-05516c51d076
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 088e219e120eeb6b4608db9379811caf1b5406cd
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="add-a-filter-report-builder-and-ssrs"></a>加入篩選 (報表產生器及 SSRS)
  當您想要針對計算或顯示包含或排除特定值時，請將篩選加入至資料集、資料區或群組。 篩選會在執行階段先套用至資料集、套用至資料區，然後套用至群組 (按照群組階層的由上而下順序)。 在資料表、矩陣或清單中，系統會針對資料列群組、資料行群組和相鄰群組獨立套用篩選。 在圖表中，系統會針對類別目錄群組和數列群組獨立套用篩選。  
  
 若要加入篩選，您必須指定一或多個篩選方程式。 篩選方程式包含一個識別您想要篩選之資料的運算式、一個運算子和一個要比較的值。 篩選資料和值的資料類型必須相符。 不支援針對資料集或資料區的彙總值進行篩選。  
  
 若要篩選圖表中的資料點，您可以針對類別目錄群組或數列群組設定篩選。 依預設，圖表會使用內建函數 Sum，將屬於相同群組的值彙總成數列中的個別資料點。 如果您變更數列的彙總函式，就必須變更篩選運算式中的彙總函式。  
  
 如需篩選內嵌和共用資料集的詳細資訊，請參閱 [Add a Filter to a Dataset &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md) (將篩選加入資料集中 (報表產生器及 SSRS))。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-filter-on-a-data-region"></a>若要設定資料區的篩選  
  
1.  在 **[設計]** 檢視中，開啟報表。  
  
2.  選取設計介面上，資料區，然後以滑鼠右鍵按一下*\<資料區 >***屬性**。 若為量測計，請選取 **[量測計面板屬性]**。 *\<資料區 >***屬性**對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  在 Tablix 資料區上，以滑鼠右鍵按一下邊角資料格或是資料列或資料行控制代碼，然後按一下 [Tablix 屬性]。  
  
3.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
4.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
5.  在 **[運算式]**中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
6.  在下拉式方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
7.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
8.  在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]**中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱 [Filter Equation Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md) (篩選方程式範例 (報表產生器及 SSRS))。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-tablix-row-or-column-group"></a>設定 Tablix 資料列或資料行群組的篩選  
  
1.  在 **[設計]** 檢視中，開啟報表。  
  
2.  以滑鼠右鍵按一下設計介面上的資料表、矩陣或清單資料區域，即可加以選取。 [群組] 窗格會顯示選定項目的群組。  
  
3.  在 [群組] 窗格中，以滑鼠右鍵按一下群組，然後按一下 [編輯群組]。 **[Tablix 群組]** 對話方塊隨即開啟。  
  
4.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
5.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
6.  在 **[運算式]**中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
7.  在下拉式方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
8.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
9. 在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]**中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱 [Filter Equation Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md) (篩選方程式範例 (報表產生器及 SSRS))。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-category-group"></a>設定圖表類別目錄群組的篩選  
  
1.  在 **[設計]** 檢視中，開啟報表。  
  
2.  在設計介面上，按兩下圖表，即可開啟資料、數列和類別目錄欄位放置區。  
  
3.  以滑鼠右鍵按一下類別目錄欄位放置區所包含的欄位，然後選取 [類別目錄群組屬性]。  
  
4.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
5.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
6.  在 **[運算式]**中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
7.  在下拉式方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
8.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
9. 在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]**中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱 [Filter Equation Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md) (篩選方程式範例 (報表產生器及 SSRS))。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-series-group"></a>設定圖表數列群組的篩選  
  
1.  在 **[設計]** 檢視中，開啟報表。  
  
2.  在設計介面上，按兩下圖表，即可開啟資料、數列和類別目錄欄位放置區。  
  
3.  以滑鼠右鍵按一下數列欄位放置區所包含的欄位，然後選取 [數列群組屬性]。  
  
4.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
5.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
6.  在 **[運算式]**中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
7.  在下拉式方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
8.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
9. 在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]**中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱[篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
