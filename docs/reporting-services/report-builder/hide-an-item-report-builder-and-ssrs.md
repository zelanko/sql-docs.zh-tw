---
title: "隱藏項目 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aa3e4553ddeb529ec8565a5599b2ce861f91bc38
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="hide-an-item-report-builder-and-ssrs"></a>隱藏項目 (報表產生器及 SSRS)
  當您想要有條件地根據報表參數或是您所指定的某些其他運算式來隱藏項目時，請設定報表項目的可見性。  
  
 您也可以設計報表來允許使用者根據按一下報表中文字方塊的動作來切換報表項目的可見性，例如針對鑽研報表。 如需詳細資訊，請參閱 [將展開或摺疊動作加入項目中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)。  
  
 下列程序描述如何根據常數或運算式，顯示或隱藏轉譯報表中的報表項目。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>隱藏報表項目  
  
1.  在報表設計檢視中，以滑鼠右鍵按一下報表項目，然後開啟其 [屬性] 頁面。  
  
    > [!NOTE]  
    >  若要選取整個資料表或矩陣資料區，請在資料區中按一下來選取它，以滑鼠右鍵按一下資料列、資料行或角控點，然後按一下 [Tablix 屬性]。  
  
2.  按一下 **[可見性]**。  
  
3.  在 **[一開始執行報表時]**中，指定當您一開始檢視報表時，是否要隱藏此項目：  
  
    -   若要顯示此項目，請按一下 **[顯示]**。  
  
    -   若要隱藏此項目，請按一下 **[隱藏]**。  
  
    -   若要指定在執行階段評估的運算式，請按一下 [依據運算式顯示或隱藏]。 輸入運算式或按一下運算式 (**fx**) 按鈕，在 [運算式] 對話方塊中建立運算式。  
  
        > [!NOTE]  
        >  當您指定可見性的運算式時，會設定報表項目的 Hidden 屬性，如下圖所示。 評估之後的運算式會在值為 False 時顯示此報表項目，並在值為 True 時隱藏此報表項目。   
        > ![Properties_Visibility 對話方塊與隱藏的屬性](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Properties_Visibility dialog and Hidden property")  
  
4.  按兩次 **[確定]** 。  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>隱藏資料表、矩陣或清單中的靜態資料列  
  
1.  在報表設計檢視中，按一下資料表、矩陣或清單來顯示資料列和資料行控點。  
  
2.  以滑鼠右鍵按一下資料列控點，然後按一下 [資料列可見性]。 **[資料列可見性]** 對話方塊隨即開啟。  
  
3.  若要設定可見性，請遵循第一個程序中的步驟 3 和 4。  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>若要隱藏資料表、矩陣或清單中的靜態資料行  
  
1.  在 [設計] 檢視中，選取資料表、矩陣或清單來顯示資料列和資料行控點。  
  
2.  以滑鼠右鍵按一下資料行控點，然後按一下 [資料行可見性]。  
  
3.  在 **[資料行可見性]** 對話方塊中，遵循第一個程序中的步驟 3 和 4。  
  
## <a name="see-also"></a>請參閱＜  
 [向下鑽研動作 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [將展開或摺疊動作加入項目中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
