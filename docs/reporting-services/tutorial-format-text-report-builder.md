---
title: "教學課程： 格式化文字 （報表產生器） |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: cfbe1001a049466af839363db29156df6b972556
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---

# <a name="tutorial-format-text-report-builder"></a>教學課程：格式化文字 (報表產生器)

在本教學課程中，您可以在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分頁報表中練習以各種不同的方式格式化文字。 您可以實驗不同的格式。 

使用資料來源和資料集設定空白報表之後，您可以挑選想要瀏覽的格式。 下圖顯示報表，與您將要建立的報表相似。  
  
![report-build-format-report](../reporting-services/media/report-build-format-report.png) 
  
您在某個步驟故意出錯，所以知道錯誤的原因是什麼。 接著您要更正錯誤以便達到想要的效果。  
    
完成這個教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="CreateReport"></a>建立含資料來源和資料集的空白報表  
  
### <a name="to-create-a-blank-report"></a>建立空白報表  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果您看不到 [新報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
 
2.  在 **[使用者入門]** 對話方塊的左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[空白報表]**。  
  
### <a name="to-create-a-data-source"></a>建立資料來源  
  
1.  在 [報表資料] 窗格中，按一下 [新增] > [資料來源]。  

    如果您看不到 [報表資料] 窗格，請核取 [檢視] 索引標籤上的 [報表資料]。
  
2.  在 [名稱] 方塊中，輸入：**TextDataSource**  
  
3.  按一下 **[使用內嵌於報表中的連接]**。  
  
4.  確認連接類型為 Microsoft SQL Server，然後在**連接字串**方塊中，輸入：`Data Source = <servername>`  
  
    > [!NOTE]  
    > `<servername>`運算式 (例如 Report001) 會指定已安裝 SQL Server Database Engine 執行個體的電腦名稱。 本教學課程無須任何特定資料。您只需要 SQL Server 資料庫的連接。 如果您已有資料來源連接列於 [資料來源連接] 底下，就可以選取該連接並移至下一個程序「建立資料集」。 如需詳細資訊，請參閱[取得資料連接的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-dataset"></a>建立資料集  
  
1.  在 [報表資料] 窗格中，按一下 [新增] > [資料集]。  
  
2.  確認資料來源為 **TextDataSource**。  
  
3.  在 [名稱] 方塊中，輸入：**TextDataset**。  
  
4.  確認已選取 **[文字]** 查詢類型，然後按一下 **[查詢設計工具]**。  
  
5.  按一下 **[當成文字編輯]**。  
  
6.  將下列查詢貼入查詢窗格中：  

    > [!NOTE]  
    > 在本教學課程中，查詢已經包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  按一下 [執行] (**!**) 來執行查詢。  
  
    查詢結果會成為可供報表顯示的資料。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="AddField"></a>將欄位加入至報表設計介面  
如果希望擷取自資料集的欄位出現在報表中，您可能會不加思索地直接將欄位拖曳到設計介面。 此練習將點出為何這樣做無效，以及應該改用的方法。  
  
### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>將欄位加入至報表 (會得到錯誤的結果)  
  
1.  從 [報表資料] 窗格，將 [FullName] 欄位拖曳到設計介面。  
  
    報表產生器會建立一個內有運算式 (以 `<Expr>` 表示) 的文字方塊。  
  
2.  按一下 **[執行]**。  
  
    您只會看到一筆記錄 **Fernando Ross**，這是查詢中依字母為第一順位的記錄。 欄位並未重複成顯示該欄位內的其他記錄。  
  
3.  按一下 **[設計]** 返回 [設計] 檢視。  
  
4.  選取文字方塊中的運算式 `<Expr>`。  
  
5.  在 [屬性] 窗格中，您會看到 [Value] 屬性如下 (若未看見 [屬性] 窗格，請核取 [檢視] 索引標籤上的 [屬性])：  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
    `First` 函數是設計成僅擷取欄位內的第一個值，而其目的也已達到。  
  
    直接將欄位拖曳到設計介面會建立文字方塊。 文字方塊本身並非資料區，所以不會顯示來自報表資料集的資料。 位於資料區 (例如資料表、矩陣和清單) 內的文字方塊才會顯示資料。  
  
6.  選取文字方塊 (如果您已選取運算式，請按 ESC 鍵選取文字方塊)，然後按下 DELETE 鍵。  
  
### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>將欄位加入至報表 (會得到正確的結果)  
  
1.  在功能區的 [插入] 索引標籤上，按一下 [資料區域] 區域內的 [清單]。 按一下設計介面，然後進行拖曳以建立寬約 2 英吋且高約 1 英吋的方塊。  
  
2.  從 [報表資料] 窗格，將 [FullName] 欄位拖曳到清單方塊中。  
  
    這回報表產生器會建立一個內有運算式 `[FullName]` 的文字方塊。  
  
3.  按一下 **[執行]**。  
  
    請注意，此時方塊已經重複成顯示查詢中的所有記錄。  
  
4.  按一下 **[設計]** 返回 [設計] 檢視。  
  
5.  選取文字方塊中的運算式。  
  
6.  在 [屬性] 窗格中，您會看到 [Value] 屬性如下：  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
    透過將文字方塊拖曳到清單資料區，就可以顯示資料集內該欄位中的資料。  
  
7.  選取清單方塊，然後按下 DELETE 鍵。  
  
## <a name="AddTable"></a>將資料表加入至報表設計介面  
建立這個資料表，以便能夠在其中放置超連結和旋轉的文字。   
  
1.  在 [插入] 索引標籤 > [資料表] > [資料表精靈]。  
  
2.  在 [新增資料表或矩陣精靈] 的 [選擇資料集] 頁面上，按一下 [選擇這份報表中現有的資料集或共用資料集] > [TextDataset (在此報表中)] > [下一步]。  
  
3.  在 [排列欄位] 頁面上，將 [Territory]、[LinkText] 和 [Product] 欄位拖曳到 [資料列群組]，並將 [Sales] 欄位拖曳到 [值]，然後按一下 [下一步]。  

    ![report-builder-text-arrange-fields](../reporting-services/media/report-builder-text-arrange-fields.png)
  
4.  在 [選擇配置] 頁面上，取消選取 [展開或摺疊群組] 核取方塊以便可看見整個資料表，然後按一下 [下一步]。 
  
5.  按一下 **[完成]**。  
  
6.  按一下 **[執行]**。  
  
    資料表看起來似乎沒問題，不過卻有兩個總計資料列。 [LinkText] 資料行不需要 [總計] 資料列。  
    
    ![report-builder-format-2-totals](../reporting-services/media/report-builder-format-2-totals.png)
  
8.  按一下 **[設計]** 返回 [設計] 檢視。  
  
9. 選取 [LinkText] 資料行中的 [Total] 資料格，然後按住 SHIFT 鍵並選取其右邊的兩個資料格：[Product] 資料行中的空白資料格，以及 [Sales] 資料行中的 `[Sum(Sales)]` 資料格。  
  
11. 在選取這三個資料格之後，以滑鼠右鍵按一下其中一個資料格，然後按一下 [刪除資料列]。  

    ![report-builder-format-delete-rows](../reporting-services/media/report-builder-format-delete-rows.png)
  
12. 按一下 **[執行]**。  

    現有，它只有一個 [總計] 資料列。
    
    ![report-builder-format-one-total](../reporting-services/media/report-builder-format-one-total.png)
  
## <a name="AddHyperlink"></a>加入超連結至報表  
在本節中，您要加入超連結指向上一節資料表中的文字。  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下含有 `[LinkText]` 的資料格，然後按一下 [文字方塊屬性]。  
  
3.  在 [動作] 索引標籤上，按一下 [移至 URL]。  
  
5.  在 [選取 URL] 方塊中，按一下 [URL]，然後按一下 [確定]。  
  
6.  請注意，文字看起來並無任何改變。 您需要進行調整使其彷彿連結文字。  
  
7.  選取 [`[LinkText]`]。  
  
8.  在 [主資料夾] 索引標籤 > [字型] 上，選取 [底線]，並將 [色彩] 變更為 [藍色]。  
  
9. 按一下 **[執行]**。  
  
    文字現在看起來就像一個連結。  
    
    ![report-builder-format-hyperlink](../reporting-services/media/report-builder-format-hyperlink.png)
  
10. 按一下該連結。 如果您的電腦已連接至網際網路，瀏覽器將會開啟報表產生器說明主題。  
  
## <a name="RotateText"></a>旋轉報表中的文字  
在本節中，您要旋轉前幾節資料表中的部分文字。  
 
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  按一下包含下列項目的資料格： `[Territory].`  
  
3.  在 [主資料夾] 索引標籤的 [字型] 區段中，按一下 [粗體] 按鈕。  
  
4.  如果 [屬性] 窗格並未開啟，請選取 [檢視] 索引標籤上的 [屬性] 核取方塊。  
  
5.  在 [屬性] 窗格中，找出 WritingMode 屬性，並將它從 [預設] 變更為 [Rotate270]。  
 
    > [!NOTE]  
    > 當 [屬性] 窗格中的屬性組織成一些類別目錄時，WritingMode 位於 [當地語系化] 類別目錄中。 請確定您已選取資料格，而不是文字。 WritingMode 是文字方塊的屬性，並非文字的屬性。  

    ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
   
6.  在 [主資料夾] 索引標籤 > [段落] 區段上，選取 [中間] 和 [中心]，將文字水平且垂直地定位於資料格中央。  
  
8.  按一下 [執行] (**!**)。  
  
如今 `[Territory]` 資料格中的文字已呈垂直方向，從資料格底部往上書寫。  

![report-builder-format-rotate-270](../reporting-services/media/report-builder-format-rotate-270.png)

## <a name="FormatCurrency"></a>將貨幣格式化  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  按一下含有 `[Sum(Sales)]` 的最上方資料表資料格，然後按住 SHIFT 鍵，再按一下含有 `[Sum(Sales)]` 的底部資料表資料格。  
  
3.  在 [主資料夾] 索引標籤 > [數值] 群組 > [貨幣] 按鈕。  
  
4.  (選擇性)     如果您的地區設定為 [英文 (美國)]，則預設範例文字會是 [**$12,345.00**]。 如果您看不到範例貨幣值，請按一下 [數值] 群組中的 [預留位置樣式] > [範例值]。  

    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
  
5.  (選擇性) 在 [主資料夾] 索引標籤的 [數字] 群組中，按兩次 [減少小數位數] 按鈕以顯示沒有分的貨幣數字。  
  
6.  按一下 [執行] (**!**) 預覽報表。  
  
報表如今已顯示格式化的資料，更容易閱讀。  

![report-build-format-report](../reporting-services/media/report-build-format-report.png)
    
## <a name="FormatHTML"></a>顯示 HTML 格式的文字  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  在 [插入] 索引標籤上，按一下 [文字方塊]，然後按一下設計介面並進行拖曳，以在資料表底下建立大約寬 4 英吋且高 3 英吋的文字方塊。  
  
3.  複製以下文字並將其貼入文字方塊中：  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  拖曳文字方塊的下邊緣，以納入所有文字。 您會注意到設計介面會隨著您拖曳而變得較大。

5. 選取文字方塊中的所有文字。  
  
5.  以滑鼠右鍵按一下所有選取的文字，然後按一下 [文字屬性]。  
  
    因為這是文字的屬性，而非文字方塊屬性，您可以在單一文字方塊中混雜純文字與使用 HTML 標記做為樣式的文字。  
  
6.  在 [一般] 索引標籤上，按一下 [標記類型] 底下的 [HTML - 將 HTML 標記解譯為樣式]。  
  
7.  按一下 **[確定]**。  
  
8.  按一下 [執行] (**!**) 預覽報表。  
  
文字方塊中的文字會顯示成標頭、段落和項目符號清單。  
  
![report-builder-format-html](../reporting-services/media/report-builder-format-html.png)

## <a name="Save"></a>儲存報表  
您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。  
  
本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
    「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 [名稱] 中，將預設名稱取代為您選擇的名稱。

5.  按一下 **[儲存]**。  
  
報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[桌面]**、 **[我的文件]**或 **[我的電腦]**，然後瀏覽到您要儲存報表的資料夾。  
  
3.  在 [名稱] 中，將預設名稱取代為您選擇的名稱。 
  
4.  按一下 **[儲存]**。  

## <a name="next-steps"></a>後續步驟

在報表產生器中，格式化文字的方法有好幾種。 [教學課程： 建立自由格式報表](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)包含更多的範例。  

[報表產生器教學課程](../reporting-services/report-builder-tutorials.md)  
[格式化報表項目](../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
[SQL Server 2016 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
