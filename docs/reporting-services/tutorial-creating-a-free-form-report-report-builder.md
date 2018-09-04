---
title: 教學課程：建立自由格式報表 (報表產生器) | Microsoft Docs
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfd009008af99f853079c26e566a3b7194b4e304
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265920"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>教學課程：建立自由格式報表 (報表產生器)
在本教學課程中，您會建立分頁報表，作為電子報。 每個頁面會顯示靜態文字、摘要的視覺效果，以及詳細的範例銷售資料。

![report-builder-free-form-report-complete](../reporting-services/media/report-builder-free-form-report-complete.png)

此報表會依領域將資訊分組，並顯示各領域的銷售經理姓名以及詳細和摘要銷售資訊。 您一開始會使用清單資料區作為自由格式報表的基礎，然後新增含有影像的裝飾面板、插入資料的靜態文字、顯示詳細資訊的資料表，以及 (選擇性) 顯示摘要資訊的圓形圖和直條圖。  
  
完成這個教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="BlankReport"></a>1.建立空白報表、資料來源與資料集  
  
> [!NOTE]  
> 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
### <a name="to-create-a-blank-report"></a>建立空白報表  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果您看不到 [新增報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
  
2.  在左窗格中，確認已選取 [新增報表]。 
 
3.  在右窗格中，按一下 **[空白報表]**。  
  
### <a name="to-create-a-new-data-source"></a>建立新資料來源  
  
1.  在 [報表資料] 窗格中，按一下 [新增] > [資料來源]。  
  
2.  在 **[名稱]** 方塊中，輸入 **ListDataSource**。  
  
3.  按一下 **[使用內嵌於報表中的連接]**。  
  
4.  確認連線類型為 Microsoft SQL Server，接著在 [連接字串] 方塊中鍵入 **Data Source = \<伺服器名稱>**  
  
    **\<伺服器名稱>** (例如 Report001) 指定已安裝 SQL Server Database Engine 執行個體的電腦名稱。 由於此報表的資料不是擷取自 SQL Server 資料庫，您不必加上資料庫的名稱。 指定之伺服器上的預設資料庫只用來剖析查詢。  
  
5.  按一下 [認證] ，並輸入連接到 SQL Server Database Engine 執行個體所需的認證。  
  
6.  按一下 [確定] 。  
  
### <a name="to-create-a-new-dataset"></a>建立新資料集  
  
1.  在 [報表資料] 窗格中，按一下 [新增] > [資料集]。  
  
2.  在 [名稱] 方塊中，鍵入 **ListDataset**。  
  
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
  
7.  按一下 [執行] 圖示 (!) 即可執行查詢。  
  
    查詢結果會成為可供報表顯示的資料。  
  
    ![report-builder-free-form-tutorial-data](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="List"></a>2.加入及設定清單  
在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，清單範本相當適合用來建立自由格式報表。 它是根據 *tablix* 資料區域，就和資料表和矩陣一樣。 如需詳細資訊，請參閱 [使用清單建立發票和表單](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
您將使用清單，在格式類似新聞稿的報表中顯示各銷售領域的銷售資訊。 此資訊是依領域分組。 您要加入新的資料列群組來依領域分組資料，然後刪除內建的 [詳細資料] 資料列群組。  
  
### <a name="to-add-a-list"></a>加入清單  
  
1.  在 [插入] 索引標籤 > [資料區域] > [清單]。 

2. 按一下報表主體 (標題和頁尾區域之間)，並拖曳以形成清單方塊。 將清單方塊調整成高 7 英吋且寬 6.25 英吋。 若要取得確切的大小，請在 [屬性] 窗格的 [位置] 下，鍵入 [寬度] 和 [高度] 屬性的值。
  
    > [!NOTE]  
    > 此報表會使用 Letter (8.5 X11) 紙張大小和 1 英吋的邊界。 若清單方塊高度超過 9 英吋或寬度超過 6.5 英吋，則可能產生空白頁面。  
  
2.  按一下清單方塊內部，並以滑鼠右鍵按一下清單頂端的列，然後按一下 [Tablix 屬性]。  
  
    ![report-builder-free-form-tablix-properties](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  從 **[資料集名稱]** 下拉式清單中，選取 **[ListDataset]**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在清單內部按一下滑鼠右鍵，然後按一下 [矩形屬性] 。  
  
6.  在 [一般] 索引標籤上，選取 [在後方新增分頁符號] 核取方塊。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>加入新的資料列群組並刪除 [詳細資料] 群組  
  
1.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下 [詳細資料] 群組，然後指向 **[加入群組]**，再按一下 **[父群組]**。  
  
    ![report-builder-free-form-add-parent-group](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  在 [群組依據] 清單中，選取 `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    包含 `[Territory]` 資料格的資料行會新增至清單。
  
4.  以滑鼠右鍵按一下清單中的 [Territory] 資料行，再按一下 **[刪除資料行]**。  
  
    ![report-builder-free-form-delete-columns](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  選取 [只刪除資料行]。  
  
6.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下 [詳細資料] 群組 > [刪除群組]。  
   
7.  選取 [只刪除群組]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Graphics"></a>3.新增圖形元素  
清單資料區的一項好處是，您可以在任何位置加入矩形和文字方塊等報表項目，而不必侷限於表格式配置。 您將要透過加入圖形 (有填色的矩形) 加強報表的外觀。  
  
### <a name="to-add-graphic-elements-to-the-report"></a>加入圖形元素至報表中  
  
1.  在 [插入] 索引標籤上，選取 [矩形]。 

2. 按一下清單左上角並拖曳，形成高 7 英吋且寬 3.5 英吋的矩形。 同樣地，若要取得確切的大小，請在 [屬性] 窗格的 [位置] 下，鍵入 [寬度] 和 [高度] 的值。
  
2.  以滑鼠右鍵按一下矩形 > [矩形屬性]。  
  
3.  按一下 **[填滿]** 索引標籤。  
  
4.  在 [填滿色彩] 中，選取 [淺灰]。  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  按一下 **[執行]** 預覽報表。  
  
報表左側現在會有由淺灰色矩形組成的垂直圖形，如下圖所示。  
  
![report-builder-free-form-gray-rectangle](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="Text"></a>4.加入自由格式文字  
您可以新增文字方塊以顯示在每個報表頁面上重複的靜態文字，還有資料欄位。  
  
### <a name="to-add-text-to-the-report"></a>在報表中加入文字  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [插入] 索引標籤 > [文字方塊] 上。 按一下清單的左上角，在您先前新增的矩形內，並拖曳形成大約寬 3.45 英吋且高約 5 英吋的文字方塊。  
  
3.  將滑鼠游標置於文字方塊內，然後輸入： **Newsletter for** 。 在單字 "for" 後面加上一個空格來分隔的文字和您將在下一個步驟新增的欄位。   
  
    ![新增新聞稿標題文字](../reporting-services/media/tutorial-newsletterfor.png "新增新聞稿標題文字")  
  
4.  將 `[Territory]` 欄位從 [報表資料] 窗格中的 ListDataSet 拖曳到 "Newsletter for " 之後。  
  
    ![report-builder-free-form-territory-field](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  選取文字和 `[Territory]` 欄位。  
  
6.  在 [主資料夾] 索引標籤 > [字型]，選取︰ 
  
    *  [Segoe Semibold]。
    *  [20 pt]。
    *  [蕃茄紅]。  
  
9. 將滑鼠游標置於您在步驟 3 輸入的文字下方，然後輸入： **Hello** ，並在這個字後加上一個空格以分隔文字和您將在下一個步驟中新增的欄位。  
 
10. 將 `[FullName]` 欄位從 [報表資料] 窗格中的 ListDataSet 拖曳到文字方塊，放在 "Hello " 之後，然後輸入一個逗號 (,)。  
   
11. 選取您在之前的步驟新增的文字。
  
12. 在 [主資料夾] 索引標籤 > [字型]，選取︰ 
  
    *  [Segoe Semibold]。
    *  [16 pt]。
    *  **黑色**。  
   
15. 將滑鼠游標置於您在步驟 9 至步驟 13 加入的文字下方，然後複製並貼入下列無意義的文字：  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. 選取您剛才新增的文字。  
  
17.  在 [主資料夾] 索引標籤 > [字型]，選取︰ 
  
      *  [Segoe UI]。
      *  [10 pt]。
      *  **黑色**。  
 
20. 將滑鼠游標置於文字方塊內，在無意義文字底下輸入︰ **Congratulations on your total sales of**，並在文字之後以一個空格分隔文字和您將在下一個步驟新增的欄位。 
  
21. 將 [Sales] 欄位拖曳到文字方塊中，置於您在前一個步驟輸入的文字後面，然後輸入一個驚嘆號 (!)。  

25. 選取文字和您剛才新增的欄位。  
  
17.  在 [主資料夾] 索引標籤 > [字型]，選取︰ 
  
      *  [Segoe Semibold]。
      *  [16 pt]。
      *  **黑色**。  
  
22. 只選取 `[Sales]` 欄位，然後以滑鼠右鍵按一下欄位 > [運算式]。  
  
23. 在 [運算式] 方塊中，將運算式變更成包含 Sum 函式，如下所示：  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![report-builder-free-form-text-box](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. 在仍然選取 `[Sum(Sales)]` 的情況下，在 [主資料夾] 索引標籤 > [數字] 群組 > [貨幣]。  
  
30. 以滑鼠右鍵按一下包含「按一下以加入標題」字樣的文字方塊，然後按一下 **[刪除]**。  
  
31. 選取清單方塊。 選取兩個雙箭號，然後將它移至頁面頂端。  

    ![report-builder-drag-list](../reporting-services/media/report-builder-drag-list.png)
  
32. 按一下 **[執行]** 預覽報表。  
  
報表會顯示靜態文字，而且每個報表頁面含有與特定領域相關的資料。 銷售額則格式化為貨幣。  
  
![report-builder-newsletter-page-preview](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="Table"></a>5.加入資料表以顯示銷售詳細資料  
使用新增資料表和矩陣精靈，將資料表加入至自由格式報表。 在完成精靈之後，您將要手動加入一個總計資料列。  
  
### <a name="to-add-a-table"></a>加入資料表  
  
1.  在 [插入] 索引標籤 > [資料區域] 區域 > [資料表] > [資料表精靈]。  
  
2.  在 [選擇資料集] 頁面上，按一下 [ListDataset] > [下一步]。  
  
4.  在 [排列欄位] 頁面上，將 [Product] 欄位從 [可用的欄位] 拖曳至 [值]。  
  
5.  針對 SalesDate、Quantity 和 Sales 重複步驟 3。 將 SalesDate 放到 Product 底下、Quantity 放到 SalesDate 底下、Sales 放到 Quantity 底下。  
  
6.  按 [下一步] 。  
  
7.  在 [選擇配置]  頁面上，檢視資料表的配置。  
  
    資料表很簡單︰五個資料行，且沒有資料列或資料行群組。 由於沒有群組，與群組相關的配置選項無法使用。 稍後在本教學課程中，您將要手動更新資料表使其包括總計。  
  
8.  按 [下一步] 。  
  
9. 按一下 **[完成]**。  
  
11. 將資料表拖曳到您在第 4 課加入的文字方塊下方。  
  
    > [!NOTE]  
    > 請確定資料表在清單方塊內，而且在灰色矩形內。  
  
12. 在選取資料表的情況下，於 [資料列群組] 窗格中以滑鼠右鍵按一下 [詳細資料] > [新增總計] > [之後]。  
  
    ![report-builder-free-form-table-totals](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. 選取 Product 資料行中的資料格並輸入 **Total**。

    ![report-builder-free-form-type-total](../reporting-services/media/report-builder-free-form-type-total.png)

12. 選取 [SalesDate] 欄位。 在 [主資料夾] 索引標籤 > [數字]，將 [預設] 變更為 [日期]。

13. 選取 [Sum(Sales)] 欄位。 在 [主資料夾] 索引標籤 > [數字]，將 [預設] 變更為 [貨幣]。

按一下 **[執行]** 預覽報表。  
  
報表會顯示含有銷售額詳細資料及總計的資料表。  
  
![report-builder-free-form-with-table](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="Save"></a>6.儲存報表  
您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。  
  
本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
    「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 **[名稱]** 中，將預設名稱取代為 **SalesInformationByTerritory**。  
  
5.  按一下 **[儲存]**。  
  
報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
### <a name="to-save-the-report-on-your-computer"></a>將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[桌面]**、 **[我的文件]** 或 **[我的電腦]**，然後瀏覽到您要儲存報表的資料夾。  
  
3.  在 **[名稱]** 中，將預設名稱取代為 **SalesInformationByTerritory**。  
  
4.  按一下 **[儲存]**。  
  
## <a name="Line"></a>7.(選擇性) 加入線條以區隔報表的各區域  
加入線條以區隔報表的編輯區和詳細資料區。  
  
### <a name="to-add-a-line"></a>加入線條  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [插入] 索引標籤 > [報表項目] > [線條]。  
  
3.  在您於第 4 課新增的文字方塊下方繪製線條。  
  
4.  按一下線條，然後在 [主資料夾] 索引標籤 > [框線]，選取︰
     * **寬度** 選取 **3** pt。
     * **色彩** 選取 [蕃茄紅]。  
  
## <a name="Visualization"></a>8.(選擇性) 新增摘要資料視覺效果  
矩形可以協助您控制報表的轉譯方式。 將圓形圖和直條圖放到矩形內，以確保報表轉譯為您希望的外觀。  
  
### <a name="to-add-a-rectangle"></a>若要加入矩形  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [插入] 索引標籤 > [報表項目] >  [矩形]。 將清單方塊內的矩形拖曳到資料表的右邊，形成大約寬 2.25 英吋且高 7.9 英吋的矩形。  
  
3.  在選取新矩形的情況下，在 [屬性] 窗格中，讓 **BorderColor**成為 LightGrey、 **BorderStyle**成為 Solid、 **BorderWidth**成為 2pt。 

4. 對齊矩形和資料表的上緣。  
  
## <a name="to-add-a-pie-chart"></a>加入圓形圖  
  
1.  在 [插入] 索引標籤 > [資料視覺效果] > [圖表] > [圖表精靈]。  
  
2.  在 [選擇資料集] 頁面上，按一下 [ListDataset] > [下一步]。  
  
3.  按一下 [圓形圖] > [下一步]。  
  
4.  在 [排列圖表欄位] 頁面上，將 [Product] 拖曳至 [類別目錄]。  
  
5.  將 [Quantity] 拖曳至 [值]，然後按一下 [下一步]。  
  
6.  按一下 **[完成]**。  
  
8.  調整報表左上角顯示的圖表大小，成為大約寬 2.25 英吋且高 3.6 英吋。  
  
9. 將圖表拖曳到矩形內。  
   
10. 選取圖表標題，然後輸入︰ **Product Quantities Sold**。  
  
12. 在 [主資料夾] 索引標籤 > [字型]，讓標題成為︰
    * **字型** **Segoe UI SemiBold**。
    * **大小** **12 pt**。
    * **色彩** **黑色**。  

13. 以滑鼠右鍵按一下圖例 > [圖例屬性]。

14. 在 [一般] 索引標籤的 [圖例位置] 下，選取底部的中心點。 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. 視需要拖曳，讓圖表區域變高。

     ![report-builder-free-form-pie](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>加入直條圖  
  
1.  在 [插入] 索引標籤 > [資料視覺效果] > [圖表] > [圖表精靈]。  
  
2.  在 [選擇資料集] 頁面上，按一下 [ListDataset] ，然後按一下 [下一步] 。  
  
3.  按一下 [直條圖]，然後按一下 [下一步]。  
  
4.  在 [排列圖表欄位] 頁面上，將 [Product] 欄位拖曳至 [類別目錄]。  
  
5.  將 [Sales] 拖曳至 [值]，然後按一下 [下一步]。  
  
    值會顯示在垂直軸上。  
  
6.  按一下 **[完成]**。  
  
    直條圖隨即加入至報表的左上角。  
  
8.  調整圖表成為大約寬 2.25 英吋且高將近 4 英吋。  
  
9. 將圖表拖曳到矩形內。  
   
10. 選取圖表標題，然後輸入︰ **Product Sales**。  
  
12. 在 [主資料夾] 索引標籤 > [字型]，讓標題成為︰
    * **字型** **Segoe UI SemiBold**。
    * **大小** **12 pt**。
    * **色彩** **黑色**。  
  
15. 以滑鼠右鍵按一下圖例，然後按一下 **[刪除圖例]**。  
  
    > [!NOTE]  
    > 當為小型圖表時，移除圖例會讓圖表更容易閱讀。  
  
    ![report-builder-free-form-column](../reporting-services/media/report-builder-free-form-column.png)

12. 選取圖表軸，然後在 [主資料夾] 索引標籤 > [數字] > [貨幣]。

13. 選取 [減少小數位數] 兩次，讓數字只顯示元而不顯示分。      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>確認圖表位於矩形內部  

您可以使用矩形當作報表頁面上其他項目的容器。 深入了解 [矩形當作容器](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)。
  
1.  選取您稍早在本課程中建立並新增圖表的矩形。  
  
    在 [屬性] 窗格中， **Name** 屬性會顯示該矩形的名稱。  
  
    ![report-builder-free-form-rectangle-name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  按一下圓形圖。  
  
3.  在 [屬性]  窗格中，確認 **Parent** 屬性包含矩形的名稱。  
  
     ![report-builder-free-form-pie-parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  按一下直條圖，然後重複步驟 3。  
  
    > [!NOTE]  
    > 如果圖表不是在矩形內部，轉譯後的報表將不會一併顯示圖表。  
  
### <a name="to-make-the-charts-the-same-size"></a>將圖表調整成相同的大小  
  
1.  選取圓形圖、按下 Ctrl 鍵，然後選取直條圖。  
  
2.  在選取兩個圖表的情況下，以滑鼠右鍵按一下 > [配置] > [設定成相同寬度]。  
  
    > [!NOTE]  
    > 先按的項目會決定所有已選取項目的寬度。  
  
3.  按一下 **[執行]** 預覽報表。  
  
報表如今會以圓形圖和直條圖顯示摘要銷售資料。  
  

  
## <a name="next-steps"></a>Next Steps  
以上總結如何建立自由格式報表的教學課程。  
  
如需清單的詳細資訊，請參閱： 
* [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [使用清單建立發票和表單](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
如需查詢設計工具的詳細資訊，請參閱[查詢設計工具 &#40;報表產生器&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9) 和[以文字為基礎的查詢設計工具使用者介面 &#40;報表產生器&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)。  
  
## <a name="see-also"></a>另請參閱  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md) 
  

