---
title: 第 5 課：格式化報表 (Reporting Services) | Microsoft Docs
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "65105931"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>第 5 課：格式化報表 (Reporting Services)

既然您已經將資料區域和某些欄位加入到銷售訂單報表，您可以格式化日期和貨幣欄位，以及資料行標頭。

## <a name="format-the-date"></a><a name="bkmk_format_date"></a>將日期格式化

依預設，[Date] 欄位運算式會顯示日期和時間資訊。 您可以格式化該欄位以便只顯示日期。

1. 選取 [設計]  索引標籤。
2. 以滑鼠右鍵按一下含有 `[Date]` 欄位運算式的資料格，然後選取 [文字方塊屬性]  。
3. 按一下 [數字]  ，然後在 [類別目錄]  欄位中選取 [日期]  。
4. 在 **[類型]** 方塊中，選取 **[January 31, 2000]** 。
5. 選取 [確定]  來套用格式。
6. 預覽報表以查看 `[Date]` 欄位格式的變更，然後變更回設計檢視。

## <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>將貨幣格式化

LineTotal 欄位運算式會顯示一般數字。 您可以格式化該欄位，將數字顯示為貨幣。

1. 以滑鼠右鍵按一下含有 `[LineTotal]` 運算式的資料格，然後選取 [文字方塊屬性]  。
2. 在最左邊的資料行清單方塊中選取 [數字]  ，然後從 [類別]  清單方塊選取 [貨幣]  。
3. 如果您的地區設定為英文 (北美洲)，[類型]  清單方塊中的預設值應為：
    - **小數位數：2**
    - **負數：($12345.00)**
    - **符號：$ 英文 (美國)**
4. 選取 [使用千分位 (,) 符號]  。 如果範例文字顯示 **$12,345.00**，表示您的設定正確。
5. 選取 [確定]  來套用格式。
6. 預覽報表以查看 `[LineTotal]` 運算式資料行的變更，然後變更回設計檢視。  

## <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>變更文字樣式和資料行寬度

您可以透過將標頭資料列反白顯示，新增其他格式到您的報表，並調整資料行的寬度。

### <a name="to-format-header-rows-and-table-columns"></a>格式化標頭資料列和資料表資料行

1. 選取資料表，使資料行和資料列控點出現在資料表的上面和旁邊。 沿著資料表頂端和側邊的灰色長條是資料行和資料列控點。

2. 指向資料行控點之間的線條，使游標變成雙箭頭。 將資料行拖曳到所需的大小。
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. 選取包含資料行標頭標籤的資料列，然後從 [格式]  功能表選取 [字型]   > [粗體]  。

4. 預覽報表。 報表應顯示如下所示的內容：

    ![具有粗體資料行標頭的資料表預覽](media/rs-basictabledetailsformattedpreview.png "具有粗體資料行標頭的資料表預覽")  

5. 按一下 [檔案]  功能表上的 **[全部儲存]** ，即可儲存報表。

## <a name="next-steps"></a>後續步驟

您已經在本課成功格式化資料行標頭和欄位運算式。 下一步，您會將群組和總計加入至報表。 請繼續[第 6 課：新增群組和總計 &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)。

## <a name="see-also"></a>另請參閱

[格式化數字和日期 &#40;報表產生器及 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[ 轉譯行為 &#40;報表產生器及 SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
