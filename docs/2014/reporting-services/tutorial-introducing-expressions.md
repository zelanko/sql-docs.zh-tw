---
title: 教學課程：運算式簡介 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 73bcce5c157ad412fabb677302eeddbd40a8b54e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075848"
---
# <a name="tutorial-introducing-expressions"></a>教學課程：運算式簡介
  運算式可協助您建立強大而靈活的報表。 本教學課程將教您建立和實作使用一般函數和運算子的運算式。 您將使用**運算式**對話方塊，即可撰寫運算式以串連名稱值、 查閱值在不同的資料集中，顯示不同的圖片，根據欄位的值，並依此類推。  
  
 報表是橫條報表，其中採用白色和某種色彩交替的資料列色彩。 報表包含選取非白色資料列色彩的參數。  
  
 下圖顯示報表，與您將要建立的報表相似。  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何執行下列作業：  
  
1.  [從資料表或矩陣精靈建立資料表報表和資料集](#Setup)  
  
2.  [更新預設名稱的資料來源和資料集](#UpdateNames)  
  
3.  [顯示名字、 縮寫和姓氏的名稱](#Concatenate)  
  
4.  [使用影像顯示性別](#Gender)  
  
5.  [查閱 CountryRegion 名稱](#Lookup)  
  
6.  [計算自上次購買後的日數](#Count)  
  
7.  [使用指標顯示銷售比較](#Indicator)  
  
8.  [製作 「 綠色橫條 」 報表的報表](#GreenBar)  
  
### <a name="other-optional-steps"></a>其他選擇性步驟  
  
-   [格式化日期資料行](#DateFormat)  
  
-   [加入報表標題](#Title)  
  
-   [儲存報表](#Save)  
  
 完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Setup"></a> 1.從資料表或矩陣精靈建立資料表報表和資料集  
 建立資料表報表、資料來源與資料集。 當您配置資料表時，只會包含少數欄位。 在完成精靈之後，您將手動加入資料行。 精靈方便您配置資料表並套用樣式。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併為一個程序。 如需如何瀏覽至報表伺服器、選擇資料來源以及建立資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
#### <a name="to-create-a-new-table-report"></a>若要建立新資料表報表  
  
1.  按一下 **開始**，指向**程式**，按一下  [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**，然後按一下**報表產生器**。  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
    > [!NOTE]  
    >  如果 **[使用者入門]** 對話方塊沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。  
  
    > [!NOTE]  
    >  如果您偏好使用報表產生器的 ClickOnce 版本，開啟報表管理員，然後按一下**報表產生器**，或移至 SharePoint 網站的 Reporting Services 內容類型，例如報告已啟用，並且按一下**報表產生器報表**上**新的文件**功能表上的**文件**共用文件庫 索引標籤。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  在 **[選擇資料集]** 頁面上，按一下 **[建立資料集]**。  
  
5.  按 [下一步] 。  
  
6.  在 **[選擇與資料來源的連接]** 頁面上，選取類型為 **[SQL Server]** 的資料來源。 請從清單中選取資料來源，或者瀏覽到報表伺服器再進行選取。  
  
7.  按 [下一步] 。  
  
8.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
9. 將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     查詢會指定資料行名稱，其中包括出生日期、名字、姓氏、省份、國家/地區識別碼、性別，以及今年到目前的購買記錄。  
  
10. 在查詢設計工具工具列上，按一下 **[執行]** \(**!**)。 結果集會顯示 20 個資料列，並且包括下列資料行：FirstName、LastName、StateProvince、CountryRegionID、Gender、YTDPurchase 和 LastPurchase。  
  
11. 按 [下一步] 。  
  
12. 在 [排列欄位] 頁面上，依指定的順序將下列欄位從 [可用的欄位] 清單拖曳至 [值] 清單。  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     由於 CountryRegionID 和 YTDPurchase 包含數值資料，因此預設會套用 SUM 彙總。  
  
    > [!NOTE]  
    >  但是不包括 [FirstName] 和 [LastName] 欄位。 您將在後續步驟中加入這兩個欄位。  
  
13. 在 **值**清單中，以滑鼠右鍵按一下`CountryRegionID`然後按一下**總和**選項。  
  
     [加總] 不再套用至 CountryRegionID。  
  
14. 以滑鼠右鍵按一下 [值] 清單中的 [YTDPurchase]，然後按一下 [加總] 選項。  
  
     [加總] 不再套用至 YTDPurchase。  
  
15. 按 [下一步] 。  
  
16. 在 [選擇配置] 頁面上，按 一下 [下一步]。  
  
17. 在上**選擇樣式**頁面上，按一下**Slate**，然後按一下**完成**。  
  
##  <a name="UpdateNames"></a> 2.更新資料來源和資料集的預設名稱  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>若要更新資料來源的預設名稱  
  
1.  在 [報表資料] 窗格中，展開 [資料來源]。  
  
2.  以滑鼠右鍵按一下 **DataSource1**，然後按一下 [資料來源屬性]。  
  
3.  在 [名稱] 方塊中，鍵入 **ExpressionsDataSource**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>若要更新資料集的預設名稱  
  
1.  在 [報表資料] 窗格中，展開 [資料集]。  
  
2.  以滑鼠右鍵按一下 **DataSet1**，然後按一下 [資料集屬性]。  
  
3.  在 [名稱] 方塊中，輸入**運算式**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Concatenate"></a> 3.顯示名字、縮寫和姓氏  
 在運算式中，使用 **Left** 函數和 **Concatenate** (**&**) 運算子，以將結果評估為包括縮寫和姓氏的名稱。 您可以逐步建立運算式，或是在程序中先略過，再從教學課程將運算式複製/貼上至 [運算式] 對話方塊中。  
  
#### <a name="to-add-the-name-column"></a>若要加入名稱資料行  
  
1.  以滑鼠右鍵按一下 **StateProvince** 資料行，指向 [插入資料行]，然後按一下 [左方]。  
  
     新資料行就會新增至 **StateProvince** 資料行的左方。  
  
2.  按一下新資料行的標題，並輸入**名稱**。  
  
3.  以滑鼠右鍵按一下 [名稱] 資料行的資料格，然後按一下 [運算式]。  
  
4.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [文字]。  
  
5.  在 [項目] 清單中，按兩下 [左方]。  
  
     **Left** 函數隨即新增至運算式中。  
  
6.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
7.  在 [值] 清單中，按兩下 **FirstName**。  
  
8.  輸入 **, 1)**  
  
     此運算式會從 **FirstName** 值中擷取一個字元 (從左邊算起)。  
  
9. 輸入 **&" "&**  
  
10. 在 [值] 清單中，按兩下 **LastName**。  
  
     完成的運算式為： `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Gender"></a> 4.使用影像顯示性別  
 使用影像顯示人員的性別，並且使用第三個影像識別未知的性別值。 您會在報表中加入三個隱藏影像，以及一個新的資料行來顯示這些影像，然後依據 [Gender] 欄位中的值決定出現在資料行中的影像。  
  
 若要在製作橫條報表時套用色彩至包含影像的資料表資料格，您會先加入矩形，然後將影像加入矩形中。 您必須使用矩形，才能將背景色彩套用至矩形，而不是套用至影像。  
  
 本教學課程會使用 Windows 所安裝的影像，不過您可以使用任何影像。 您將使用內嵌影像，這些影像不必安裝到本機電腦或報表伺服器上。  
  
#### <a name="to-add-images-to-the-report-body"></a>若要將影像加入至報表主體  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在功能區的 [插入] 索引標籤上，按一下 [影像]，然後按一下資料表下方的報表主體。  
  
     [影像屬性] 對話方塊隨即開啟。  
  
3.  按一下 [匯入] 並導覽至 C:\Users\Public\Public Pictures\Sample Pictures。  
  
4.  按一下 Penguins.JPG，然後按一下[開啟]。  
  
     在 [影像屬性] 對話方塊中，按一下 [可見性]，然後按一下 [隱藏] 選項。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  重複步驟 2 到 5，但選擇 Koala.JPG。  
  
7.  重複步驟 2 到 5，但是選擇 Tulips.JPG。  
  
#### <a name="to-add-the-gender-column"></a>若要加入性別資料行  
  
1.  以滑鼠右鍵按一下 [名稱] 資料行，指向 [插入資料行]，然後按一下 [右方]。  
  
     新資料行就會新增至 [名稱] 資料行的右方。  
  
2.  按一下新資料行的標題，並輸入**性別**。  
  
#### <a name="to-add-a-rectangle"></a>若要加入矩形  
  
-   在功能區的 [插入] 索引標籤上，按一下 [矩形]，然後按一下 [性別] 資料行的資料格。  
  
     如此矩形就會加入至資料格。  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>若要將影像加入矩形中  
  
1.  以滑鼠右鍵按一下矩形，指向 [插入]，然後按一下 [影像]。  
  
2.  在 [影像屬性] 對話方塊中，按一下 [使用此影像] 旁邊的向下鍵，並選取您新增的其中一個影像，例如 Penguins.JPG。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>若要使用影像顯示性別  
  
1.  在 [性別] 資料行的資料格中，以滑鼠右鍵按一下影像，然後按一下 [影像屬性]。  
  
2.  在 [影像屬性] 對話方塊中，按一下 [使用此影像] 文字方塊旁邊的運算式 **fx** 按鈕。  
  
3.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [程式流程]。  
  
4.  在 [項目] 清單中，按兩下 [Switch]。  
  
5.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
6.  在 [值] 清單中，按兩下 [性別]。  
  
7.  輸入 **="Male", "Koala",**  
  
8.  在 [值] 清單中，按兩下 [性別]。  
  
9. 輸入 **="Female", "Penguins",**  
  
10. 在 [值] 清單中，按兩下 [性別]。  
  
11. 輸入 **="Unknown", "Tulips")**  
  
     完成的運算式為： `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. 再按一次 [確定]，關閉 [影像屬性] 對話方塊。  
  
14. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Lookup"></a> 5.查閱 CountryRegion 名稱  
 建立 CountryRegion 資料集並使用 **Lookup** 函數顯示國家/地區的名稱，而不使用國家/地區的識別碼。  
  
#### <a name="to-create-the-countryregion-dataset"></a>若要建立 CountryRegion 資料集  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，按一下 [新增]，然後按一下 [資料集]。  
  
3.  按一下 [使用內嵌在我的報表中的資料集]。  
  
4.  在 [資料來源] 清單中，選取 ExpressionsDataSource。  
  
5.  在 [名稱] 方塊中，鍵入 **CountryRegion**  
  
6.  驗證已選取 [文字] 查詢類型，並按一下 [查詢設計工具]。  
  
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
  
9. 按一下 **[執行]** \(**!**) 來執行查詢。  
  
     查詢結果為國家/地區識別碼和名稱。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 再按一次 [確定]，關閉 [資料集屬性] 對話方塊。  
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>若要查閱 CountryRegion 資料集中的值  
  
1.  按一下 [國家/地區 ID] 資料行標題，並刪除 ID 這兩個字。  
  
2.  以滑鼠右鍵按一下 [國家/地區] 資料行的資料格，然後按一下 [運算式]。  
  
3.  刪除運算式，但保留開頭的等號 (=)。  
  
     剩下的運算式為： `=`  
  
4.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [其他]。  
  
5.  在 [項目] 清單中，按兩下 [Lookup]。  
  
6.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
7.  在 **值**清單中，按兩下`CountryRegionID`。  
  
8.  如果游標不在 `CountryRegionID.Value` 的正後方，請將它放至該處。  
  
9. 刪除右括號，然後輸入 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**  
  
     完成的運算式為： `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     **Lookup** 函數的語法會在 CountryRegion 資料集中指定 CountryRegionID 與 ID 之間的查閱，而該資料集會傳回 CountryRegion 值，並在同一個資料集中包含此值。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 按一下 **[執行]** 預覽報表。  
  
##  <a name="Count"></a> 6.計算自上次購買後的日數  
 新增資料行，然後使用 **Now** 函數或 `ExecutionTime` 內建全域變數，計算某人自上次購買後至今的天數。  
  
#### <a name="to-add-the-days-ago-column"></a>若要加入 [天前] 資料行  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下 [上次購買] 資料行，指向 [插入資料行]，然後按一下 [右方]。  
  
     新資料行就會新增至 [上次購買] 資料行的右方。  
  
3.  在資料行標頭中，輸入 **天前**。  
  
4.  以滑鼠右鍵按一下 [天前] 資料行的資料格，然後按一下 [運算式]。  
  
5.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [日期和時間]。  
  
6.  在 [項目] 清單中，按兩下 [DateDiff]。  
  
7.  如果游標不在 `DateDiff(` 的正後方，請將它放至該處。  
  
8.  輸入 **"d",**  
  
9. 在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
10. 在 [值] 清單中，按兩下 **LastPurchase**。  
  
11. 如果游標不在 `Fields!LastPurchase.Value` 的正後方，請將它放至該處。  
  
12. 輸入 **,**  
  
13. 在 [類別清單] 中，再次按一下 [日期和時間]。  
  
14. 在 [項目] 清單中，按兩下 [Now]。  
  
    > [!WARNING]  
    >  在生產報表中，不應該在隨報表轉譯而評估多次的運算式中使用 **Now** 函數 (例如，報表的詳細資料列)。 **Now** 的值會依資料列而改變，而不同的值會影響運算式的評估結果，導致結果稍微不一致。 因此，您應該改用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供的 `ExecutionTime` 全域變數。  
  
15. 如果游標不在 `Now(` 的正後方，請將它放至該處。  
  
16. 刪除左括號，然後輸入 **)**  
  
     完成的運算式為： `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Indicator"></a> 7.使用指標顯示銷售比較  
 加入新的資料行，並使用指標顯示某人今年到目前 (YTD) 的購買為高於或低於平均 YTD 購買。 **Round** 函數會移除值的小數。  
  
 設定指標及其狀態需要進行許多步驟。 您可以先略過「設定指標」程序，再從本教學課程將完成的運算式複製/貼上至 [運算式] 對話方塊中。  
  
#### <a name="to-add-the--or---avg-sales-column"></a>若要加入平均銷售增減資料行  
  
1.  以滑鼠右鍵按一下 [YTD 購買] 資料行，指向 [插入資料行]，然後按一下 [右方]。  
  
     新資料行就會新增至 [YTD 購買] 資料行的右方。  
  
2.  按一下資料行的標題，並輸入**平均銷售增減**。  
  
#### <a name="to-add-an-indicator"></a>若要加入指標  
  
1.  在功能區的 [插入] 索引標籤上，按一下 [指標]，然後按一下 [平均銷售增減] 資料行的資料格。  
  
     [選取指標類型] 對話方塊隨即開啟。  
  
2.  在圖示集的 [方向性] 群組中，按一下三個灰色箭頭的圖示集。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>若要設定指標  
  
1.  以滑鼠右鍵按一下指標，按一下 [指標屬性]，然後按一下 [值和狀態]。  
  
2.  按一下 [值] 文字方塊旁邊的 [運算式 fx] 按鈕。  
  
3.  在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [數學]。  
  
4.  在 [項目] 清單中，按兩下 [Round]。  
  
5.  在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
6.  在 [值] 清單中，按兩下 **YTDPurchase**。  
  
7.  如果游標不在 `Fields!YTDPurchase.Value` 的正後方，請將它放至該處。  
  
8.  輸入 **-**  
  
9. 再次展開 [一般函數]，然後按一下 [彙總]。  
  
10. 在 [項目] 清單中，按兩下 [Avg]。  
  
11. 在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
12. 在 [值] 清單中，按兩下 **YTDPurchase**。  
  
13. 如果游標不在 `Fields!YTDPurchase.Value` 的正後方，請將它放至該處。  
  
14. 輸入 **, "Expressions"))**  
  
     完成的運算式為： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. 在 [狀態度量單位] 方塊中，選取 [數值]。  
  
17. 在具有向下鍵的資料列中，按一下 [開始] 值的文字方塊右邊的 **fx** 按鈕。  
  
18. 在 [運算式] 對話方塊中，展開 [一般函數]，並按一下 [數學]。  
  
19. 在 [項目] 清單中，按兩下 [Round]。  
  
20. 在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
21. 在 [值] 清單中，按兩下 **YTDPurchase**。  
  
22. 如果游標不在 `Fields!YTDPurchase.Value` 的正後方，請將它放至該處。  
  
23. 輸入 **-**  
  
24. 再次展開 [一般函數]，然後按一下 [彙總]。  
  
25. 在 [項目] 清單中，按兩下 [Avg]。  
  
26. 在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
27. 在 [值] 清單中，按兩下 **YTDPurchase**。  
  
28. 如果游標不在 `Fields!YTDPurchase.Value` 的正後方，請將它放至該處。  
  
29. 輸入 **, "Expressions")) < 0**  
  
     完成的運算式為： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. 在 [結束] 值的文字方塊中，輸入 **0**。  
  
32. 按一下具有橫向箭號的資料列，然後按一下 [刪除]。  
  
33. 在具有向上鍵的資料列中，於 [開始] 方塊中輸入 **0**。  
  
34. 按一下 [結束] 值的文字方塊右邊的 **fx** 按鈕。  
  
35. 在 **運算式**對話方塊方塊中，建立運算式： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. 再按一次 [確定]，關閉 [指標屬性] 對話方塊。  
  
38. 按一下 **[執行]** 預覽報表。  
  
##  <a name="GreenBar"></a> 8。製作「綠色橫條」的報表  
 使用參數指定套用至報表中交替資料列的色彩，使其變成橫條報表。  
  
#### <a name="to-add-a-parameter"></a>若要加入參數  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [參數]，然後按一下 [加入參數]。  
  
     **[報表參數屬性]** 對話方塊隨即開啟。  
  
3.  在 [提示] 中，鍵入**選擇色彩**  
  
4.  在 [名稱] 中，輸入 **RowColor**。  
  
5.  在左窗格中，按一下 [可用的值]。  
  
6.  按一下 [指定值]。  
  
7.  按一下 **[加入]**。  
  
8.  在 [標籤] 方塊中，輸入 **Yellow**。  
  
9. 在 [值] 方塊中，輸入 **Yellow**。  
  
10. 按一下 **[加入]**。  
  
11. 在 [標籤] 方塊中，鍵入 **Green**  
  
12. 在 [值] 方塊中，鍵入 **PaleGreen**  
  
13. 按一下 **[加入]**。  
  
14. 在 [標籤] 方塊中，鍵入 **Blue**  
  
15. 在 [值] 方塊中，鍵入 **LightBlue**  
  
16. 按一下 **[加入]**。  
  
17. 在 [標籤] 方塊中，鍵入 **Pink**  
  
18. 在 [值] 方塊中，輸入 **Pink**。  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>若要套用交替色彩至詳細資料列  
  
1.  按一下功能區上的 [檢視] 索引標籤，並確認已選取 [屬性]。  
  
2.  按一下 [名稱] 資料行的資料格，然後按 Shift 鍵。  
  
3.  逐一按下資料列中的其他資料格。  
  
4.  在 [屬性] 窗格中，按一下 **BackgroundColor**。  
  
     如果 [屬性] 窗格中依類別目錄列出屬性，您將會在 [填滿] 類別目錄底下找到 **BackgroundColor**。  
  
5.  按一下向下鍵，然後按一下 [運算式]。  
  
6.  在 [運算式] 對話方塊中，展開 [一般函數]，然後按一下 [程式流程]。  
  
7.  在 [項目] 清單中，按兩下 [IIf]。  
  
8.  展開 [一般函數]，然後按一下 [彙總]。  
  
9. 在 [項目] 清單中，按兩下 [RunningValue]。  
  
10. 在 [類別目錄] 清單中，按一下 [欄位 (運算式)]。  
  
11. 在 [值] 清單中，按兩下 **FirstName**。  
  
12. 如果游標不在 `Fields!FirstName.Value` 的正後方，請將它放至該處並輸入 **,**  
  
13. 展開 [一般函數]，然後按一下 [彙總]。  
  
14. 在 [項目] 清單中，按兩下 [Count]。  
  
15. 如果游標不在 `Count(` 的正後方，請將它放至該處。  
  
16. 刪除左括號，然後輸入 **,“Expressions”)**  
  
    > [!NOTE]  
    >  “Expressions” 是要在其中計算資料列的資料集名稱。  
  
17. 展開 [運算子] 並按一下 [算術]。  
  
18. 在 [項目] 清單中，按兩下 [Mod]。  
  
19. 如果游標不在 `Mod` 的正後方，請將它放至該處。  
  
20. 輸入 **2 =0,**  
  
    > [!IMPORTANT]  
    >  務必在輸入數字 2 之前加入一個空格。  
  
21. 按一下 [參數]，然後在 [值] 清單中按兩下 [RowColor]。  
  
22. 如果游標不在 `Parameters!RowColor.Value` 的正後方，請將它放至該處。  
  
23. 輸入 **, “White”)**  
  
     完成的運算式為： `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>執行報表  
  
1.  如果您不是在 [首頁] 索引標籤上，請按一下 [首頁] 返回設計檢視。  
  
2.  按一下 **[執行]**。  
  
3.  在 [選擇色彩] 下拉式清單中，選取報表上非白色橫條的色彩。  
  
4.  按一下 **[檢視報表]**。  
  
     報表隨即呈現，而且交替的資料列會使用您選擇的背景。  
  
##  <a name="DateFormat"></a> （選擇性）格式化日期資料行  
 格式化包含日期的 [上次購買] 資料行。  
  
#### <a name="to-format-date-column"></a>若要格式化日期資料行  
  
1.  按一下 **[設計]** 返回 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下 [上次購買] 資料行的資料格，然後按一下 [文字方塊屬性]。  
  
3.  在 [文字方塊屬性] 對話方塊中，依序按一下 [數字] 和 [日期]，然後輸入 **\*1/31/2000**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Title"></a> （選擇性）加入報表標題  
 加入報表的標題。  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入**銷售比較摘要**，然後按一下文字方塊外部。  
  
3.  以滑鼠右鍵按一下包含**銷售比較摘要**的文字方塊，然後按一下 [文字方塊屬性]。  
  
4.  在 [文字方塊屬性] 對話方塊中，按一下 [字型]。  
  
5.  在 [大小] 清單中，選取 [18pt]。  
  
6.  在 [色彩] 清單中，選取 [灰色]。  
  
7.  選取 [粗體] 和 [斜體]。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> （選擇性）儲存報表  
 您可以將報表儲存至報表伺服器、SharePoint 文件庫或您的電腦上。 如需詳細資訊，請參閱[儲存報表 &#40;報表產生器&#41;](report-builder/saving-reports-report-builder.md)。  
  
 本教學課程會將報表儲存至報表伺服器。 如果您沒有報表伺服器的存取權，請將報表儲存在您的電腦上。  
  
#### <a name="to-save-the-report-to-a-report-server"></a>若要將報表儲存至報表伺服器  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     「正在連接到報表伺服器」訊息隨即顯示。 連接完成時，您將會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 [名稱] 中，將預設名稱取代為**銷售比較摘要**。  
  
5.  按一下 **[儲存]**。  
  
 報表就會儲存至報表伺服器。 您連接之報表伺服器的名稱會顯示在視窗底部的狀態列中。  
  
#### <a name="to-save-the-report-to-your-computer"></a>若要將報表儲存到您的電腦上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **桌面`, `我的文件**，或**我的電腦**，然後瀏覽至您要儲存報表的資料夾。  
  
3.  在 [名稱] 中，將預設名稱取代為**銷售比較摘要**。  
  
4.  按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [指標&#40;報表產生器及 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [影像、 文字方塊、 矩形和線條&#40;報表產生器及 SSRS&#41;](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
