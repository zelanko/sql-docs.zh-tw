---
title: 教學課程：將文字格式化 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dc58232ed3025063fb329392b58895ed667465f4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098895"
---
# <a name="tutorial-format-text-report-builder"></a>教學課程：將文字格式化 (報表產生器)
  在本教學課程中，您將能練習以各種不同的方式格式化文字。 使用資料來源和資料集設定空白報表之後，您可以挑選想要探索的步驟來進行。  
  
 下圖顯示報表，與您將要建立的報表相似。  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 您在某個步驟故意出錯，所以知道錯誤的原因是什麼。 接著您要更正錯誤以便達到想要的效果。  
  
 本教學課程所建立的報表另有一個增強型版本，可從範例 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 報表產生器報表取得。 如需有關下載這個範例報表和其他人的詳細資訊，請參閱[報表產生器範例報表](https://go.microsoft.com/fwlink/?LinkId=184851)。  
  
##  <a name="BackToTop"></a> 您將了解  
  
### <a name="set-up-the-report"></a>設定報表  
 1. [建立空白的報表資料來源和資料集](#CreateReport)  
  
 2. [（不正確，然後正確），將欄位加入至報表設計介面](#AddField)  
  
 3. [將資料表加入至報表設計介面](#AddTable)  
  
### <a name="pick-and-choose"></a>隨意挑選  
 [將超連結加入至報表](#AddHyperlink)  
  
 [旋轉報表中的文字](#RotateText)  
  
 [顯示 HTML 格式的文字](#FormatHTML)  
  
 [將貨幣格式化](#FormatCurrency)  
  
 [儲存報表](#Save)  
  
 估計的時間才能完成本教學課程：20 分鐘的時間。  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="CreateReport"></a> 建立空白的報表資料來源和資料集  
  
#### <a name="to-create-a-blank-report"></a>建立空白報表  
  
1.  按一下 [ **開始**]、依序指向 [ **程式集**] 和 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**]，然後按一下 [ **報表產生器**]。  
  
    > [!NOTE]  
    >  **[使用者入門]** 對話方塊應會隨即出現。 如果沒有出現，請從 [報表產生器] 按鈕按一下 **[新增]**。  
  
2.  在 **[使用者入門]** 對話方塊的左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[空白報表]**。  
  
#### <a name="to-create-a-data-source"></a>建立資料來源  
  
1.  在 [報表資料] 窗格中，按一下 **[新增]**，然後按一下 **[資料來源]**。  
  
2.  在 [名稱] 方塊中，輸入：**TextDataSource**  
  
3.  按一下 **[使用內嵌於報表中的連接]**。  
  
4.  確認連接類型為 Microsoft SQL Server，然後在 [連接字串] 方塊中輸入：**Data Source = \<伺服器名稱>**  
  
    > [!NOTE]  
    >  運算式\<伺服器名稱 >，例如 Report001，指定 SQL Server Database Engine 的執行個體安裝所在的電腦。 本教學課程無須任何特定資料，您只需要連接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 資料庫。 如果您已有資料來源連接列於 [資料來源連接] 底下，就可以選取該連接並移至下一個程序「建立資料集」。 如需詳細資訊，請參閱[取得資料連線的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>建立資料集  
  
1.  在 [報表資料] 窗格中，按一下 **[新增]**，然後按一下 **[資料集]**。  
  
2.  確認資料來源為 **TextDataSource**。  
  
3.  在 [名稱] 方塊中，輸入：**TextDataset。**  
  
4.  確認已選取 **[文字]** 查詢類型，然後按一下 **[查詢設計工具]**。  
  
5.  按一下 **[當成文字編輯]**。  
  
6.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  按一下 [執行]\(**!**) 來執行查詢。  
  
     查詢結果會成為可供報表顯示的資料。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="AddField"></a> 將欄位加入至報表設計介面  
 如果希望擷取自資料集的欄位出現在報表中，您可能會不加思索地直接將欄位拖曳到設計介面。 此練習將點出為何這樣做無效，以及應該改用的方法。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>將欄位加入至報表 (會得到錯誤的結果)  
  
1.  將 [FullName] 欄位從 [報表資料] 窗格拖曳到設計介面。  
  
     報表產生器會建立一個文字方塊內有運算式，表示為與\<Expr >。  
  
2.  按一下 **[執行]**。  
  
     請注意，只有一項記錄， **Fernando Ross**，依字母順序，這是在查詢中的第一筆記錄。 欄位並未重複成顯示該欄位內的其他記錄。  
  
3.  按一下 **[設計]** 返回 [設計] 檢視。  
  
4.  選取的運算式\<Expr > 在文字方塊中。  
  
5.  在 [屬性] 窗格中，您會看到 [值] 屬性如下 (若未看見 [屬性] 窗格，請檢查 [檢視] 索引標籤上的 [屬性])：  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     `First` 函數是設計成僅擷取欄位內的第一個值，而其目的也已達到。  
  
     直接將欄位拖曳到設計介面會建立文字方塊。 文字方塊本身並非資料區，所以不會顯示來自報表資料集的資料。 位於資料區 (例如資料表、矩陣和清單) 內的文字方塊才會顯示資料。  
  
6.  選取文字方塊 (如果您已選取運算式，請按 ESC 鍵選取文字方塊)，然後按下 DELETE 鍵。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>將欄位加入至報表 (會得到正確的結果)  
  
1.  在功能區的 [插入] 索引標籤上，按一下 [資料區] 區域內的 [清單]。 按一下設計介面，然後進行拖曳以建立寬約 2 英吋且高約 1 英吋的方塊。  
  
2.  將 [FullName] 欄位從 [報表資料] 窗格拖曳到清單方塊中。  
  
     這回報表產生器會建立一個內有運算式 `[FullName]` 的文字方塊。  
  
3.  按一下 **[執行]**。  
  
     請注意，此時方塊已經重複成顯示查詢中的所有記錄。  
  
4.  按一下 **[設計]** 返回 [設計] 檢視。  
  
5.  選取文字方塊中的運算式。  
  
6.  在 [屬性] 窗格中，您會看到 [值] 屬性如下：  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     透過將文字方塊拖曳到清單資料區，就可以顯示資料集內的資料。  
  
7.  選取清單方塊，然後按下 DELETE 鍵。  
  
##  <a name="AddTable"></a> 將資料表加入至報表設計介面  
 建立這個資料表，以便能夠在其中放置超連結和旋轉的文字。  
  
#### <a name="to-add-a-table-to-the-report"></a>將資料表加入至報表  
  
1.  上**插入**功能表上，按一下**表格**，然後按一下**資料表精靈**。  
  
2.  上**選擇資料集**頁面的 新增資料表或矩陣精靈，按一下**選擇現有的資料集，在這份報表或共用資料集**，然後按一下**TextDataset （在此報表中）**，然後按一下**下一步**。  
  
3.  上**排列欄位**頁面上，將**Territory**， **LinkText**，以及**產品**欄位**資料列群組**，拖曳**銷售**欄位設為**值**，然後按一下**下一個**。  
  
4.  在 [**選擇版面配置**頁面上，清除**展開/摺疊群組**核取方塊，以便您可以看到整個資料表，然後按一下**下一步]**。  
  
5.  在上**選擇樣式**頁面上，按一下**Slate**，然後按一下**完成**。  
  
6.  將資料表拖曳到標題區塊下方。  
  
7.  按一下 **[執行]**。  
  
     資料表看起來似乎沒問題，不過卻有兩個總計資料列。 **LinkText**欄位不需要總計資料列。  
  
8.  按一下 **[設計]** 返回 [設計] 檢視。  
  
9. 以滑鼠右鍵按一下文字方塊，其中包含`[LinkText]`，然後按一下**分割儲存格**。  
  
10. 選取下方的空資料格中`[LinkText]`儲存格，然後按住 SHIFT 鍵，然後選取其右邊的兩個資料格：**總**格中**產品**資料行和`[Sum(Sales)]`中的資料格**銷售**資料行。  
  
11. 選取這三個資料格，以滑鼠右鍵按一下其中一個資料格，然後按一下**刪除資料列**。  
  
12. 按一下 **[執行]**。  
  
##  <a name="AddHyperlink"></a> 將超連結加入至報表  
 在本節中，您要加入超連結指向上一節資料表中的文字。  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>加入超連結至報表  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下含有 `[LinkText]` 的資料格，然後按一下 [文字方塊屬性]。  
  
3.  在 **文字方塊內容**方塊中，按一下**動作**。  
  
4.  按一下 **移至 URL**。  
  
5.  在 **選取 URL**方塊中，按一下 **[URL]**，然後按一下 **確定**。  
  
6.  請注意，文字看起來並無任何改變。 您需要進行調整使其彷彿連結文字。  
  
7.  選取 [ `[LinkText]`]。  
  
8.  在 **字型**一節**首頁**索引標籤上，按一下 **加上底線**按鈕，然後再按一下下拉箭號旁**色彩** 按鈕，按一下 **藍色**。  
  
9. 按一下 **[執行]**。  
  
     文字現在看起來就像一個連結。  
  
10. 按一下該連結。 如果您的電腦已連接至網際網路，瀏覽器將會開啟報表產生器說明主題。  
  
##  <a name="RotateText"></a> 旋轉報表中的文字  
 在本節中，您要旋轉前幾節資料表中的部分文字。  
  
#### <a name="to-rotate-text"></a>旋轉文字  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  按一下包含下列項目的資料格： `[Territory].`  
  
3.  在 [主資料夾] 索引標籤的 [字型] 區段中，按一下 [粗體] 按鈕。  
  
4.  如果 [屬性] 窗格並未開啟，請選取 [檢視] 索引標籤上的 [屬性] 核取方塊。  
  
5.  在 [屬性] 窗格中，尋找 WritingMode 屬性。  
  
    > [!NOTE]  
    >  當 [屬性] 窗格中的屬性組織成類別目錄時，WritingMode 會位於 [當地語系化] 類別目錄中。 請確定您已選取資料格，而不是文字。 WritingMode 是文字方塊的屬性，並非文字的屬性。  
  
6.  在清單方塊中，按一下**Rotate270**。  
  
7.  上**首頁**索引標籤中**段落**區段中，按一下**中間**並**Center**按鈕，將文字定位在儲存格的這兩個中心垂直和水平。  
  
8.  按一下 [執行]\(**!**)。  
  
 如今 `[Territory]` 資料格中的文字已呈垂直方向，從資料格底部往上書寫。  
  
##  <a name="FormatHTML"></a> 顯示 HTML 格式的文字  
  
#### <a name="to-display-text-formatted-as-html"></a>顯示格式化為 HTML 的文字  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  在 [插入] 索引標籤上，按一下 [文字方塊]，然後在設計介面上按一下並拖曳，以在資料表底下建立大約 4 英吋寬、3 英吋高的文字方塊。  
  
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
  
4.  選取文字方塊中的所有文字。  
  
     因為這是文字的屬性，而非文字方塊屬性，您可以在單一文字方塊中混雜純文字與使用 HTML 標記做為樣式的文字。  
  
5.  以滑鼠右鍵按一下所有選取的文字，然後按一下 [文字屬性]。  
  
6.  在 **一般**頁面的 **標記的型別**，按一下  **HTML-將 HTML 標記解譯為樣式**。  
  
7.  按一下 [確定] 。  
  
8.  按一下 [執行]\(**!**) 預覽報表。  
  
 文字方塊中的文字會顯示成標頭、段落和項目符號清單。  
  
##  <a name="FormatCurrency"></a> 將貨幣格式化  
  
#### <a name="to-format-numbers-as-currency"></a>將數字格式化為貨幣  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  按一下含有 `[Sum(Sales)]`的最上方資料表資料格，然後按住 SHIFT 鍵，再按一下含有 `[Sum(Sales)]`的底部資料表資料格。  
  
3.  在 [主資料夾] 索引標籤的 [數字] 群組中，按一下 [貨幣] 按鈕。  
  
4.  （選擇性）在上**首頁**索引標籤**數目**群組中，按一下**預留位置樣式**按鈕，然後按一下**範例值**若要查看如何將數字會格式化。  
  
5.  (選擇性) 在 [主資料夾] 索引標籤的 [數字] 群組中，按一下[減少小數位數] 按鈕兩次，顯示沒有分的貨幣數字。  
  
6.  按一下 [執行]\(**!**) 預覽報表。  
  
 報表如今已顯示格式化的資料，更容易閱讀。  
  
##  <a name="Save"></a> 儲存報表  
 您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。  
  
 本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 [名稱] 中，將預設名稱取代為您選擇的名稱。  
  
5.  按一下 [儲存] 。  
  
 報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[桌面]**、 **[我的文件]** 或 **[我的電腦]**，然後瀏覽到您要儲存報表的資料夾。  
  
3.  在 [名稱] 中，將預設名稱取代為您選擇的名稱。  
  
4.  按一下 [儲存] 。  
  
## <a name="next-steps"></a>後續步驟  
 有很多種，格式化文字在報表產生器[教學課程：建立自由格式報表&#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)包含更多範例。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
