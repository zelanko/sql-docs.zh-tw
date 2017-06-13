---
title: "教學課程： 運算式簡介 |Microsoft 文件"
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97b19aaffd06a196d3cbd39e44b49c971a146edf
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="tutorial-introducing-expressions"></a>教學課程：運算式簡介
在此 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] 教學課程中，您將使用含有一般函數和運算子的運算式，來建立功能強大且靈活的 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 編頁報表。 

您將撰寫運算式以串連名稱值、在不同的資料集中查閱值、依據欄位值顯示不同色彩等功能。  
  
報表是帶狀報表，其中採用白色和某種色彩交替的資料列。 報表包含選取非白色資料列色彩的參數。  
  
此圖顯示報表，與您將要建立的報表相似。  
  
![report-builder-expression-tutorial-in-browser](../reporting-services/media/report-builder-expression-tutorial-in-browser.png) 
  
完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Setup"></a>1.從資料表或矩陣精靈建立資料表報表和資料集  
在本節中，您會建立資料表報表、資料來源與資料集。 當您配置資料表時，只會包含少數欄位。 在完成精靈之後，您將手動加入資料行。 這個精靈可讓您輕鬆配置資料表。  
  
> [!NOTE]  
> 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
### <a name="to-create-a-table-report"></a>建立資料表報表  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果未顯示 [新報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  在 [選擇資料集] 頁面上，按一下 [建立資料集] > [下一步]。  
  
6.  在 **[選擇與資料來源的連接]** 頁面上，選取類型為 **[SQL Server]**的資料來源。 請從清單中選取資料來源，或者瀏覽到報表伺服器再進行選取。  

    > [!NOTE]  
    > 只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連接的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
7.  按一下 **[下一步]**。  
  
8.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
9. 將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Female' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2015-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2015-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2015-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2015-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2015-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2015-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2015-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2015-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2015-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2015-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2015-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2015-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2015-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2015-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2015-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2015-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2015-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    ```  

  
10. 在查詢設計工具工具列上，按一下 [執行] (**!**)。 結果集會顯示 23 個資料列，包括下列資料行：FirstName、LastName、StateProvince、CountryRegionID、Gender、YTDPurchase 和 LastPurchase。  

    ![report-builder-expression-tutorial-query-as-text](../reporting-services/media/report-builder-expression-tutorial-query-as-text.png)
  
11. 按一下 **[下一步]**。  
  
12. 在 [排列欄位] 頁面上，依指定的順序從 [可用的欄位] 清單將下列欄位拖曳至 [值] 清單。  
  
    -   StateProvince   
    -   CountryRegionID  
    -   LastPurchase  
    -   YTDPurchase  
  
    由於 CountryRegionID 和 YTDPurchase 包含數值資料，因此預設會套用 SUM 彙總，但您不想要它們是加總。  
   
13. 以滑鼠右鍵按一下 [值] 清單中的 **CountryRegionID**，然後清除 [加總] 核取方塊。  
  
    [加總] 不再套用至 CountryRegionID。  
  
14. 以滑鼠右鍵按一下 [值] 清單中的 **YTDPurchase**，然後按一下 [加總] 選項。  
  
    [加總] 不再套用至 YTDPurchase。  
    
    ![report-builder-expression-not-sum](../reporting-services/media/report-builder-expression-not-sum.png)
  
15. 按一下 **[下一步]**。  
  
16. 在 [選擇配置] 頁面上，保留所有預設設定，然後按一下 [下一步]。  

    ![report-builder-expression-tutorial-choose-layout](../reporting-services/media/report-builder-expression-tutorial-choose-layout.png)
  
17. 按一下 **[完成]**。  
  
## <a name="UpdateNames"></a>2.更新資料來源和資料集的預設名稱  
  
### <a name="to-update-the-default-name-of-the-data-source"></a>若要更新資料來源的預設名稱  
  
1.  在 [報表資料] 窗格中，展開 [資料來源] 資料夾。  
  
2.  以滑鼠右鍵按一下 **DataSource1**，然後按一下 [資料來源屬性]。  
  
3.  在 [名稱] 方塊中，輸入 **ExpressionsDataSource**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-update-the-default-name-of-the-dataset"></a>若要更新資料集的預設名稱  
  
1.  在 [報表資料] 窗格中，展開 [資料集] 資料夾。  
  
2.  以滑鼠右鍵按一下 **DataSet1**，然後按一下 [資料集屬性]。  

    ![report-builder-expression-tutorial-rename-dataset](../reporting-services/media/report-builder-expression-tutorial-rename-dataset.png)
  
3.  在 [名稱] 方塊中，輸入**運算式**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Concatenate"></a>3.顯示名字、縮寫和姓氏  
在本節中，您在運算式中使用 **Left** 函數和 **Concatenate** (**&**) 運算子，以將結果評估為包括縮寫和姓氏的名稱。 您可以逐步建立運算式，或是在程序中先略過，再從教學課程將運算式複製/貼上至 [運算式] 對話方塊中。   
  
1.  以滑鼠右鍵按一下 **StateProvince** 資料行，指向 [插入資料行]，然後按一下 [左方]。  
  
    新資料行就會新增至 **StateProvince** 資料行的左方。 
    
    ![report-builder-expression-tutorial-insert-column](../reporting-services/media/report-builder-expression-tutorial-insert-column.png) 
  
2.  按一下新資料行的標頭，並輸入**名稱**。  
  
3.  以滑鼠右鍵按一下 [名稱] 資料行的資料格，然後按一下 [運算式]。  

    ![report-builder-expression-tutorial-insert-expression](../reporting-services/media/report-builder-expression-tutorial-insert-expression.png)
  
4.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [文字]。  
  
5.  在 [項目] 清單中，按兩下 [Left]。  
  
    **Left** 函數隨即新增至運算式中。  
    
    ![report-builder-expression-tutorial-left-function](../reporting-services/media/report-builder-expression-tutorial-left-function.png)
  
6.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
7.  在 [值] 清單中，按兩下 **FirstName**。  
  
8.  輸入 **, 1)**  
  
    此運算式會從 **FirstName** 值中擷取一個字元 (從左邊算起)。  
  
9. 輸入 **&". "&**  

    如此會在運算式之後新增句號和空格。
  
10. 在 [值] 清單中，按兩下 **LastName**。  
  
    完成的運算式為： `=Left(Fields!FirstName.Value, 1) &". "& Fields!LastName.Value`  
    
    ![report-builder-expression-tutorial-complete-name-expression](../reporting-services/media/report-builder-expression-tutorial-complete-name-expression.png)
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 按一下 **[執行]** 預覽報表。  

## <a name="DateFormat"></a>(選擇性) 格式化日期和貨幣資料行和標頭資料列  
在本節中，您格式化 [上次購買] 資料行 (其中包含日期) 和 [YTDPurchase] 資料行 (其中包含貨幣)。 您也會格式化標頭資料列。  
  
### <a name="to-format-the-date-column"></a>格式化日期資料行  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  選取 [上次購買] 資料行中的資料格，然後在 [首頁] 索引標籤 > [數字] 區段中，選取 [日期]。  

    ![report-builder-expression-tutorial-date-format](../reporting-services/media/report-builder-expression-tutorial-date-format.png)
  
3.  此外，在 [數字] 區段中，按一下 [預留位置樣式] 旁的箭號，然後選取 [範例值]。 

    ![report-builder-expression-tutorial-sample-values](../reporting-services/media/report-builder-expression-tutorial-sample-values.png)

    現在您可以看到所選取的格式化範例。 
  
### <a name="to-format-the-currency-column"></a>格式化貨幣資料行

- 選取 [YTDPurchase] 資料行中的資料格，然後在 [數字] 區段中，選取 [貨幣]。
 
### <a name="to-format-the-column-headers"></a>格式化資料行標頭

1. 選取資料行標頭的資料列。

2. 在 [首頁] 索引標籤 > [段落] 區段中，選取 [左方]。 

    ![report-builder-expression-tutorial-format-headings](../reporting-services/media/report-builder-expression-tutorial-format-headings.png)

3. 按一下 **[執行]** 預覽報表。 

以下是到目前為止的報表，日期、貨幣和資料行標頭都已格式化。

![report-builder-expression-tutorial-preview-formatted](../reporting-services/media/report-builder-expression-tutorial-preview-formatted.png)

  
## <a name="Gender"></a>4.使用色彩顯示性別  
在本節中，您會新增色彩來顯示人員的性別。 您會新增資料行來顯示色彩，然後依據 [Gender] 欄位中的值決定出現在資料行中的色彩。  
  
在使報表成為帶狀報表時，若要保留已在該資料表儲存格中套用的色彩，請新增一個矩形，然後新增矩形的背景色彩。  
    
 
### <a name="to-add-an-mf-column"></a>新增 M/F 資料行  
  
1.  以滑鼠右鍵按一下 [名稱] 資料行，指向 [插入資料行]，然後按一下 [左方]。  
  
    新資料行就會新增在 [名稱] 資料行的左方。  
  
2.  按一下新資料行的標頭，並輸入 **M/F**。  
  
### <a name="to-add-a-rectangle"></a>若要加入矩形  
  
1.   在 [插入] 索引標籤上，按一下 [矩形]，然後按一下 [M/F] 資料行的資料格。  
  
     如此矩形就會加入至資料格。  
     
     ![report-builder-expression-tutorial-insert-rectangle](../reporting-services/media/report-builder-expression-tutorial-insert-rectangle.png)
  
2. 拖曳 [M/F] 和 [名稱] 之間的資料行分隔線，讓 [M/F] 資料行較窄。

    ![report-builder-expression-tutorial-narrow-column](../reporting-services/media/report-builder-expression-tutorial-narrow-column.png)
  
### <a name="to-use-color-to-show-gender"></a>使用色彩顯示性別  
  
1.  在 [M/F] 資料行的資料格中，以滑鼠右鍵按一下矩形，然後按一下 [矩形屬性]。  
  
2.  在 [矩形屬性] > [填滿] 索引標籤中，按一下 [填滿色彩] 旁邊的運算式 **fx** 按鈕。  
  
3.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [程式流程]。  
  
4.  在 [項目] 清單中，按兩下 [Switch]。  
  
5.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
6.  在 [值] 清單中，按兩下 [性別]。  
  
7.  輸入 **="Male",** (包括逗號)。

8. 在 [類別] 清單中，按一下 [常數]，然後在 [值] 方塊中，按一下 [矢菊花藍]。

    ![report-builder-expression-tutorial-color-expression-cornflower-blue](../reporting-services/media/report-builder-expression-tutorial-color-expression-cornflower-blue.png)

9. 在它後面輸入一個逗號。 
  
5.  在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，再按兩下 [Gender]。  
  
7.  輸入 **="Female",** (包括逗號)。 

8. 在 [類別] 清單中，按一下 [常數]，然後在 [值] 方塊中，按一下 [蕃茄紅]。

13. 在它之後輸入右括號 **)**。 
  
    完成的運算式為： `=Switch(Fields!Gender.Value ="Male", "CornflowerBlue",Fields!Gender.Value ="Female","Tomato")`  
    
    ![report-builder-expression-tutorial-color-expression-complete](../reporting-services/media/report-builder-expression-tutorial-color-expression-complete.png)
  
12. 按一下 [確定]，然後再按一下 [確定] 以關閉 [矩形屬性] 對話方塊。  
  
14. 按一下 **[執行]** 預覽報表。  

    ![report-builder-expression-tutorial-preview-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-m-f-column.png)

### <a name="to-format-the-color-rectangles"></a>格式化色彩矩形

1. 按一下 **[設計]** 返回 [設計] 檢視。  

16. 選取 [M/F] 資料行中的矩形。 在 [屬性] 窗格的 [框線] 區段中，設定這些屬性︰

    - BorderColor = White
    - BorderStyle = Solid
    - BorderWidth = 5pt
    
    ![report-builder-expression-tutorial-format-m-f-column](../reporting-services/media/report-builder-expression-tutorial-format-m-f-column.png)

18. 按一下 [執行] 再次預覽報表。 這次色彩區塊周圍有空白。

    ![report-builder-expression-tutorial-preview-formatted-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-formatted-m-f-column.png)  
  
## <a name="Lookup"></a>5.查閱 CountryRegion 名稱  
在本節中，您會建立 CountryRegion 資料集並使用 **Lookup** 函數顯示國家/地區的名稱，而不是國家/地區的識別碼。  
  
### <a name="to-create-the-countryregion-dataset"></a>若要建立 CountryRegion 資料集  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，按一下 [新增]，然後按一下 [資料集]。  
  
3.  在 * * 資料集的內容，然後按一下**使用內嵌在我的報表中的資料集**。  
  
4.  在 [資料來源] 清單中，選取 ExpressionsDataSource。  
  
5.  在 [名稱] 方塊中，輸入 **CountryRegion**。  
  
6.  確認已選取 [文字] 查詢類型，並且按一下 [查詢設計工具]。  
  
7.  按一下 **[當成文字編輯]**。  
  
8.  複製下列查詢並貼入查詢窗格中：  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. 按一下 [執行] (**!**) 來執行查詢。  
  
    查詢結果為國家/地區識別碼和名稱。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 再按一次 [確定]，關閉 [資料集屬性] 對話方塊。  

     現在您在 [報表資料] 資料行中有第二個資料集。
  
### <a name="to-look-up-values-in-the-countryregion-dataset"></a>若要查閱 CountryRegion 資料集中的值  
  
1.  按一下 [國家/地區 ID] 資料行標頭，並刪除文字 [ID]，使它成為 [國家/地區]。  
  
2.  以滑鼠右鍵按一下 [國家/地區] 資料行的資料格，然後按一下 [運算式]。  
  
3.  刪除運算式，但保留開頭的等號 (=)。  
  
    剩下的運算式為： `=`  
  
4.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [其他]，在 [項目] 清單中，按兩下 [Lookup]。  
  
6.  在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [CountryRegionID]。  
  
8.  將游標放在緊接 `CountryRegionID.Value`, and type **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**之後  
  
    完成的運算式為： `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
    **Lookup** 函數的語法會指定在 Expressions 資料集的 CountryRegionID 與 CountryRegion 資料集的 ID 之間的查閱，從 CountryRegion 資料集傳回 CountryRegion 值。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 按一下 **[執行]** 預覽報表。  
  
## <a name="Count"></a>6.計算自上次購買後的日數  
在本節中，您會新增資料行，然後使用 **Now** 函數或 `ExecutionTime` 內建全域變數，計算客戶自上次購買後至今的天數。  
  
### <a name="to-add-the-days-ago-column"></a>若要加入 [天前] 資料行  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下 [上次購買] 資料行，指向 [插入資料行]，然後按一下 [右方]。  
  
    新資料行就會新增至 [上次購買] 資料行的右方。  
  
3.  在資料行標頭中，輸入**天前**。  
  
4.  以滑鼠右鍵按一下 [天前] 資料行的資料格，然後按一下 [運算式]。  
  
5.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [日期和時間]。  
  
6.  在 [項目] 清單中，按兩下 [DateDiff]。  
  
7.  緊接在 `DateDiff(` 之後，輸入 **"d",** (包括引號 "" 和逗號)。 
  
9. 在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [LastPurchase]。  
  
11. 緊接在 `Fields!LastPurchase.Value` 之後，輸入 **,** (逗號)。 
  
13. 在 [類別] 清單中，再按一下 [日期和時間]，然後在 [項目] 清單中，按兩下 [Now]。  
  
    > [!WARNING]  
    > 在生產報表中，不應該在隨報表轉譯而評估多次的運算式中使用 **Now** 函數 (例如，報表的詳細資料列)。 **Now** 的值會依資料列而改變，而不同的值會影響運算式的評估結果，導致結果稍微不一致。 因此，請改用 `ExecutionTime` 提供的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 全域變數。  
  
15. 刪除 `Now(`之後的左括號，然後輸入右括號 **)**  
  
    完成的運算式為： `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
    
    ![report-builder-expression-tutorial-date-since-last-purchase](../reporting-services/media/report-builder-expression-tutorial-date-since-last-purchase.png)
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

11. 按一下 **[執行]** 預覽報表。  
  
## <a name="Indicator"></a>7.使用指標顯示銷售比較  
在本節中，您會新增資料行，並使用指標顯示某人今年到目前 (YTD) 的購買為高於或低於平均 YTD 購買。 **Round** 函數會移除值的小數。  
  
設定指標和其狀態需要許多步驟。 您要的話，可以略過「設定指標」程序，再從本教學課程將完成的運算式複製/貼上至 [運算式] 對話方塊中。  
  
### <a name="to-add-the--or---avg-sales-column"></a>若要加入平均銷售增減資料行  
  
1.  以滑鼠右鍵按一下 [YTD 購買] 資料行，指向 [插入資料行]，然後按一下 [右方]。  
  
    新資料行就會新增至 [YTD 購買] 資料行的右方。  
  
2.  按一下資料行標頭，並輸入**平均銷售增減**。  
  
### <a name="to-add-an-indicator"></a>若要加入指標  
  
1.  在 [插入] 索引標籤上，按一下 [指標]，然後按一下 [平均銷售增減] 資料行的資料格。  
  
    [選取指標類型] 對話方塊隨即開啟。  
  
2.  在圖示集的 [方向性] 群組中，按一下三個灰色箭頭的圖示集。  

    ![report-builder-expression-tutorial-select-indicator](../reporting-services/media/report-builder-expression-tutorial-select-indicator.png)
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-configure-the-indicator"></a>若要設定指標  
  
1.  以滑鼠右鍵按一下指標，按一下 [指標屬性]，然後按一下 [值和狀態]。  
  
2.  按一下 [值] 文字方塊旁邊的運算式 **fx** 按鈕。  
  
3.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [數學]。  
  
4.  在 [項目] 清單中，按兩下 [Round]。  
  
5.  在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [YTDPurchase]。  
  
7.  緊接在 `Fields!YTDPurchase.Value` 之後，輸入 **-** (減號)。 
  
9. 再次展開 [一般函數]、按一下 [彙總]，然後在 [項目] 清單中，按兩下 [Avg]。  
  
11. 在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [YTDPurchase]。  
  
13. 緊接在 `Fields!YTDPurchase.Value`之後，輸入 **, "Expressions"))**  
  
    完成的運算式為： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. 在 [狀態度量單位] 方塊中，選取 [數值]。  
  
17. 在具有向下鍵的資料列中，按一下 [開始] 值的文字方塊右邊的 **fx** 按鈕。  

    ![report-builder-expression-tutorial-indicator-start](../reporting-services/media/report-builder-expression-tutorial-indicator-start.png)
  
18. 在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [數學]。  
  
19. 在 [項目] 清單中，按兩下 [Round]。  
  
20. 在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [YTDPurchase]。  
  
22. 緊接在 `Fields!YTDPurchase.Value` 之後，輸入 **-** (減號)。 
  
24. 再次展開 [一般函數]、按一下 [彙總]，然後在 [項目] 清單中，按兩下 [Avg]。  
  
26. 在 [類別] 清單中，按一下 [欄位 (運算式)]，然後在 [值] 清單中，按兩下 [YTDPurchase]。  
  
28. 緊接在 `Fields!YTDPurchase.Value` 之後，輸入 **, "Expressions")) < 0**  
  
    完成的運算式為： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. 在 [結束] 值的文字方塊中，輸入 **0**。  
  
32. 按一下具有橫向箭號的資料列，然後按一下 [刪除]。  

    ![report-builder-expression-tutorial-delete-indicator-state](../reporting-services/media/report-builder-expression-tutorial-delete-indicator-state.png)
    
    現在只有兩個箭號，向上或向下。
  
33. 在具有向上鍵的資料列中，於 [開始] 方塊中輸入 **0**。  
  
34. 按一下 [結束] 值的文字方塊右邊的 **fx** 按鈕。  
  
35. 在**運算式**對話方塊中，刪除**100**和建立運算式：`=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. 再按一次 [確定]，關閉 [指標屬性] 對話方塊。  
  
38. 按一下 **[執行]** 預覽報表。  

    ![report-builder-expression-tutorial-preview-indicator](../reporting-services/media/report-builder-expression-tutorial-preview-indicator.png)
  
## <a name="GreenBar"></a>8.製作帶狀報表  
建立參數，讓報表讀者可以指定套用至報表中交替資料列的色彩，使其變成帶狀報表。  
  
### <a name="to-add-a-parameter"></a>若要加入參數  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [參數]，然後按一下 [加入參數]。  

    ![report-builder-expression-tutorial-add-parameter](../reporting-services/media/report-builder-expression-tutorial-add-parameter.png)
  
    **[報表參數屬性]** 對話方塊隨即開啟。  
  
3.  在 [提示] 中，輸入**選擇色彩**。  
  
4.  在 [名稱] 中，輸入 **RowColor**。  
  
5.  在 [可用的值] 索引標籤上，按一下 [指定值]。  
  
7.  按一下 **[加入]**。  
  
8.  在 [標籤] 方塊中，輸入 **Yellow**。  
  
9. 在 [值] 方塊中，輸入 **Yellow**。  
  
10. 按一下 **[加入]**。  
  
11. 在 [標籤] 方塊中，輸入 **Green**。  
  
12. 在 [值] 方塊中，輸入 **PaleGreen**。  
  
13. 按一下 **[加入]**。  
  
14. 在 [標籤] 方塊中，輸入 **Blue**。  
  
15. 在 [值] 方塊中，輸入 **LightBlue**。  
  
16. 按一下 **[加入]**。  
  
17. 在 [標籤] 方塊中，輸入 **Pink**。  
  
18. 在 [值] 方塊中，輸入 **Pink**。  

    ![report-builder-expression-tutorial-parameter-available](../reporting-services/media/report-builder-expression-tutorial-parameter-available.png)
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-apply-alternating-colors-to-detail-rows"></a>若要套用交替色彩至詳細資料列  
  
1.   選取在資料列中所有儲存格，但 [M/F] 資料行中的儲存格除外，它有自己的背景色彩。  

     ![report-builder-expression-tutorial-select-banded](../reporting-services/media/report-builder-expression-tutorial-select-banded.png)
  
4.  在 [屬性] 窗格中，按一下 **BackgroundColor**。 

     如果看不到 [屬性] 窗格，請在 [檢視] 索引標籤上選取 [屬性] 方塊。  
  
    如果 [屬性] 窗格中依類別列出屬性，則您會在 **Misc** 類別中發現 **BackgroundColor**。  
  
5.  按一下向下鍵，然後按一下 [運算式]。  

    ![report-builder-expression-tutorial-banded-color-property](../reporting-services/media/report-builder-expression-tutorial-banded-color-property.png)
  
6.  在 [運算式] 對話方塊中，展開 [一般函數]，然後按一下 [程式流程]。  
  
7.  在 [項目] 清單中，按兩下 [IIf]。  
  
8.  在 [一般函數]，按一下 [其他]，然後在 [項目] 清單中，按兩下 [RowNumber]。  

9. 緊接在 **RowNumber(** 之後，輸入 **Nothing) MOD 2,**
  
8. 按一下 [參數]，然後在 [值] 清單中按兩下 [RowColor]。  
  
22. 緊接在 `Parameters!RowColor.Value`之後，輸入 **, “White”)**  
  
    完成的運算式為： `=IIF(RowNumber(Nothing) MOD 2, Parameters!RowColor.Value, “White”)`  
    
    ![report-builder-expression-tutorial-banded-color-expressn](../reporting-services/media/report-builder-expression-tutorial-banded-color-expressn.png)
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="run-the-report"></a>執行報表  
  
1.  在 [首頁] 索引標籤上，按一下 [執行]。  

    現在當您執行報表時，要等到您選擇非白色區間的色彩之後才能看到報表。
  
3.  在 [選擇色彩] 清單中，選取報表中非白色區間的色彩。  
    
    ![report-builder-expression-tutorial-select-color](../reporting-services/media/report-builder-expression-tutorial-select-color.png)
  
4.  按一下 **[檢視報表]**。  
  
    報表隨即呈現，而且交替的資料列會使用您選擇的背景。 
    
    ![report-builder-expression-tutorial-preview-banded](../reporting-services/media/report-builder-expression-tutorial-preview-banded.png) 
  
## <a name="Title"></a>(選擇性) 加入報表標題  
加入報表的標題。  
  
### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入**銷售比較摘要**，然後選取文字。  
  
3.  在 [首頁] 索引標籤的 [字型] 方塊中，設定︰

    -  Size = 18
    -  Color = Gray
    -  粗體字
  
4.  在 [首頁] 索引標籤上，按一下 [執行]。  
  
3.  選取報表中非白色區間的色彩，然後按一下 [檢視報表]。  
  
## <a name="Save"></a>(選擇性) 儲存報表  
您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。 如需詳細資訊，請參閱[儲存報表 &#40;報表產生器&#41;](../reporting-services/report-builder/saving-reports-report-builder.md)。  
  
在本教學課程中，您會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
### <a name="to-save-the-report-to-a-report-server"></a>若要將報表儲存至報表伺服器  
  
1.  在 [檔案] 功能表 > [另存新檔]。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
    「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您將會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  指定報表名稱，然後按一下 [儲存]。  
  
報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。

現在您的報表讀者可以在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 入口網站檢視您的報表。

![report-builder-expression-tutorial-final-in-browser](../reporting-services/media/report-builder-expression-tutorial-final-in-browser.png)

   
## <a name="see-also"></a>另請參閱  
[運算式 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
[運算式範例 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
[指標 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
[影像、文字方塊、矩形和線條 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
[資料表 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[報表資料集 &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
  


