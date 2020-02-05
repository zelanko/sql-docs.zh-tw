---
title: 教學課程：建立矩陣報表 (報表產生器) | Microsoft Docs
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ed53800a1b45dd79548c59aaab57f71bd700d94d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63294698"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>教學課程：建立矩陣報表 (報表產生器)
本教學課程會引導您建立 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分頁報表，其中具有巢狀資料列和資料行群組的範例銷售資料矩陣。 

您也會建立相鄰的資料行群組、格式化資料行，以及旋轉文字。 下圖顯示報表，與您將要建立的報表相似。  
  
![report-builder-matrix-tutorial](../reporting-services/media/report-builder-matrix-tutorial.png)
   
完成這個教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的資訊，請參閱 [教學課程的必要條件](../reporting-services/prerequisites-for-tutorials-report-builder.md)。 
  
## <a name="CreateMatrix"></a>1.從新增資料表或矩陣精靈建立矩陣報表和資料集  
在本節中，您會選擇共用資料來源、建立內嵌資料集，然後在矩陣中顯示資料。  
  
> [!NOTE]  
> 在本教學課程中，查詢已經包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
### <a name="to-create-a-matrix"></a>建立矩陣  
  
1.  從您的電腦、[ Web 入口網站或 SharePoint 整合模式](../reporting-services/report-builder/start-report-builder.md)啟動報表產生器[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]。  
  
    [新報表或資料集]  對話方塊隨即開啟。  
  
    如果您看不到 [新增報表或資料集]  對話方塊，請按一下 [檔案]  功能表 > [新增]  。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]** 。  
  
4.  在 **[選擇資料集]** 頁面上，按一下 **[建立資料集]** 。  
  
5.  按 [下一步]  。  
  
6.  在 [選擇與資料來源的連線]  頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源。 如果沒有資料來源可用，或無法存取報表伺服器，您可以改用內嵌資料來源。 如需建立內嵌資料來源的資訊，請參閱[教學課程︰建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
7.  按 [下一步]  。  
  
8.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]** 。  
  
9. 複製下列查詢並貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. (選擇性) 按一下 [執行] 圖示 (!) 執行查詢並查看資料。

11. 按 [下一步]  。  
  
## <a name="Groups"></a>2.從新增資料表或矩陣精靈組織資料、選擇配置  
使用精靈提供起始設計來顯示資料。 精靈中的預覽窗格可協助您在完成矩陣設計之前，先視覺化群組資料的結果。  
  
1.  在 [排列欄位]  頁面上，從 [可用的欄位]  將 [Territory] 拖曳至 [資料列群組]  。  
  
2.  將 [SalesDate] 拖曳至 [資料列群組]  並放置在 [Territory] 之下。  
  
    欄位列於 [資料列群組]  中的順序定義了群組階層。 步驟 1 和步驟 2 會先依領域再依銷售日期，組織欄位的值。  
  
3.  將 [Subcategory] 拖曳至 [資料行群組]  。  
  
4.  將 [Product] 拖曳至 [資料行群組]  並放置在 [Subcategory] 之下。  
  
    同樣地，欄位列於 [資料行群組]  中的順序定義了群組階層。 步驟 3 和步驟 4 會先依子類別目錄再依產品，組織欄位的值。  
  
5.  將 [Sales] 拖曳至 [值]  。  
  
    [Sales] 是使用 Sum 函數進行摘要，此為摘要數值欄位的預設函數。  
  
6.  將 [Quantity] 拖曳至 [值]  。  
  
    [Quantity] 是使用 Sum 函數進行摘要。  
  
    步驟 5 和步驟 6 指定了矩陣資料格要顯示的資料。
    
    ![report-builder-arrange-fields-report-wizard](../reporting-services/media/report-builder-arrange-fields-report-wizard.png)  
  
7.  按 [下一步]  。  
  
8.  在 [選擇配置] 頁面的 [選項]  下方，確定已選取 [顯示小計和總計]  。  
  
9. 驗證已選取 [區塊式，小計位於下方]  。  
  
10. 確定已選取 [展開/摺疊群組]  選項。  
  
11. 按 [下一步]  。  
  
13. 按一下 [完成]  。  
  
    矩陣會加入至設計介面。 [資料列群組] 窗格將顯示兩個資料列群組：Territory 和 SalesDate。 [資料行群組] 窗格則顯示這兩個資料行群組：Subcategory 和 Product。 詳細資料是資料集查詢擷取的所有資料。  
    
    ![report-builder-row-and-column-groups](../reporting-services/media/report-builder-row-and-column-groups.png)
  
14. 按一下 **[執行]** 預覽報表。  
  
    矩陣會針對特定日期銷售的每個產品，顯示產品所屬的子類別目錄和銷售領域。  

14. 展開子類別 您可以看到報表很快變寬。

![report-builder-expand-matrix](../reporting-services/media/report-builder-expand-matrix.png)
  
## <a name="FormatData"></a>3.將資料格式化  
根據預設，[Sales] 欄位的摘要資料會顯示一般數字，而 [SalesDate] 欄位會顯示日期加上時間資訊。 在本節中，您會格式化以使 [Sales] 欄位將數字顯示為貨幣，讓 [SalesDate] 欄位只顯示日期。 切換 [預留位置樣式]  ，將格式化的文字方塊和預留位置文字顯示為範例值。  
  
### <a name="to-format-fields"></a>格式化欄位  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  按下 Ctrl 鍵，然後選取包含 `[Sum(Sales)]`的 9 個資料格。  
  
3.  在 [主資料夾]  索引標籤 > [數字]   > [貨幣]  上。 這些資料格就會變更為顯示格式化貨幣。  
  
    如果您的地區設定為 [英文 (美國)]，則預設範例文字會是 [ **$12,345.00**]。 如果您看不到範例貨幣值，請按一下 [數字]  群組中的 [預留位置樣式]   > [範例值]  。  
    
    ![report-builder-placeholder-value](../reporting-services/media/report-builder-placeholder-value.png)
  
4.  按一下包含 `[SalesDate]`的資料格。  
  
5.  在 [數字]  群組 > [日期]  中。  
  
    資料格就會顯示範例日期 **[1/31/2000]** 。 如果您看不到範例日期，請按一下 [數字]  群組中的 [預留位置樣式]  ，然後按一下 [範例值]  。  
  
6.  按一下 [執行]  以預覽報表。  
  
日期值如今只顯示日期，而銷售值顯示為貨幣。  
  
## <a name="AdjacentGroup"></a>4.加入相鄰資料行群組  
您可以將資料列和資料行群組巢狀套疊為父子關聯性，或彼此相鄰的同層級關聯性。  
  
在本節中，您會新增一個與 Subcategory 資料行群組相鄰的資料行群組、複製資料格以填入新資料行群組，然後使用運算式建立新資料行群組頁首的值。  
  
### <a name="to-add-an-adjacent-column-group"></a>加入相鄰資料行群組  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下包含 `[Subcategory]` 的資料格，並指向 [新增群組]  ，然後按一下 [右方相鄰]  。  
  
    **[Tablix 群組]** 對話方塊隨即開啟。  
  
3.  在 [群組依據]  清單中選取 [SalesDate]，然後按一下 [確定]  。  
  
    新的資料行群組就會新增到 Subcategory 資料行群組的右邊。  
  
4.  以滑鼠右鍵按一下新資料行群組中包含 `[SalesDate],` 的資料格，然後按一下 [運算式]  。  
  
5.  將下列運算式複製到 [運算式] 方塊中。  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
    此運算式會從銷售日期擷取星期幾。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
6.  以滑鼠右鍵按一下 Subcategory 資料行群組中包含 [Total] 的資料格，然後按一下 [複製]  。  
  
7.  以滑鼠右鍵按一下步驟 5 建立之運算式所在資料格正下方的資料格，然後按一下 [貼上]  。  
  
8.  按下 Ctrl 鍵。  
  
9. 在 Subcategory 群組中，按一下 [Sales] 資料行標頭及其下方的三個資料格，並按一下滑鼠右鍵，然後按一下 [複製]  。  
  
10. 將這四個資料格貼至新資料行群組中的四個空白資料格。  
  
11. 按一下 **[執行]** 預覽報表。  
  
報表多出兩個資料行，名為「星期一」和「星期二」。 資料集只包含這兩天的資料。  

![report-builder-matrix-weekdays](../reporting-services/media/report-builder-matrix-weekdays.png)
  
> [!NOTE]  
> 如果資料中還有別的星期，報表也會納入其資料行。 每個資料行包含各領域的總銷售額，而資料行標頭是 [Sales]  。  
  
## <a name="Width"></a>5.變更資料行寬度  
含有矩陣的報表在執行時，通常會水平且垂直地展開。 若您打算將報表匯出為印刷報表採用的格式，如 Microsoft Word 或 Adobe PDF，控制水平展開程度就特別重要。 如果報表水平地展開成跨多個頁面，將造成印刷報表難以判讀。 為了盡量減少水平展開程度，您可將資料行寬度調整成以不換行的方式顯示資料所需的量。 您也可以重新命名資料行，使顯示資料所需的寬度恰能容納其標題。  
  
### <a name="to-rename-and-resize-the-columns"></a>資料行重新命名與調整大小  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  選取離左邊最遠的 [Quantity] 資料行中的文字，然後鍵入 **QTY**。  
  
    該資料行標題現已變成 QTY。  
  
3.  針對名為 Quantity 的其餘兩個資料行重複步驟 2，
  
4.  按一下矩陣，使資料行和資料列控點出現在矩陣的上面和旁邊。  
  
    沿著資料表頂端和側邊的灰色長條是資料行和資料列控點。  
    
    ![report-builder-column-handles](../reporting-services/media/report-builder-column-handles.png)
  
5.  首先要調整最左邊 QTY 資料行的大小：指向該資料行控點之間的線條，使游標變成雙箭頭。 將資料行往左拖曳，直到其寬度為 1/2 英吋。  
  
    要顯示數量的資料行有 1/2 英吋寬就已足夠。  
  
6.  針對名為 QTY 的其餘資料行重複步驟 5。  
  
7.  按一下 [執行]  以預覽報表。  
  
包含數量的資料行現在較窄，而且名為 QTY。  
  
## <a name="MergeCells"></a>6.合併矩陣資料格  
邊角區域是位於矩陣的左上角。 邊角區域內的資料格數目，會隨矩陣中的資料列與資料行群組數目而有所不同。 本教學課程建置的矩陣其邊角區域內有四個資料格。 這些資料格排成兩列兩欄，反映了資料列與資料行群組階層的深度。 本報表用不到這四個資料格，因此您要將其合併為單一資料格。  
  
### <a name="to-merge-matrix-cells"></a>合併矩陣資料格  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  按一下矩陣，使資料行和資料列控點出現在矩陣的上面和旁邊。  
  
3.  按下 Ctrl 鍵，然後選取四個邊角資料格。  
  
4.  以滑鼠右鍵按一下這些資料格，然後按一下 [合併資料格]  。  
  
5.  以滑鼠右鍵按一下新的合併資料格，然後按一下 [文字方塊屬性]  。  
  
6.  在 [框線]  索引標籤 > [預設]   > [無]  。
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 按一下 [執行]  以預覽報表。  
  
不再顯示矩陣上方角落的資料格。 
  
## <a name="HeaderTitle"></a>7.加入報表頁首和報表標題  
報表標題會出現在報表的頂端。 您可以將報表標題放置在報表頁首，如果報表不使用報表頁首，則可以放置在報表主體頂端的文字方塊中。 在本教學課程中，您將移除報表頂端的文字方塊，然後加入標題至頁首。  
  
### <a name="to-add-a-report-header-and-report-title"></a>加入報表頁首和報表標題  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  選取報表主體頂端包含 [按一下以新增標題]  的文字方塊，然後按 Delete 鍵。  
  
3.  在 [插入]  索引標籤 > [標頭]   > [新增標頭]  上。  
  
    頁首就會加入至報表主體頂端。  
  
4.  在 [插入]  索引標籤上，按一下 [文字方塊]  ，然後將文字方塊拖曳至報表標題。 將文字方塊調整成長約 6 英吋且高約 3/4 英吋，然後放到報表頁首的左側。  
  
5.  在文字方塊中，鍵入 **Sales by Territory, Subcategory, and Day**。  
  
6.  選取您輸入的文字，在 [首頁]  索引標籤 > [字型]  ：
    * **大小 24 pt**
    * **色彩 暗紅色**
 
10. 按一下 **[執行]** 預覽報表。  
  
在報表中，報表頁首包含報表標題。  
  
## <a name="Save"></a>8.儲存報表  
您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。  
  
本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]** 。  
  
2.  按一下 **[最近使用的網站和伺服器]** 。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
    「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您將會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 [名稱]  中，將預設名稱取代為 **SalesByTerritorySubcategory**。  
  
5.  按一下 [檔案]  。  
  
報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]** 。  
  
2.  按一下 **[桌面]** 、 **[我的文件]** 或 **[我的電腦]** ，然後瀏覽到您要儲存報表的資料夾。  
  
3.  在 [名稱]  中，將預設名稱取代為 **SalesByTerritorySubcategory**。  
  
4.  按一下 [檔案]  。  
  
## <a name="RotateTextBox"></a>9.(選擇性) 將文字方塊旋轉 270 度  
含有矩陣的報表在執行時，可能會水平且垂直地展開。 如果將文字方塊旋轉 270 度 (垂直旋轉)，就比較不佔水平空間。 這樣轉譯後的報表將會變窄，且若匯出為 Microsoft Word 等格式，則大概都能容納於單一列印頁面上。  
  
文字方塊也可以將文字顯示成水平、垂直 (由上而下) 的方向。 如需詳細資訊，請參閱[文字方塊 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)。  
  
### <a name="to-rotate-text-box-270-degrees"></a>將文字方塊旋轉 270 度  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  選取包含的資料格。 `[Territory].` 

    >**注意**︰選取資料格，而不是文字。 WritingMode 屬性只適用於資料格。
    
     ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
  
3.  在 [屬性] 窗格中，找出 WritingMode 屬性，並將其從 [預設]  變更為 [Rotate270]  。  
  
    如果 [屬性] 窗格並未開啟，請按一下功能區的 [檢視]  索引標籤，然後選取 [屬性]  。  
  
4.  確認 CanGrow 屬性已設定為 **True**。  
  
5.  在 [主資料夾]  索引標籤 > [段落]  區段上，選取 [中間]  和 [置中]  ，將文字定位在儲存格的垂直及水平中心。  
 
6. 將 [Territory] 資料行的寬度調整成 1/2 英吋，並刪除資料行標題。  
6.  按一下 [執行]  以預覽報表。  
  
領域名稱的寫法為由上而下的垂直方向。 Territory 資料列群組的高度會依領域名稱的長度而變化。  
  
## <a name="next-steps"></a>後續步驟  
以上總結如何建立矩陣報表的教學課程。 如需矩陣的詳細資訊，請參閱： 
-    [資料表、矩陣和清單](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)
-    [建立矩陣](../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)
-    [Tablix 資料區的區域](../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md) 
-    [Tablix 資料區資料格、資料列及資料行](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md)  
[SQL Server 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

