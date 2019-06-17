---
title: 資料集屬性對話方塊、 篩選 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10025"
ms.assetid: 933a6f44-4eb7-4e73-9c40-ac0fd17b23d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 01d9c5b6ae0e69febd45008bf0aa7b6c3b5a83d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109375"
---
# <a name="dataset-properties-dialog-box-filters-report-builder"></a>資料集屬性對話方塊、篩選 (報表產生器)
  選取 **[資料集屬性]** 對話方塊上的 **[篩選]** ，即可建立資料集的篩選。  
  
 屬於報表伺服器上共用資料集定義之一部分的篩選會影響所有使用共用資料集的報表。 當共用資料集加入至報表之後，可以為共用資料集指定其他篩選。 這些篩選只會影響其定義所在的報表。  
  
 內嵌資料集的篩選只會影響其定義所在的報表。  
  
 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項  
 **[加入]**  
 將新的篩選子句加入到清單中。  
  
 **刪除**  
 從清單中刪除選取的篩選子句。  
  
 **向上箭頭**  
 將清單中所選取的篩選向上移動。  
  
 **向下箭頭**  
 將清單中所選取的篩選向下移動  
  
 **運算式**  
 輸入或選擇您要套用篩選的目標運算式。 請按一下 [運算式]\(**fx**) 按鈕來編輯運算式。  
  
 **Data type**  
 選擇 [值]  的資料類型。 可能的話，請選擇符合 **[運算式]** 資料類型的資料類型。  
  
 **[運算式]** 與 **[值]** 中的值必須評估為相同的資料類型。 例如，如果 [運算式]  設定為具有 System.Int32 資料類型的欄位，而 [值]  設定為 7，請從下拉式清單中，選擇 [整數]  。  
  
 如果您所需要的資料類型選項不在此下拉式清單中，請撰寫運算式，以便將此值轉換為正確的資料類型。 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
 **運算子**  
 選擇要用來比較運算式和值的運算子。  
  
 **值**  
 評估在 [運算式]  方塊中指定的運算式時，輸入要使用的運算式或值。 請按一下 [運算式]\(**fx**) 按鈕來編輯運算式。  
  
## <a name="see-also"></a>另請參閱  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [將篩選加入資料集&#40;報表產生器及 SSRS&#41;](report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)   
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
