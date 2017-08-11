---
title: "資料區域 （報表產生器及 SSRS） 中設定沒有資料的訊息 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6d349eece0774513a2552fa1f7248ca89165769
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>在資料區域中設定沒有資料的訊息 (報表產生器及 SSRS)
  當您想要指定要在轉譯報表中顯示的文字來取代沒有資料的資料區時，請為資料表、矩陣或清單資料區域設定 NoRowsMessage 屬性，為圖表資料區設定 NoDataMessage，並為地圖的色階設定 NoDataText。 在執行階段，報表處理器會針對報表中的每一個資料集來執行查詢，而且資料集查詢可能不會產生任何結果集。 如果是繫結至空資料集的資料區，您可以指定要顯示的文字，而不是顯示空的資料區。 執行階段時如果子報表中的資料集都沒有資料，您也可以為子報表設定 NoRowsMessage 屬性。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>為資料表、矩陣或清單設定 NoRowsMessage 屬性  
  
1.  在 [設計] 檢視中，按一下設計介面上的資料表、矩陣或清單資料區或子報表來加以選取。 [屬性] 窗格會顯示所選取項目的屬性。  
  
2.  在 [屬性] 窗格中，輸入您想要在 **[NoRowsMessage]** 屬性欄位中顯示為訊息的文字。  
  
     另外，您也可以從下拉式清單按一下 [運算式]，開啟 [運算式] 對話方塊，然後建立運算式。  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>為圖表設定 NoDataMessage 屬性  
  
1.  在 [設計] 檢視中，按一下設計介面上的圖表加以選取。 [屬性] 窗格會顯示所選取項目的屬性。  
  
2.  在 [屬性] 窗格中，展開 **NoDataMessage**的節點。  
  
3.  在 **[屬性]**窗格中，輸入您想要在 **[NoDataMessage]** 屬性欄位中顯示為訊息的文字。  
  
     另外，您也可以從下拉式清單按一下 [運算式]，開啟 [運算式] 對話方塊，然後建立運算式。  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>為子報表設定 NoRowsMessage  
  
1.  在 [設計] 檢視中，按一下設計介面上的子報表加以選取。 [屬性] 窗格會顯示所選取項目的屬性。  
  
2.  在 [屬性] 窗格中，輸入您想要在 **[NoRowsMessage]** 屬性欄位中顯示為訊息的文字。  
  
     另外，您也可以從下拉式清單按一下 [運算式]，開啟 [運算式] 對話方塊，然後建立運算式。  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>若要為地圖的色階設定 NoDataText 屬性  
  
1.  在 [設計] 檢視中，按一下地圖上的色階加以選取。 [屬性] 窗格會顯示所選取項目的屬性。  
  
2.  在 [屬性] 窗格的 **[NoDataText]**中，輸入您要顯示成色彩標籤的文字 (不含資料值)。  
  
     另外，您也可以從下拉式清單按一下 [運算式]，開啟 [運算式] 對話方塊，然後建立運算式。  
  
## <a name="see-also"></a>另請參閱  
 [子報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [資料表、 矩陣和清單 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [對應 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [子報表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)  
  
  
