---
title: 教學課程：將走勢圖加入至報表 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1fddfc39b7f6e5764dbe11bf6b069136fba8420d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294726"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>教學課程：將走勢圖加入至報表 (報表產生器)
  在本教學課程中，您要根據範例銷售資料建立基本資料表報表，然後將走勢圖加入至資料表中的儲存格。  
  
 本教學課程所建立的報表另有一個增強型版本，可從範例 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 報表產生器報表取得。 如需有關下載這個範例報表和其他人的詳細資訊，請參閱[報表產生器範例報表](https://go.microsoft.com/fwlink/?LinkId=184851)。 下圖顯示與您將要建立的報表相似的範例報表。  
  
 ![rs_SparklineMatrixTutorial](../../2014/tutorials/media/rs-sparklinematrixtutorial.gif "rs_SparklineMatrixTutorial")  
  
 影片[How to:資料表 （報表產生器影片） 中建立走勢圖](https://technet.microsoft.com/bi/ff871942.aspx)說明如何建立包含走勢圖的類似報表。  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何執行下列作業：  
  
 1. [建立含資料表的報表](#CreateTable)  
  
 2. [在資料表或矩陣精靈建立查詢](#Query)  
  
 3. [將走勢圖加入至資料表](#Sparkline)  
  
 4. [垂直和水平對齊走勢圖](#AlignSparklines)  
  
### <a name="other-optional-steps"></a>其他選擇性步驟  
 5. [將資料格式化為貨幣](#FormatCurrency)  
  
 6. [將資料格式化為日期](#FormatDates)  
  
 7. [變更資料行寬度](#Width)  
  
 8. [加入報表標題](#Title)  
  
 9. [儲存報表](#Save)  
  
 完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="CreateTable"></a> 1.建立含資料表的報表  
  
#### <a name="to-create-a-report"></a>建立報表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
     **[使用者入門]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果 **[使用者入門]** 對話方塊沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  在 **[選擇資料集]** 頁面上，選取 **[建立資料集]**，然後按 **[下一步]**。 **[選擇與資料來源的連接]** 頁面隨即開啟。  
  
    > [!NOTE]  
    >  本教學課程無須任何特定資料，您只需要連接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 資料庫。 如果您已有資料來源連接列於 [資料來源連接] 底下，就可以選取該連接並移至步驟 10。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
5.  按一下 **[新增]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
6.  在 [名稱] 中鍵入 **Product Sales** 作為資料來源的名稱。  
  
7.  在 [選取連線類型] 中，驗證已選取 [Microsoft SQL Server]。  
  
8.  在 [連接字串] 中，鍵入下列文字：  
  
     **Data Source=\<servername>**  
  
     運算式\<伺服器名稱 >，例如 Report001，指定 SQL Server Database Engine 的執行個體安裝所在的電腦。 由於報表資料不是擷取自 SQL Server 資料庫，您不必加上資料庫的名稱。 指定之伺服器上的預設資料庫將用來剖析查詢。  
  
9. 按一下 **[認證]**。 輸入您存取外部資料來源所需的認證。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     您會回到 [選擇與資料來源的連線] 頁面。  
  
11. 若要確認您能夠連接至資料來源，請按一下 **[測試連接]**。  
  
     「成功建立連接」訊息就會出現。  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. 按一下 [下一步] 。  
  
##  <a name="Query"></a> 2.在資料表精靈中建立查詢  
 在報表中，您可以使用擁有預先定義查詢的共用資料集，或是建立只在報表中使用的內嵌資料集。 在本教學課程中，您將建立內嵌資料集。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-query"></a>建立查詢  
  
1.  [設計查詢] 頁面上會開啟關聯式查詢設計工具。 在這個教學課程中，您將使用以文字為基礎的查詢設計工具。  
  
2.  按一下 [當成文字編輯]。 以文字為基礎的查詢設計工具會顯示查詢窗格和結果窗格。  
  
3.  將下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢貼入 [查詢] 方塊。  
  
    ```  
    SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2010-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  在查詢設計工具的工具列上，按一下 [執行]\(**!**)。  
  
     查詢隨即執行，並顯示 **SalesDate**、 **Subcategory**、 **Product**、 **Sales**和 **Quantity**欄位的結果集。  
  
5.  按一下 [下一步] 。  
  
6.  在 [排列欄位] 頁面上，將 [Sales] 拖曳至 [值]。  
  
     **Sales** 是透過 Sum 函數彙總。 值為 [Sum(Sales)]。  
  
7.  將 [Product] 拖曳至 [資料列群組]。  
  
8.  將 [SalesDate] 拖曳至 [資料行群組]。  
  
9. 按一下 [下一步] 。  
  
10. 在 **[選擇配置]** 頁面的 **[選項]** 下方，確定已選取 **[顯示小計和總計]** 。  
  
     精靈的 [預覽] 窗格會顯示含有三個資料列的資料表。 當您執行報表時，每個資料列都會以下列方式顯示：  
  
    1.  第一個資料列會針對資料表出現一次，以顯示資料行標題。  
  
    2.  第二個資料列會針對每個產品重複一次，並顯示產品名稱、每日小計和產品線總計。  
  
    3.  第三個資料列會針對資料表出現一次，以顯示總計。  
  
11. 按一下 [下一步] 。  
  
12. 在 **[選擇樣式]** 頁面的 **[樣式]** 窗格中，選取 **[石板]**。  
  
     [預覽] 窗格隨即顯示採用該樣式的資料表範例。  
  
13. 按一下 **[完成]**。  
  
14. 資料表會加入至設計介面。 該資料表具有三個資料行和三個資料列。  
  
     請查看 [群組] 窗格。 如果未顯示 [群組] 窗格，請按一下 [檢視] 功能表上的 [群組]。 [資料列群組] 窗格會顯示一個資料列群組：**產品**。 [資料行群組] 窗格會顯示一個資料行群組：**SalesDate**。 詳細資料是資料集查詢擷取的所有資料。  
  
15. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Sparkline"></a> 3.加入走勢圖  
  
#### <a name="to-add-a-sparkline-chart-to-a-table"></a>將走勢圖加入至資料表  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  選取資料表中的 [總計] 資料行。  
  
3.  按一下滑鼠右鍵，指向 [插入資料行]，然後按一下 [左方]。  
  
4.  在新的資料行，以滑鼠右鍵按一下 [Product] 資料列中，指向**插入**功能區索引標籤，然後按一下**走勢圖**。  
  
5.  請確定在第一個走勢圖**資料行**資料列已選取，然後按一下**確定**。  
  
6.  按一下走勢圖以顯示 [圖表資料] 窗格。  
  
7.  按一下加號 （+） 登入 [值] 方塊中，然後**銷售**。  
  
     **Sales** 欄位內的值現在即為走勢圖的值。  
  
8.  按一下加號 （+） 登入類別目錄群組 方塊中，然後**SalesDate**。  
  
9. 按一下 [執行] 以預覽報表。  
  
     請注意資料表的每一列內都有走勢圖，但是圖表並不正確。 圖表中的橫條沒有彼此切齊。 第二個資料列只有四個橫條，而第一列有六個，因此前者的橫條比後者的橫條還要寬。 這樣您無法比較各產品每日的值， 這些橫條必須彼此貼齊。  
  
     同時請注意，每一列內最高的橫條都和該列等高。 這也會產生誤導，因為每個資料列的最大值是否不相等： 針對 Budget Movie-maker 的最大值為 $10400，但 Slim Digital 的最大值是 $26,576-超過兩次一樣大。 然而，這兩列內最大值橫條的高度幾乎一樣， 這些橫條需要能夠隨著其他走勢圖縮放。  
  
     ![rs_SprklineMtrxUnaligndBars](../../2014/tutorials/media/rs-sprklinemtrxunaligndbars.gif "rs_SprklineMtrxUnaligndBars")  
  
##  <a name="AlignSparklines"></a> 4.垂直與水平對齊走勢圖  
 走勢圖很難讀取時它們不都使用相同的度量。 每一個走勢圖的水平和垂直軸都需要符合其餘的走勢圖。  
  
#### <a name="to-set-alignment-for-the-sparklines-in-the-table"></a>設定資料表中走勢圖的對齊方式  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下走勢圖，然後按一下 [垂直軸屬性]。  
  
3.  選取 [軸對齊位置] 核取方塊。  
  
     清單中會顯示 Tablix1。 此為唯一的選項。 這是將每個走勢圖內的橫條高度設定成彼此的相對值。  
  
4.  按一下 [確定] 。  
  
5.  以滑鼠右鍵按一下走勢圖，然後按一下 [水平軸屬性]。  
  
6.  選取 [軸對齊位置] 核取方塊。  
  
     清單中會顯示 Tablix1。 此為唯一的選項。 這是將每個走勢圖內的橫條寬度設定成彼此的相對值。 如果某些走勢圖的橫條數目較少，則這些走勢圖將以空白代表缺資料。  
  
7.  按一下 [確定] 。  
  
8.  按一下 [執行] 來重新預覽報表。  
  
 請注意，所有橫條現在已與其他列內的橫條對齊。  
  
##  <a name="FormatCurrency"></a> 5.(選擇性) 將資料格式化為貨幣  
 根據預設， **Sales** 欄位的摘要資料會顯示一般數字。 格式化該欄位，將數字顯示為貨幣。 切換 [預留位置樣式]，將格式化的文字方塊和預留位置文字顯示為範例值。  
  
#### <a name="to-format-a-currency-field"></a>格式化貨幣欄位  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  按一下 （底下的資料行標題資料列） 的第二個資料列中的資料格**SalesDate**資料行並拖曳以選取包含的所有資料格`[Sum(Sales)]`。  
  
3.  在 [主資料夾] 索引標籤的 [數字] 群組中，按一下 [貨幣] 按鈕。 這些資料格就會變更為顯示格式化貨幣。  
  
     如果您的地區設定為 [英文 (美國)]，則預設範例文字會是 [**$12,345.00**]。 如果您看不到範例貨幣值，請按一下**預留位置樣式**中**數字**群組，並再按**範例值**。  
  
4.  按一下 [執行] 以預覽報表。  
  
 摘要值**銷售**顯示為貨幣。  
  
##  <a name="FormatDates"></a> 6.(選擇性) 將資料格式化為日期  
 根據預設， **SalesDate** 欄位會同時顯示日期和時間資訊。 您可以將該欄位格式化，以便只顯示日期。  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>將日期欄位格式化成預設格式  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  按一下包含 `[SalesDate]`的資料格。  
  
3.  功能區上**首頁**索引標籤中，於**數目**群組中，從下拉式清單中選取**日期**。  
  
     資料格就會顯示範例日期 **[1/31/2000]**。 如果您看不到範例日期，請按一下 [數字] 群組中的 [預留位置樣式]，然後按一下 [範例值]。  
  
4.  按一下 **[執行]** 預覽報表。  
  
 **SalesDate**值會以預設的日期格式顯示。  
  
##  <a name="Width"></a> 7.(選擇性) 變更資料行寬度  
 根據預設，資料表中的每個資料格都會包含一個文字方塊。 頁面轉譯時，文字方塊會垂直展開以容納文字。 在轉譯的報表中，每一個資料列都會依照資料列中最高的轉譯文字方塊高度展開。 設計介面上資料列的高度對於轉譯報表中資料列的高度並無影響。  
  
 若要減少每個資料列佔用的垂直空間數量，請展開資料行寬度以容納一行上資料行中預期的文字方塊內容。  
  
#### <a name="to-change-the-width-of-columns"></a>變更資料行的寬度  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  按一下資料表，使資料行和資料列控點出現在資料表的上面和旁邊。  
  
     沿著資料表頂端和側邊的灰色長條是資料行和資料列控點。  
  
3.  指向資料行控點之間的線條，使游標變成雙箭頭。 將資料行拖曳到所需的大小。 例如，展開 資料行**產品**，讓產品名稱顯示在同一行。  
  
4.  按一下 [執行] 以預覽報表。  
  
##  <a name="Title"></a> 8.(選擇性) 加入報表標題  
 報表標題會出現在報表的頂端。 您可以將報表標題放置在報表頁首，如果報表不使用報表頁首，則可以放置在報表主體頂端的文字方塊中。 在本教學課程中，您將使用自動放置在報表主體頂端的文字方塊。  
  
 您可以將不同的字型樣式、大小和色彩套用到文字的片語和個別字元，進一步加強文字。 如需詳細資訊，請參閱[在文字方塊中將文字格式化 &#40;報表產生器及 SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **Product Sales**，然後按一下文字方塊外部。  
  
3.  以滑鼠右鍵按一下包含 [Product Sales] 的文字方塊，然後按一下 [文字方塊屬性]。  
  
4.  在 [文字方塊屬性] 對話方塊中，按一下 [字型]。  
  
5.  在 [大小] 清單中，選取 [18pt]。  
  
6.  在 **色彩**清單中，選取**暗紅色**。  
  
7.  選取 [粗體]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> 9.儲存報表  
 將報表儲存至報表伺服器或您的電腦。 如果沒有將報表儲存到報表伺服器，就無法使用數個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如報表組件和子報表。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  將 [名稱] 中的預設名稱取代為 **Product Sales**。  
  
5.  按一下 **[儲存]**。  
  
 報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 [桌面]、[我的文件] 或 [我的電腦]，然後瀏覽到您要儲存報表的資料夾。  
  
3.  將 [名稱] 中的預設名稱取代為 **Product Sales**。  
  
4.  按一下 [儲存] 。  
  
## <a name="next-steps"></a>後續步驟  
 這總結本教學課程：建立含走勢圖的資料表報表。 如需走勢圖的詳細資訊，請參閱[走勢圖和資料橫條 &#40;報表產生器和 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
