---
title: "教學課程： 將橫條圖加入至報表 （報表產生器） |Microsoft 文件"
ms.custom: 
ms.date: 06/15/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: af11d5fdee9122663431f4f00ef5e40fb765c7b4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>教學課程：將橫條圖加入至報表 (報表產生器)
在本教學課程中，您會使用 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] 中的精靈，在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分頁報表中建立圓形圖。 接著新增篩選，並加強圖表。 

橫條圖會以水平方向顯示類別目錄資料。 這樣有助於：  
  
-   讓使用者容易閱讀冗長的類別目錄名稱。  
-   讓使用者容易了解繪製成值的時間。   
-   比較多個數列的相對值。  
  
下圖顯示您將建立的橫條圖，其中從最大到最小 (2015 年銷售額) 順序列出 2014 和 2015 年前五名銷售人員的銷售額。  
  
![report-builder-bar-chart](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> 在本教學課程中，精靈的步驟會合併為一個程序。 逐步說明如何瀏覽至報表伺服器中，建立資料集，並選擇 資料來源，請參閱本系列的第一個教學課程：[教學課程： 建立基本資料表報表 &#40;報表產生器 &#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
完成本教學課程的估計時間：15 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Chart"></a>1.從圖表精靈建立圖表報表  
在其中，您可以建立內嵌資料集、選擇共用資料來源，以及使用 [圖表精靈] 建立橫條圖。  
  
> [!NOTE]  
> 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
1.  從[Web 入口網站，從 SharePoint 整合模式中的報表伺服器，或從您的電腦](../reporting-services/report-builder/start-report-builder.md) 啟動報表產生器 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] web portal, 啟動報表產生器 report server in SharePoint integrated mode, or from your computer.  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
     ![報表產生器開始](../reporting-services/media/rb-getstarted.png "開始使用報表產生器")  
  
     如果您看不到 [使用者入門] 對話方塊，請按一下 [檔案] >[新增]。 [新報表或資料集] 對話方塊大部分的內容和 [使用者入門] 對話方塊相同。 
      
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **圖表精靈**。  
  
4.  在**選擇資料集**頁面上，按一下**建立資料集**，然後按一下 **下一步**。  
  
5.  在**選擇資料來源的連接**頁面上，選取現有的資料來源或瀏覽至報表伺服器並選取資料來源，然後按一下**下一步**。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    > 只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按一下 **[下一步]**。  
  
## <a name="ChartType"></a>2.建立橫條圖  
 
1.  在**選擇圖表類型**頁面上，直條圖是預設的圖表類型。  
  
2.  按一下**列**，然後按一下 **下一步**。  
  
    在**排列圖表欄位**頁面上，有四個欄位中的**可用的欄位**窗格： FirstName、 LastName、 SalesYear2015 和 SalesYear2014。  
  
3.  將 [LastName] 拖曳至 [類別目錄] 窗格。  
  
4.  將 [SalesYear2015] 拖曳至 [值] 窗格。 SalesYear2015 代表每位銷售人員 2015 年的銷售量。 [值] 窗格會顯示 `[Sum(SalesYear2015)]` ，因為圖表會顯示每項產品的彙總。  
  
5.  將 [SalesYear2014] 拖曳至 [SalesYear2015] 下的 [值] 窗格。 SalesYear2014 代表每位銷售人員 2014 年的銷售量。  
  
6.  按一下 **[下一步]**。  
  
7.  按一下 **[完成]**。  
  
    圖表就會加入至設計介面。 請注意，新的橫條圖只會顯示代表性資料。 圖例會顯示 Last Name A、Last Name B 等，而非人員的名稱，只會提供報表的外觀。 
  
9. 按一下圖表，即可顯示圖表控點。 拖曳圖表的右下角，即可增加圖表的大小。 請注意，設計介面會隨著您拖曳而變得較大。 
  
10. 按一下 **[執行]** 預覽報表。  
  
橫條圖會顯示每位銷售人員 2014 和 2015 年的銷售額。 橫條圖的長度對應至銷售總額。  
  
## <a name="AllValues"></a>3.在垂直軸上顯示所有名稱  
根據預設，垂直軸上只會顯示部分值。 您可以變更圖表以顯示所有類別目錄。  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下垂直軸，然後按一下 **垂直軸屬性**。  
  
3.  在下**軸範圍和間隔**，請在**間隔**方塊中，輸入**1**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  按一下 **[執行]** 預覽報表。  
  
> [!NOTE]  
> 如果您無法在垂直軸上讀到銷售人員的名稱，可增加圖表的高度或變更軸標籤的格式選項。  
  
### <a name="CategoryExpression"></a>在垂直軸上顯示姓氏和名字  
您可以變更類別目錄運算式，以依序包含每位銷售人員的姓氏和名字。  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示**圖表資料**窗格。  
  
3.  在**類別目錄群組**區域中，以滑鼠右鍵按一下 [LastName]，然後按一下**類別目錄群組屬性**。  
  
4.  在 [標籤] 中，按一下運算式 (Fx) 按鈕。  
  
5.  輸入下列運算式： `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    此運算式會串連姓氏、逗號和名字。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  按一下 **[執行]** 預覽報表。  
  
如果您執行報表時未出現名字，可以手動重新整理資料。 時，在依然在預覽模式**執行**索引標籤中**瀏覽**群組中，按一下**重新整理**。  
  
> [!NOTE]  
> 如果您無法在垂直軸上讀到銷售人員的名稱，可增加圖表的高度或變更軸標籤的格式選項。  
  
## <a name="Sort"></a>4.變更垂直軸的排序次序  
當您排序圖表上的資料時，也會變更類別目錄軸上值的順序。  
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示**圖表資料**窗格。  
  
3.  在**類別目錄群組**區域中，以滑鼠右鍵按一下 [LastName]，然後按一下**類別目錄群組屬性**。  
  
4.  按一下 **[排序]**。 **變更排序選項**頁面會顯示排序運算式的清單。 根據預設，此清單包含的排序運算式與原始類別目錄群組運算式相同。  
  
5.  在**排序**，按一下  **[SalesYear2015]**。  
  
6.  在**順序**清單中，選取**A 到 Z**如此名稱就會顯示順序從最大到最小 2015年銷售。
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 按一下 **[執行]** 預覽報表。  
  
水平軸上的名稱會從最大到最小 (2015 年銷售額) 進行排序，而 **Zeng** 位於頂端。  
  
## <a name="Legend"></a>5.移動圖例  
為了改善圖表值的可讀性，您可能會想要移動圖表圖例。 例如，在水平顯示橫條的橫條圖中，您可以變更圖例的位置，讓它位於圖表區域的上方或下方。 這樣會提供更多水平空間給橫條。  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>在橫條圖的圖表區域下方顯示圖例  
  
1.  切換到報表設計檢視。  
  
2.  以滑鼠右鍵按一下圖表上的圖例。  
  
3.  選取**圖例屬性**。  
  
4.  如**圖例 position**，選取不同的位置。 例如，您可以將位置設定為中間底部。  
  
    當圖例位於圖表的頂端或底部時，圖例的配置就會從垂直變更為水平。 您可以選取不同的版面配置從**配置**下拉式清單。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  按一下 **[執行]** 預覽報表。  
  
## <a name="ChartTitle"></a>6.為圖表加上標題  
  
1.  切換到報表設計檢視。  
  
2.  選取的文字**圖表標題**在圖表的頂端，然後輸入： **Sales for 2014 和 2015年**。  
  
3.  在 [屬性] 窗格中，選取，標題將**色彩**至**黑色**和**FontSize**至**12pt**。 
  
4.  按一下 **[執行]** 預覽報表。  
  
## <a name="Horizontal"></a>7.格式化及標示水平軸  
根據預設，水平軸會以一般格式顯示值，此格式會自動調整為適合圖表的大小。 您可以將它變更為貨幣格式。  
   
1.  切換到報表設計檢視。  
  
2.  沿著圖表的底部，按一下以選取水平軸。  
  
3.  在**首頁** 索引標籤 >**數目**群組 >**貨幣**。 水平軸標籤就會變更為貨幣。  
  
3.  (選擇性) 移除小數位數。 接近**貨幣**按鈕，再按一下**減少小數位數**按鈕兩次。  
  
4.  以滑鼠右鍵按一下水平軸，然後按一下**水平軸屬性**。  
  
5.  在**數目**索引標籤上，選取**以千為單位顯示值**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  以滑鼠右鍵按一下水平軸，然後選取**顯示軸標題**。
  
7.  在**軸標題**方塊中，輸入**銷售單位： 千**按下 Enter。  

    >**注意︰** 輸入時，[軸標題] 方塊會顯示在垂直軸上。 但是，當您按 Enter 時，它會移至水平軸。
  
9. 按一下 **[執行]** 預覽報表。  
  
報表會將水平軸上的銷售量顯示為以千為單位的貨幣，且沒有小數位數。  
  
## <a name="Filter"></a>8.加入篩選以顯示前五個值  
您可以將篩選加入至圖表，以指定要在圖表中包含或排除資料集中的哪些資料。   
  
1.  切換到報表設計檢視。  
  
2.  按兩下圖表以顯示**圖表資料**窗格。  
  
3.  在**類別目錄群組**區域中，[LastName] 欄位中，按一下滑鼠右鍵，然後按一下**類別目錄群組屬性**。  
  
4.  按一下 **[篩選]**。 **變更篩選**頁面可以顯示篩選運算式的清單。 根據預設，此清單是空的。  
  
5.  按一下 **[加入]**。 新的空白篩選隨即顯示。  
  
6.  在**運算式**，型別**[Sum(SalesYear2015)]**。 這會建立基礎運算式`=Sum(Fields!SalesYear2015.Value)`，您可以看到如果您按一下**fx**  按鈕。  
  
7.  確認資料類型為**文字**。  
  
8.  在**運算子**，選取**Top N**從下拉式清單。  
  
9. 在**值**，輸入下列運算式： **= 5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 按一下 **[執行]** 預覽報表。  
  
如果您執行報表時結果並未經過篩選，可以手動重新整理資料。 在**執行**索引標籤中**瀏覽**群組中，按一下**重新整理**。  
  
此圖表就會顯示 2015 銷售資料中前五名的銷售人員名稱。  
  
## <a name="Title"></a>9.加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **銷售橫條圖**並按 ENTER，然後輸入 **2015 年前五名銷售人員**，其外觀如下：  
  
    **銷售橫條圖**  
  
    **2015 年前五名銷售人員**  
  
3.  選取 [銷售橫條圖]，然後按一下 [粗體] 按鈕。  
  
4.  選取**年前五 2015年**，然後在**字型**區段**首頁**索引標籤上，將字型大小設定為**10**。  
  
5.  (選擇性) 您可能需要增加 [標題] 文字方塊的高度，並降低橫條圖的頂端，才能容納兩行文字。  
  
    這個標題就會顯示在報表的頂端。 如果未定義任何頁首，則位於報表主體頂端的項目就相當於報表頁首。  
  
6.  按一下 **[執行]** 預覽報表。  
  
## <a name="Save"></a>10.儲存報表  
  
1.  切換到報表設計檢視。  
  
2.  按一下 [檔案] > [另存新檔]。  
  
3.  在**名稱**，型別**銷售橫條圖**。  

    您可以將它儲存至電腦或報表伺服器。
  
4.  按一下 **[儲存]**。   
  
## <a name="next-steps"></a>後續步驟  
您已順利完成「將橫條圖加入至報表」教學課程。 若要深入了解圖表，請參閱 [圖表](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 和 [橫條圖](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md)  
[SQL Server 2016 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


