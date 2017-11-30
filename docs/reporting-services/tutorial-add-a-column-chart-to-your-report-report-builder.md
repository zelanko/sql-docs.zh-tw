---
title: "教學課程：將直條圖新增至報表 (報表產生器) | Microsoft Docs"
ms.custom: 
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b1768cbe53155ec37c5f6dd690542b90e22a59cd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>教學課程：將直條圖加入至報表 (報表產生器)
在本教學課程中，您將建立包含直條圖的 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分頁報表，而直條圖是依據類別目錄群組，將數列顯示為一組垂直線。 

直條圖可用於：  
  
-   顯示一段時間的資料變更。  
-   比較多個數列的相對值。  
-   顯示移動平均來呈現趨勢。  
  
下圖顯示您將建立的直條圖，內含移動平均。  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> 在本教學課程中，精靈的步驟會合併為一個程序。 如需如何瀏覽至報表伺服器、選擇資料來源以及建立資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
完成本教學課程的估計時間：15 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Chart"></a>1.從圖表精靈建立圖表報表  
在本節中，您可以使用 [圖表精靈] 建立內嵌資料集，並選擇共用資料來源，然後建立直條圖。  
  
> [!NOTE]  
> 在本教學課程中，查詢包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
### <a name="to-create-a-chart-report"></a>建立圖表報表  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果您看不到 [新增報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 [圖表精靈]。  
  
4.  在 [選擇資料集] 頁面上，按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    > 只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按一下 **[下一步]**。  
  
## <a name="ChartType"></a>2.選擇圖表類型  
您可以從數個預先定義的圖表類型中進行選擇，然後在完成精靈之後修改圖表。  
  
### <a name="to-add-a-column-chart"></a>加入直條圖  
  
1.  在 [選擇圖表類型] 頁面上，直條圖是預設圖表類型。 按一下 **[下一步]**。  
  
2.  在 [排列圖表欄位] 頁面上，將 [SalesDate] 欄位拖曳至 [類別目錄]。 類別目錄會顯示在水平軸上。  
  
3.  將 [Sales] 欄位拖曳至 [值]。 [值] 方塊會顯示 [Sum(Sales)]，因為系統會針對每個日期彙總銷售總計值的總和。 值會顯示在垂直軸上。  
  
4.  按一下 **[下一步]**。  
 
6.  按一下 **[完成]**。  
  
    圖表就會加入至設計介面。 請注意，新的直條圖只會顯示代表性資料。 圖例會顯示 Sales Date A、Sales Date B 等，只會提供報表的外觀。 
    
    ![report-builder-column-chart-1-design-view](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，即可增加圖表的大小。 請注意，報表設計介面的大小會放大，以容納圖表的大小。  
  
8.  按一下 **[執行]** 預覽報表。  

    ![report-builder-column-chart-1-preview](../reporting-services/media/report-builder-column-chart-1-preview.png)

請注意，圖表並未在水平軸上標示每個類別目錄。 根據預設，只有容納在軸旁的標籤才會包含在內。 
  
## <a name="Horizontal"></a>3.格式化水平軸上的日期  
根據預設，水平軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下水平軸 > [水平軸屬性]。  
  
3.  在 [數字] 索引標籤的 [類別目錄] 中，選取 [日期]。  
  
5.  在 [類型] 方塊中，選取 [31 Jan 2000]。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在 [主資料夾] 索引標籤上，按一下 [執行] 預覽報表。  
  
日期會以您所選取的日期格式顯示。 圖表仍然未在水平軸上標示每個類別目錄。 

![report-builder-column-chart-2-preview](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
您可以透過旋轉標籤和指定間隔，自訂標籤顯示。  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4.旋轉水平軸上的軸標籤  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下水平軸標題，然後按一下 [顯示軸標題] 以移除標題。 因為水平軸會顯示日期，所以不需要這個標題。  
  
3.  以滑鼠右鍵按一下水平軸 > [水平軸屬性]。  
  
5.  在 [標籤] 索引標籤的 [變更軸標籤自動調整選項] 下，選取 [停用自動調整]。  
  
7.  在 [標籤旋轉角度] 中，選取 [-90]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    水平軸的範例文字會旋轉 90 度。  
    
    ![report-builder-column-chart-rotate-x-axis](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. 按一下 **[執行]** 預覽報表。  
  
在圖表上，會旋轉標籤。  

![report-builder-column-chart-rotate-x-axis-preview](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5.移動圖例  
圖例是從類別目錄和數列資料自動建立。 您可以移動直條圖之圖表區域下方的圖例。  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圖表上的圖例 > [圖例屬性]。  
  
3.  在 [配置與位置] 下，選取不同的位置。 例如，選取下層中間選項。  
  
    當圖例位於圖表的頂端或底部時，圖例的配置就會從垂直變更為水平。 您可以在 [配置] 方塊中選取不同的配置。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (選擇性) 因為這個教學課程只有一個類別目錄，所以圖表不需要圖例。 若要移除它，請以滑鼠右鍵按一下圖例 > [刪除圖例]。  
  
6.  按一下 **[執行]** 預覽報表。  
  
## <a name="ChartTitle"></a>6.為圖表加上標題  
    
1.  切換到報表設計檢視。  
  
2.  選取圖表頂端的 [圖表標題] 這幾個字，然後鍵入 **Store Sales Order Totals**。  
  
3.  按一下 **[執行]** 預覽報表。  
  
## <a name="Vertical"></a>7.格式化及標示垂直軸  
根據預設，垂直軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。   
  
1.  切換到報表設計檢視。  
  
2. 在圖表的側邊，按一下垂直軸上的標籤，以便選取。  
  
3.  在 [主資料夾] 索引標籤 > [數字] 群組中，按一下 [貨幣] 按鈕。 這些軸標籤就會變更為顯示貨幣格式。  
  
4.  按兩次 [減少小數位數] 按鈕，以顯示四捨五入到最接近之美金的數字。  
  
5.  以滑鼠右鍵按一下垂直軸 > [垂直軸屬性]。  
  
6.  在 [數字] 索引標籤上，請注意，[類別目錄] 方塊中已選取 [貨幣]，而且 [小數位數] 已經是 [0] (零)。  
  
7.  核取 [值的顯示單位]。 已選取 [千]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 以滑鼠右鍵按一下垂直軸 > [顯示軸標題]。 

10. 以滑鼠右鍵按一下垂直軸標題 > [軸標題屬性]。  
  
10. 將 [標題文字] 欄位中的文字取代為 [銷售總計 (以千為單位)]。 您也可以指定各種有關如何格式化標題的選項。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 按一下 **[執行]** 預覽報表。  

    ![report-builder-column-chart-format-y-axis](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8.顯示水平 (x) 軸上的所有標籤

您會注意到只會在 x 軸上顯示部分標籤。 在本節中，您可以在 [屬性] 窗格中設定要全部顯示的屬性。

1.  切換到報表設計檢視。  
  
2.  按一下圖表，然後選取水平軸標籤。

3. 在 [屬性] 窗格中，將 LabelInterval 設為 1。

    ![report-builder-column-chart-set-label-interval](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    這個圖表與在設計檢視中相同。 
    
5.  按一下 **[執行]** 預覽報表。

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    現在，圖表會顯示其所有標籤。
  
## <a name="Average"></a>9.新增具有導出數列的移動平均  

移動平均是數列中資料的平均，是根據時間而計算。 移動平均可以找出趨勢。
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示 [圖表資料] 窗格。  
  
3.  以滑鼠右鍵按一下 [值] 區域中的 [Sum(Sales)] 欄位，然後按一下 [新增導出數列]。  

     ![report-builder-column-chart-add-calculated-series](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  在 [公式] 中，確認已選取 [移動平均]。  
  
5.  在 [設定公式參數] 中，針對 [週期] 選取 [4]。  
  
6.  在 [框線] 索引標籤的 [線條寬度] 中，選取 [3pt]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 按一下 **[執行]** 預覽報表。  
  
圖表會顯示一條線，代表依照日期區分之總銷售量的移動平均 (每四個日期的平均)。 深入了解如何 [將移動平均新增至圖表](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)。 

![report-builder-column-chart-moving-average](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10.加入報表標題  
  
1.  切換到報表設計檢視。  
  
2.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
3.  輸入 **銷售圖表**並按 ENTER，然後輸入 **2015 年 1 月到 12 月**，其外觀如下：  
  
    **銷售圖表**  
  
    **2015 年 1 月到 12 月**  
  
4.  選取 [銷售圖表]，然後選取 [主資料夾] 索引標籤 > [字型] 區段 > [粗體]。  
  
5.  選取 [2015 年 1 月到 12 月]，然後選取 [主資料夾] 索引標籤 > [字型] 區段 > 將字型大小設為 [10]。  
  
6.  (選擇性) 您可能需要增加 [標題] 文字方塊的高度，才能容納兩行文字。 當您按下邊緣的中間時，會下拉雙箭號。 而且，您可能需要拖曳圖表的頂端，讓標題不重疊。  
  
    這個標題會出現在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
7.  按一下 **[執行]** 預覽報表。  
  
## <a name="Save"></a>11.儲存報表  
  
### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  在 [報表產生器] 按鈕中，按一下 **[另存新檔]**。  

    您可以將它儲存至電腦或報表伺服器。
  
3.  在 [名稱] 中，鍵入 **Sales Order Column Chart**。  
  
4.  按一下 **[儲存]**。  
  
## <a name="next-steps"></a>後續步驟  
您已成功完成「將直條圖加入至報表」教學課程。 若要深入了解圖表，請參閱[圖表 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 和[走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
-    [報表產生器教學課程](../reporting-services/report-builder-tutorials.md) 
-    [SQL Server 2016 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

