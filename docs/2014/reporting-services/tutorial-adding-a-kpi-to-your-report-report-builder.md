---
title: 教學課程：將 KPI 新增至報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5362e72fefa36102737e362a1b4ec8b11b96c77f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946016"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>教學課程：將 KPI 新增至報表 (報表產生器)
  關鍵效能指標 (KPI) 是具有商務重要性的可測量值。 本教學課程將說明如何將 KPI 加入至報表。 在這個案例中，依產品子類別排列的銷售摘要便是 KPI。 KPI 的目前狀態會使用色彩、量測計和指標顯示。  
  
 下圖顯示您將建立的報表。  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何根據資料格的值設定資料表資料格的背景色彩來加入 KPI，以及加入和設定量測計和指標。 您也將學習如何撰寫設定資料表資料格背景色彩的運算式。  
  
 本教學課程包含下列程序：  
  
1.  [從資料表或矩陣精靈建立資料表報表和資料集](#Table)  
  
2.  [組織資料、 選擇配置和樣式從資料表或矩陣精靈](#CompleteWizard)  
  
3.  [使用背景色彩顯示 KPI](#BackgroundColors)  
  
4.  [藉由使用量測計顯示 KPI](#Gauge)  
  
5.  [使用指標顯示 KPI](#Indicator)  
  
6.  [加入報表標題](#Title)  
  
7.  [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併成兩個程序：一個程序用來建立資料集，另一個程序用來建立資料表。 如需如何瀏覽至報表伺服器、選擇資料來源、建立資料集，以及執行精靈的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估計的時間才能完成本教學課程：15 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Table"></a> 1.從資料表或矩陣精靈建立資料表報表和資料集  
 從**開始使用** 對話方塊中，選擇共用的資料來源、 建立內嵌資料集，並顯示資料表中的資料。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-new-table"></a>若要建立新資料表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
    > [!NOTE]  
    >  如果**快速入門** 對話方塊沒有出現，從 報表產生器 按鈕中，按一下**新增**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  在 [選擇資料集] 頁面中，按一下**建立資料集**。  
  
5.  按一下 [下一步] 。  
  
6.  在 [選擇與資料來源的連線] 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源。 如果沒有資料來源可用，或無法存取報表伺服器，您可以改用內嵌資料來源。 如需詳細資訊，請參閱[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
7.  按一下 [下一步] 。  
  
8.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
9. 複製下列查詢並貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. 按一下 [下一步] 。  
  
##  <a name="CompleteWizard"></a> 2.從資料表或矩陣精靈組織資料、選擇配置和樣式  
 使用精靈提供起始設計來顯示資料。 精靈中的預覽窗格可協助您在完成資料表或矩陣設計之前，先視覺化群組資料的結果。  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>若要將資料組織成群組、選擇配置和樣式  
  
1.  在 [排列欄位] 頁面上，將 [Product] 拖曳至 [值]。  
  
2.  將 [Quantity] 拖曳至 [值] 並放置在 [Product] 之下。  
  
     [Quantity] 是使用 Sum 函數摘要的，這個函數是摘要數值欄位的預設函數。  
  
3.  將 [Sales] 拖曳至 [值] 並放置在 [Quantity] 之下。  
  
     步驟 1、2 和 3 會指定要在資料表中顯示的資料。  
  
4.  將 [SalesDate] 拖曳至 [資料列群組]。  
  
5.  將 [Subcategory] 拖曳至 [資料列群組] 並放置在 [SalesDate] 之下。  
  
     步驟 4 和 5 會依日期組織欄位的值，然後再依該日期的所有銷售進行組織。  
  
6.  按一下 [下一步] 。  
  
     當您執行報表時，資料表會顯示每個日期、每個日期的所有訂單，以及每個訂單的所有產品、數量和銷售總額。  
  
7.  在 [選擇配置] 頁面的 [選項] 下方，確定已選取 [顯示小計和總計]。  
  
8.  驗證已選取 [區塊式，小計位於下方]。  
  
9. 清除 [展開/摺疊群組] 選項。  
  
     在本教學課程中，您建立的報表不會使用向下鑽研功能，此功能可讓使用者展開父群組階層，以顯示子群組資料列和詳細資料列。  
  
10. 按一下 [下一步] 。  
  
11. 在 [選擇樣式] 頁面的 [樣式] 窗格中選取樣式。  
  
     完成的報表圖顯示報表使用 [海洋] 樣式。  
  
12. 按一下 **[完成]**。  
  
     資料表會加入至設計介面。 這個資料表具有五個資料行和五個資料列。 [資料列群組] 窗格會顯示三個資料列群組：SalesDate、Subcategory 和 Details。 詳細資料是資料集查詢擷取的所有資料。  
  
13. 按一下 **[執行]** 預覽報表。  
  
 資料表會針對特定日期銷售的每個產品顯示產品名稱、銷售數量和銷售總額。 資料會先依銷售日期排列，然後再依子類別排列。  
  
##  <a name="BackgroundColors"></a> 3.使用背景色彩顯示 KPI  
 您可以將背景色彩設定成執行報表時評估的運算式。  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>若要使用背景色彩來顯示 KPI 的目前狀態  
  
1.  在資料表中，以滑鼠右鍵按一下兩個資料格往下從`[Sum(Sales)]`儲存格 （的小計資料列會顯示子類別銷售額），然後再按一下**文字方塊內容**。  
  
2.  在 **填滿**，按一下**fx**旁邊**填滿色彩**選項，然後輸入下列運算式中的**設定運算式對象：** 欄位中輸入下列運算式：  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 這樣就會針對含有大於或等於 5000 之 `[Sum(Sales)]` 彙總總和的每個資料格，使用名為「亮綠」的綠色陰影，將背景色彩變更為綠色。 介於 2500 與 5000 之間的 `[Sum(Sales)]` 值會以黃色著色。 小於 2500 的值會以紅色著色。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  按一下 **[執行]** 預覽報表。  
  
 在顯示子類別銷售額的小計資料列中，資料格的背景色彩會根據銷售總和的值變成紅色、黃色或綠色。  
  
##  <a name="Gauge"></a> 4.使用量測計顯示 KPI  
 量測計可說明資料集中的單一值。 這個教學課程使用水平的線性量測計，因為它的形狀和簡單性，即使很小並用於資料表資料格內，也很容易閱讀。 如需詳細資訊，請參閱 [量測計 &#40;報表產生器及 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>若要使用量測計來顯示 KPI 的目前狀態  
  
1.  切換至 [設計] 檢視。  
  
2.  在資料表中，以滑鼠右鍵按一下資料行處理常式針對您在上一個程序中變更的資料格，指向**插入資料行**，然後按一下**右**。 新的資料行就會加入至此資料表。  
  
3.  型別**KPI**欄標題中。  
  
4.  在上**插入**索引標籤中，於**資料區域**群組中，按一下**量測計**，然後按一下 外部資料表的設計介面。 **[選取量測計類型]** 對話方塊隨即出現。  
  
5.  按一下 **線性**。 第一個線性量測計類型**水平**，已選取。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     量測計就會加入至設計介面。  
  
7.  將 [Sales] 從 [報表資料] 窗格拖曳至量測計。 當您將 [Sales] 拖曳到量測計上時，[量測計資料] 窗格隨即開啟。  
  
8.  Sales 放置**值**清單。  
  
     當您將欄位放置到量測計上時，欄位會使用內建的 Sum 函數進行彙總。  
  
9. 以滑鼠右鍵按一下量測計的指標，然後按一下 **指標屬性**。  
  
10. 在 **指標類型**，選取**列**。 這樣就會將指標從標記變更為橫條，以便在量測計加入至資料表時更明顯。  
  
11. 按一下 **指標填滿**。 在 **次要色彩**挑選**黃色**。 漸層填滿模式將從白色變更為黃色。  
  
12. 以滑鼠右鍵按一下量測計中的標尺，然後按一下 [標尺屬性]。  
  
13. 設定**最大**選項設為 25000。  
  
    > [!NOTE]  
    >  除了 25000 這類常數，您也可以使用運算式動態計算 [最大值] 選項的值。 運算式會使用彙總功能進行彙總，看起來就類似於運算式 `=Max(Sum(Fields!Sales.value), "Tablix1")`。  
  
14. 將資料表內部的量測計拖曳至小計資料列的第三個資料格，此小計資料列顯示您插入之資料行的子類別銷售額。  
  
    > [!NOTE]  
    >  您可能必須重新調整資料行，使水平的線性量測計能夠納入資料格中。 若要調整資料行的大小，請按一下資料行標頭，並使用控點來水平及垂直地調整資料格的大小。  
  
15. 按一下 **[執行]** 預覽報表。  
  
     量測計中橫條的水平長度會根據 KPI 的值而變更。  
  
16. (選擇性) 加入最大指針來處理溢位，使任何超過刻度最大值的值都永遠會指向最大指針：  
  
    1.  開啟 [屬性] 窗格。  
  
    2.  按一下標尺。 線性標尺的屬性會顯示在 [屬性] 窗格中。  
  
    3.  在 **標尺指針**分類中，展開**MaximumPin**節點。  
  
    4.  設定**啟用**屬性設`True`。 指針會顯示在標尺的最大值之後。  
  
    5.  設定**BorderColor**至`Lime`。  
  
17. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Indicator"></a> 5.使用指標顯示 KPI  
 指標是小型的簡單量測計，可一目了然資料值。 由於指標的尺寸小加上簡單明瞭，因此常用於資料表和矩陣。 如需詳細資訊，請參閱[指標 &#40;報表產生器及 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>若要使用指標來顯示 KPI 的目前狀態  
  
1.  切換至 [設計] 檢視。  
  
2.  在資料表中，以滑鼠右鍵按一下資料行處理常式針對您在上一個程序中變更的資料格，指向**插入資料行**，然後按一下**右**。 新的資料行就會加入至此資料表。  
  
3.  型別**KPI**欄標題中。  
  
4.  按一下子類別小計的資料格。  
  
5.  在 **插入**索引標籤**資料區域**群組中，按兩下**指標。**  
  
     [選取指標類型] 對話方塊隨即開啟。  
  
6.  按一下 **圖形**。 第一個形狀類型**3 三交通號誌 （無框）** 已選取。  
  
     您將在教學課程中使用這個指標。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     指標會加入至設計介面。  
  
8.  以滑鼠右鍵按一下指標，然後按一下 [指標屬性]。  
  
9. 按一下 **值和狀態**。  
  
10. 在 [值] 下拉式清單中，選取 **[sum （sales)]**，但不是變更任何其他選項。  
  
     根據預設，整個資料區域會進行資料同步處理，而您會在 [同步處理範圍] 方塊中看到值 **Tablix1**，這是報表中的資料表資料區域的名稱。  
  
     在此報表中，您也可以變更子類別小計資料格中放置之指標的範圍，以同步處理 [SalesDate] 欄位。  
  
11. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Title"></a> 6.加入報表標題  
 報表標題會出現在報表的頂端。 您可以將報表標題放置在報表頁首，如果報表不使用報表頁首，則可以放置在報表主體頂端的文字方塊中。 您將使用自動放置在報表主體頂端的文字方塊。  
  
 您可以將不同的字型樣式、大小和色彩套用到文字的片語和個別字元，進一步加強文字。 如需詳細資訊，請參閱[在文字方塊中將文字格式化 &#40;報表產生器及 SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  型別**產品銷售 KPI**，然後按一下文字方塊外部。  
  
3.  （選擇性） 在文字方塊中，其中包含以滑鼠右鍵按一下**產品銷售 KPI**，按一下**文字方塊內容**，然後在 [字型] 索引標籤上選取不同的字型樣式、 大小和色彩。  
  
4.  按一下 **[執行]** 預覽報表。  
  
##  <a name="Save"></a> 7.儲存報表  
 將報表儲存至報表伺服器或您的電腦。 如果沒有將報表儲存到報表伺服器，就無法使用數個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如報表組件和子報表。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  將 [名稱] 中的預設名稱取代為**產品銷售 KPI**。  
  
5.  按一下 [儲存] 。  
  
 報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 [桌面]、[我的文件] 或 [我的電腦]，然後瀏覽到您要儲存報表的資料夾。  
  
> [!NOTE]  
>  如果您無法存取報表伺服器，請按一下 [桌面]、[我的文件] 或 [我的電腦]，然後將報表儲存到您的電腦。  
  
1.  將 [名稱] 中的預設名稱取代為**產品銷售 KPI**。  
  
2.  按一下 [儲存] 。  
  
## <a name="next-steps"></a>後續步驟  
 您已成功完成「將 KPI 加入至報表」教學課程。 如需詳細資訊，請參閱 < 量測計 （報表產生器）[指標&#40;報表產生器及 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
