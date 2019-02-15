---
title: 教學課程：將橫條圖加入至報表 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6bd2d801c4f6aae8d87764bdefbe153f3d9743f8
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295986"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>教學課程：將橫條圖加入至報表 （報表產生器）
  橫條圖會以水平方向顯示類別目錄資料。 這樣有助於：  
  
-   讓使用者容易閱讀冗長的類別目錄名稱。  
  
-   讓使用者容易了解繪製成值的時間。  
  
-   比較多個數列的相對值。  
  
 下圖顯示您將建立的橫條圖，其中以字母順序列出 2008 和 2009 年前五名銷售人員的銷售額。  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何執行下列作業：  
  
1.  [從圖表精靈建立圖表](#Chart)  
  
2.  [選擇圖表類型](#ChartType)  
  
3.  [在垂直軸上顯示所有類別目錄值](#AllValues)  
  
4.  [修改垂直軸上的名稱顯示](#Sort)  
  
5.  [移動圖例](#Legend)  
  
6.  [移動圖表標題](#ChartTitle)  
  
7.  [格式化及標示水平軸](#Horizontal)  
  
8.  [加入篩選以顯示前五個值](#Filter)  
  
9. [加入報表標題](#Title)  
  
10. [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併為一個程序。 如需如何瀏覽至報表伺服器的逐步指示，建立資料集，並選擇資料來源，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表&#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 完成本教學課程的估計時間：15 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Chart"></a> 1.從圖表精靈建立圖表報表  
 從**開始使用** 對話方塊中，建立內嵌資料集、 選擇共用的資料來源，並使用圖表精靈 建立橫條圖。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-new-chart-report"></a>建立新的圖表報表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
    > [!NOTE]  
    >  如果**快速入門** 對話方塊不會出現，按一下 報表產生器 按鈕，然後按一下**新增**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 [圖表精靈]。  
  
4.  在 [選擇資料集] 頁面上，按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    >  只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按一下 [下一步] 。  
  
##  <a name="ChartType"></a> 2.選擇圖表類型  
 您可以選擇各種不同預先定義的圖表類型。  
  
#### <a name="to-add-a-column-chart"></a>加入直條圖  
  
1.  在 [選擇圖表類型] 頁面上，直條圖是預設圖表類型。  
  
2.  按一下 [橫條圖]，然後按一下 [下一步]。  
  
     在 **排列圖表欄位**頁面上，有四個欄位中的**可用的欄位**窗格：FirstName、 LastName、 SalesYear2009 和 SalesYear2008。  
  
3.  將 [LastName] 拖曳至 [類別目錄] 窗格。  
  
4.  將 [SalesYear2009] 拖曳至 [值] 窗格。 SalesYear2009 代表每位銷售人員 2009 年的銷售量。 [值] 窗格會顯示 `[Sum(SalesYear2009)]` ，因為圖表會顯示每項產品的彙總。  
  
5.  將 [SalesYear2008] 拖曳至 [SalesYear2009] 下的 [值] 窗格。 SalesYear2008 代表每位銷售人員 2008 年的銷售量。  
  
6.  按一下 [下一步] 。  
  
7.  在 [**選擇樣式**] 頁面上，在 [樣式] 窗格中，選取樣式。  
  
     樣式會指定字型樣式、色彩集和框線樣式。 當您選取樣式時，[預覽] 窗格會顯示具有該樣式的圖表範例。  
  
8.  按一下 **[完成]**。  
  
     圖表就會加入至設計介面。  
  
9. 按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，即可增加圖表的大小。  
  
10. 按一下 **[執行]** 預覽報表。  
  
 報表會顯示每位銷售人員 2008 和 2009 年的銷售額橫條圖。 橫條圖的長度對應至銷售總額。  
  
##  <a name="AllValues"></a> 3.修改垂直軸上的名稱顯示  
 根據預設，垂直軸上只會顯示部分值。 您可以變更圖表以顯示所有類別目錄。  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>沿著橫條圖的類別目錄軸顯示所有銷售人員  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下垂直軸，，然後按一下**垂直軸屬性**。  
  
3.  在 [軸範圍和間隔] 的 [間隔] 方塊中，鍵入 **1**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  以滑鼠右鍵按一下垂直**軸標題**並清除**顯示軸標題**核取方塊。  
  
6.  按一下 **[執行]** 預覽報表。  
  
> [!NOTE]  
>  如果您無法在垂直軸上讀到銷售人員的名稱，可增加圖表的高度或變更軸標籤的格式選項。  
  
###  <a name="CategoryExpression"></a> 垂直軸上顯示姓氏和名字  
 您可以變更類別目錄運算式，以依序包含每位銷售人員的姓氏和名字。  
  
##### <a name="to-change-the-category-expression"></a>變更類別目錄運算式  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示 [圖表資料] 窗格。  
  
3.  在 [類別目錄群組] 區域中，以滑鼠右鍵按一下 [LastName]，然後按一下 [類別目錄群組屬性]。  
  
4.  在 [標籤] 中，按一下運算式 (Fx) 按鈕。  
  
5.  輸入下列運算式： `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
     此運算式會串連姓氏、逗號和名字。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  按一下 **[執行]** 預覽報表。  
  
 如果您執行報表時未出現名字，可以手動重新整理資料。 當您依然在預覽模式時，於 [執行] 索引標籤的 [巡覽] 群組中，按一下 [重新整理]。  
  
> [!NOTE]  
>  如果您無法在垂直軸上讀到銷售人員的名稱，可增加圖表的高度或變更軸標籤的格式選項。  
  
##  <a name="Sort"></a> 4.變更垂直軸上名稱的排序次序  
 當您排序圖表上的資料時，也會變更類別目錄軸上值的順序。  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>在橫條圖上按照字母順序排序名稱  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示 [圖表資料] 窗格。  
  
3.  在 [類別目錄群組] 區域中，以滑鼠右鍵按一下 [LastName]，然後按一下 [類別目錄群組屬性]。  
  
4.  按一下 **[排序]**。 [變更排序選項] 頁面會顯示排序運算式的清單。 根據預設，此清單包含的排序運算式與原始類別目錄群組運算式相同。  
  
5.  在 [排序依據，也可以按一下運算式 (**Fx**)] 按鈕。  
  
6.  輸入下列運算式： `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  按一下 [確定] 。  
  
8.  回到**類別目錄群組屬性**頁面上，於**順序**下拉式清單中，選取**Z 到 A**。這樣會選取反向字母順序，如此這些名稱就會按照由上而下的順序顯示。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 按一下 **[執行]** 預覽報表。  
  
 水平軸上的名稱會依反向順序排序，與**Alerca**頂端並**Zeng**底部。  
  
##  <a name="Legend"></a> 5.移動圖例  
 為了改善圖表值的可讀性，您可能會想要移動圖表圖例。 例如，在水平顯示橫條的橫條圖中，您可以變更圖例的位置，讓它位於圖表區域的上方或下方。 這樣會提供更多水平空間給橫條。  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>在橫條圖的圖表區域下方顯示圖例  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圖表上的圖例。  
  
3.  選取 [圖例屬性]。  
  
4.  針對 [圖例位置]，選取不同的位置。 例如，您可以將位置設定為中間底部。  
  
     當圖例位於圖表的頂端或底部時，圖例的配置就會從垂直變更為水平。 您可以從 [配置] 下拉式清單中選取不同的配置。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  按一下 **[執行]** 預覽報表。  
  
##  <a name="ChartTitle"></a> 6.為圖表加上標題  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>變更橫條圖之圖表區域上方的圖表標題  
  
1.  切換到報表設計檢視。  
  
2.  選取的詞彙**圖表標題**在上方的圖表，然後輸入下列文字：**Sales for 2008 和 2009 年**。  
  
3.  按一下文字外的任何位置。  
  
4.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Horizontal"></a> 7.格式化及標示水平軸  
 根據預設，水平軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>格式化水平軸上的數字  
  
1.  切換到報表設計檢視。  
  
2.  沿著圖表的底部，按一下以選取水平軸。  
  
     功能區上**首頁**索引標籤中，於**數目**群組中，按一下**貨幣** 按鈕。 水平軸標籤就會變更為貨幣。  
  
3.  (選擇性) 移除小數位數。 在 [貨幣] 按鈕附近按兩次 [減少小數位數] 按鈕。  
  
4.  以滑鼠右鍵按一下水平軸，然後按一下 [水平軸屬性]。  
  
5.  在 **數字**索引標籤上，選取**以千為單位顯示值。**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  以滑鼠右鍵按一下**軸標題**然後按一下**軸標題屬性**。  
  
8.  在 **標題文字**方塊中，輸入**銷售以千為單位**，按一下 **確定**。  
  
9. 按一下 **[執行]** 預覽報表。  
  
 報表會將水平軸上的銷售量顯示為以千為單位的貨幣，且沒有小數位數。  
  
##  <a name="Filter"></a> 8.加入篩選以顯示前五個值  
 您可以將篩選加入至圖表，以指定要在圖表中包含或排除資料集中的哪些資料。  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>加入篩選並顯示前五個值  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示 [圖表資料] 窗格。  
  
3.  在 [類別目錄群組] 區域中，以滑鼠右鍵按一下 [LastName] 欄位，然後按一下 [類別目錄群組屬性]。  
  
4.  按一下 **[篩選]**。 [變更篩選] 頁面可顯示篩選運算式的清單。 根據預設，此清單是空的。  
  
5.  按一下 **[加入]**。 新的空白篩選隨即顯示。  
  
6.  在 **運算式**，型別 **[Sum(SalesYear2009)]**。 這樣會建立基礎運算式 `=Sum(Fields!SalesYear2009.Value)`，如果您按一下 [fx] 按鈕可以看到此運算式。  
  
7.  確認資料類型是 **Text**。  
  
8.  在 [運算子] 中，從下拉式清單選取 [前 N 個]。  
  
9. 在 [值] 中，鍵入下列運算式：**=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 按一下 **[執行]** 預覽報表。  
  
 如果您執行報表時結果並未經過篩選，可以手動重新整理資料。 在 [執行] 索引標籤的 [巡覽] 群組中，按一下 [重新整理]。  
  
 此圖表就會顯示 2009 銷售資料中前五名的銷售人員名稱。  
  
##  <a name="Title"></a> 9.加入報表標題  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  型別**銷售橫條圖**，按下 ENTER，接著再輸入**年前五名銷售人員 2009年**，因此它看起來像這樣：  
  
     **銷售橫條圖**  
  
     **2009 年前五名銷售人員**  
  
3.  選取 [銷售橫條圖]，然後按一下 [粗體] 按鈕。  
  
4.  選取 **年前五名銷售人員 2009年**，然後在**字型**區段**首頁**索引標籤上，將字型大小設定為**10**。  
  
5.  (選擇性) 您可能需要增加 [標題] 文字方塊的高度，才能容納兩行文字。  
  
     這個標題就會顯示在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
6.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Save"></a> 10.儲存報表  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
3.  在 [名稱] 中，鍵入 **Sales Bar Chart**。  
  
4.  按一下 [儲存] 。  
  
 您的報表就會儲存在報表伺服器上。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利完成「將橫條圖加入至報表」教學課程。 若要深入了解圖表，請參閱[圖表 &#40;報表產生器及 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) 和[走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
