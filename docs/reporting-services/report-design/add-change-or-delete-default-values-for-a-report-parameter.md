---
title: "加入、 變更或刪除報表參數的預設值 |Microsoft 文件"
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
f1_keywords:
- "10460"
- sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: aca61d548532fcb6f61c23130e34bf426c8672c9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="add-change-or-delete-default-values-for-a-report-parameter"></a>為報表參數加入、變更或刪除預設值
  當您建立報表參數以後，可以提供預設值的清單。 如果所有的參數都有有效的預設值，當您第一次檢視或預覽報表時，報表就會自動執行。  
  
 報表參數可代表一個值或多個值。 如果是單一值，您可以提供常值或運算式。 如果是多個值，您可以提供靜態清單或報表資料集中的清單。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 在您發行報表之後，可以在報表伺服器上設定參數屬性值，藉以覆寫您在報表撰寫工具中定義於報表的預設值。 您也可以建立連結報表來提供多組預設參數值。 如需詳細資訊，請參閱  [Report Parameters &#40;Report Builder and Report Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>為報表參數加入或變更預設值  
  
1.  在 [報表資料] 窗格中，展開 [參數] 節點。 以滑鼠右鍵按一下此參數，然後按一下 [編輯]。 **[報表參數屬性]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視]，然後按一下 [報表資料]。  
  
2.  按一下 **[預設值]**。  
  
3.  選取預設選項：  
  
    -   若要手動提供某個值或值清單，請按一下 [指定值]。 按一下 [加入]，然後在 [值] 文字方塊中輸入值。 您可以撰寫值的運算式。 資料類型必須符合參數的資料類型。 欄位名稱不能用於參數的運算式。  
  
         如果是多值參數，請重複這個步驟，盡量提供您想要的值。 您在這個清單中看到的項目順序會決定使用者在下拉式清單中看到它們的順序。 若要變更某個項目在清單中的順序，請按一下 [值] 文字方塊來選取此項目，然後使用向上箭頭和向下箭頭按鈕，將此項目移到清單中的更高或更低位置。  
  
    -   若要提供現有資料集名稱 (該資料集會擷取值)，請按一下 [從查詢取得值]。 在 **[資料集]**中，選擇此資料集的名稱。  
  
         在 **[值欄位]**中，選擇可提供參數值的欄位名稱。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>移除報表參數的預設值  
  
1.  在 [報表資料] 窗格中，展開 [參數] 節點。 以滑鼠右鍵按一下此參數，然後按一下 [編輯]。 **[報表參數屬性]** 對話方塊隨即開啟。  
  
2.  按一下 **[預設值]**。  
  
3.  在 [選取下列其中一個選項] 中，按一下 [沒有預設值]。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計工具 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [將串聯參數加入至報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教學課程： 將參數加入您的報表 &#40;報表產生器 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [加入資料集篩選、 資料區域篩選和群組篩選 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [參數集合參考 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [變更報表參數 &#40; 順序報表產生器及 SSRS &#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [加入、 變更或刪除報表參數 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
