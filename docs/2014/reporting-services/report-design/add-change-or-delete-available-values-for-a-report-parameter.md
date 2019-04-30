---
title: 加入、 變更或刪除可用的值為報表參數 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e0807838468e00ea9d6a323ac5ab1542ac1e06d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185938"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter-report-builder-and-ssrs"></a>為報表參數加入、變更或刪除可用的值 (報表產生器及 SSRS)
  當您建立報表參數之後，可以指定要對使用者顯示的可用值清單。 可用值清單會將使用者可以做的選擇限制為參數的有效值。  
  
 當執行報表時，可用的值會出現在工具列上報表參數旁邊的下拉式清單中。 報表參數可代表一個值或多個值。 如果是多個值，清單的最開頭是 **[全選]** 功能，好讓使用者只需按一下就可以選取或清除所有值。  
  
 您可以提供靜態值清單或是報表資料集中的清單。 您可以選擇指定標籤欄位來提供值的易記名稱。 例如，如果是根據 `ProductID` 欄位的參數，您可以在參數標籤中顯示 `ProductName` 欄位。 當報表執行時，使用者可以從產品名稱中進行選擇，但是實際選擇的值會是對應的 `ProductID`。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 在您發行報表之後，可以在報表伺服器上設定參數屬性值，藉以覆寫您在報表撰寫工具中定義於報表的可用值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>為報表參數加入或變更可用的值  
  
1.  在 [報表資料] 窗格中，展開 [參數] 節點。 以滑鼠右鍵按一下參數，然後按一下 [參數屬性]。 **[報表參數屬性]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視]，然後按一下 [報表資料]。  
  
2.  按一下 **[可用的值]**。 選取可用的值選項：  
  
    -   按一下 [指定值]，以手動方式提供值的清單，並可選擇提供值的易記名稱 (標籤)。  
  
         按一下 **[加入]** ，然後在 **[值]** 文字方塊中輸入值，並選擇在 **[標籤]** 文字方塊內輸入標籤。 若未提供標籤，就會使用這個值。 您可以撰寫值的運算式。 資料類型必須符合參數的資料類型。 欄位名稱不能用於參數的運算式。 如需範例，請參閱[常用的篩選 &#40;報表產生器及 SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)。  
  
         請重複這個步驟，盡量提供您想要的值。 您在這個清單中看到的項目順序會決定使用者在下拉式清單中看到它們的順序。 若要變更某個項目在清單中的順序，請按一下 **[值]** 或 **[標籤]** 文字方塊來選取此項目，然後使用向上箭頭和向下箭頭按鈕，將此項目移到清單中的更高或更低位置。  
  
    -   按一下 **[從查詢取得值]** 可提供現有資料集名稱 (該資料集會擷取值)，並可選擇為這個參數提供易記名稱。  
  
        > [!IMPORTANT]  
        >  如果相同資料集包含報表參數的對應查詢參數，報表就會在您嘗試執行時顯示錯誤訊息。 使用不同資料集來擷取值，即可解決這個錯誤。  
  
         在 **[資料集]** 中，選擇此資料集的名稱。  
  
         在 **[值欄位]** 中，選擇可提供參數值的欄位名稱。  
  
         在 **[標籤欄位]** 中，選擇可為參數提供易記名稱的欄位名稱。 如果易記名稱沒有個別的欄位，請選擇與 **[值]** 欄位相同的欄位。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     當您預覽報表時，您會看到此參數之可用值的下拉式清單。  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>移除報表參數的可用值  
  
1.  在 [報表資料] 窗格中，展開 [參數] 節點。 以滑鼠右鍵按一下參數，然後按一下 [參數屬性]。 **[報表參數]** 對話方塊隨即開啟。  
  
2.  按一下 **[可用的值]**。  
  
3.  在 **[選取下列其中一個選項]** 中，按一下 **[無]**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     當您預覽報表時，此參數之可用值的下拉式清單便不再出現。  
  
## <a name="see-also"></a>另請參閱  
 [變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [加入、變更或刪除報表參數 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [將串聯參數加入至報表 &#40;報表產生器及 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [為報表參數加入、變更或刪除預設值 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
