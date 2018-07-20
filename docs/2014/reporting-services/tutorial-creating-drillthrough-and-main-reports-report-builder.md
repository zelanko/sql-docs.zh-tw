---
title: 教學課程：建立鑽研及主報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7168c8d3-cef5-4c4a-a0bf-fff1ac5b8b71
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 69d6d5352c2f537add31fe2481166bb3a7982d56
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084040"
---
# <a name="tutorial-creating-drillthrough-and-main-reports-report-builder"></a>教學課程：建立鑽研及主報表 (報表產生器)
  本教學課程將教導您如何建立兩種報表：鑽研報表與主報表。 這些報表中使用的範例銷售資料是從 Analysis Services Cube 擷取的。 下圖顯示您將建立的報表。  
  
 ![rs_DrillthroughCubeTutorial](../../2014/tutorials/media/rs-drillthroughcubetutorial.gif "rs_DrillthroughCubeTutorial")  
  
 下圖顯示主報表中的欄位值 Games and Toys 如何顯示在鑽研報表的標題中。 鑽研報表中的資料與 Games and Toys 產品類別目錄有關。  
  
 ![rs_DrillthroughCubeTutorialParmExpr](../../2014/tutorials/media/rs-drillthroughcubetutorialparmexpr.gif "rs_DrillthroughCubeTutorialParmExpr")  
  
## <a name="what-you-will-learn"></a>學習內容  
 **鑽研報表中您將了解如何：**  
  
1.  [從資料表或矩陣精靈建立鑽研矩陣報表和資料集](#DMatrixAndDataset)  
  
    1.  [指定資料連接](#DConnection)  
  
    2.  [建立 MDX 查詢](#DMDXQuery)  
  
    3.  [將資料組織為群組樣式](#DLayout)  
  
    4.  [加入小計和總計](#DTotals)  
  
    5.  [選擇樣式](#DStyle)  
  
2.  [將資料格式化為貨幣](#DFormat)  
  
3.  [資料行加入走勢圖中顯示銷售值](#DSparkline)  
  
4.  [加入具有產品類別目錄名稱的報表標題](#DReportTitle)  
  
5.  [更新參數屬性](#DParameter)  
  
6.  [將報表儲存至 SharePoint 文件庫](#DSave)  
  
 **主報表中您將了解如何：**  
  
1.  [從資料表或矩陣精靈建立主要矩陣報表和資料集](#MMatrixAndDataset)  
  
    1.  [指定資料連接](#MConnection)  
  
    2.  [建立 MDX 查詢](#MMDXQuery)  
  
    3.  [將資料組織成群組](#MLayout)  
  
    4.  [加入小計和總計](#MTotals)  
  
    5.  [選擇樣式](#MStyle)  
  
2.  [移除總計資料列](#MGrandTotal)  
  
3.  [設定用於鑽研的文字方塊動作](#MDrillthrough)  
  
4.  [以指標取代數值](#MIndicators)  
  
5.  [更新參數屬性](#MParameter)  
  
6.  [加入報表標題](#MTitle)  
  
7.  [將報表儲存至 SharePoint 文件庫](#MSave)  
  
8.  [執行主報表和鑽研報表](#MRunReports)  
  
 完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
 這個教學課程需要能夠存取 Contoso Sales Cube。 這個需求同時適用於鑽研報表和主報表。 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="DMatrixAndDataset"></a> 1.從資料表或矩陣精靈建立鑽研報表  
 從 [使用者入門] 對話方塊中，使用 **[資料表或矩陣精靈]** 建立矩陣報表。 精靈中可用的模式有兩種：報表設計和共用資料集設計。 在本教學課程中，您將使用報表設計模式。  
  
#### <a name="to-create-a-new-report"></a>建立新的報表  
  
1.  按一下 **開始**，指向**程式**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**，然後按一下**報表產生器**。  
  
     **[使用者入門]** 對話方塊隨即開啟。 如果沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，確認已選取 **[資料表或矩陣精靈]** 。  
  
##  <a name="DConnection"></a> 1a。 指定資料連接  
 資料連接包含連接至外部資料來源所需的資訊，例如 Analysis Services Cube 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 若要指定資料連接，您可以使用來自報表伺服器的共用資料來源，或是建立僅在此報表中使用的內嵌資料來源。 在本教學課程中，您將使用內嵌資料來源。 若要深入了解如何使用共用資料來源，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
#### <a name="to-create-an-embedded-data-source"></a>建立內嵌資料來源  
  
1.  在 **[選擇資料集]** 頁面上，選取 **[建立資料集]**，然後按 **[下一步]**。 **[選擇與資料來源的連接]** 頁面隨即開啟。  
  
2.  按一下 **[新增]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
3.  在 **[名稱]** 中輸入 **Online and Reseller Sales Detail** 做為資料來源的名稱。  
  
4.  在 **[選取連接類型]** 中，選取 **[Microsoft SQL Server Analysis Services]**，然後按一下 **[建立]**。  
  
5.  在 **[資料來源]** 中，確認資料來源為 **[Microsoft SQL Server Analysis Services (AdomdClient)]**。  
  
6.  在 **[伺服器名稱]** 中，輸入安裝 Analysis Services 執行個體所在伺服器的名稱。  
  
7.  在 [選取或輸入資料庫名稱] 中，選取 [Contoso] Cube。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 確認 **[連接字串]** 包含下列語法：  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
     `<servername>` 是已安裝 Analysis Services 之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
10. 按一下 **[認證類型]**。  
  
    > [!NOTE]  
    >  根據如何設定資料來源的權限而定，您可能需要變更預設的驗證選項。 如需詳細資訊，請參閱[安全性 &#40;報表產生器&#41;](report-builder/security-report-builder.md)。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **[選擇與資料來源的連接]** 頁面隨即出現。  
  
12. 若要確認您能夠連接至資料來源，請按一下 **[測試連接]**。  
  
     **「成功建立連接」** 訊息就會出現。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. 按 [下一步] 。  
  
##  <a name="DMDXQuery"></a> 1b。 建立 MDX 查詢  
 在報表中，您可以使用擁有預先定義查詢的共用資料集，或是建立只在報表中使用的內嵌資料集。 在本教學課程中，您將建立內嵌資料集。  
  
#### <a name="to-create-query-filters"></a>若要建立查詢篩選  
  
1.  在 **[設計查詢]** 頁面的 [中繼資料] 窗格中，按一下 **(…)** 按鈕。  
  
2.  在 [選取 Cube] 對話方塊中，按一下 [Sales]，然後按一下 [確定]。  
  
    > [!TIP]  
    >  如果您不想要手動建立 MDX 查詢，請按一下![切換到設計模式](../analysis-services/media/rsqdicon-designmode.gif "切換到設計模式")圖示，將查詢設計工具切換到 [查詢] 模式，並將完成的 MDX 貼到查詢設計工具，然後繼續進行[建立資料集](#DSkip)中的步驟 6。  
  
    ```  
    SELECT NON EMPTY { [Measures].[Sales Amount], [Measures].[Sales Return Amount] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS * [Product].[Product Subcategory Name].[Product Subcategory Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
    ```  
  
3.  在 [量值群組] 窗格中，展開 Channel，然後將 Channel Name 拖曳到篩選窗格中的 [階層] 資料行。  
  
     維度名稱 Channel 就會自動新增至 [維度] 資料行。 請勿變更 **[維度]** 或 **[運算子]** 資料行。  
  
4.  若要開啟 **[篩選運算式]** 清單，按一下 **[篩選運算式]** 資料行。  
  
5.  在篩選運算式清單中，展開 **[所有通道]**，然後依序按一下 **[線上]**、 **[轉售商]** 和 **[確定]**。  
  
     此查詢現在包含一個僅內含下列通道的篩選：線上和轉售商。  
  
6.  展開 Sales Territory 維度，然後將 Sales Territory Group 拖曳至 [階層] 資料行 (在 **Channel Name** 底下)。  
  
7.  開啟 **[篩選運算式]** 清單，展開 **[所有銷售領域]**，按一下 **[北美洲]**，然後按一下 **[確定]**。  
  
     此查詢現在有一個僅包含 [北美洲] 銷售額的篩選。  
  
8.  在 [量值群組] 窗格中，展開 Date，然後將 Calendar Year 拖曳至篩選窗格中的 [階層] 資料行。  
  
     維度名稱 Date 就會自動新增至 [維度] 資料行。 請勿變更 **[維度]** 或 **[運算子]** 資料行。  
  
9. 若要開啟 **[篩選運算式]** 清單，按一下 **[篩選運算式]** 資料行。  
  
10. 在篩選運算式清單中，展開 **[所有日期]**，按一下 **[2009 年]**，然後按一下 **[確定]**。  
  
     此查詢現在包含一個僅內含 2009 年日曆年度的篩選。  
  
#### <a name="to-create-the-parameter"></a>若要建立參數  
  
1.  展開 Product 維度，然後將 Product Category Name 成員拖曳至 [階層] 資料行 (在 **Calendar Year** 底下)。  
  
2.  開啟 **[篩選運算式]** 清單，按一下 **[所有產品]**，然後按一下 **[確定]**。  
  
3.  按一下 **[參數]** 核取方塊。 此查詢現在包含參數 ProductProductCategoryName。  
  
    > [!NOTE]  
    >  此參數包含產品類別目錄的名稱。 當您按一下主報表中的產品類別目錄名稱時，系統會使用此參數將其名稱傳遞到鑽研報表。  
  
###  <a name="DSkip"></a> 若要建立資料集  
  
1.  從 Channel 維度中，將 Channel Name 拖曳至資料窗格。  
  
2.  從 Product 維度中，將 Product Category Name 拖曳到資料窗格，然後將其放置在 Channel Name 的右側。  
  
3.  從 Product 維度中，將 Product Subcategory Name 拖曳到資料窗格，然後將其放置在 Product Category Name 的右側。  
  
4.  在 [中繼資料] 窗格中，展開 [量值]，然後展開 Sales。  
  
5.  將 Sales Amount 量值拖曳到資料窗格中，然後將其放置到 Product Subcategory Name 的右側。  
  
6.  在查詢設計工具工具列上，按一下 **[執行 (!)]**。  
  
7.  按 [下一步] 。  
  
##  <a name="DLayout"></a> 1 c。 將資料組織為群組  
 當您選取將資料分組的欄位時，會設計包含資料列和資料行的矩陣，以顯示詳細資料和彙總資料。  
  
#### <a name="to-organize-data-into-groups"></a>若要將資料組織為群組  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  在 [排列欄位] 頁面上，將 Product_Subcategory_Name 拖曳至 [資料列群組]。  
  
    > [!NOTE]  
    >  名稱中的空格會以底線 (_) 取代。 例如，Product Category Name 是 Product_Category_Name。  
  
3.  將 Channel_Name 拖曳至 [資料行群組]。  
  
4.  將 Sales_Amount 拖曳至 [值]。  
  
     Sum 函數 (數值欄位的預設彙總) 會自動彙總 Sales_Amount。 值為 `[Sum(Sales_Amount)]`。  
  
     若要檢視其他可用的彙總函式，開啟下拉式清單 (不要變更彙總函式)。  
  
5.  將 Sales_Return_Amount 拖曳至 [值]，並將其放置在 `[Sum(Sales_Amount)]` 之下。  
  
     步驟 4 和步驟 5 指定了矩陣中要顯示的資料。  
  
6.  按 [下一步] 。  
  
##  <a name="DTotals"></a> 1d。 加入小計和總計  
 建立群組之後，您可以加入並格式化要顯示欄位彙總值的資料列。 您也可以選擇要顯示所有資料，或是讓使用者以互動方式展開和摺疊分組資料。  
  
#### <a name="to-add-subtotals-and-totals"></a>加入小計和總計  
  
1.  在 **[選擇配置]** 頁面的 **[選項]** 下方，確定已選取 **[顯示小計和總計]** 。  
  
     精靈的 [預覽] 窗格會顯示含有四個資料列的矩陣。  
  
2.  按 [下一步] 。  
  
##  <a name="DStyle"></a> 1e。 選擇樣式  
 樣式會指定字型樣式、色彩集和框線樣式。  
  
#### <a name="to-specify-a-style"></a>若要指定樣式  
  
1.  在 **[選擇樣式]** 頁面的 [樣式] 窗格中，選取 [石板]。  
  
2.  按一下 **[完成]**。  
  
     資料表會加入至設計介面。  
  
3.  若要預覽報表，按一下 **[執行 (!)]**。  
  
##  <a name="DFormat"></a> 2.將資料格式化為貨幣  
 將貨幣格式套用到鑽研報表中的銷售量欄位。  
  
#### <a name="to-format-data-as-currency"></a>若要將資料格式化為貨幣  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  若要一次選取並格式化多個資料格，按下 Ctrl 鍵，然後選取包含數值銷售資料的資料格。  
  
3.  在 **[主資料夾]** 索引標籤的 **[數值]** 群組中，按一下 **[貨幣]**。  
  
##  <a name="DSparkline"></a> 3.加入資料行以便在走勢圖中顯示銷售值  
 報表會顯示走勢圖中的值，而不會將銷售額與銷售報酬顯示為貨幣值。  
  
#### <a name="to-add-sparklines-to-columns"></a>若要將走勢圖加入至資料行  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  在矩陣的 [總計] 群組中，以滑鼠右鍵按一下 **[銷售量]** 資料行，按一下 **[插入資料行]**，然後按一下 **[右方]**。  
  
     空白資料行就會加入至 **[銷售量]** 的右方。  
  
3.  在功能區上，按一下 [矩形]，然後按一下 [Product_Subcategory] 資料列群組中 `[Sum(Sales_Amount)]` 資料格右側的空資料格。  
  
4.  在功能區上，按一下 **[走勢圖]** 圖示，然後按一下加入矩形的資料格。  
  
5.  在 **[選取走勢圖類型]** 對話方塊中，確認已選取 **[資料行]** 類型。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  以滑鼠右鍵按一下走勢圖。  
  
8.  在 [圖表資料] 窗格中，按一下**新增欄位**圖示，然後按一下 [Sales_Amount]。  
  
9. 以滑鼠右鍵按一下 `Sales_Return_Amount` 資料行，然後將資料行加入至該資料行的右側。  
  
10. 重複步驟 2 至 6。  
  
11. 以滑鼠右鍵按一下走勢圖。  
  
12. 在 [圖表資料] 窗格中，按一下**新增欄位** 圖示，然後按一下 [Sales_Return_Amount]。  
  
13. 若要預覽報表，按一下 **[執行]**。  
  
##  <a name="DReportTitle"></a> 4.加入具有產品類別目錄名稱的報表標題  
 報表標題會出現在報表的頂端。 您可以將報表標題放置在報表頁首，如果報表不使用報表頁首，則可以放置在報表主體頂端的文字方塊中。 在本教學課程中，您將使用自動放置在報表主體頂端的文字方塊。  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
3.  輸入 **Sales and Returns for Category:**。  
  
4.  以滑鼠右鍵按一下，然後按一下 **[建立預留位置]**。  
  
5.  按一下 **[值]** 清單右側的 **(fx)** 按鈕。  
  
6.  在 **[運算式]** 對話方塊的 [類別目錄] 窗格中，按一下 **[資料集]**，然後在 **[值]** 清單中，按兩下 `First(Product_Category_Name)`。  
  
     **[運算式]** 方塊包含下列運算式：  
  
    ```  
    =First(Fields!Product_Category_Name.Value, "DataSet1")  
    ```  
  
7.  若要預覽報表，按一下 **[執行]**。  
  
 報表標題包含第一個產品類別目錄的名稱。 稍後，在您當做鑽研報表執行此報表之後，產品類別目錄名稱將會動態變更，以反映在主報表中按下之產品類別目錄的名稱。  
  
##  <a name="DParameter"></a> 5.更新參數屬性  
 參數預設是可見的，但不適合這個報表。 您將要更新鑽研報表的參數屬性。  
  
#### <a name="to-hide-a-parameter"></a>若要隱藏參數  
  
1.  在 [報表資料] 窗格中，展開 **[參數]**。  
  
2.  以滑鼠右鍵按一下\@ProductProductCategoryName，然後按一下**參數屬性**。  
  
    > [!NOTE]  
    >  \@名稱旁邊的字元表示這是否為參數。  
  
3.  在 **[一般]** 索引標籤上，按一下 **[隱藏]**。  
  
4.  在 **[提示]** 方塊中，輸入 **Product Category**。  
  
    > [!NOTE]  
    >  參數是隱藏的，因此絕不會使用這個提示。  
  
5.  或者，按一下 **[可用的值]** 和 **[預設值]** ，然後檢閱其選項。 請不要變更這些索引標籤上的任何選項。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="DSave"></a> 6.將報表儲存至 SharePoint 文件庫  
 您可以將報表儲存至 SharePoint 文件庫、報表伺服器或您的電腦上。 如果將報表儲存到您的電腦，就無法使用數個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如報表組件和子報表。 在本教學課程中，您會將報表儲存至 SharePoint 程式庫。  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  在報表產生器的按鈕中，按一下 **[儲存]**。 **[另存為報表]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果您重新儲存報表，報表會自動重新儲存到之前的位置。 若要變更位置，使用 **[另存新檔]** 選項。  
  
2.  若要顯示最近使用過的報表伺服器和 SharePoint 網站清單，按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之 SharePoint 網站的名稱。  
  
     SharePoint 文件庫的 URL 具有下列語法：  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
4.  按一下 **[儲存]**。  
  
     **[最近使用的網站和伺服器]** 會列出 SharePoint 網站上的文件庫。  
  
5.  導覽到您將儲存報表的文件庫。  
  
6.  在 **[名稱]** 方塊中，將預設名稱取代為 **ResellerVSOnlineDrillthrough**。  
  
    > [!NOTE]  
    >  您會將主報表儲存至相同的位置。 如果您想要將主報表和鑽研報表儲存到不同的網站或文件庫，必須在主報表中更新 **[移至報表]** 動作的路徑。  
  
7.  按一下 **[儲存]**。  
  
##  <a name="MMatrixAndDataset"></a> 1.從資料表或矩陣精靈建立新報表  
 從 **[使用者入門]** 對話方塊中，使用 **[資料表或矩陣精靈]** 建立矩陣報表。  
  
#### <a name="to-create-a-new-report"></a>建立新的報表  
  
1.  按一下 **開始**，指向**程式**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**，然後按一下**報表產生器**。  
  
2.  在 **[使用者入門]** 對話方塊中，確認已選取 **[新增報表]** ，然後按一下 **[資料表或矩陣精靈]**。  
  
##  <a name="MConnection"></a> 1a。 指定資料連接  
 您會將內嵌的資料來源儲存到主報表。  
  
#### <a name="to-create-an-embedded-data-source"></a>建立內嵌資料來源  
  
1.  在 **[選擇資料集]** 頁面上，選取 **[建立資料集]**，然後按 **[下一步]**。  
  
2.  按一下 **[新增]**。  
  
3.  在 **[名稱]** 中輸入 **Online and Reseller Sales Main** 做為資料來源的名稱。  
  
4.  在 **[選取連接類型]** 中，選取 **[Microsoft SQL Server Analysis Services]**，然後按一下 **[建立]**。  
  
5.  在 **[資料來源]** 中，確認資料來源為 **[Microsoft SQL Server Analysis Services (AdomdClient)]**。  
  
6.  在 **[伺服器名稱]** 中，輸入安裝 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體所在伺服器的名稱。  
  
7.  在 [選取或輸入資料庫名稱] 中，選取 [Contoso] Cube。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 確認 **[連接字串]** 包含下列語法：  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
10. 按一下 **[認證類型]**。  
  
     根據如何設定資料來源的權限而定，您可能需要變更預設的驗證。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 若要確認您能夠連接至資料來源，請按一下 **[測試連接]**。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. 按 [下一步] 。  
  
##  <a name="MMDXQuery"></a> 1b。 建立 MDX 查詢  
 接著，建立內嵌的資料集。 若要這樣做，您將使用查詢設計工具建立篩選、參數、導出成員，以及資料集本身。  
  
#### <a name="to-create-query-filters"></a>若要建立查詢篩選  
  
1.  在 **[設計查詢]** 頁面的 [中繼資料] 窗格中，按一下 Cube 區段中的省略符號 **(...)**。  
  
2.  在 [選取 Cube] 對話方塊中，按一下 [Sales]，然後按一下 [確定]。  
  
    > [!TIP]  
    >  如果您不想要手動建立 MDX 查詢，請按一下![切換到設計模式](../analysis-services/media/rsqdicon-designmode.gif "切換到設計模式") 示，將查詢設計工具切換到 [查詢] 模式，並將完成的 MDX 貼到查詢設計工具，然後繼續進行[建立資料集](#MSkip)中的步驟 5。  
  
    ```  
    WITH MEMBER [Measures].[Net QTY] AS [Measures].[Sales Quantity] -[Measures].[Sales Return Quantity] MEMBER [Measures].[Net Sales] AS [Measures].[Sales Amount] - [Measures].[Sales Return Amount] SELECT NON EMPTY { [Measures].[Net QTY], [Measures].[Net Sales] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGSQuery text: Code.  
    ```  
  
3.  在 [量值群組] 窗格中，展開 Channel，然後將 Channel Name 拖曳到篩選窗格中的 [階層] 資料行。  
  
     維度名稱 Channel 就會自動新增至 [維度] 資料行。 請勿變更 **[維度]** 或 **[運算子]** 資料行。  
  
4.  若要開啟 **[篩選運算式]** 清單，按一下 **[篩選運算式]** 資料行。  
  
5.  在篩選運算式清單中，展開 **[所有通道]**，然後依序按一下 **[線上]** 、 **[轉售商]** 和 **[確定]**。  
  
     此查詢現在包含一個僅內含下列通道的篩選：線上和轉售商。  
  
6.  展開 Sales Territory 維度，然後將 Sales Territory Group 拖曳至 [階層] 資料行 (在 **Channel Name** 底下)。  
  
7.  開啟 **[篩選運算式]** 清單，展開 **[所有銷售領域]**，按一下 **[北美洲]**，然後按一下 **[確定]**。  
  
     此查詢現在有一個僅包含 [北美洲] 銷售額的篩選。  
  
8.  在 [量值群組] 窗格中，展開 Date，然後將 Calendar Year 拖曳至篩選窗格中的 [階層] 資料行。  
  
     維度名稱 Date 就會自動新增至 [維度] 資料行。 請勿變更 **[維度]** 或 **[運算子]** 資料行。  
  
9. 若要開啟 **[篩選運算式]** 清單，按一下 **[篩選運算式]** 資料行。  
  
10. 在篩選運算式清單中，展開 **[所有日期]**，按一下 **[2009 年]**，然後按一下 **[確定]**。  
  
     此查詢現在包含一個僅內含 2009 年日曆年度的篩選。  
  
#### <a name="to-create-the-parameter"></a>若要建立參數  
  
1.  展開 Product 維度，然後將 Product Category Name 拖曳至 [階層] 資料行 (在 **Sales Territory Group** 底下)。  
  
2.  開啟 **[篩選運算式]** 清單，按一下 **[所有產品]**，然後按一下 **[確定]**。  
  
3.  按一下 **[參數]** 核取方塊。 此查詢現在包含參數 ProductProductCategoryName。  
  
#### <a name="to-create-calculated-members"></a>若要建立導出成員  
  
1.  將游標放在 [導出成員] 窗格內部，按一下滑鼠右鍵，然後按一下 **[新增導出成員]**。  
  
2.  在 [中繼資料] 窗格中，展開 [量值]，然後展開 Sales。  
  
3.  將 Sales Quantity 量值拖曳至 [運算式] 方塊，並鍵入減號字元 (-)，然後將 Sales Return Quantity 量值拖曳至 [運算式] 方塊，將其放置在減號字元後面。  
  
     下列程式碼顯示運算式：  
  
    ```  
    [Measures].[Sales Quantity] - [Measures].[Sales Return Quantity]  
    ```  
  
4.  在 [名稱] 中，輸入 **Net QTY**，然後按一下 **[確定]**。  
  
     [導出成員] 窗格會列出 **Net QTY** 導出成員。  
  
5.  以滑鼠右鍵按一下 **[導出成員]**，然後按一下 **[新增導出成員]**。  
  
6.  在 [中繼資料] 窗格中，展開 [量值]，然後展開 Sales。  
  
7.  將 Sales Amount 量值拖曳至 [運算式] 方塊，並鍵入減號字元 (-)，然後將 Sales Return Amount 量值拖曳至 [運算式] 方塊，將其放置在減號字元後面。  
  
     下列程式碼顯示運算式：  
  
    ```  
    [Measures].[Sales Amount] - [Measures].[Sales Return Amount]  
    ```  
  
8.  在 **[名稱]** 方塊中輸入  **Net Sales**，然後按一下 **[確定]**。[導出成員] 窗格會列出 **Net Sales** 導出成員。  
  
###  <a name="MSkip"></a> 若要建立資料集  
  
1.  從 Channel 維度中，將 Channel Name 拖曳至資料窗格。  
  
2.  從 Product 維度中，將 Product Category Name 拖曳到資料窗格，然後將其放置在 Channel Name 的右側。  
  
3.  從 [導出成員] 中，將 `Net QTY` 拖曳至資料窗格，然後將其放置在 Product Category Name 的右側。  
  
4.  從 [導出成員] 中，將 Net Sales 拖曳到資料窗格，然後將其放置在 `Net QTY`的右側。  
  
5.  在查詢設計工具工具列上，按一下 **[執行 (!)]**。  
  
     檢閱查詢結果集。  
  
6.  按 [下一步] 。  
  
##  <a name="MLayout"></a> 1 c。 將資料組織為群組  
 當您選取將資料分組的欄位時，會設計包含資料列和資料行的矩陣，以顯示詳細資料和彙總資料。  
  
#### <a name="to-organize-data-into-groups"></a>若要將資料組織為群組  
  
1.  在 [排列欄位] 頁面上，將 Product_Category_Name 拖曳至 [資料列群組]。  
  
2.  將 Channel_Name 拖曳至 [資料行群組]。  
  
3.  將 `Net_QTY` 拖曳至 **[值]**。  
  
     `Net_QTY` 。 值為 `[Sum(Net_QTY)]`。  
  
     若要檢視其他可用的彙總函式，開啟下拉式清單。 請不要變更彙總函式。  
  
4.  將 `Net_Sales_Return` 拖曳至 **[值]** ，並將其放置在 `[Sum(Net_QTY)]`之下。  
  
     步驟 3 和步驟 4 指定了矩陣中要顯示的資料。  
  
##  <a name="MTotals"></a> 1d。 加入小計和總計  
 您可以在報表中顯示小計和總計。 主報表中的資料會顯示為指標，而且您將會在完成精靈後移除總計。  
  
#### <a name="to-add-subtotals-and-grand-totals"></a>若要加入小計和總計  
  
1.  在 **[選擇配置]** 頁面的 **[選項]** 下方，確定已選取 **[顯示小計和總計]** 。  
  
     精靈的 [預覽] 窗格會顯示含有四個資料列的矩陣。  當您執行報表時，每個資料列都會以下列方式顯示：第一個資料列是資料行群組、第二個資料列包含資料行標題、第三個資料列包含產品類別目錄資料 (`[Sum(Net_ QTY)]` 和 `[Sum(Net_Sales)]`，而第四個資料列包含總計。  
  
2.  按 [下一步] 。  
  
##  <a name="MStyle"></a> 1e。 選擇樣式  
 將 [石板] 樣式套用到報表。 這是鑽研報表使用的相同樣式。  
  
#### <a name="to-specify-a-style"></a>若要指定樣式  
  
1.  在 **[選擇樣式]** 頁面的 [樣式] 窗格中，選取 [石板]。  
  
2.  按一下 **[完成]**。  
  
3.  若要預覽報表，按一下 **[執行]**。  
  
##  <a name="MGrandTotal"></a> 2.移除總計資料列  
 資料值會顯示為指標狀態，包括資料行群組總計。 移除顯示總計的資料列。  
  
#### <a name="to-remove-the-grand-total-row"></a>若要移除總計資料列  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  按一下 [總計] 資料列 (矩陣中的最後一個資料列)，按一下滑鼠右鍵，然後按一下 **[刪除資料列]**。  
  
3.  若要預覽報表，按一下 **[執行]**。  
  
##  <a name="MDrillthrough"></a> 3.設定用於鑽研的文字方塊動作  
 若要啟用鑽研，請在主報表的文字方塊上指定動作。  
  
#### <a name="to-enable-an-action"></a>若要啟用動作  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  以滑鼠右鍵按一下包含 Product_Category_Name 的資料格，然後按一下 [文字方塊屬性]。  
  
3.  按一下 **[動作]** 索引標籤。  
  
4.  選取 **[移至報表]**。  
  
5.  在 **[指定報表]** 中，按一下 **[瀏覽]**，然後找出名稱為 ResellerVSOnlineDrillthrough 的鑽研報表。  
  
6.  若要加入參數以執行鑽研報表，按一下 **[加入]**。  
  
7.  在 [名稱] 清單中，選取 ProductProductCategoryName。  
  
8.  在 **[值]** 中，輸入 `[Product_Category_Name.UniqueName]`。  
  
     Product_Category_Name 是資料集中的欄位。  
  
    > [!IMPORTANT]  
    >  您必須加入 `UniqueName` 屬性，因為鑽研動作需要唯一的值。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-format-the-drillthrough-field"></a>若要格式化鑽研欄位  
  
1.  以滑鼠右鍵按一下包含 `Product_Category_Name`的資料格，然後按一下 **[文字方塊屬性]**。  
  
2.  按一下 **[字型]** 索引標籤。  
  
3.  在 **[效果]** 清單中，選取 **[底線]**。  
  
4.  在 **[色彩]** 清單中，選取 **[藍色]**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  若要預覽報表，按一下 **[執行]**。  
  
 產品類別目錄名稱會採用一般連結的格式 (藍色和底線)。  
  
##  <a name="MIndicators"></a> 4.以指標取代數值  
 使用指標顯示 [線上] 與 [轉售商] 通道之數量與銷售額的狀態。  
  
#### <a name="to-add-an-indicator-for-net-qty-values"></a>若要加入 Net QTY 值的指標  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  在功能區上，按一下 **[矩形]** 圖示，然後在 `[Sum(Net QTY)]` 資料行群組的 `[Product_Category_Name]` 資料列群組中，按一下 `Channel_Name` 資料格。  
  
3.  在功能區上，按一下 **[指標]** 圖示，然後按一下矩形內部。 **[選取指標類型]** 對話方塊隨即開啟，其中已選取 **[方向性]** 指標。  
  
4.  按一下 **[三記號]** 類型，然後按一下 **[確定]**。  
  
5.  以滑鼠右鍵按一下指標，然後在 [量測計資料] 窗格中，按一下 **[(未指定)]** 旁邊的向下鍵。 選取 `Net_QTY`。  
  
6.  在 `[Sum(Net QTY)]` [總計] `[Product_Category_Name]` 內，針對 **資料列群組中的**資料格，重複步驟 2 到 5。  
  
#### <a name="to-add-an-indicator-for-net-sales-values"></a>若要加入 Net Sales 值的指標  
  
1.  在功能區上，按一下 **[矩形]** 圖示，然後在 `[Sum(Net_Sales)]` 資料行群組的 `[Product_Category_Name]` 資料列群組中，按一下 `Channel_Name` 資料格內部。  
  
2.  在功能區上，按一下 **[指標]** 圖示，然後按一下矩形內部。  
  
3.  按一下 **[三記號]** 類型，然後按一下 **[確定]**。  
  
4.  以滑鼠右鍵按一下指標，然後在 [量測計資料] 窗格中，按一下 **[(未指定)]** 旁邊的向下鍵。 選取 `Net_Sales`。  
  
5.  在 `[Sum(Net_Sales)]` [總計] `[Product_Category_Name]` 內，針對 **資料列群組中的**資料格，重複步驟 1 到 4。  
  
6.  若要預覽報表，按一下 **[執行]**。  
  
##  <a name="MParameter"></a> 5.更新參數屬性  
 參數預設是可見的，但不適合這個報表。 您將更新參數屬性，讓參數變成內部的。  
  
#### <a name="to-make-the-parameter-internal"></a>若要將參數變成內部的  
  
1.  在 [報表資料] 窗格中，展開 **[參數]**。  
  
2.  以滑鼠右鍵按一下 `@ProductProductCategoryName,` ，然後按一下 **[參數屬性]**。  
  
3.  在 **[一般]** 索引標籤上，按一下 **[內部]**。  
  
4.  或者，按一下 **[可用的值]** 和 **[預設值]** 索引標籤，然後檢閱其選項。 請不要變更這些索引標籤上的任何選項。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="MTitle"></a> 6.加入報表標題  
 將標題加入到主報表中  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  類型 **2009 Product Category Sales:Online and Reseller Category:**。  
  
3.  選取您輸入的文字。  
  
4.  在功能區的 **[主資料夾]** 索引標籤上，選取 [字型] 群組中的 **[Times New Roman]** 字型、 **[16pt]** 大小，以及 **[粗體]** 和 **[斜體]** 樣式。  
  
5.  若要預覽報表，按一下 **[執行]**。  
  
##  <a name="MSave"></a> 7.將主報表儲存至 SharePoint 文件庫  
 將主報表儲存至 SharePoint 文件庫。  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  若要切換成 [設計] 檢視，按一下 **[設計]**。  
  
2.  在報表產生器的按鈕中，按一下 **[儲存]**。  
  
3.  或者，若要顯示最近使用過的報表伺服器和 SharePoint 網站清單，按一下 **[最近使用的網站和伺服器]**。  
  
4.  選取或輸入您有權儲存報表之 SharePoint 網站的名稱。 SharePoint 文件庫的 URL 具有下列語法：  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
5.  導覽到您要儲存報表的文件庫。  
  
6.  在 **[名稱]** 中，將預設名稱取代成 **ResellerVSOnlineMain**。  
  
    > [!IMPORTANT]  
    >  將主報表儲存到儲存鑽研報表的相同位置。 若要將主報表和鑽研報表儲存到不同的網站或文件庫，請確認主報表中的 **[移至報表]** 動作指向鑽研報表的正確路徑。  
  
7.  按一下 **[儲存]**。  
  
##  <a name="MRunReports"></a> 8。執行主報表和鑽研報表  
 執行主報表，然後按一下產品類別目錄資料行中的值以執行鑽研報表。  
  
#### <a name="to-run-the-reports"></a>若要執行報表  
  
1.  開啟儲存報表的 SharePoint 文件庫。  
  
2.  按兩下 ResellerVSOnlineMain。  
  
     報表就會執行並顯示產品類別目錄銷售資訊。  
  
3.  在包含產品類別目錄名稱的資料行中，按一下 **[Games and Toys]** 連結。  
  
     鑽研報表便會執行，並只顯示 Games and Toys 產品類別目錄的值。  
  
4.  若要返回主報表，按一下 Internet Explorer 的 [上一頁] 按鈕。  
  
5.  或者，按一下其他產品類別目錄的名稱以進行探索。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)  
  
  
