---
title: 教學課程：建立自由格式報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fe42fc3dd5e1398cc0e66ad2c37cd14a3fedd67a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202808"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>教學課程：建立自由格式報表 (報表產生器)
  本教學課程將教導您如何建立類似套印信件的 SSRS 自由格式報表。 您可以排列報表項目，以建立具有文字方塊、影像和其他資料區域的表單。  
  
 您在本教學課程中建立的報表，是以教學課程中所包含的範例銷售資料為基礎。 此報表會依領域將資訊分組，並顯示各領域的銷售經理姓名以及詳細和摘要銷售資訊。 您將使用清單資料區做為自由格式報表的基礎，然後加入含有影像的裝飾面板、插入資料的靜態文字、顯示詳細資訊的資料表，以及 (選擇性) 顯示摘要資訊的圓形圖和直條圖。  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何執行下列作業：  
  
-   [建立空白報表、 資料來源和資料集](#BlankReport)  
  
-   [新增及設定清單](#List)  
  
-   [加入圖形](#Graphics)  
  
-   [加入自由格式文字](#Text)  
  
-   [加入資料表以顯示詳細資料](#Table)  
  
-   [將資料格式化](#Format)  
  
-   [儲存報表](#Save)  
  
### <a name="other-optional-steps"></a>其他選擇性步驟  
  
-   [加入線條以區隔報表的區域](#Line)  
  
-   [加入摘要資料視覺效果](#Visualization)  
  
 完成這個教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="BlankReport"></a> 1.建立空白報表、資料來源與資料集  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此報表不需要外部資料來源。 使用這種內部資料類型最適合用於學習目的，但這種方法會使查詢相當冗長。 執行個體時提供 SQL Server 登入。  
  
#### <a name="to-create-a-blank-report"></a>建立空白報表  
  
1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。  
  
    > [!NOTE]  
    >  **[使用者入門]** 對話方塊應會隨即出現。 如果沒有出現，請從 [報表產生器] 按鈕按一下 **[新增]**。  
  
2.  在 **[使用者入門]** 對話方塊的左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[空白報表]**。  
  
#### <a name="to-create-a-new-data-source"></a>建立新資料來源  
  
1.  在 [報表資料] 窗格中，按一下 **[新增]**，然後按一下 **[資料來源]**。  
  
2.  在 `Name`方塊中，輸入： **ListDataSource**  
  
3.  按一下 **[使用內嵌於報表中的連接]**。  
  
4.  確認連線類型為 Microsoft SQL Server，接著在 [連接字串] 方塊中鍵入 **Data Source = \<伺服器名稱>**  
  
     \<伺服器名稱 >，例如 Report001，指定 SQL Server Database Engine 的執行個體安裝所在的電腦。 由於報表資料不是擷取自 SQL Server 資料庫，您不必加上資料庫的名稱。 指定之伺服器上的預設資料庫將用來剖析查詢。  
  
5.  按一下 [認證] ，並輸入連接到 SQL Server Database Engine 執行個體所需的認證。  
  
6.  按一下 [確定] 。  
  
#### <a name="to-create-a-new-dataset"></a>建立新資料集  
  
1.  在 [報表資料] 窗格中，按一下 **[新增]**，然後按一下 **[資料集]**。  
  
2.  在 `Name`方塊中，輸入： **listdataset。**  
  
3.  按一下 [使用內嵌在我的報表中的資料集] ，並確認資料來源是 **ListDataSource**。  
  
4.  確認已選取 **[文字]** 查詢類型，然後按一下 **[查詢設計工具]**。  
  
5.  按一下 **[當成文字編輯]**。  
  
6.  複製下列查詢並貼入查詢窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  按一下 [執行] 圖示即可執行查詢。  
  
     查詢結果會成為可供報表顯示的資料。  
  
     ![查詢設計工具](../../2014/tutorials/media/tutorial-querydesigner.png "查詢設計工具")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="List"></a> 2.加入及設定清單  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供三個資料區範本：資料表、矩陣和清單。 這些範本都是以 Tablix 資料區域為基礎。  
  
 在本教學課程中，您將使用清單，在類似新聞稿的報表中顯示各銷售領域的銷售資訊。 此資訊是依領域分組。 您要加入新的資料列群組來依領域分組資料，然後刪除內建的 [詳細資料] 資料列群組。 這個清單範本相當適合用來建立自由格式報表。 如需詳細資訊，請參閱 <<c0> [ 列出&#40;報表產生器及 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。</c0>  
  
> [!NOTE]  
>  此報表會使用 Letter (8.5 X11) 紙張大小和 1 英吋的邊界。 若報表頁面高度超過 9 英吋或寬度超過 6 1/2 英吋，則可能產生空白頁面。  
  
#### <a name="to-add-a-list"></a>加入清單  
  
1.  在功能區的 **[插入]** 索引標籤上，按一下 **[資料區域]** 區域內的 **[清單]** ，然後將清單拖曳到報表主體內。 將清單調整成高 7 英吋且寬 6.25 英吋。  
  
2.  按一下清單內部，在清單頂端按一下滑鼠右鍵，然後按一下 [Tablix 屬性] 。  
  
     ![新增清單](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "加入清單")  
  
3.  從 **[資料集名稱]** 下拉式清單中，選取 **[ListDataset]**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在清單內部按一下滑鼠右鍵，然後按一下 [矩形屬性] 。  
  
     ![矩形屬性命令](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "矩形屬性命令")  
  
6.  在 **[一般]** 索引標籤上，選取 **[在後方加入分頁符號]** 核取方塊。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>加入新的資料列群組並刪除 [詳細資料] 群組  
  
1.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下 [詳細資料] 群組，然後指向 **[加入群組]**，再按一下 **[父群組]**。  
  
     ![父群組命令](../../2014/tutorials/media/tutorial-parentgroupcommand.png "父群組命令")  
  
2.  從下拉式清單中選取 `[Territory].`。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     清單中會加入一個資料行。 資料行包含儲存格 `[Territory].`  
  
4.  以滑鼠右鍵按一下清單中的 [Territory] 資料行，再按一下 **[刪除資料行]**。  
  
     ![刪除資料行](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "刪除資料行")  
  
5.  按一下 [只刪除資料行] 。  
  
     ![刪除資料行對話方塊](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "刪除的資料行對話方塊")  
  
6.  在 [資料列群組] 窗格中，在 [詳細資料]  群組上按一下滑鼠右鍵，然後按一下 [刪除群組] 。  
  
     ![刪除詳細資料群組](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "刪除詳細資料群組")  
  
7.  按一下 **[僅刪除群組]**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Graphics"></a> 3.加入圖形  
 使用清單資料區的好處是，您可以在任何位置加入矩形和文字方塊等報表項目，而不必侷限於表格式配置。 您將要透過加入圖形 (有填色的矩形) 加強報表的外觀。  
  
#### <a name="to-add-graphic-elements-to-the-report"></a>加入圖形元素至報表中  
  
1.  在 [**插入**] 索引標籤的功能區中，按一下**矩形**，然後將矩形拖曳到清單的左上角。 將矩形調整成高 7 英吋且寬為 1 英吋。  
  
2.  以滑鼠右鍵按一下矩形，然後按一下 **[矩形屬性]**。  
  
3.  按一下 **[填滿]** 索引標籤。  
  
4.  在 [填滿色彩]  下拉式清單中，按一下 [更多色彩] ，然後選取 [暗灰色]  。  
  
     ![選取填滿色彩](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "選取填滿色彩")  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  按一下 **[執行]** 預覽報表。  
  
 報表左側現在會有深灰色矩形組成的垂直圖形。  
  
##  <a name="Text"></a> 4.加入自由格式文字  
 文字方塊會包含將在每個報表頁面上重複的靜態文字，還有資料欄位。  
  
#### <a name="to-add-text-to-the-report"></a>在報表中加入文字  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在在功能區的 [插入]  索引標籤上，按一下 [文字方塊] ，然後拖曳一個文字方塊到清單的左上角，放在您剛加入的矩形內。 將文字方塊調整成高約 3 英吋且寬約 5 英吋。  
  
3.  將滑鼠游標置於文字方塊的上半部，然後輸入 **Newsletter for** 。  
  
     ![新增新聞稿標題文字](../../2014/tutorials/media/tutorial-newsletterfor.png "新增新聞稿標題文字")  
  
    > [!NOTE]  
    >  記得在單字 "for" 後面多加一個空格。 此空格會將本段文字和下一個步驟要加入的欄位區隔開來。  
  
4.  將 [Territory] 欄位拖曳到文字方塊中，置於您在步驟 3 輸入的文字後面。  
  
     ![新增領土欄位](../../2014/tutorials/media/tutorial-addterritorialfield.png "新增領土欄位")  
  
5.  全選所有文字，再按一下滑鼠右鍵，然後按一下 **[文字屬性]**。  
  
6.  按一下 **[字型]** 索引標籤。  
  
7.  在 [字型]  清單中選取 [Times New Roman] 、[大小]  選取 [20 pt] 、[色彩]  選取 [紅色] 。  
  
     ![文字屬性](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "文字屬性")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 將滑鼠游標置於您在步驟 3 輸入的文字下方，然後輸入 **Hello** 。  
  
    > [!NOTE]  
    >  記得在單字 "Hello" 後面多加一個空格。 此空格會將本段文字和下一個步驟要加入的欄位區隔開來。  
  
10. 將 [FullName] 欄位拖曳到文字方塊中，置於您在步驟 9 輸入的文字後面，接著再輸入一個逗號 (,)。  
  
     ![新增全名欄位](../../2014/tutorials/media/tutorial-addfullnamefield.png "新增全名欄位")  
  
11. 選取您在步驟 9 和步驟 10 加入的文字，再按一下滑鼠右鍵，然後按一下 **[文字屬性]**。  
  
12. 按一下 **[字型]** 索引標籤。  
  
13. 在 [字型]  清單中選取 [Times New Roman] 、[大小]  選取 [16 pt] 、[色彩]  選取 [黑色]  。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 將滑鼠游標置於您在步驟 9 至步驟 13 加入的文字下方，然後複製並貼入下列「馬賽克」文字：  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel.   
    ```  
  
16. 選取您在步驟 15 加入的文字，再按一下滑鼠右鍵，然後按一下 **[文字屬性]**。  
  
17. 按一下 **[字型]** 索引標籤。  
  
18. 從 **[字型]** 清單中選取 **[Arial]**、 **[大小]** 選取 **[10 pt]**、 **[色彩]** 選取 **[黑色]**。  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![新增新聞稿文字](../../2014/tutorials/media/tutorial-newslettertext.png "新增新聞稿文字")  
  
20. 將滑鼠游標置於您在步驟 15 貼入的文字下方，然後輸入 **Congratulations on your total sales of** 。  
  
    > [!NOTE]  
    >  記得在單字 "of" 後面多加一個空格。 此空格會將本段文字和下一個步驟要加入的欄位區隔開來。  
  
21. 將 [Sales] 欄位拖曳到文字方塊中，置於您在步驟 20 輸入的文字後面，接著再輸入一個驚嘆號 (!)。  
  
22. 反白顯示 Sales 欄位，以滑鼠右鍵按一下  欄位中，然後按一下**運算式**。  
  
23. 在運算式方塊中，將運算式改為包含 Sum 函數，如下所示：  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![新增運算式到銷售欄位](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "新增運算式到銷售欄位")  
  
25. 選取您在步驟 20 至步驟 23 加入的文字，再按一下滑鼠右鍵，然後按一下 **[文字屬性]**。  
  
26. 按一下 **[字型]** 索引標籤。  
  
27. 在 [字型]  清單中選取 [Times New Roman] 、[大小]  選取 [16 pt] 、[色彩]  選取 [紅色] 。  
  
28. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
29. 選取 `[Sum(Sales)]` 並於 **[主資料夾]** 索引標籤上，按一下 **[數值]** 群組中的 **[貨幣]** 按鈕。  
  
     ![新增貨幣符號](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "新增貨幣符號")  
  
30. 以滑鼠右鍵按一下包含「按一下以加入標題」字樣的文字方塊，然後按一下 **[刪除]**。  
  
31. 選取清單方塊，然後利用方向鍵將其移到頁面頂端。  
  
32. 按一下 **[執行]** 預覽報表。  
  
 報表會顯示靜態文字，而且每個報表頁面含有與特定領域相關的資料。 銷售額則格式化為貨幣。  
  
 ![新聞稿預覽](../../2014/tutorials/media/tutorial-newsletters.png "新聞稿預覽")  
  
##  <a name="Table"></a> 5.加入資料表以顯示銷售詳細資料  
 使用新增資料表和矩陣精靈，將資料表加入至自由格式報表。 在完成精靈之後，您將要手動加入一個總計資料列。  
  
#### <a name="to-add-a-table"></a>加入資料表  
  
1.  在功能區的 **[插入]** 索引標籤上，按一下 **[資料區域]** 區域內的 **[資料表]**，然後按一下 **[資料表精靈]**。  
  
2.  在 [選擇資料集] 頁面上，按一下 **[ListDataset]**。  
  
3.  按 [下一步] 。  
  
4.  在 [排列欄位] 頁面上，將 [Product] 欄位從 [可用的欄位] 拖曳至 [值]。  
  
5.  針對 SalesDate、Quantity 和 Sales 重複步驟 4。 將 SalesDate 放到 Product 底下、Quantity 放到 SalesDate 底下、Sales 放到 Quantity 底下。  
  
6.  按 [下一步] 。  
  
7.  在 [選擇配置]  頁面上，檢視資料表的配置。  
  
     這個資料表非常單純， 其中包含五個資料行，而沒有任何資料列或資料行群組。 由於沒有群組，與群組相關的配置選項無法使用。 稍後在本教學課程中，您將要手動更新資料表使其包括總計。  
  
8.  按 [下一步] 。  
  
9. 在 **[選擇樣式]** 頁面的 **[樣式]** 窗格中，選取 **[石板]**。  
  
10. 按一下 **[完成]**。  
  
11. 將資料表拖曳到您在第 4 課加入的文字方塊下方。  
  
    > [!NOTE]  
    >  務必將資料表置於清單內。  
  
12. 確認已選取該資料表，然後在 [資料列群組] 窗格的 [詳細資料] 上按一下滑鼠右鍵，指向 [加入總計] ，再按一下 [之後] 。  
  
     ![新增報表總計](../../2014/tutorials/media/tutorial-addtotal.png "新增報表總計")  
  
13. 按一下 **[執行]** 預覽報表。  
  
 報表會顯示含有銷售額詳細資料及總計的資料表。  
  
 ![在報表中的銷售總額](../../2014/tutorials/media/tutorial-reportsalestotals.png "報表中的銷售總額")  
  
##  <a name="Format"></a> 6.將資料格式化  
 將數值資料格式化為貨幣，並將日期格式化為只有日和時間。  
  
#### <a name="to-format-fields-table"></a>格式化欄位資料表  
  
1.  按一下 **[設計]** ，切換到 [設計] 檢視。  
  
2.  按一下資料表中包含 `[Sum(SalesSales)]` 的資料格，接著在 **[主資料夾]** 索引標籤的 **[數值]** 群組中，按一下 **[貨幣]** 按鈕。  
  
     ![新增貨幣符號至銷售總和](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "新增貨幣符號至銷售總和")  
  
3.  按一下包含 `[SalesDate]` 的資料格，然後從 **[數值]** 群組的下拉式清單中，選取 **[日期]**。  
  
4.  按一下 **[執行]** 預覽報表。  
  
 報表如今已顯示格式化的資料，更容易閱讀。  
  
 ![格式化報表中的銷售總額](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "格式化報表中的總銷售額")  
  
##  <a name="Save"></a> 7.儲存報表  
 您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。 您也可以將報表匯出成各種格式 (例如 Word 和 PDF)，方法是執行報表，然後從 [匯出]  功能表選取格式。  
  
 本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在  `Name`，將預設名稱取代**SalesInformationByTerritory**。  
  
5.  按一下 **[儲存]**。  
  
 報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[桌面]**、 **[我的文件]** 或 **[我的電腦]**，然後瀏覽到您要儲存報表的資料夾。  
  
3.  在  `Name`，將預設名稱取代**SalesInformationByTerritory**。  
  
4.  按一下 **[儲存]**。  
  
##  <a name="Line"></a> 8。(選擇性) 加入線條以區隔報表的各區域  
 加入線條以區隔報表的編輯區和詳細資料區。  
  
#### <a name="to-add-a-line"></a>加入線條  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在功能區的 **[插入]** 索引標籤上，按一下 **[報表項目]** 區域內的 **[線條]**。  
  
3.  將線條拖曳到您在第 4 課加入的自由格式文字方塊下方。  
  
4.  按一下該線條。  
  
5.  按一下 **[主資料夾]** 索引標籤。  
  
6.  在 [框線]  區域內，寬度選取 [4 1/2]  點，色彩則選取 [紅色] 。  
  
     ![報表中加入一行](../../2014/tutorials/media/tutorial-reportwithline.png "新增報表行")  
  
##  <a name="Visualization"></a> 9。(選擇性) 加入摘要資料視覺效果  
 矩形可以協助您控制報表的轉譯方式。 將圓形圖和直條圖放到矩形內，以確保報表轉譯為您希望的外觀。  
  
#### <a name="to-add-a-rectangle"></a>若要加入矩形  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在功能區的 **[插入]** 索引標籤上，按一下 **[報表項目]** 區域內的 **[矩形]**，然後將矩形拖曳到清單中的資料表右側。 將矩形調整成寬為 2 英吋且高 4 英吋。  
  
3.  對齊矩形和資料表的上緣。  
  
#### <a name="to-add-a-pie-chart"></a>加入圓形圖  
  
1.  在功能區的 [插入]  索引標籤上，按一下 [資料視覺效果]  區域中的 [圖表]  ，然後按一下 [圖表精靈] 。  
  
2.  在 [選擇資料集] 頁面上，按一下 **[ListDataset]**，然後按 **[下一步]**。  
  
3.  按一下 **[圓形圖]**，然後按 **[下一步]**。  
  
4.  在 [排列圖表欄位] 頁面上，將 [Product] 拖曳至 [類別目錄]。  
  
5.  拖曳數量**值**，然後按一下**下一步**。  
  
6.  在 **[選擇樣式]** 頁面的 **[樣式]** 窗格中，選取 **[石板]**。  
  
7.  按一下 **[完成]**。  
  
8.  調整報表左上角顯示的圖表大小，成為高 1 1/2 英吋且寬為 2 英吋。  
  
9. 將圖表拖曳到矩形內。  
  
     ![新增圓形圖](../../2014/tutorials/media/tutorial-addpiechart.png "加入圓形圖")  
  
10. 在圖表標題上按一下滑鼠右鍵，然後按一下 [標題屬性] 。  
  
11. 在 **[圖表標題屬性]** 對話方塊中，為 [標題文字] 輸入 **Product Quantities Sold**。  
  
12. 按一下 **[字型]** 索引標籤，然後從 **[大小]** 清單中按一下 **[10pt]**。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-column-chart"></a>加入直條圖  
  
1.  在功能區的 [插入]  索引標籤上，按一下 [資料視覺效果]  區域中的 [圖表]  ，然後按一下 [圖表精靈] 。  
  
2.  在 [選擇資料集]  頁面上，按一下 [ListDataset] ，然後按 [下一步] 。  
  
3.  按一下 **[直條圖]**，然後按 **[下一步]**。  
  
4.  在 [排列圖表欄位] 頁面中，產品將欄位拖曳至**分類**。  
  
5.  將 [Sales] 拖曳至 [值]，然後按一下 [下一步]。  
  
     值會顯示在垂直軸上。  
  
6.  在 **[選擇樣式]** 頁面的 **[樣式]** 窗格中，選取 **[石板]**。  
  
7.  按一下 **[完成]**。  
  
     直條圖隨即加入至報表的左上角。  
  
8.  將圖表大小調整成寬為 2 英吋且高 2 英吋。  
  
9. 將圖表拖曳到矩形內。  
  
     ![新增直條圖](../../2014/tutorials/media/tutorial-addcolumnchart.png "新增直條圖")  
  
10. 在圖表標題上按一下滑鼠右鍵，然後按一下 [標題屬性] 。  
  
11. 在 **[圖表標題屬性]** 對話方塊中，為 [標題文字] 輸入 **Product Sales**。  
  
12. 按一下 [字型]  索引標籤，並在 [大小]  清單中按一下 [10pt] ，然後按一下 [確定] 。  
  
13. 在直條圖中，以滑鼠右鍵按一下垂直軸，然後將 **[顯示軸標題]** 取消選取。  
  
14. 針對水平軸重複步驟 13。  
  
15. 以滑鼠右鍵按一下圖例，然後按一下 **[刪除圖例]**。  
  
    > [!NOTE]  
    >  移除軸標題和圖例可以讓較小的圖表更具可讀性。  
  
 ![變更圖表標題和移除軸標題](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "變更圖表標題和移除軸標題")  
  
#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>確認圖表位於矩形內部  
  
1.  按一下您稍早在這一課中加入的矩形。  
  
     在 [屬性] 窗格中，`Name`屬性顯示矩形的名稱。  
  
     ![矩形的名稱](../../2014/tutorials/media/tutorial-rectanglename.png "矩形的名稱")  
  
2.  按一下圓形圖。  
  
3.  在 **屬性**窗格中，確認`Parent`屬性包含矩形的名稱。  
  
     ![父屬性圓形圖](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "父屬性的圓形圖")  
  
4.  按一下直條圖，然後重複步驟 2 和步驟 3。  
  
    > [!NOTE]  
    >  如果圖表不是在矩形內部，轉譯後的報表將不會一併顯示圖表。  
  
#### <a name="to-make-the-charts-the-same-size"></a>將圖表調整成相同的大小  
  
1.  按一下圓形圖，再按下 Ctrl 鍵，然後按一下直條圖。  
  
2.  當兩個圖表都已選取後，按一下滑鼠右鍵，指向 **[配置]**，再按一下 **[設定成相同寬度]**。  
  
     ![將圖表寬度相同](../../2014/tutorials/media/tutorial-makechartssamewidth.png "將圖表寬度相同")  
  
    > [!NOTE]  
    >  先按的項目會決定所有已選取項目的寬度。  
  
3.  按一下 **[執行]** 預覽報表。  
  
 報表如今會以圓形圖和直條圖顯示摘要銷售資料。  
  
 ![SSRS 教學課程中，自由格式報表](../../2014/tutorials/media/tutorial-reportfinal.png "SSRS 教學課程中，自由格式報表")  
  
## <a name="more-information"></a>[詳細資訊]  
 如需清單的詳細資訊，請參閱[資料表、 矩陣和清單&#40;報表產生器及 SSRS&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)，[列出&#40;報表產生器及 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)， [Tablix 的資料區域&#40;報表產生器及 SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)，並[Tablix 資料區資料格、 資料列和資料行&#40;報表產生器&#41;和 SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 如需查詢設計工具的詳細資訊，請參閱[查詢設計工具 &#40;報表產生器&#41;](../../2014/reporting-services/query-designers-report-builder.md) 和[以文字為基礎的查詢設計工具使用者介面 &#40;報表產生器&#41;](report-data/text-based-query-designer-user-interface-report-builder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
