---
title: 教學課程：將直條圖新增至報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ae6c6adad91625ba5d5e898b7da36dc9e818d893
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023945"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>教學課程：將直條圖加入至報表 (報表產生器)
  直條圖是依據類別目錄群組，將數列顯示為一組垂直線。 直條圖可用於：  
  
-   顯示一段時間的資料變更。  
  
-   比較多個數列的相對值。  
  
-   顯示移動平均來呈現趨勢。  
  
 下圖顯示您將建立的直條圖，內含移動平均。  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="BackToTop"></a> 您將學習  
 在本教學課程中，您將學習如何執行下列作業：  
  
1.  [從圖表精靈建立圖表](#Chart)  
  
2.  [選擇圖表類型](#ChartType)  
  
3.  [格式化及標示水平軸](#Horizontal)  
  
4.  [移動圖例](#Legend)  
  
5.  [圖表加上標題](#ChartTitle)  
  
6.  [格式化及標示垂直軸](#Vertical)  
  
7.  [加入移動平均](#Average)  
  
8.  [加入報表標題](#Title)  
  
9. [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併為一個程序。 如需如何瀏覽至報表伺服器、選擇資料來源以及建立資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 完成本教學課程的估計時間：15 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Chart"></a> 1.從圖表精靈建立圖表報表  
 從**入門**對話方塊，請使用圖表精靈建立內嵌資料集，選擇共用的資料來源，並建立直條圖。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-new-chart-report"></a>建立新的圖表報表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
    > [!NOTE]  
    >  如果 **[使用者入門]** 對話方塊沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 [圖表精靈]。  
  
4.  在 [選擇資料集] 頁面上，按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    >  只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2009-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2009-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2009-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2009-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2009-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2009-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2009-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2009-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2009-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2009-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2009-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2009-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2009-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2009-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2009-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2009-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按 [下一步] 。  
  
##  <a name="ChartType"></a> 2.選擇圖表類型  
 您可以選擇各種不同預先定義的圖表類型。  
  
#### <a name="to-add-a-column-chart"></a>加入直條圖  
  
1.  在 [選擇圖表類型] 頁面上，直條圖是預設圖表類型。 按 [下一步] 。  
  
2.  在 [排列圖表欄位] 頁面上，將 [SalesDate] 欄位拖曳至 [類別目錄]。 類別目錄會顯示在水平軸上。  
  
3.  將 [Sales] 欄位拖曳至 [值]。 [值] 方塊會顯示 [Sum(Sales)]，因為系統會針對每個日期彙總銷售總計值的總和。 值會顯示在垂直軸上。  
  
4.  按 [下一步] 。  
  
5.  在**選擇樣式** 頁面上，樣式 方塊中選取樣式。  
  
     樣式會指定字型樣式、色彩集和框線樣式。 當您選取樣式時，[預覽] 窗格會顯示具有該樣式的圖表範例。  
  
6.  按一下 **[完成]**。  
  
     圖表就會加入至設計介面。  
  
7.  按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，即可增加圖表的大小。 請注意，報表設計介面的大小會放大，以容納圖表的大小。  
  
8.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Horizontal"></a> 3.格式化及標示水平軸  
 根據預設，水平軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>若要格式化水平軸上的日期  
  
1.  切換到報表設計檢視。  
  
2.  水平軸，以滑鼠右鍵按一下，然後按一下 **水平軸屬性**。  
  
3.  按一下 **[數值]**。  
  
4.  在**類別**，選取**日期**。  
  
5.  在 [類型] 方塊中，選取 [31 Jan 2000]。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在 [主資料夾] 索引標籤上，按一下 [執行] 預覽報表。  
  
 日期會以您所選取的日期格式顯示。 請注意，圖表並未在水平軸上標示每個類別目錄。 根據預設，只有容納在軸旁的標籤才會包含在內。  
  
 您可以透過旋轉標籤和指定間隔，自訂標籤顯示。  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>若要沿著水平軸旋轉軸標籤和變更顯示間隔  
  
1.  切換到報表設計檢視。  
  
2.  水平軸標題，以滑鼠右鍵按一下，然後按一下 **顯示軸標題**以移除標題。 因為水平軸會顯示日期，所以不需要這個標題。  
  
3.  以滑鼠右鍵按一下水平軸，然後按一下 **水平軸屬性**。  
  
4.  在**軸選項**頁面**軸範圍和間隔**，型別**3**如**間隔**。 圖表將會顯示每隔三天的資料。  
  
5.  按一下 **[標籤]**。  
  
6.  在**變更軸標籤自動調整選項**，選取**停用自動調整**。  
  
7.  在 [標籤旋轉角度] 中，選取 [-90]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     水平軸的範例文字會旋轉 90 度。  
  
9. 按一下 **[執行]** 預覽報表。  
  
 在圖表上，標籤會旋轉而且會顯示每隔三天的標籤。  
  
##  <a name="Legend"></a> 4.移動圖例  
 圖例是從類別目錄和數列資料自動建立。  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>若要移動直條圖之圖表區域下方的圖例  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圖表上的圖例，然後按一下**圖例屬性**。  
  
3.  如**配置及位置**，選取不同的位置。 例如，您可以將位置設定為中間底部。  
  
     當圖例位於圖表的頂端或底部時，圖例的配置就會從垂直變更為水平。 您可以從 [配置] 下拉式清單中選取不同的配置。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (選擇性) 因為這個教學課程只有一個類別目錄，所以不需要圖例。 若要移除圖例，以滑鼠右鍵按一下圖例，然後按一下 **刪除圖例**。  
  
6.  按一下 **[執行]** 預覽報表。  
  
##  <a name="ChartTitle"></a> 5.為圖表加上標題  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>若要變更圖表區域上方的圖表標題  
  
1.  切換到報表設計檢視。  
  
2.  選取的文字**圖表標題**頂端的圖表，然後輸入下列文字：**商店銷售訂單總計**。  
  
3.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Vertical"></a> 6.格式化及標示垂直軸  
 根據預設，垂直軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>若要將垂直軸上的數字格式化成貨幣  
  
1.  切換到報表設計檢視。  
  
2.  沿著圖表的側邊，按兩下垂直軸上的標籤，以便選取。  
  
3.  在功能區 上**首頁**索引標籤的**數目**群組中，按一下**貨幣** 按鈕。 這些軸標籤就會變更為顯示貨幣格式。  
  
4.  在功能區 上**首頁**索引標籤的**數目**群組中，按一下**減少小數位數**按鈕兩次，顯示四捨五入到最接近之美元的數字。  
  
5.  以滑鼠右鍵按一下垂直軸，然後按一下**垂直軸屬性**。  
  
6.  按一下 **[數值]**。 請注意，**貨幣**中已選取**類別** 方塊中，和**小數位數**已經**0** （零）。  
  
7.  在**中顯示值**方塊中，按一下**數千**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 沿著圖表的側邊的垂直軸標題上按一下滑鼠右鍵，然後按一下**軸標題屬性**。  
  
10. 取代文字中的**標題文字**欄位包含下列文字：**銷售總計 （以千為單位）**。 您也可以指定各種有關如何格式化標題的選項。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Average"></a> 7.加入移動平均  
  
#### <a name="to-add-a-moving-average"></a>若要加入移動平均  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示 [圖表資料] 窗格。  
  
3.  以滑鼠右鍵按一下 **[sum （sales)]** 欄位處於**值**區域，，然後按一下**加入導出數列**。  
  
4.  在 [公式] 中，確認已選取 [移動平均]。  
  
5.  在 [設定公式參數] 中，針對 [週期] 選取 [4]。  
  
6.  按一下**框線**。  
  
7.  在**線條寬度**，選取**3pt**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 按一下 **[執行]** 預覽報表。  
  
 圖表會顯示一條線，代表依照日期區分之總銷售量的移動平均 (每四個日期的平均)。  
  
##  <a name="Title"></a> 8。加入報表標題  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  切換到報表設計檢視。  
  
2.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
3.  型別**銷售圖表**中按下 ENTER，然後再輸入**年 1 月到 12 月 2009年**，因此它看起來像這樣：  
  
     **銷售圖表**  
  
     **年 1 月到 2009 年 12 月**  
  
4.  選取**銷售圖表**，然後按一下**粗體**按鈕**字型**區段**首頁**功能區 索引標籤。  
  
5.  選取**年 1 月到 12 月 2009年**，然後在**字型**區段**首頁**索引標籤上，將字型大小設定為**10**。  
  
6.  （選擇性）您可能需要進行**標題**文字方塊的高度，才能容納兩行文字，藉以向下雙箭號上當您按一下底端邊緣的中間。  
  
     這個標題就會顯示在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
7.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Save"></a> 第 9。儲存報表  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  在 [報表產生器] 按鈕中，按一下 **[另存新檔]**。  
  
3.  在 [名稱] 中，鍵入 **Sales Order Column Chart**。  
  
4.  按一下 **[儲存]**。  
  
## <a name="next-steps"></a>後續步驟  
 您已成功完成「將直條圖加入至報表」教學課程。 若要深入了解圖表，請參閱[圖表 &#40;報表產生器及 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) 和[走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  