---
title: 第 5 課：格式化報表 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f1acd7bf033ca2170a2a2b0cb1f701606510bf14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108426"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lesson 5: Formatting a Report (Reporting Services)
  既然您已經將資料區域和某些欄位加入到銷售訂單報表，您可以格式化日期和貨幣欄位，以及資料行標頭。  
  
 本主題內容：  
  
-   [格式化日期](#bkmk_format_date)  
  
-   [將貨幣格式化](#bkmk_format_currency)  
  
-   [變更文字樣式和資料行寬度](#bkmk_change_textstyle)  
  
##  <a name="bkmk_format_date"></a>格式化日期  
 依預設，[Date] 欄位會顯示日期和時間資訊。 您可以格式化該欄位以便只顯示日期。  
  
#### <a name="to-format-a-date-field"></a>將日期欄位格式化  
  
1.  按一下 **[設計]** 索引標籤。  
  
2.  以滑鼠右鍵按一下含有 `[Date]` 欄位運算式的資料格，然後按一下 [文字方塊屬性]****。  
  
3.  按一下 [**數位**]，然後在 [**類別目錄**] `Date`欄位中選取 []。  
  
4.  在 **[類型]** 方塊中，選取 **[January 31, 2000]**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  預覽報表以查看 `[Date]` 欄位的變更，然後變更回設計檢視。  
  
##  <a name="bkmk_format_currency"></a>將貨幣格式化  
 [LineTotal] 欄位會顯示一般數字。 格式化該欄位，將數字顯示為貨幣。  
  
#### <a name="to-format-a-currency-field"></a>格式化貨幣欄位  
  
1.  以滑鼠右鍵按一下含有 `[LineTotal]` 欄位運算式的資料格，然後按一下 [文字方塊屬性]****。  
  
2.  按一下 **[數字]**，然後在 **[類別目錄]** 欄位中選取 **[貨幣]**。  
  
3.  如果您的地區設定為英文 (美國)，預設值應為：  
  
    -   **小數位數：2**  
  
    -   **負數：（$12345.00）**  
  
    -   **符號： $ 英文（美國）**  
  
4.  選取 [使用千分位 (,) 符號]****。  
  
     如果範例文字為：**$12,345.00**，表示您的設定正確。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  預覽報表以查看 `[LineTotal]` 欄位的變更，然後變更回設計檢視。  
  
##  <a name="bkmk_change_textstyle"></a>變更文字樣式和資料行寬度  
 您也可以變更標頭資料列的格式，以便與報表中資料的資料列區分。 最後，您將調整資料行的寬度。  
  
#### <a name="to-format-header-rows-and-table-columns"></a>格式化標頭資料列和資料表資料行  
  
1.  按一下資料表，使資料行和資料列控點出現在資料表的上面和旁邊。  
  
     ![設計具有頁首資料列和詳細資料列的資料表](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "設計具有頁首資料列和詳細資料列的資料表")  
  
     沿著資料表頂端和側邊的灰色長條是資料行和資料列控點。  
  
2.  指向資料行控點之間的線條，使游標變成雙箭頭。 將資料行拖曳到所需的大小。  
  
3.  選取資料列包含資料行標頭標籤，然後從 **[格式]** 功能表指向 **[字型]** ，然後按一下 **[粗體]**。  
  
4.  若要預覽報表，請按一下 [**預覽**] 索引標籤。看起來應該像這樣：  
  
     ![具有粗體資料行標頭的資料表預覽](../../2014/tutorials/media/rs-basictabledetailsformattedpreview.gif "具有粗體資料行標頭的資料表預覽")  
  
5.  按一下 **[檔案]** 功能表上的 **[全部儲存]** ，即可儲存報表。  
  
## <a name="next-steps"></a>後續步驟  
 您已經成功格式化資料行標頭和日期以及貨幣值。 下一步，您會將群組和總計加入至報表。 請參閱[第 6 課：新增群組和總計 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
