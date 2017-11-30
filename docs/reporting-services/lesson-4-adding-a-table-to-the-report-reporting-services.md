---
title: "第 4 課：將資料表新增至報表 (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
caps.latest.revision: "64"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: c073de93cfb1abee01a05e207fbce087ec44ade0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>第 4 課：將資料表加入至報表 (Reporting Services)
定義資料集之後，您就可以開始設計報表。 您可以將資料區域、文字方塊、影像和您要包含在報表中的其他項目拖放至設計介面來建立報表配置。  
  
包含基礎資料集之重複資料列的項目稱為「資料區域」。 基本報表只有一個資料區域，但是您可以加入其他資料區域，例如，當您想要將圖表加入至表格式報表時。 加入資料區域之後，您可以將欄位加入到資料區域中。  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>將資料表資料區域和欄位加入到報表配置中  
  
1.  在 [工具箱] 中，按一下 [資料表]，然後按一下設計介面並拖曳滑鼠。 報表設計師會繪製一個資料表資料區域，而且在設計介面的中央包含三個資料行。 [工具箱] 可能會顯示為 [報表資料] 窗格左側的索引標籤。 若要開啟 [工具箱]，請將指標移至 [工具箱] 索引標籤。如果看不到 [工具箱]，請按一下 [檢視] 功能表上的 [工具箱]。
  
     ![ssrs_ssdt_addtable](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  您也可以從設計介面中將資料表新增至報表。  以滑鼠右鍵按一下設計介面，按一下 [插入]，然後按一下 [資料表]。
2.  在 [報表資料] 窗格中，展開 **AdventureWorksDataset** 資料集來顯示欄位。  
  
3.  將 [日期] 欄位從 [報表資料] 窗格拖曳到資料表中的第一個資料行。  
  
    當您將欄位放到第一個資料行時，會出現兩種情況。 首先，資料將會顯示欄位名稱，也就是所謂的「欄位運算式」，並以方括弧括住：`[Date]`。 接著，資料行標頭值會自動加到標頭資料列中，就在欄位運算式的正上方。 依預設，這個資料行是欄位的名稱。 您可以選取標頭資料列文字，然後輸入新的名稱。  
  
4.  將 [順序] 欄位從 [報表資料] 窗格拖曳到資料表中的第二個資料行。  
  
5.  將 [產品] 欄位從 [報表資料] 窗格拖曳到資料表中的第三個資料行。  
  
6.  將 Qty 欄位拖曳到第三個資料行的右邊緣，直到出現垂直游標，而且滑鼠指標有一個加號 [+]。 放開滑鼠按鈕時，就會為 `[Qty]`建立第四個資料行。  
![ssrs_tutorial_addcolumn](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  以相同的方式加入 LineTotal 欄位，以建立第五個資料行。 資料行標頭是 Line Total。 報表設計師會將 LineTotal 分割成兩個字，藉以自動建立資料行的易記名稱。  
  
  
下圖顯示已擴展這些欄位的資料表資料區域：Date、Order、Product、Qty 和 Line Total。  
![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>預覽報表  
預覽報表讓您不必先將報表發行到報表伺服器，就可以檢視轉譯過的報表。 您可能想要時常在設計階段預覽您的報表。 此外，預覽報表也會針對設計和資料連接執行驗證，讓您能夠先更正錯誤和問題，然後再將報表發行至報表伺服器。  
  
#### <a name="to-preview-a-report"></a>若要預覽報表  
  
-   按一下 **預覽** 索引標籤。此時報表設計師會執行報表，並將它顯示在 [預覽] 檢視中。
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    下圖顯示 [預覽] 檢視中的部分報表。  
  
    ![預覽，有 5 個資料行的資料表詳細資料列](../reporting-services/media/rs-basictabledetailspreview.png "預覽，有 5 個資料行的資料表詳細資料列")  
  
    請注意，貨幣 (在 Line Total 資料行中) 具有 6 個小數位數，而且日期具有時間戳記。 您將在下一課中修正該格式。  
  
> [!NOTE]  
> 按一下 **[檔案]** 功能表上的 **[全部儲存]** ，即可儲存報表。  
  
## <a name="next-steps"></a>後續步驟  
您已經成功將資料表資料區域加入到報表中、將欄位加入到資料區域中，並預覽過您的報表。 下一步，您將格式化資料行標頭和日期以及貨幣值。 請參閱[第 5 課：格式化報表 &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
[資料表 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
