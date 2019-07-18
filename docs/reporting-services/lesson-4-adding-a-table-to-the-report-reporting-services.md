---
title: 第 4 課：將資料表新增至報表 (Reporting Services) | Microsoft Docs
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106011"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>第 4 課：將資料表加入至報表 (Reporting Services)

定義資料集之後，您就可以開始設計報表。 您會透過將「報表物件」  從 [工具箱]  窗格拖放到 [設計介面]  ，以建立報表版面配置。 某些報表物件的型別包含：

- Table
- 文字方塊
- image
- 線條
- 矩形
- 圖表
- 對應

包含基礎資料集之重複資料列的項目稱為「資料區域」  。 加入資料區域之後，您可以將欄位加入到資料區域中。 基本報表將只有一個資料區域。 您可以新增其他資料區域以顯示更多資訊，例如圖表。

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>將資料表資料區域和欄位新增至報表版面配置

1. 在報表設計師的左窗格中，選取 [工具箱]  索引標籤。 使用滑鼠選取 [資料表]  物件，並將它拖曳至報表設計介面。 報表設計師會繪製一個資料表資料區域，而且在設計介面的中央包含三個資料行。 如果您沒有看到 [工具箱]  索引標籤，請選取 [檢視]  功能表 > [工具箱]  。

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    您也可以從設計介面中將資料表新增至報表。 以滑鼠右鍵按一下設計介面，然後選取 [插入]   > [資料表]  。

2. 在 [報表資料]  窗格中，展開 AdventureWorksDataset 來顯示欄位。

3. 將 `[Date]` 欄位從 [報表資料]  窗格拖曳到資料表中的第一個資料行。

    > [!IMPORTANT]
    > 當您將欄位放到第一個資料行時，會出現兩種情況。 首先，報表設計師將會顯示欄位名稱，也就是所謂的「欄位運算式」  ，並在資料格中以方括弧括住：`[Date]`。 接著，會將資料行標籤加到標頭資料列，就在欄位運算式的正上方。 依預設，這個資料行標籤是欄位的名稱。 如果想要變更資料行標籤的值，可以選取該標籤，然後輸入新值。

4. 將 `[Order]` 欄位從 [報表資料]  窗格拖曳到資料表中的第二個資料行。

5. 將 `[Product]` 欄位從 [報表資料]  窗格拖曳到資料表中的第三個資料行。

6. 將 `[Qty]` 欄位拖曳到第三個資料行的右邊緣，直到出現垂直游標，而且滑鼠指標顯示一個加號 [+]。 放開滑鼠按鈕時，就會為 `[Qty]` 欄位運算式建立第四個資料行。

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. 以相同的方式加入 `[LineTotal]` 欄位，以建立第五個資料行。 資料行標籤會新增為 "Line Total"。 報表設計師會將 LineTotal 分割成兩個字，藉以自動建立資料行的易記名稱。

下圖顯示已擴展這些欄位的資料表資料區域：Date、Order、Product、Qty 和 Line Total。
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>預覽報表

預覽報表讓您不必先將報表發行到報表伺服器，就可以檢視轉譯過的報表。 請在設計報表時經常預覽報表。 這可以讓您驗證設計與資料連線，藉此在設計過程中更正錯誤與問題。

### <a name="to-preview-a-report"></a>若要預覽報表

- 選取 [預覽]  索引標籤。報表設計師會執行報表，並將在 [預覽]  檢視中顯示。

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

下圖顯示 [預覽]  檢視中的部分報表。

   ![預覽，有五個資料行的資料表詳細資料列](media/rs-basictabledetailspreview.png "預覽，有五個資料行的資料表詳細資料列")

看看日期和產品線總計值。 在下一課中，您將會了解如何將它們格式化以更整齊地顯示。

> [!NOTE]
> 按一下 [檔案]  功能表上的 **[全部儲存]** ，即可儲存報表。

## <a name="next-steps"></a>後續步驟

您已經成功將資料表資料區域加入到報表中、將欄位加入到資料區域中，並預覽過您的報表。 在下一課中，您將會了解如何將資料行標頭和欄位運算式格式化。 接著請繼續[第 5 課：格式化報表 &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)。
  
## <a name="see-also"></a>另請參閱

[資料表 &#40;報表產生器及 SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[資料集欄位集合 &#40;報表產生器及 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
