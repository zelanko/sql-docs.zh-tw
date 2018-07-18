---
title: 教學課程：將圓形圖新增至報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 70d23d19f2719aaa86ba81617bfb33544279bd2b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236238"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>教學課程：將圓形圖加入至報表 (報表產生器)
  圓形圖和環圈圖會將資料顯示為整體所佔的百分比。 圓形圖最常用於在群組之間進行比較。 圓形圖和環圈圖以及金字塔圖和漏斗圖會構成一組稱為形狀圖的圖表。 形狀圖沒有軸。 在形狀圖上放置數值欄位時，圖表會計算出每個值佔整體的百分比。  
  
 如果圓形圖上的資料點過多，資料點標籤可能會太擁擠而難以閱讀。 在這種狀況下，請考慮使用折線圖。 只有在您已將資料彙總成少數資料點之後，才應該考慮使用圓形圖。  
  
 下圖顯示您將建立的圓形圖。  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學會如何：  
  
1.  [從圖表精靈建立圓形圖](#Chart)  
  
2.  [選擇圖表類型](#ChartType)  
  
3.  [在每個配量中顯示百分比](#Percentages)  
  
4.  [將小配量結合成一個扇區](#CombineSlices)  
  
5.  [自訂繪圖效果](#DrawingEffect)  
  
6.  [加入報表標題](#Title)  
  
7.  [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併為兩個程序。 如需如何瀏覽至報表伺服器、新增資料來源以及新增資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 完成本教學課程的估計時間：10 分鐘  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Chart"></a> 1.從圖表精靈建立圓形圖  
 從 [使用者入門] 對話方塊，使用 [圖表精靈] 建立內嵌資料集，並選擇共用資料來源，然後建立圓形圖。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-new-chart-report"></a>建立新的圖表報表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
     [使用者入門] 對話方塊隨即出現。  
  
    > [!NOTE]  
    >  如果 [使用者入門] 對話方塊沒有出現，請從 [報表產生器] 按鈕按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 [圖表精靈]。  
  
4.  在 [選擇資料集] 頁面上，按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    >  只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按 [下一步] 。  
  
##  <a name="ChartType"></a> 2.選擇圖表類型  
 您可以選擇各種不同預先定義的圖表類型。  
  
#### <a name="to-add-a-pie-chart"></a>加入圓形圖  
  
1.  在 [**選擇圖表類型**頁面上，按一下**圓形圖**，然後按一下**下一步]**。 [排列圖表欄位] 頁面隨即開啟。  
  
     在 [排列圖表欄位] 頁面上，將 [Product] 欄位拖曳至 [類別目錄] 窗格。 類別目錄會定義圓形圖中的配量數目。 在這則範例中，共有八個配量，每一個代表一個產品。  
  
2.  將 [Sales] 欄位拖曳至 [值] 窗格。 Sales 代表每個子類別目錄的銷售量。 因為圖表會顯示每項產品的彙總，所以 [值] 窗格會顯示 `[Sum(Sales)]`。  
  
3.  按 [下一步] 。  
  
4.  在 [**選擇樣式**] 頁面上，在 [樣式] 窗格中，選取樣式。  
  
     樣式會指定字型樣式、色彩集和框線樣式。 當您選取樣式時，[預覽] 窗格會顯示具有該樣式的圖表範例。  
  
5.  按一下 **[完成]**。  
  
     圖表就會加入至設計介面。  
  
6.  按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，即可增加圖表的大小。 請注意，報表設計介面的大小會放大，以容納圖表的大小。  
  
7.  按一下 **[執行]** 預覽報表。  
  
 報表會顯示畫分有八個配量的圓形圖，每一塊表示一個產品。 每個配量的大小代表該產品的銷售量。 其中 3 塊配量極少。  
  
##  <a name="Percentages"></a> 3.在每一塊配量中顯示百分比  
 在圓形圖的每個配量上，您可以顯示這個配量相較於整個圓形圖的百分比。  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>若要在圓形圖的每個配量中顯示百分比  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圓形圖，然後按一下 [顯示資料標籤]。 資料標籤就會顯示在圖表上。  
  
3.  以滑鼠右鍵按一下標籤，然後按一下**數列標籤屬性**。  
  
4.  在 標籤資料，從下拉式清單方塊中，選取 **#PERCENT{P0}</USERINPUT&GT**。  
  
     若要以百分比顯示值，UseValueAsLabel 屬性必須為 False。 如果系統提示您在 [確認動作] 對話方塊中設定這個值，請按一下 [是]。  
  
5.  （選擇性）若要指定標籤所顯示的小數位數，請輸入`#PERCENT{Pn}`何處*n*是要顯示的小數位數。 例如，若要顯示任何小數位數，請輸入`#PERCENT{P0}`。  
  
    > [!NOTE]  
    >  當您格式化百分比時，[數列標籤屬性] 對話方塊中的 [數字格式] 沒有任何作用。 這會將標籤格式化成百分比，但是不會計算每個配量所代表的圓形圖百分比。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  按一下 **[執行]** 預覽報表。  
  
 報表會顯示每個圓形圖配量佔整體的百分比。  
  
##  <a name="CombineSlices"></a> 4.將較小的配量收集成一塊配量  
 圓形圖中有 3 塊配量極少。 您可以將多個比例較小的配量結合為一個代表所有配量的較大配量。  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>若要將圓形圖上小於 5% 的任何配量結合成單一配量  
  
1.  切換到報表設計檢視。  
  
2.  在 **檢視**索引標籤中，於**顯示/隱藏**群組中，選取**屬性**。  
  
3.  在設計介面上按一下圓形圖的任何配量。 數列的屬性會顯示在 [屬性] 窗格中。  
  
4.  在 [一般]  區段中，展開 [CustomAttributes]  節點。  
  
5.  將 **CollectedStyle** 屬性設定為 **SingleSlice**。  
  
6.  確認 **CollectedThreshold** 屬性設定為 5。  
  
7.  確認 **CollectedThresholdUsePercent** 屬性設定為 **True**。  
  
8.  功能區上**首頁**索引標籤上，按一下**執行**預覽報表。  
  
 在圖例中，現在「其他」類別目錄就會存在。 新的圓形圖配量會將低於 5% 的所有配量結合成一個佔整個圓形圖 6% 的配量。  
  
##  <a name="DrawingEffect"></a> 5.自訂繪圖效果  
 在 [圖表精靈] 中，圓形圖的自訂樣式為 Ocean，外觀具有 Concave 的繪圖效果。 您可以在執行精靈後變更這個項目。  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>若要將繪製效果加入至圓形圖  
  
1.  切換到報表設計檢視。  
  
2.  如果 [屬性] 窗格尚未開啟，在**檢視**索引標籤上，選取**屬性**。  
  
3.  按兩下圓形圖本身。 圓形圖的數列屬性就會顯示在 [屬性] 窗格中。  
  
4.  在 [屬性] 窗格中，展開 **[CustomAttributes]** 節點。  
  
5.  設定**PieDrawingStyle**要 **[softedge]**。  
  
    > [!NOTE]  
    >  繪製效果和三維效果是互斥的選項。 如果圖表已經套用，三維效果**PieDrawingStyle**並沒有出現在 [屬性] 窗格。  
  
6.  按一下 **[執行]** 預覽報表。  
  
 下圖顯示具有柔邊效果的圓形圖。  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6.加入報表標題  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **Camera and Camcorder Sales**並按 ENTER，然後輸入 **As a Percentage of Total Sales**，它看起來如下：  
  
     **Camera and Camcorder Sales**  
  
     **As a Percentage of Total Sales**  
  
3.  選取**相機與攝錄影機銷售**，然後按一下**粗體**按鈕**字型**一節**首頁**功能區 索引標籤。  
  
4.  選取  **As a Percentage of Total Sales**，然後在**字型**區段**首頁**索引標籤上，將字型大小設定為**10**。  
  
5.  (選擇性) 您可能需要增加 [標題] 文字方塊的高度，才能容納兩行文字。  
  
     這個標題就會顯示在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
6.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Save"></a> 7.儲存報表  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  在 [報表產生器] 按鈕中，按一下 **[另存新檔]**。  
  
3.  在 [名稱] 中，鍵入 **Sales Pie Chart**。  
  
4.  按一下 **[儲存]**。  
  
 您的報表就會儲存在報表伺服器上。  
  
## <a name="next-steps"></a>後續步驟  
 您已成功完成「將圓形圖加入至報表」教學課程。 若要深入了解圖表，請參閱[圖表 &#40;報表產生器及 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) 和[走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
