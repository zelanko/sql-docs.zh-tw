---
title: 篩選頁面、圖表對話方塊（報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.filters.f1
- "10409"
- sql12.rtp.rptdesigner.seriesgroupproperties.filters.f1
- "10401"
- sql12.rtp.rptdesigner.chartproperties.filters.f1
- "10165"
ms.assetid: fab97b2f-d53f-42f2-900c-c159653d89ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 268ca47f33e8e2514b297c2bb2a30eb77b7a8f08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109135"
---
# <a name="filters-page-chart-dialog-boxes-report-builder-and-ssrs"></a>篩選頁面、圖表對話方塊 ((報表產生器及 SSRS)
  按一下以下對話方塊中的 **[篩選]** ：  
  
-   [**類別目錄群組屬性**] 對話方塊，在依類別目錄分組的數列中篩選資料點。  
  
-   [**圖表屬性**] 對話方塊，定義圖表的篩選選項。  
  
-   [**數列群組屬性**] 對話方塊，以限制所選群組中的數列數目。  
  
## <a name="options"></a>選項。  
 **加入**  
 按一下即可將新的篩選子句加入到清單。  
  
 **刪除**  
 按一下即可從清單中刪除選取的篩選子句。  
  
 **向上箭頭**  
 按一下即可將選取的篩選在清單中向上移動。  
  
 **向下箭頭**  
 按一下即可將選取的篩選在清單中向下移動。  
  
 **運算式**  
 輸入或選擇您要套用篩選的目標運算式。 請按一下 [運算式]\(**fx**) 按鈕來編輯運算式。  
  
 **資料類型**  
 選擇 [值]**** 的資料類型。 可能的話，請選擇符合 **[運算式]** 資料類型的資料類型。  
  
 
  **[運算式]** 與 **[值]** 中的值必須評估為相同的資料類型。 例如，如果 [運算式]**** 設定為具有 System.Int32 資料類型的欄位，而 [值]**** 設定為 7，請從下拉式清單中，選擇 [整數]****。  
  
 如果您所需要的資料類型選項不在此下拉式清單中，請撰寫運算式，以便將此值轉換為正確的資料類型。 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
 **運算子**  
 選擇要用來比較運算式和值的運算子。  
  
 **ReplTest1**  
 在 [運算式]**** 中，輸入運算式或是要用來評估運算式的值。  
  
## <a name="see-also"></a>另請參閱  
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
