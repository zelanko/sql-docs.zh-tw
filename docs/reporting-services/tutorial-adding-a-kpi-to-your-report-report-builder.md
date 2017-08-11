---
title: "教學課程： 將 KPI 加入至報表 （報表產生器） |Microsoft 文件"
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
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6ff993552c5c5b8a3e48c672a29f6567107f2331
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>教學課程：將 KPI 加入至報表 (報表產生器)
在此 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] 教學課程中，您會將關鍵效能指標 (KPI) 新增至 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 編頁報表。  

KPI 是具有商務重要性的可測量值。 在這個案例中，依產品子類別排列的銷售摘要便是 KPI。 KPI 的目前狀態會以色彩、量測計和指標顯示。
  
您將建立的報表應類似下圖。  
  
![report-builder-kpi-report](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> 在本教學課程中，精靈的步驟會合併成兩個程序：一個程序用來建立資料集，另一個程序用來建立資料表。 如需如何瀏覽至報表伺服器、選擇資料來源、建立資料集以及執行精靈的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
完成本教學課程的估計時間：15 分鐘。  
  
## <a name="requirements"></a>요구 사항  
如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Table"></a>1.從資料表或矩陣精靈建立資料表報表和資料集  
在本節中，您會選擇共用資料來源、建立內嵌資料集，並在資料表中顯示資料。  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>若要建立含內嵌資料集的資料表  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果您看不到 [新增報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  在 **[選擇資料集]** 頁面上，按一下 **[建立資料集]**。  
  
5.  按一下 **[下一步]**。  
  
6.  在**選擇資料來源的連接**頁面上，選取現有的資料來源或瀏覽至報表伺服器並選取資料來源。 如果沒有資料來源可用，或無法存取報表伺服器，您可以改用內嵌資料來源。 如需詳細資訊，請參閱[教學課程： 建立基本資料表報表 &#40;報表產生器 &#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  按一下 **[下一步]**。  
  
8.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
9. 複製下列查詢並貼入查詢窗格中：  

    > [!NOTE]  
    > 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. 在查詢設計工具的工具列上，按一下 [執行](**!**)。

11. 按一下 **[下一步]**。  
  
## <a name="CompleteWizard"></a>2.在精靈中組織資料並選擇配置  
[資料表或矩陣精靈] 提供用於顯示資料的起始設計。 精靈中的預覽窗格可協助您在完成資料表或矩陣設計之前，先視覺化群組資料的結果。  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>將資料組織成群組，並選擇配置 
  
1.  在 [排列欄位] 頁面上，拖曳產品**值**。  
  
2.  將 [Quantity] 拖曳至 [值] 並放置在 [Product] 之下。  
  
    [Quantity] 是使用 Sum 函數摘要的，這個函數是摘要數值欄位的預設函數。  
  
3.  將銷售拖曳到**值**，並將 [Quantity] 之下。  
  
    步驟 1、2 和 3 會指定要在資料表中顯示的資料。  
  
4.  將 [SalesDate] 拖曳至 [資料列群組]。  
  
5.  將 [Subcategory] 拖曳至 [資料列群組] 並放置在 [SalesDate] 之下。  
  
    步驟 4 和 5 會依日期組織欄位的值，然後再依該日期的所有銷售進行組織。  
  
6.  按一下 **[下一步]**。  
  
    當您執行報表時，資料表會顯示每個日期、每個日期的所有訂單，以及每個訂單的所有產品、數量和銷售總額。  
  
7.  在 選擇配置頁面的 **選項**，確認**顯示小計和總計**已選取。  
  
8.  驗證已選取 [區塊式，小計位於下方]。  
  
9. 清除 [展開/摺疊群組] 選項。  
  
    在本教學課程中，您建立的報表不會使用向下鑽研功能，此功能可讓使用者展開父群組階層，以顯示子群組資料列和詳細資料列。  
  
10. 按一下 **[下一步]**。  
  
11. 按一下 **[完成]**。  
  
      資料表會加入至設計介面。 這個資料表具有五個資料行和五個資料列。 [資料列群組] 窗格會顯示三個資料列群組：[SalesDate]、[Subcategory] 和 [Details]。 詳細資料是資料集查詢擷取的所有資料。 [資料行群組] 窗格是空的。  
      
      ![report-builder-kpi-row-groups](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. 按一下 **[執行]** 預覽報表。  
  
資料表會針對特定日期銷售的每個產品顯示產品名稱、銷售數量和銷售總額。 資料會先依銷售日期排列，然後再依子類別排列。 

![report-builder-kpi-basic-table](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>格式化日期和貨幣
現在，我們來加寬資料行，並設定日期和貨幣格式。

1. 按一下**設計**来回到 [設計] 檢視中。

2. 產品名稱應該可以使用更多空間。 若要讓 Product 資料行更寬，請選取整個資料表，然後拖曳 Product 資料行右上角的控點。

3. 按下 Ctrl 鍵，然後選取包含 [Sum(Sales)] 的 4 個資料格。

4. 在**首頁** 索引標籤 >**數目** > **貨幣**。 這些資料格就會變更為顯示格式化貨幣。

   如果您的地區設定為 [英文 (美國)]，則預設範例文字會是 [$12,345.00]。 若未看見範例貨幣值中**數字**群組中，按一下**預留位置樣式** > **範例值**。
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (選擇性) 在 [主資料夾] 索引標籤的 [數字] 群組中，按一下[減少小數位數] 按鈕兩次，顯示沒有分的貨幣數字。

6. 按一下包含 [SalesDate] 的資料格。

6. 在**數目**群組 >**日期**。

   資料格就會顯示範例日期 [1/31/2000]。 

12. 按一下 **[執行]** 預覽報表。  
 
![report-builder-kpi-format-numbers](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3.使用背景色彩顯示 KPI  
您可以將背景色彩設定成執行報表時評估的運算式。  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>若要使用背景色彩來顯示 KPI 的目前狀態  
  
1.  在資料表中，以滑鼠右鍵按一下第二個`[Sum(Sales)]`儲存格 （的小計資料列會顯示子類別銷售額），然後按一下**文字方塊內容**。 

    請確定您已經選取資料格，而不是在資料格中，若要檢視的文字**文字方塊內容**。 
    
    ![report-builder-text-box-properties](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  在**填滿**索引標籤上，按一下  **fx**旁邊**填滿色彩**並輸入下列運算式中的**設定運算式對象： BackgroundColor**欄位：  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     這樣一來，如果資料格含有大於或等於 5000 的 `[Sum(Sales)]` 彙總總和，就會將其背景色彩變更為「亮綠色」。 介於 2500 與 5000 之間的 `[Sum(Sales)]` 值會以「黃色」顯示。 小於 2500 的值會以「紅色」顯示。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  按一下 **[執行]** 預覽報表。  
  
在顯示子類別銷售額的小計資料列中，資料格的背景色彩會根據銷售總和的值變成紅色、黃色或綠色。  

![report-builder-kpi-colors](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4.使用量測計顯示 KPI  
量測計可說明資料集中的單一值。 這個教學課程使用水平的線性量測計，因為它的形狀一目了然，即使很小並用於資料表資料格內，也很容易閱讀。 如需詳細資訊，請參閱 [量測計 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)。  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>若要使用量測計來顯示 KPI 的目前狀態  
  
1.  切換回設計檢視。  
  
2.  在資料表中，以滑鼠右鍵按一下 Sales 資料行的資料行控制代碼 >**插入資料行** > **右邊**。 新的資料行就會加入至此資料表。  

    ![report-builder-kpi-insert-column](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  在資料行標題中，輸入 **線性 KPI** 。  
  
4.  在**插入** 索引標籤 >**資料視覺效果** > **量測計**，然後按一下資料表外部的設計介面。   
  
5.  在**選取量測計類型** 對話方塊中，選取第一個線性量測計類型，**水平**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    量測計就會加入至設計介面。  
  
7.  從 [報表資料] 窗格，將 `Sales` 欄位拖曳到量測計。 [量測計資料] 窗格隨即開啟。  
  
    當您卸除`Sales`欄位拖曳到量測計中，移至**值**清單，並使用內建的 Sum 函數彙總資料。  
   
    ![report-builder-kpi-drag-sales-field](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. 在**量測計資料** 窗格中，按一下箭號旁**LinearPointer1** > **指標屬性**。  
  
10. 在**線性指標屬性**對話方塊 >**指標選項** 索引標籤 >**指標類型**，請確定**列**已選取。 
 
11. 按一下 **[確定]**。  
  
12. 以滑鼠右鍵按一下量測計標尺，然後按一下**標尺屬性**。  
  
13. 在**線性標尺屬性**對話方塊 >**一般**索引標籤上，設定**最大**設為 25000。  

    > [!NOTE]  
    > 除了像是 25000 的常數，您可以使用運算式動態計算的值**最大**選項。 運算式會使用彙總功能進行彙總，看起來就類似於運算式 `=Max(Sum(Fields!Sales.value), "Tablix1")`。  

14. 在**標籤**索引標籤上，核取**隱藏標尺標籤**。

15. 按一下 **[確定]**。
  
14. 將資料表內部的量測計拖曳至「線性 KPI」資料行中的第二個空白儲存格；具體位置為顯示 `Subcategory` 欄位小計銷售額的資料列，以及您已新增背景色彩公式的欄位旁邊。  
  
    > [!NOTE]  
    > 您可能必須重新調整資料行，使水平的線性量測計能夠納入資料格中。 若要調整資料行的大小，請選取資料表，並拖曳資料行控點。 報表設計介面會調整大小以配合資料表的尺寸。  
  
15. 按一下 **[執行]** 預覽報表。  
  
    量測計中綠色橫條的水平長度會根據 KPI 的值而變更。  
  
![report-builder-linear-kpi](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5.使用指標顯示 KPI  
指標是小型的簡單量測計，可一目了然資料值。 由於指標的尺寸小加上簡單明瞭，因此常用於資料表和矩陣。 如需詳細資訊，請參閱[指標 &#40;報表產生器及 SSRS &#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>若要使用指標來顯示 KPI 的目前狀態  
  
1.  切換至 [設計] 檢視。  
  
2.  在資料表中，以滑鼠右鍵按一下您在上一個程序中加入的線性的 KPI 資料行的資料行控制代碼 >**插入資料行** > **右邊**。 新的資料行就會加入至此資料表。  
  
3.  在資料行標題中輸入 **警示燈 KPI** 。  
  
4.  按一下子類別小計的資料格 (位於您在上一個程序中新增的線性量測計旁邊)。  
  
5.  在**插入** 索引標籤 >**資料視覺效果**> 按兩下**指標。**  
  
6.  在**選取指標類型**對話方塊的 **圖形**，選取第一個形狀類型**3 三交通號誌 （無框）**。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    即會將指標新增至新的「警示燈 KPI」資料行中的資料格。  
  
8.  以滑鼠右鍵按一下指標，然後按一下**指標屬性**。  
  
9. 在**值和狀態**索引標籤的**值**方塊中，選取**[sum （sales)]**。 請不要變更任何其他選項。  
  
    根據預設，資料同步處理會整個資料區域，而且您會看到值**Tablix1**，在報表中，資料表資料區域的名稱在**同步處理範圍**方塊。  
  
    在此報表中，您也可以變更子類別小計資料格中放置之指標的範圍，以同步處理 [SalesDate] 欄位。  
  
11. 按一下 **[確定]**。

11. 按一下 **[執行]** 預覽報表。  

![report-builder-kpi-stoplight](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6.加入報表標題  
報表標題會出現在報表的頂端。 您可以將報表標題放置在報表頁首，如果報表不使用報表頁首，則可以放置在報表主體頂端的文字方塊中。 在本節中，您將使用自動放置在報表主體頂端的文字方塊。  
  
您可以將不同的字型樣式、大小和色彩套用到文字的片語和個別字元，進一步加強文字。 如需詳細資訊，請參閱[在文字方塊中將文字格式化 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **產品銷售 KPI**，然後按一下文字方塊外部。  
  
3.  （選擇性） 包含的文字方塊中以滑鼠右鍵按一下**產品銷售 KPI**，按一下 **文字方塊內容**，然後在 字型 索引標籤上選取不同的字型樣式、 大小和色彩。  
  
4.  按一下 **[執行]** 預覽報表。  
  
## <a name="Save"></a>7.儲存報表  
將報表儲存至報表伺服器或您的電腦。 如果沒有將報表儲存到報表伺服器，就無法使用數個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如報表組件和子報表。  
  
### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
    「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在**名稱**，將預設名稱取代**產品銷售 KPI**。  
  
5.  按一下 **[儲存]**。  
  
報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 [桌面]、[我的文件] 或 [我的電腦]，然後瀏覽到您要儲存報表的資料夾。  
  
> [!NOTE]  
> 如果您沒有報表伺服器的存取權，請按一下**桌面**，**我的文件**，或**我的電腦**並將報表儲存到您的電腦。  
  
1.  在**名稱**，將預設名稱取代**產品銷售 KPI**。  
  
2.  按一下 **[儲存]**。  
  
## <a name="next-steps"></a>後續步驟  
您已成功完成「將 KPI 加入至報表」教學課程。 如需詳細資訊，請參閱：
*  [量測計](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [指標](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
* [報表產生器教學課程](../reporting-services/report-builder-tutorials.md)
* [SQL Server 2016 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


