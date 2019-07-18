---
title: 變更報表參數的順序 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a1d9413332ed19bd4db94fc60beecff85f02ac7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106325"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>變更報表參數的順序 (報表產生器及 SSRS)
  當您的相依參數列在它所相依的參數之前時，請變更報表參數的順序。 當您具有串聯參數，或是當您想要為使用者顯示一個參數的預設值，然後使用者才可選擇其他參數值時，參數順序會很重要。 相依報表參數包含了查詢參數的參考 (在它的預設值查詢或是有效值查詢中)，該查詢參數會指向 [報表資料] 窗格中參數清單內列在它後面的報表參數。  
  
 您在報表檢視器工具列上看到的參數顯示順序是由 [報表資料] 窗格內的參數順序所決定。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-order-of-report-parameters"></a>變更報表參數的順序  
  
1.  在 [報表資料] 窗格中，展開 [參數] 節點。  
  
2.  按一下參數，並使用 [報表資料] 窗格工具列上的向上箭頭和向下箭頭按鈕，在清單中將參數上移或下移。 下圖顯示報表產生器中的 [報表資料] 窗格。  
  
     ![報表資料窗格](../media/reportdatapane.png "報表資料窗格")  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [將串聯參數加入至報表 &#40;報表產生器和 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
