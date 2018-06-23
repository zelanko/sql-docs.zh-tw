---
title: 篩選頁面、 圖表對話方塊 （報表產生器及 SSRS） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.filters.f1
- "10409"
- sql12.rtp.rptdesigner.seriesgroupproperties.filters.f1
- "10401"
- sql12.rtp.rptdesigner.chartproperties.filters.f1
- "10165"
ms.assetid: fab97b2f-d53f-42f2-900c-c159653d89ed
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5b695b45a43f388a7dabf64bad327404ef4f6510
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132363"
---
# <a name="filters-page-chart-dialog-boxes-report-builder-and-ssrs"></a>篩選頁面、圖表對話方塊 ((報表產生器及 SSRS)
  按一下以下對話方塊中的 **[篩選]** ：  
  
-   **[類別目錄群組屬性]** 對話方塊，在依類別目錄分組的數列中篩選資料點。  
  
-   **[圖表屬性]** 對話方塊，定義圖表的篩選選項。  
  
-   **[數列群組屬性]** 對話方塊，以限制選定群組中的數列數。  
  
## <a name="options"></a>選項。  
 **[加入]**  
 按一下即可將新的篩選子句加入到清單。  
  
 **刪除**  
 按一下即可從清單中刪除選取的篩選子句。  
  
 **向上箭頭**  
 按一下即可將選取的篩選在清單中向上移動。  
  
 **向下箭頭**  
 按一下即可將選取的篩選在清單中向下移動。  
  
 **運算式**  
 輸入或選擇您要套用篩選的目標運算式。 請按一下 [運算式]\(**fx**) 按鈕來編輯運算式。  
  
 **Data type**  
 選擇 [值] 的資料類型。 可能的話，請選擇符合 **[運算式]** 資料類型的資料類型。  
  
 **[運算式]** 與 **[值]** 中的值必須評估為相同的資料類型。 例如，如果 [運算式] 設定為具有 System.Int32 資料類型的欄位，而 [值] 設定為 7，請從下拉式清單中，選擇 [整數]。  
  
 如果您所需要的資料類型選項不在此下拉式清單中，請撰寫運算式，以便將此值轉換為正確的資料類型。 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
 **[運算子]**  
 選擇要用來比較運算式和值的運算子。  
  
 **ReplTest1**  
 在 [運算式] 中，輸入運算式或是要用來評估運算式的值。  
  
## <a name="see-also"></a>另請參閱  
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [篩選、 分組和排序資料&#40;報表產生器和 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  