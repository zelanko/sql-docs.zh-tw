---
title: 在報表中捲動時將標頭保持可見 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 82a31e583123cf04893cffc928b0d8db80906489
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59951954"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>在報表中捲動時將標頭保持可見 (報表產生器及 SSRS)
  若要避免資料列和資料行的標籤在轉譯報表之後捲動到檢視畫面以外，可以將資料列或資料行的標題凍結。  
  
 如何控制資料列和資料行取決於您擁有資料表還是矩陣。 如果您有資料表，請設定靜態成員 (資料列和資料行標題) 來維持可見度。 如果您有矩陣，請設定資料列和資料行群組標頭來維持可見度。  
  
 如果您將報表匯出到 Excel，標頭將不會自動凍結。 您可以在 Excel 中凍結窗格。 如需詳細資訊，請參閱[匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)的**頁首和頁尾**一節。  
  
> [!NOTE]  
>  即使資料表包含資料列和資料行群組，您還是無法在捲動時維持這些群組標頭的可見度  
  
 下圖顯示一個資料表。  
  
 ![資料表](../media/table.png "資料表")  
  
 下圖顯示一個矩陣。  
  
 ![矩陣](../media/matrix.png "矩陣")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>若要在捲動時維持矩陣群組標頭的可見度  
  
1.  以滑鼠右鍵按一下 Tablix 資料區的資料列、資料行或角控點，然後按一下 **[Tablix 屬性]**。  
  
2.  在 **[一般]** 索引標籤的 **[資料列標頭]** 或 **[資料行標頭]** 下方選取 **[捲動時，標頭應保持可見]**。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>若要在捲動時將靜態 Tablix 成員 (資料列或資料行) 保持可見  
  
1.  在設計介面上，按一下資料表中的任何地方即可在群組窗格中顯示靜態成員以及群組。  
  
     ![群組窗格](../media/grouppane-updated.png "群組窗格")  
  
     [資料列群組] 窗格會顯示資料列群組階層的階層式靜態及動態成員，[資料行群組] 窗格則會為資料行群組階層顯示類似的內容。  
  
2.  在 [群組] 窗格的右邊按一下向下箭頭，然後按一下 **[進階模式]**。  
  
3.  在捲動時按一下您要保持可見的靜態成員 (資料列或資料行)。 [屬性] 窗格會顯示 **[Tablix 成員]** 屬性。  
  
     ![Tablix 成員屬性](../media/grouppane-tablixmember-updated.png "Tablix 成員屬性")  
  
4.  在 [屬性] 窗格中，設定**FixedData**至`True`。  
  
5.  針對您要在捲動時保持可見的相鄰成員重複這個步驟。  
  
6.  預覽報表。  
  
 當您向下或向側邊捲動一頁時，靜態的 Tablix 成員仍會維持在檢視中。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [在多個頁面上顯示資料列和資料行標頭 &#40;報表產生器及 SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [群組窗格 &#40;報表產生器&#41;](grouping-pane-report-builder.md)  
  
  
