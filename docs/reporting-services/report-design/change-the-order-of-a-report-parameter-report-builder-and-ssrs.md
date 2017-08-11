---
title: "變更報表參數 （報表產生器及 SSRS） 的順序 |Microsoft 文件"
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
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3377e943ddf7d8c7bd06aeab52ee263a754af25c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>變更報表參數的順序 (報表產生器及 SSRS)
  當您的相依參數列在它所相依的參數之前時，請變更報表參數的順序。 當您具有串聯參數，或是當您想要為使用者顯示一個參數的預設值，然後使用者才可選擇其他參數值時，參數順序會很重要。 相依報表參數包含指向報表參數之後的參數清單中的查詢參數的參考，它的預設值查詢或是有效值查詢中**報表資料**窗格。  
  
 您所看到的參數顯示在報表檢視器工具列上，當您執行報表時，決定內的參數順序**報表資料**窗格和自訂參數窗格中參數的位置。 如需詳細資訊，請參閱[自訂參數窗格中的報表 &#40;報表產生器 &#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>變更報表參數的順序  
  
您可以執行下列其中一項動作，來變更報表參數的順序：  
  
-   按一下中的參數**報表資料** 窗格中，並使用向上箭頭和向下箭頭按鈕，將參數高或較低的清單中，在下圖所示。  當您在 [報表資料] 窗格中變更參數的順序時，參數在參數窗格中的位置會變更。  
  
     ![變更報表資料 窗格中的參數順序](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "變更報表資料 窗格中參數的順序")  
  
-   在參數窗格中，將參數拖曳到窗格中的不同資料行或資料列。 當您變更在窗格中參數的位置時，參數順序會變更在**報表資料**窗格。 如需有關在窗格中移動參數的詳細資訊，請參閱[自訂參數窗格中的報表 &#40;報表產生器 &#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計工具 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [對話方塊、 窗格和精靈的報表產生器說明](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [將串聯參數加入至報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教學課程： 將參數加入您的報表 &#40;報表產生器 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [加入資料集篩選、 資料區域篩選和群組篩選 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [參數集合參考 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
