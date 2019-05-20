---
title: 變更報表參數的順序 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48da3d62e18a77bc8629d43ef170ca2b0622fe16
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581705"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>變更報表參數的順序 (報表產生器及 SSRS)
  當您的相依參數列在它所相依的參數之前時，請變更報表參數的順序。 當您具有串聯參數，或是當您想要為使用者顯示一個參數的預設值，然後使用者才可選擇其他參數值時，參數順序會很重要。 相依報表參數包含了查詢參數的參考 (在它的預設值查詢或是有效值查詢中)，該查詢參數會指向 [報表資料] 窗格中參數清單內列在它後面的報表參數。  
  
 當您執行報表時在報表檢視器工具列上看到的參數顯示順序，是由 [報表資料] 窗格內的參數順序和自訂參數窗格中參數的位置所決定。 如需詳細資訊，請參閱[自訂報表中的參數窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>變更報表參數的順序  
  
您可以執行下列其中一項動作，來變更報表參數的順序：  
  
-   按一下 [報表資料] 窗格中的參數，並使用向上箭頭和向下箭頭按鈕，在清單中將參數上移或下移，如下圖所示。  當您在 [報表資料] 窗格中變更參數的順序時，參數在參數窗格中的位置會變更。  
  
     ![變更 [報表資料] 窗格中的參數順序](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "變更 [報表資料] 窗格中的參數順序")  
  
-   在參數窗格中，將參數拖曳到窗格中的不同資料行或資料列。 當您變更參數在窗格中的位置時，[報表資料] 窗格中的參數順序會變更。 如需在窗格中移動參數的詳細資訊，請參閱[自訂報表中的參數窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [將串聯參數加入至報表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
