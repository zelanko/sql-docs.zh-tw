---
title: 教學課程：將圓形圖新增至報表 (報表產生器) | Microsoft Docs
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b25a2f955ddd630c7093a1dc82a22c2cd0ba41b0
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710729"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>教學課程：將圓形圖加入至報表 (報表產生器)
在本教學課程中，您會在 Reporting Services 分頁報表中建立圓形圖。 您將新增百分比，並將小配量合併為單一配量。

圓形圖和環圈圖會將資料顯示為整體所佔的百分比。 它們都沒有軸。 在圓形圖中新增數值欄位時，圖表會計算出每個值佔整體的百分比。  

此圖顯示您將建立的圓形圖。 
 
![report-builder-pie-chart-final](../reporting-services/media/report-builder-pie-chart-final.png)
  
如果圓形圖上的資料點過多，資料點標籤可能會太擁擠而難以閱讀。 在該情況下，請考慮將多個小配量合併成一個較大配量。 將資料彙總成少數資料點時，圓形圖會更容易讀取。  
 
> [!NOTE]  
> 在本教學課程中，精靈的步驟會合併為兩個程序。 如需如何瀏覽至報表伺服器、新增資料來源以及新增資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
完成本教學課程的估計時間：10 分鐘  
  
## <a name="requirements"></a>需求  
如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Chart"></a>1.從圖表精靈建立圓形圖  
在本節中，您可以使用 [圖表精靈] 建立內嵌資料集，並選擇共用資料來源，然後建立圓形圖。  

  
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

    > [!NOTE]  
    > 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢變得冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
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
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您報表所依據的資料。  
  
9. 按 [下一步] 。  
  
## <a name="ChartType"></a>2.選擇圖表類型  
您可以選擇各種不同預先定義的圖表類型。  

  
1.  在 [選擇圖表類型] 頁面上，按一下 [圓形圖]，然後按一下 [下一步]。 [排列圖表欄位] 頁面隨即開啟。  
  
    在 [排列圖表欄位] 頁面上，將 [Product] 欄位拖曳至 [類別目錄] 窗格。 類別目錄會定義圓形圖中的配量數目。 在這則範例中，共有八個配量，每一個代表一個產品。  
  
2.  將 [Sales] 欄位拖曳至 [值] 窗格。 Sales 代表每個子類別目錄的銷售量。 因為圖表會顯示每項產品的彙總，所以 [值] 窗格會顯示 `[Sum(Sales)]`。  
  
3.  按一下 [下一步]，以查看預覽。  
  
5.  按一下 **[完成]**。  
  
    圖表就會加入至設計介面。 您看不到圓形圖的實際值，而是看到產品 1、產品 2 等等，以了解圖表的外觀。  
    
    ![report-builder-pie-chart-first-design](../reporting-services/media/report-builder-pie-chart-first-design.png)
  
6.  按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，使其變大。 請注意，報表設計介面也會變大，以容納圖表的大小。  
  
7.  按一下 **[執行]** 預覽報表。  
  
報表會顯示畫分有八個配量的圓形圖，每一塊表示一個產品。 現在，您會看到實際產品，而且每個配量的大小都代表該產品的銷售量。 其中 3 塊配量極少。  

![report-builder-pie-chart-first-preview](../reporting-services/media/report-builder-pie-chart-first-preview.png)
  
## <a name="Percentages"></a>3.在每一塊配量中顯示百分比  
在圓形圖的每個配量上，您可以顯示這個配量相較於整個圓形圖的百分比。  

  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圓形圖，然後按一下 [顯示資料標籤]。 資料標籤就會顯示在圖表上。  
  
3.  以滑鼠右鍵按一下標籤，然後按一下 [數列標籤屬性]。  
  
4.  在 [標籤資料] 方塊中，選取 **#PERCENT**。  
    
5.  (選擇性) 若要指定標籤所顯示的小數位數，請在 [標籤資料] 方塊中，於 **#PERCENT** 後面輸入 **{Pn}**，其中 *n* 是要顯示的小數位數。 例如，如果不要顯示任何小數位數，請輸入 **#PERCENT{P0}**。  

6.  若要以百分比顯示值，UseValueAsLabel 屬性必須為 False。 如果系統提示您在 [確認動作] 對話方塊中設定這個值，請按一下 [是]。  
  
    > [!NOTE]  
    > 當您格式化百分比時，[數列標籤屬性] 對話方塊中的 [數字格式] 沒有任何作用。 這會將標籤格式化成百分比，但是不會計算每個配量所代表的圓形圖百分比。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  按一下 **[執行]** 預覽報表。  
  
報表會顯示每個圓形圖配量佔整體的百分比。  

![report-builder-pie-chart-preview-percents](../reporting-services/media/report-builder-pie-chart-preview-percents.png)
  
## <a name="CombineSlices"></a>4.將較小的配量收集成一塊配量  
圓形圖中有 3 塊配量極少。 您可以將多個小配量合併為一個代表這三個配量的較大「其他」配量。  

1.  切換到報表設計檢視。  
  
2.  如果看不到 [屬性] 窗格，請在 [檢視] 索引標籤 > [顯示/隱藏] 群組 > 選取 [屬性]。  
  
3.  在設計介面上按一下圓形圖的任何配量。 數列的屬性會顯示在 [屬性] 窗格中。  
  
4.  在 [一般]  區段中，展開 [CustomAttributes]  節點。  
  
5.  將 **CollectedStyle** 屬性設定為 **SingleSlice**。  

    ![report-builder-pie-chart-single-slice-property](../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
 
6.  確認 **CollectedThreshold** 屬性設定為 5。  
  
7.  確認 **CollectedThresholdUsePercent** 屬性設定為 **True**。  
  
8.  在 [主資料夾] 索引標籤上，按一下 [執行] 預覽報表。  
  
在圖例中，您現在會看到「其他」類別目錄。 新的圓形圖配量會將低於 5% 的所有配量結合成一個佔整個圓形圖 6% 的配量。  

![report-builder-pie-chart-start-at-90](../reporting-services/media/report-builder-pie-chart-start-at-90.png)
 
## <a name="DrawingEffect"></a>5.在頂端開始繪製圓形圖值 

根據預設，在圓形圖中，資料集的第一個值是從 90 度開始 (從圓形圖頂端算起)。 您可以查看先前各節中的圓形圖。

在本節中，我們會讓第一個值於頂端開始。

1.  切換到報表設計檢視。  

2. 選取圓形圖本身。

3. 在 [屬性] 窗格的 [自訂屬性] 底下，將 PieStartAngle 從 **0** 變更為 **270**。

4. 按一下 [執行] 以預覽報表。

現在，圓形圖配量是依照字母順序，並且於頂端開始，而且結束於「其他」配量。

![report-builder-pie-chart-start-at-top](../reporting-services/media/report-builder-pie-chart-start-at-top.png)
  
## <a name="Title"></a>6.加入報表標題  
  
因為圓形圖是報表中的唯一視覺效果，所以圖表不需要有其專屬標題。 有報表標題即可。
  
1.  在圖表中，選取 [圖表標題] 方塊，然後按 DELETE。

2. 在設計介面上，按一下 [按一下以新增標題]。  
  
2.  輸入 **Camera and Camcorder Sales**並按 ENTER，然後輸入 **As a Percentage of Total Sales**，它看起來如下：  
  
    **Camera and Camcorder Sales**  
  
    **As a Percentage of Total Sales**  
  
3.  選取 [Camera and Camcorder Sales]，然後在 [首頁] 索引標籤 > [字型] 區段 > 按一下 [粗體]。  
  
4.  選取 [As a Percentage of Total Sales]，然後在 [主資料夾] 索引標籤 > [字型] 區段 > 將字型大小設為 [10]。  
  
5.  (選擇性) 您可能需要增加 [標題] 文字方塊的高度，才能容納兩行文字。  
  
    這個標題就會顯示在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
6.  按一下 **[執行]** 預覽報表。  
  
## <a name="Save"></a>7.儲存報表  
  
### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  在 [檔案] 功能表上，按一下 [儲存]。  
  
3.  在 [名稱] 中，鍵入 **Sales Pie Chart**。  
  
4.  按一下 **[儲存]**。  
  
您的報表就會儲存在報表伺服器上。  
  
## <a name="next-steps"></a>Next Steps  
您已成功完成「將圓形圖加入至報表」教學課程。 若要深入了解圖表，請參閱[圖表 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 和[走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md)  
[SQL Server 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

