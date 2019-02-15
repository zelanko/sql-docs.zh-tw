---
title: 教學課程：地圖報表 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5522f24dbb7b930b69b2656f7c2c5b53954f16ca
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290916"
---
# <a name="tutorial-map-report-report-builder"></a>教學課程：地圖報表 (報表產生器)
  本教學課程的設計在於協助您了解，可對照地理背景顯示報告資料的地圖功能。  
  
 地圖是以空間資料為基礎，通常由點、線條和多邊形所組成。 例如，多邊行可表示某一縣的輪廓，線條可表示一條路，點則可表示城市的位置。 每一種空間資料會在不同的地圖圖層上顯示為一組地圖元素。  
  
 若要變化地圖元素的外觀，可以指定一個欄位，其中包含比對地圖元素與資料集中分析資料的值。 您也可以定義規則，使色彩、大小或其他屬性根據某個資料範圍變化。  
  
 在本教學課程中，您將建立地圖報表，用於顯示紐約州各郡的商店位置。  
  
##  <a name="BackToTop"></a> 您將了解  
 在本教學課程中，您將學習如何執行下列作業：  
  
1.  [建立含多邊形圖層，從地圖精靈地圖](#Map)  
  
2.  [加入地圖點圖層以顯示商店位置](#PointLayer)  
  
3.  [加入地圖線條圖層以顯示路線](#LineLayer)  
  
4.  [加入 Bing Maps 圖格背景](#TileLayer)  
  
5.  [使圖層變透明](#Transparent)  
  
6.  [變化郡的色彩，根據銷售](#Vary)  
  
    1.  [建立空間資料與分析資料之間的關聯性](#Relationship)  
  
    2.  [指定的多邊形色彩規則](#ColorRules)  
  
    3.  [在色階中的資料格式化為貨幣](#ColorScale)  
  
    4.  [建立新的圖例](#NewLegend)  
  
    5.  [關聯的圖例與色彩規則](#Associate)  
  
    6.  [清除不含資料的郡的色彩](#NoData)  
  
7.  [加入自訂點](#CustomPoint)  
  
8.  [地圖檢視置中](#CenterView)  
  
9. [加入報表標題](#Title)  
  
10. [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併成兩個程序：一個程序用來建立資料集，另一個程序用來建立資料表。 如需如何瀏覽至報表伺服器的逐步指示，選擇資料來源、 建立資料集，以及執行精靈，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表&#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Map"></a> 1.從地圖精靈建立含多邊形圖層的地圖  
 從地圖庫將地圖加入至報表。 地圖中包含一個顯示紐約州各郡的圖層。 各郡的形狀是以空間資料為基礎的多邊形，這些資料內嵌於地圖庫的地圖中。  
  
#### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>使用新報表中的地圖精靈加入地圖  
  
1.  按一下 [ **開始**]、依序指向 [ **程式集**] 和 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**]，然後按一下 [ **報表產生器**]。  
  
     [使用者入門] 對話方塊隨即出現。  
  
    > [!NOTE]  
    >  如果 [使用者入門] 對話方塊沒有出現，請從 [報表產生器] 按鈕按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[報表]** 。  
  
3.  在右窗格中，按一下 **[地圖精靈]**。  
  
4.  按一下 [建立] 。  
  
5.  在 **[選擇空間資料的來源]** 頁面中，確認已選取 **[地圖庫]** 。  
  
6.  在 [地圖庫] 窗格中，展開 **[USA]** 下的 **[依郡的州]**，然後按一下 **[紐約]**。  
  
     [地圖預覽] 窗格會顯示紐約郡的地圖。  
  
7.  按一下 [下一步] 。  
  
8.  接受 **[選擇空間資料及地圖檢視選項]** 頁面上的預設值。 根據預設，地圖庫中的地圖元素將自動內嵌在報表定義中。  
  
9. 按一下 [下一步] 。  
  
10. 在 **[選擇地圖視覺效果]** 頁面上，確認已選取 **[基本地圖]** ，然後按 **[下一步]**。  
  
11. 在 **[選擇色彩主題和資料視覺效果]** 頁面上，選取 **[顯示標籤]** 選項。  
  
12. 如果已經選取 **[單色地圖]** 選項，請清除該選項。  
  
13. 從 **[資料欄位]** 下拉式清單中，按一下 [#COUNTYNAME]。 精靈中的 [地圖預覽] 窗格會顯示下列項目：  
  
    -   包含 **地圖標題**文字的標題。  
  
    -   顯示紐約各郡的地圖，其中各郡都是不同的色彩，而且每次郡名稱符合郡區域時就會顯示出來。  
  
    -   包含標題以及項目 1 至 5 之清單的圖例。  
  
    -   包含值 0 到 160，而且沒有色彩的色階。  
  
    -   顯示公里 (km) 和英哩 (mi) 的距離標尺。  
  
14. 按一下 **[完成]**。  
  
     地圖就會加入至設計介面。  
  
15. 按一下地圖來選取它，然後顯示 **[地圖圖層]** 窗格。 **[地圖圖層]** 窗格會顯示一個 **[內嵌]** 圖層類型的多邊形圖層。 每個郡在此圖層上都是一個內嵌的地圖元素。  
  
    > [!NOTE]  
    >  如果看不到 **[地圖圖層]** 窗格，表示它可能在目前檢視之外顯示。 請使用 [設計檢視] 視窗底部的捲軸來切換檢視。 或者，在 **[檢視]** 索引標籤中，清除 **[屬性]** 或 **[報表資料]** 選項，即可提供更多設計介面區域。  
  
16. 以滑鼠右鍵按一下地圖標題，然後按一下 **[標題屬性]**。  
  
17. 將標題文字取代成 **依商店的銷售量**。  
  
18. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
19. 預覽報表。  
  
 呈現的報表會顯示地圖標題、地圖和距離標尺。 各郡會位於地圖多邊形圖層上。 每一個郡都是一個多邊形，其色彩會依色彩調色盤的色彩而變化，但是這些色彩不會與任何資料產生關聯。 距離標尺會同時以公里和英哩顯示距離。  
  
 地圖圖例和色階因為沒有與各郡相關聯的分析資料，因此不會顯示。 您稍後將在本教學課程中加入分析資料。  
  
##  <a name="PointLayer"></a> 2.加入地圖點圖層以顯示商店位置  
 使用地圖圖層精靈加入點圖層，用於顯示商店的位置。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>根據 SQL Server 空間查詢加入點圖層  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 [新增圖層精靈] 按鈕 ![rs_IconMapLayerWizard](../../2014/tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")。  
  
3.  在 **[選擇空間資料的來源]** 頁面上，選取 **[SQL Server 空間查詢]**，然後按 **[下一步]**。  
  
4.  在 **[選擇含有 SQL Server 空間資料的資料集]** 頁面上，按一下 **[新增含有 SQL Server 空間資料的資料集]**，然後按 **[下一步]**。  
  
5.  在 **[選擇到 SQL Server 空間資料來源的連接]** 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源。  
  
6.  按一下 [下一步] 。  
  
7.  在 [設計查詢] 頁面上，按一下 **[當成文字編輯]**。  
  
8.  在 [查詢] 窗格中，貼上下列文字：  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Rochester No.2 Store' as StoreName, 700 as SellingArea, 'Rochester' as City, 'Monroe' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-77.6240415667866 43.1547066024338)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. 在查詢設計工具工具列上，按一下 **[執行]** \(**!**)。  
  
     結果集會顯示七個資料行：StoreKey、 StoreName、 SellingArea、 City、 郡、 銷售和 SpatialLocation。 此資料表示在紐約州中販賣消費品的商店集。 結果集中的每個資料列都包含一個商店識別碼、商店名稱、可用於產品展示的區域、商店所在的城市和郡、銷售總額，以及經緯度的空間位置。 展示區域的範圍是從 455 平方英尺到 1125 平方英尺。  
  
10. 按一下 [下一步] 。  
  
     此時會為您建立名為 DataSet1 的報表資料集。 在完成精靈後，可以使用 [報表資料] 來檢視其欄位集合。  
  
11. 在 **選擇空間資料及地圖檢視選項**頁面上，確認**空間欄位**是`SpatialLocation`且**圖層類型**是**點**. 接受此頁面上的其他預設值。  
  
     地圖檢視會顯示圓形，這些圓形會標示每一家商店的位置。  
  
12. 按一下 [下一步] 。  
  
13. 指定地圖類型，此地圖會顯示依分析資料更改的標記。 在 [選擇地圖視覺效果] 頁面上，按一下 **[分析標記地圖]**，然後按 **[下一步]**。  
  
14. 在 **[選擇分析資料集]** 頁面上，按一下 DataSet1。 此資料集同時包含將在新的點圖層上顯示的分析資料和空間資料。  
  
15. 按一下 [下一步] 。  
  
16. 在 **[選擇色彩主題和資料視覺效果]** 頁面上，清除 **[使用標記色彩將資料視覺化]** 選項，然後選取 **[使用標記類型將資料視覺化]** 選項。  
  
17. 在 **[資料欄位]** 中選取 `[Sum(SellingArea)]` ，讓標記類型依據保留用於顯示產品的區域大小變化。  
  
18. 按一下 **[完成]**。  
  
     地圖圖層會加入至報表。 圖例會根據 SellingArea 值顯示標記類型。  
  
     按兩下地圖來顯示 **[地圖圖層]** 窗格。 **[地圖圖層]** 窗格會顯示一個新圖層 PointLayer1，其空間資料來源類型為 **DataRegion**。  
  
19. 加入圖例標題。 以滑鼠右鍵按一下圖例標題，然後按一下 **[圖例標題屬性]**。  
  
20. 刪除標題，然後輸入 **顯示區域 (平方英尺)**。  
  
21. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
22. 檢視精靈設定的預設值。 在 **[地圖圖層]** 窗格中，以滑鼠右鍵按一下點圖層，然後按一下 **[標記類型規則]**。  
  
     在 **[一般]** 索引標籤上，標記會依照出現在圖例中的順序列出。 在 **[分佈]** 索引標籤上，子範圍的數目為 5。 在 **[圖例]** 索引標籤上，圖例文字會設為顯示每個範圍的開始和結束值。  
  
23. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. 預覽報表。  
  
 地圖會顯示紐約州商店的位置。 每家商店的標記類型是根據顯示區域而定。 有五種顯示區域範圍會自動計算。  
  
##  <a name="LineLayer"></a> 3.加入地圖線條圖層以顯示路線  
 使用地圖圖層精靈，加入顯示兩個商店之間路線的地圖圖層。 在本教學課程中，路徑是從三個商店位置建立。 在商業應用程式中，路徑可能是商店之間的最佳路線。  
  
#### <a name="to-add-a-line-layer-to-map"></a>將線條圖層加入至地圖  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 **[新增圖層精靈]**。  
  
3.  在 **[選擇空間資料的來源]** 頁面上，選取 **[SQL Server 空間查詢]** ，然後按 **[下一步]**。  
  
4.  在 **[選擇含有 SQL Server 空間資料的資料集]** 頁面上，按一下 **[新增含有 SQL Server 空間資料的資料集]** ，然後按 **[下一步]**。  
  
5.  在 **[選擇到 SQL Server 空間資料來源的連接]** 上，選取 [DataSource1]，也就是您在第一個程序中建立的資料來源。  
  
6.  按一下 [下一步] 。  
  
7.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。 查詢設計工具會切換為以文字為基礎的模式。  
  
8.  在 [查詢] 窗格中，貼上下列文字：  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. 按一下 [下一步] 。  
  
     路徑會出現在地圖上，並且連接三家商店。  
  
10. 在 **[選擇空間資料及地圖檢視選項]** 頁面上，確認 **[空間欄位]** 為 **[路線]** ，而 **[圖層類型]** 為 **[線條]**。 接受其他預設值。  
  
     地圖檢視會顯示從紐約州北部某家商店到紐約州南部某家商店的路徑。  
  
11. 按一下 [下一步] 。  
  
12. 在 **[選擇地圖視覺效果]** 頁面上，按一下 **[基本線條地圖]**，然後按 **[下一步]**。  
  
13. 在 **[選擇色彩主題和資料視覺效果]** 上，選取 **[單一色彩地圖]** 選項。 路徑會根據所選主題的單一色彩顯示。  
  
14. 按一下 **[完成]**。  
  
 地圖會顯示新的線條圖層，其空間資料來源類型為 **DataSet**。 在此範例中，空間資料來自資料集，但是分析資料與線條沒有產生關聯。  
  
##  <a name="TileLayer"></a> 4.加入 Bing Maps 圖格背景  
 加入顯示 Bing Maps 圖格背景的地圖圖層。  
  
#### <a name="to-add-a-virtual-earth-tile-background"></a>加入虛擬地球圖格背景  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下**加入圖層**![rs_IconMapAddLayer](../../2014/tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")。  
  
3.  從下拉式清單中，按一下 **[圖格圖層]**。  
  
     **[地圖圖層]** 窗格中的最後一個圖層是 TileLayer1。 根據預設，影像分割圖層會顯示路段圖樣式。  
  
    > [!NOTE]  
    >  您也可以在精靈中的 **[選擇空間資料及地圖檢視選項]** 頁面上加入圖格圖層。 若要執行這項操作，請選取 **[加入此地圖檢是的 Bing Maps 背景]**。 在呈現的報表中，圖格背景會顯示目前地圖檢視區置中與縮放層級的 Bing Maps 圖格。  
  
4.  按一下 TileLayer1 上的向下箭頭，然後按一下 **[影像分割屬性]**。  
  
5.  在 **[類型]** 中，選取 **[空照圖]**。 空照圖檢視不包含文字。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Transparent"></a> 5.使圖層變透明  
 若要讓某一個圖層上的項目透過另一個圖層顯示，您可以調整圖層的順序以及各圖層的透明度，以獲得需要的效果。  
  
#### <a name="to-set-the-transparency-of-a-layer"></a>設定圖層的透明度  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。  
  
3.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[圖層資料]**。 **[地圖多邊形圖層屬性]** 對話方塊隨即開啟。  
  
4.  按一下 **[可見性]**。  
  
5.  在 **[透明度 (%)]** 中，輸入 **30**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 設計介面會將郡顯示為半透明。  
  
##  <a name="Vary"></a> 6.依據銷售量變化郡的色彩  
 多邊形圖層上的每個郡都有不同的色彩，因為報表處理器會自動根據您在地圖精靈最後一頁上選擇的主題，指派色彩調色盤中的色彩值。  
  
 在下列的步驟中，指定一個色彩規則，讓特定色彩與每個郡的商店銷售額範圍產生關聯。 紅色、黃色、綠色分別表示相對的高、中、低銷售額。 格式化色階來顯示貨幣。 在新的圖例中顯示年度銷售額範圍。 對於未包含商店的郡，不使用色彩則表示沒有相關聯的資料。  
  
###  <a name="Relationship"></a> 6a. 建立空間資料與分析資料之間的關聯性  
 若要根據分析資料的色彩變化郡的形狀，您必須先讓分析資料與空間資料產生關聯。 在本教學課程中，您將使用郡名稱進行比對。  
  
##### <a name="to-build-a-relationship-between-spatial-data-and-analytical-data"></a>建立空間資料與分析資料間的關聯性  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。  
  
3.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[圖層資料]**。 **[地圖多邊形圖層屬性]** 對話方塊隨即開啟。  
  
4.  按一下 **[分析資料]**。  
  
5.  從下拉式清單中選取 DataSet1。 當您為各郡指定空間資料查詢時，精靈就會建立此資料集。  
  
6.  在 **[要比對的欄位]** 中，按一下 **[加入]**。 新的資料列隨即加入。  
  
7.  在 **[從空間資料集]** 的下拉式清單中，按一下 [COUNTYNAME]。  
  
8.  在 **[從分析資料集]** 的下拉式清單中，按一下 [郡]。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 預覽報表。  
  
 透過指定空間資料來源和分析資料集中的比對欄位，就可以讓報表處理器根據地圖元素為分析資料分組。 資料繫結的地圖元素擁有與您所指定值比對成功的項目。  
  
 每一個有商店的郡所使用的色彩，都是依據您在精靈中所選擇樣式的調色盤而定。  
  
###  <a name="ColorRules"></a> 6b. 指定多邊形的色彩規則  
 若要建立讓各郡的色彩隨商店銷售額變化的規則，您必須指定範圍值、該範圍中要顯示的區間數目，以及要使用的色彩。  
  
##### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>為所有擁有相關資料的多邊形指定色彩規則  
  
1.  切換至 [設計] 檢視。  
  
2.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[多邊形色彩規則]**。 **[地圖色彩規則屬性]** 對話方塊隨即開啟。 您會發現已選取 **[使用調色盤將資料視覺化]** 色彩規則選項。 此選項是由精靈設定。  
  
3.  選取 **[使用色彩範圍將資料視覺化]**。 開始色彩、中間色彩和結束色彩選項會取代調色盤選項。  
  
4.  定義每個郡銷售額的範圍值。 從 **[資料欄位]** 的下拉式清單中，選取 [ `[Sum(Sales)]`]。  
  
5.  若要改變格式，以千為單位顯示貨幣，則將運算式變更如下： `=Sum(Fields!Sales.Value)/1000`  
  
6.  將 **[開始色彩]** 變更為 **[紅色]**。  
  
7.  將 **[結束色彩]** 變更為 **[綠色]**。  
  
     **[紅色]** 表示低銷售值、 **[黃色]** 表示中銷售值，而 **[綠色]** 表示高銷售值。 報表處理器會根據這些值以及您在 **[分佈]** 頁面上選擇的選項，計算色彩範圍。  
  
8.  按一下 **[分佈]**。  
  
9. 請確認分佈類型為 **[最佳]**。 針對步驟 5 中的運算式，最佳分佈會將值分割成子範圍，這些子範圍會讓每個範圍中的項目數目和每個範圍的涵蓋範圍。  
  
10. 接受此頁面上其他選項的預設值。 如果您選取最佳分佈類型，則報表執行時，會計算子範圍的數目。  
  
11. 按一下 **[圖例]**。  
  
12. 在 **[色階選項]** 中，確認已選取 **[在色階中顯示]** 。  
  
13. 在 **[在此圖例中顯示]** 的下拉式清單中，選取空行。 現在您只能以色階顯示色彩範圍。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 色階會顯示五種色彩：紅色、橙色、黃色、黃綠色與綠色。 每一種色彩都代表一個銷售額範圍，該範圍是根據各郡的銷售額自動計算。  
  
###  <a name="ColorScale"></a> 6c. 依據貨幣格式化色階中的資料  
 根據預設，資料會使用一般格式。 您可以套用自訂格式。  
  
##### <a name="to-set-the-format-for-the-color-scale"></a>設定色階的格式  
  
1.  以滑鼠右鍵按一下色階，然後按一下 **[色階屬性]**。  
  
2.  按一下 **[數值]**。  
  
3.  在 **[類別目錄]** 中，按一下 **[貨幣]**。  
  
4.  在 **[小數位數]** 中，輸入 **0**。 此格式會指定貨幣不要有小數位數。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  預覽報表。  
  
 色階會以每個範圍的貨幣格式顯示年度銷售額。  
  
###  <a name="NewLegend"></a> 6d. 建立新的圖例  
 根據預設，所有規則都會在第一個圖例中顯示。 若要改善地圖的顯示效果，可以加入圖例。  
  
 若要改變預設顯示，可以執行兩個步驟：建立新的圖例，然後將地圖圖層的規則結果與新圖例產生關聯。  
  
##### <a name="to-create-a-new-legend"></a>建立新的圖例  
  
1.  切換至 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下檢視區外部的地圖，然後按一下 **[加入圖例]**。 新圖例會加入地圖的預設位置。  
  
3.  以滑鼠右鍵按一下圖例，然後按一下 **[圖例屬性]**。  
  
4.  在 **[位置選項]** 中，按一下指定您要讓圖例顯示在檢視區的相對位置。 設計介面上的地圖會變更，以顯示您選項的效果。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  按一下圖例上的 **[影像分割]** 來選取圖例標題。  
  
7.  再按一下 **[影像分割]** 以進入文字的插入模式。 將 **[標題]** 取代成 **[銷售額 (千)]**，然後按一下文字外部。  
  
 圖例會展開以顯示標題。  
  
###  <a name="Associate"></a> 6e。 讓圖例與色彩規則產生關聯  
 每個圖例都可以顯示一或多組規則結果。  
  
##### <a name="to-associate-a-legend-with-color-rules"></a>讓圖例與色彩規則產生關聯  
  
1.  按兩下地圖來顯示 **[地圖圖層]** 窗格。  
  
2.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[多邊形色彩規則]**。 **[地圖色彩規則屬性]** 對話方塊隨即開啟。  
  
3.  按一下 **[圖例]**。  
  
4.  在 **[色階選項]** 中，清除 **[以色階顯示]**。  
  
5.  在 **[圖例選項]** 的下拉式清單中，選取 [Legend2]。 圖例文字選項隨即出現。 根據預設，圖例文字是以一般 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 格式字串格式化。 N0 中的 0 會指定不使用小數位數。  
  
6.  在 **圖例文字**，使用下列格式來指定沒有小數位數的貨幣： `#FROMVALUE {C0} - #TOVALUE {C0}`  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     在設計介面上，圖例會顯示色彩範圍，其中範例資料會格式化為貨幣。  
  
8.  預覽報表。  
  
 與商店和銷售額相關聯的郡會依據色彩規則顯示。 沒有銷售額的郡則不會顯示任何色彩。  
  
###  <a name="NoData"></a> 6f。 變更未包含資料之郡的色彩  
 您可以針對圖層上的所有地圖元素設定預設顯示選項。 色彩規則的優先順序高於這些顯示選項。  
  
##### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>設定圖層上所有元素的顯示屬性  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。  
  
3.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[多邊形屬性]**。 **[地圖多邊形屬性]** 對話方塊隨即開啟。 此對話方塊中設定的顯示選項會先套用至圖層上的所有多邊形，然後才會套用規則為主的顯示選項。  
  
4.  按一下 **[填滿]**。  
  
5.  確認填滿樣式是**純色。** 漸層和模式會套用至所有色彩。  
  
6.  在 **[色彩]** 中，按一下向下箭頭，然後按一下 **[淺鋼青]**。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  預覽報表。  
  
 沒有相關資料的郡會顯示為藍色。 只有包含相關分析資料的郡會以您所指定色彩規則中的 **[紅色]** 到 **[綠色]** 色彩顯示。  
  
##  <a name="CustomPoint"></a> 7.加入自訂點  
 若要表示尚未建立的新商店，請指定一個點並使用 **[圖釘]** 標記類型。  
  
#### <a name="to-add-a-custom-point"></a>加入自訂點  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 **[加入圖層]**，然後按一下 **[點圖層]**。  
  
     新的點圖層便會加入至地圖中。 根據預設，點圖層的空間資料類型為 **[內嵌]**。  
  
3.  按一下 PointLayer2 上的向下箭頭，然後按一下 **[加入點]**。  
  
4.  將指標移到地圖檢視區上。 游標會變更為十字形狀。  
  
5.  按一下地圖上您要加入點的位置。 在此教學課程中，按一下某一個郡中路線開始處旁邊的位置。 以圓形標示的點就會加入至圖層中您所按的位置。 根據預設，系統會選取點。  
  
6.  以滑鼠右鍵按一下您加入的點，然後按一下 **[內嵌點屬性]**。  
  
7.  選取 **[覆寫此圖層的點選項]** 選項。 對話方塊中會出現一個額外的頁面。 您在此處設定的值，其優先順序高於圖層或色彩規則的顯示選項。  
  
8.  按一下 **[標記]**。  
  
9. 選取 **[星形]** 做為 **[標記類型]**。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 預覽報表。  
  
 您加入的新點會以 **[星形]** 顯示。  
  
#### <a name="to-add-a-label-for-the-custom-point"></a>加入自訂點的標籤  
  
1.  切換至 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下您剛加入的點，然後按一下 **[內嵌點屬性]**。  
  
3.  按一下 **[標籤]**。  
  
4.  在 **[標籤文字]** 中，輸入 **新商店**。  
  
5.  在 **[位置]** 中，按一下 **[上方]**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  預覽報表。  
  
 標籤會出現在商店位置上方。  
  
##  <a name="CenterView"></a> 地圖檢視置中  
 變更地圖檢視區的置中與縮放層級。  
  
#### <a name="to-change-the-viewport"></a>變更檢視區  
  
1.  以滑鼠右鍵按一下地圖檢視區，然後按一下 **[檢視區屬性]**。  
  
2.  按一下 **[置中與縮放]**。  
  
3.  確認已選取 **[設定檢視置中與縮放層級]** 選項。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  以滑鼠左鍵按一下地圖檢視區，然後將檢視區的中央拖曳至需要的位置。  
  
6.  使用滑鼠滾輪變更檢視區的縮放層級。  
  
7.  預覽報表。  
  
 在 [設計] 檢視中，顯示介面和檢視上的地圖是以範例資料為基礎。 在呈現的報表中，地圖檢視會在您指定的檢視上置中。  
  
##  <a name="Title"></a> 加入報表標題  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **紐約商店的銷售額** ，然後按一下文字方塊外部。  
  
 這個標題就會顯示在報表的頂端。 沒有定義任何頁首時，位於報表主體頂端的項目就相當於報表頁首。  
  
##  <a name="Save"></a> 儲存報表  
  
#### <a name="to-save-the-report"></a>若要儲存報表  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表產生器] 按鈕中，按一下 **[另存新檔]**。  
  
3.  在 **[名稱]** 中輸入 **紐約的商店銷售額**。  
  
 按一下 [儲存] 。  
  
## <a name="next-steps"></a>後續步驟  
 以上總結如何將地圖加入至報表的逐步解說。  
  
 如需詳細資訊，請參閱 < [Maps&#40;報表產生器及 SSRS&#41; ](report-design/maps-report-builder-and-ssrs.md)和 部落格文章[製圖調整空間資料的 SQL Server Reporting services](https://go.microsoft.com/fwlink/?LinkId=152771) blogs.msdn.com 上。  
  
 如需教學課程，請參閱[教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)   
 [地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
