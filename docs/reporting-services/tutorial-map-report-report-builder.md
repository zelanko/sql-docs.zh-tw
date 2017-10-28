---
title: "教學課程： 地圖報表 （報表產生器） |Microsoft 文件"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: efe91a2e1e8ca7b0744639ed718d63b70e3adc5c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-map-report-report-builder"></a>教學課程：地圖報表 (報表產生器)
在此 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] 教學課程中，您會了解在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分頁報表的地理背景上，可用來顯示資料的地圖功能。 
  
地圖是以空間資料為基礎，通常由點、線條和多邊形所組成。 例如，多邊行可表示某一縣的輪廓，線條可表示一條路，點則可表示城市的位置。 每一種空間資料會在不同的地圖圖層上顯示為一組地圖元素。  
  
若要變化地圖元素的外觀，可以指定一個欄位，其中包含比對地圖元素與資料集中分析資料的值。 您也可以定義規則，使色彩、大小或其他屬性根據某個資料範圍變化。  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
在本教學課程中，您將建立地圖報表，用於顯示紐約州各郡的商店位置。  
   
> [!NOTE]  
> 在本教學課程中，精靈的步驟會合併成兩個程序：一個程序用來建立資料集，另一個程序用來建立資料表。 如需如何瀏覽至報表伺服器、選擇資料來源、建立資料集以及執行精靈的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
完成本教學課程的估計時間：30 分鐘。  
  
## <a name="requirements"></a>需求  
針對本教學課程，報表伺服器必須設定為支援 Bing Maps 作為背景。 如需詳細資訊，請參閱[對應報表支援規劃](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)。 

如需其他需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Map"></a>1.從地圖精靈建立含多邊形圖層的地圖  
在本節中，您會從地圖庫將地圖新增至報表。 地圖中包含一個顯示紐約州各郡的圖層。 各郡的形狀是以空間資料為基礎的多邊形，這些資料內嵌於地圖庫的地圖中。  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>使用新報表中的地圖精靈加入地圖  
  
1.  從您的電腦、[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 入口網站或 SharePoint 整合模式[啟動報表產生器](../reporting-services/report-builder/start-report-builder.md)。  
  
    [新報表或資料集] 對話方塊隨即開啟。  
  
    如果未顯示 [新報表或資料集] 對話方塊，請按一下 [檔案] 功能表 > [新增]。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中，按一下 **[地圖精靈]**。  
  
4.  在 [選擇空間資料的來源] 頁面上，確認已選取 [地圖庫]。  
  
6.  在 [地圖庫] 方塊中，展開 [USA] 下的 [依郡的州]，然後按一下 [紐約]。  
  
    [地圖預覽] 窗格會顯示紐約郡的地圖。  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  按一下 **[下一步]**。  
  
8.  接受 [選擇空間資料及地圖檢視選項] 頁面上的預設值，然後按一下 [下一步]。 
 
    根據預設，地圖庫中的地圖元素會自動內嵌在報表定義中。  
  
9. 在 **[選擇地圖視覺效果]** 頁面上，確認已選取 **[基本地圖]** ，然後按 **[下一步]**。  
  
11. 在 **[選擇色彩主題和資料視覺效果]** 頁面上，選取 **[顯示標籤]** 選項。  
  
12. 如果已經選取 **[單色地圖]** 選項，請清除該選項。  
  
13. 從 [資料欄位] 下拉式清單中，按一下 [#COUNTYNAME]。 精靈中的 [地圖預覽] 窗格會顯示下列項目：  
  
    -   包含 **地圖標題**文字的標題。  
  
    -   顯示紐約各郡的地圖，其中各郡都是不同的色彩，而且每次郡名稱符合郡區域時就會顯示出來。  
  
    -   包含標題以及項目 1 至 5 之清單的圖例。  
  
    -   包含值 0 到 160，而且沒有色彩的色階。  
  
    -   顯示公里 (km) 和英哩 (mi) 的距離標尺。  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. 按一下 **[完成]**。  
  
    地圖就會加入至設計介面。  
  
13. 選取 [地圖標題] 文字，然後輸入 [依商店的銷售額)] > ENTER。  

15. 按兩下地圖來顯示 [地圖圖層] 窗格。 [地圖圖層] 窗格會顯示一個 [內嵌] 圖層類型的多邊形圖層 PolygonLayer1。 每個郡在此圖層上都是一個內嵌的地圖元素。  
  
    > [!NOTE]  
    > 如果看不到 [地圖圖層] 窗格，表示它可能在目前檢視之外顯示。 請使用 [設計檢視] 視窗底部的捲軸來切換檢視。 或者，在 [檢視] 索引標籤中，清除 [報表資料] 選項，即可提供更多設計介面區域。   

15. 選取 PolygonLayer1 旁的箭號 > [多邊形屬性]。

16. 在 [字型] 索引標籤上，將色彩變更為 [暗灰]。

17. 在 [首頁] 索引標籤上 > [執行] 預覽報表。  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
呈現的報表會顯示地圖標題、地圖和距離標尺。 各郡會位於地圖多邊形圖層上。 每一個郡都是一個多邊形，其色彩會依色彩調色盤的色彩而變化，但是這些色彩不會與任何資料產生關聯。 距離標尺會同時以公里和英哩顯示距離。  
  
地圖圖例和色階因為沒有與各郡相關聯的分析資料，因此不會顯示。 您稍後將在本教學課程中加入分析資料。  
  
## <a name="PointLayer"></a>2.加入地圖點圖層以顯示商店位置  
在本節中，您會使用地圖圖層精靈新增點圖層，用於顯示商店的位置。  
  
> [!NOTE]  
> 在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>根據 SQL Server 空間查詢加入點圖層  
  
1.  在 [執行] 索引標籤 > [設計]，切換回 [設計] 檢視。  
  
2.  按兩下地圖來顯示 [地圖圖層] 窗格。 在工具列上，按一下 **新增圖層精靈**按鈕![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")。 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  在 **[選擇空間資料的來源]** 頁面上，選取 **[SQL Server 空間查詢]**，然後按 **[下一步]**。  
  
4.  在 **[選擇含有 SQL Server 空間資料的資料集]** 頁面上，按一下 **[新增含有 SQL Server 空間資料的資料集]** > **[下一步]**。  
  
5.  在 **[選擇到 SQL Server 空間資料來源的連接]** 頁面上，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源。  

    > [!NOTE]  
    > 只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[取得資料連接的替代方式 &#40;報表產生器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  按一下 **[下一步]**。  
  
7.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
8.  複製下列文字並貼到 [查詢] 窗格：  
  
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
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. 在查詢設計工具工具列上，按一下 [執行] (**!**)。  
  
    結果集包含七個資料行，代表一組販賣消費品的紐約州商店。 以下是清單，以及對於較不明顯者的說明︰ 
    *   **StoreKey**︰商店識別碼。  
    *   **StoreName**。
    *   **SellingArea**︰可用於產品展示的區域，範圍是從 455 平方英尺到 1125 平方英尺。
    *   **City**。
    *   **County**。
    *   **Sales**：總銷售額。 
    *   **SpatialLocation**︰經度和緯度位置。 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. 按一下 **[下一步]**。  
  
    此時會為您建立名為 DataSet1 的報表資料集。 在完成精靈後，可以在 [報表資料] 窗格看到其欄位集合。  
  
11. 在 **[選擇空間資料及地圖檢視選項]** 頁面上，確認 **[空間欄位]** 為 **[SpatialLocation]** ，而 **[圖層類型]** 為 **[點]**。 接受此頁面上的其他預設值。  
  
    地圖檢視會顯示圓形，以標示每一家商店的位置。  
  
12. 按一下 **[下一步]**。  
  
13. 在 [選擇地圖視覺效果] 頁面上，針對地圖類型按一下 [泡泡地圖]，它會根據資料顯示大小不同的標記。 按一下 **[下一步]**。  
  
14. 在 [選擇分析資料集] 頁面上，按一下 DataSet1，然後按一下 [下一步]。 此資料集同時包含將在新的點圖層上顯示的分析資料和空間資料。   
  
16. 在 [選擇色彩主題和資料視覺效果] 頁面上，選取 [使用泡泡大小將資料視覺化]。  
  
17. 在 [資料欄位]中選取 `[Sum(SellingArea)]`，讓泡泡大小依據保留用於顯示產品的區域大小變化。  
  
18. 選取 [顯示標籤]，並在 [資料欄位] 中選取 `[City]`。

18. 按一下 **[完成]**。  
  
    地圖圖層會加入至報表。 圖例會根據 SellingArea 值顯示泡泡大小。  
  
 19. 按兩下地圖來顯示 [地圖圖層] 窗格。 **[地圖圖層]** 窗格會顯示一個新圖層 PointLayer1，其空間資料來源類型為 **DataRegion**。  
  
19. 加入圖例標題。 在圖例中，選取文字 [標題]、輸入 [顯示區域 (平方英尺)]，然後按 ENTER。  
  
21. 在 [地圖圖層] 窗格中，按一下 PointLayer1 旁的箭號，然後按一下 [點內容]。  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. 在 [字型] 索引標籤上，將樣式設為 [粗體]、大小設為 [10pt]。

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. 在 [一般] 索引標籤上，針對 [放置] 選取 [下]。

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. 按一下 **[執行]** 預覽報表。  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    地圖會顯示紐約州商店的位置。 每家商店的標記大小是根據顯示區域而定。 有五種顯示區域範圍會自動計算。


  
## <a name="LineLayer"></a>3.加入地圖線條圖層以顯示路線  
使用地圖圖層精靈，加入顯示兩個商店之間路線的地圖圖層。 在本教學課程中，路徑是從三個商店位置建立。 在商業應用程式中，路徑可能是商店之間的最佳路線。  
  
### <a name="to-add-a-line-layer-to-map"></a>將線條圖層加入至地圖  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 **新增圖層精靈**按鈕![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")。  
  
3.  在 **[選擇空間資料的來源]** 頁面上，選取 **[SQL Server 空間查詢]** ，然後按 **[下一步]**。  
  
4.  在 **[選擇含有 SQL Server 空間資料的資料集]** 頁面上，按一下 **[新增含有 SQL Server 空間資料的資料集]** ，然後按 **[下一步]**。  
  
5.  在 [選擇到 SQL Server 空間資料來源的連接] 上，選取您在第一個程序中使用的資料來源。  
  
6.  按一下 **[下一步]**。  
  
7.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。 查詢設計工具會切換為以文字為基礎的模式。  
  
8.  在 [查詢] 窗格中，貼上下列文字：  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. 按一下 **[下一步]**。  
  
    路徑會出現在地圖上，並且連接三家商店。  
  
10. 在 **[選擇空間資料及地圖檢視選項]** 頁面上，確認 **[空間欄位]** 為 **[路線]** ，而 **[圖層類型]** 為 **[線條]**。 接受其他預設值。  
  
    地圖檢視會顯示從紐約州北部某家商店到紐約州南部某家商店的路徑。  
  
11. 按一下 **[下一步]**。  
  
12. 在 **[選擇地圖視覺效果]** 頁面上，按一下 **[基本線條地圖]**，然後按 **[下一步]**。  
  
13. 在 **[選擇色彩主題和資料視覺效果]**上，選取 **[單一色彩地圖]**選項。 路徑會根據所選主題的單一色彩顯示。  
  
14. 按一下 **[完成]**。  

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     地圖會顯示新的線條圖層，其空間資料來源類型為 **DataRegion**。 在此範例中，空間資料來自資料集，但是分析資料與線條沒有產生關聯。  

## <a name="adjust-the-zoom"></a>調整顯示比例
1. 如果您無法看到整個紐約州，可以調整顯示比例。 在選取地圖的情況下，在 [屬性] 窗格中您會看到 **MapViewport** 屬性。 

15. 展開 [檢視] 區段，然後展開 [檢視] 以便您可以看到 **Zoom** 屬性。 將它設為 [125]。 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      這是縮放百分比。 在 125%，您會看到完整的州。
  
## <a name="TileLayer"></a>4.加入 Bing Maps 圖格背景  
在本節中，您會新增顯示 Bing Maps 圖格背景的地圖圖層。  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 **加入圖層** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")。  
  
3.  從下拉式清單中，按一下 **[圖格圖層]**。  
  
    **[地圖圖層]** 窗格中的最後一個圖層是 TileLayer1。 根據預設，影像分割圖層會顯示路段圖樣式。  
  
    > [!NOTE]  
    > 您也可以在精靈中的 **[選擇空間資料及地圖檢視選項]** 頁面上加入圖格圖層。 若要執行這項操作，請選取 **[加入此地圖檢是的 Bing Maps 背景]**。 在呈現的報表中，圖格背景會顯示目前地圖檢視區置中與縮放層級的 Bing Maps 圖格。  
  
4.  按一下 TileLayer1 旁的箭號 > [圖格屬性]。  
  
5.  在 [一般] 索引標籤的 [類型] 下，選取 [空照圖]。 空照圖檢視不包含文字。  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5.使圖層變透明  
在本節中，若要讓某一個圖層上的項目透過另一個圖層顯示，您可以調整圖層的順序以及透明度，以獲得需要的效果。 請從您建立的第一個圖層 PolygonLayer1 開始。 
  
1.  按兩下地圖來顯示 [地圖圖層] 窗格。  
  
3.  按一下 PolygonLayer1 旁的箭號 > [圖層資料]。 **[地圖多邊形圖層屬性]** 對話方塊隨即開啟。  
  
4.  在 [可見性] 索引標籤的 [透明度 (百分比)] 下，輸入 **30**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     設計介面會將郡顯示為半透明。  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6.依據銷售量變化郡的色彩  
多邊形圖層上的每個郡都有不同的色彩，因為報表處理器會自動根據您在地圖精靈最後一頁上選擇的主題，指派色彩調色盤中的色彩值。  
  
在本節中，您會指定一個色彩規則，讓特定色彩與每個郡的商店銷售額範圍產生關聯。 紅色、黃色、綠色分別表示相對的高、中、低銷售額。 格式化色階來顯示貨幣。 在新的圖例中顯示年度銷售額範圍。 對於未包含商店的郡，不使用色彩則表示沒有相關聯的資料。  
  
### <a name="Relationship"></a>6a. 建立空間資料與分析資料之間的關聯性  
若要根據分析資料的色彩變化郡的形狀，您需要先讓分析資料與空間資料產生關聯。 在本教學課程中，您將使用郡名稱進行比對。 
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 [地圖圖層] 窗格。  
  
3.  按一下 PolygonLayer1 旁的箭號，然後按一下 [圖層資料]。 **[地圖多邊形圖層屬性]** 對話方塊隨即開啟。  
  
4.  在 [分析資料] 索引標籤的 [分析資料集] 下，選取 DataSet1。 當您為各郡建立空間資料查詢時，精靈就會建立此資料集。  
  
6.  在 [要比對的欄位] 下，按一下 [新增]。 新的資料列隨即加入。  
  
7.  在 [從空間資料集] 下，按一下 [COUNTYNAME]。  
  
8.  在 [從分析資料集] 下，按一下 [County]。  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 預覽報表。  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
透過指定空間資料來源和分析資料集中的比對欄位，就可以讓報表處理器根據地圖元素為分析資料分組。 資料繫結的地圖元素擁有與您所指定值比對成功的項目。  
  
每一個有商店的郡所使用的色彩，都是依據您在精靈中所選擇樣式的調色盤而定。 其他郡是灰色。  
  
### <a name="ColorRules"></a>6b. 指定多邊形的色彩規則  
若要建立讓各郡的色彩隨商店銷售額變化的規則，您必須指定範圍值、該範圍中要顯示的區間數目，以及要使用的色彩。  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>為所有擁有相關資料的多邊形指定色彩規則  
  
1.  切換至 [設計] 檢視。  
  
2.  按一下 PolygonLayer1 旁的箭號，然後按一下 [多邊形色彩規則]。 **[地圖色彩規則屬性]** 對話方塊隨即開啟。 您會發現已選取 **[使用調色盤將資料視覺化]** 色彩規則選項。 此選項是由精靈設定。  
  
3.  選取 **[使用色彩範圍將資料視覺化]**。 開始色彩、中間色彩和結束色彩選項會取代調色盤選項。  
  
4.  定義每個郡銷售額的範圍值。 從 **[資料欄位]**的下拉式清單中，選取 [ `[Sum(Sales)]`]。  
  
5.  若要改變格式，以千為單位顯示貨幣，則將運算式變更如下： `=Sum(Fields!Sales.Value)/1000`  
  
6.  將 **[開始色彩]** 變更為 **[紅色]**。  
  
7.  將 **[結束色彩]** 變更為 **[綠色]**。  
  
    **[紅色]** 表示低銷售值、 **[黃色]** 表示中銷售值，而 **[綠色]** 表示高銷售值。 報表處理器會根據這些值以及您在 **[分佈]** 頁面上選擇的選項，計算色彩範圍。  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  按一下 **[分佈]**。  
  
9. 請確認分佈類型為 **[最佳]**。 針對步驟 5 中的運算式，最佳分佈會將值分割成子範圍，這些子範圍會讓每個範圍中的項目數目和每個範圍的涵蓋範圍。  
  
10. 接受此頁面上其他選項的預設值。 如果您選取最佳分佈類型，則報表執行時，會計算子範圍的數目。  
  
11. 按一下 **[圖例]**。  
  
12. 在 **[色階選項]**中，確認已選取 **[在色階中顯示]** 。  
  
13. 在 **[在此圖例中顯示]**的下拉式清單中，選取空行。 現在您只能以色階顯示色彩範圍。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. 預覽報表。

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    色階會顯示四種色彩：紅色、橙色、黃色與綠色。 每一種色彩都代表一個銷售額範圍，該範圍是根據各郡的銷售額自動計算。  
  
### <a name="ColorScale"></a>6c. 依據貨幣格式化色階中的資料  
根據預設，資料會使用一般格式。 在本節中，您會套用自訂格式。  
  
1. 切換至 [設計] 檢視。  

2. 選取色階。 在 [首頁] 索引標籤 > [數值] 區段中，按一下 [貨幣]。  
  
4.  仍在 [數值] 區段中，按兩次 [減少小數位數] 按鈕。  
  
    色階會以每個範圍的貨幣格式顯示年度銷售額。  
  
### <a name="NewLegend"></a>6d. 新增圖例標題   
  
1.  在仍然選取色階的情況下，在 [屬性] 窗格中您會看到 **MapColorScale**的屬性。 
  
2. 展開 [標題] 區段中，並在 Caption 屬性中，輸入 **Sales (Thousands)**。

3. 將 TextColor 屬性變更為 [白色]。  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  預覽報表。  
  
與商店和銷售額相關聯的郡會依據色彩規則顯示。 沒有銷售額的郡則不會顯示任何色彩。  
  
### <a name="NoData"></a>6f. 變更未包含資料之郡的色彩  
您可以針對圖層上的所有地圖元素設定預設顯示選項。 色彩規則的優先順序高於這些顯示選項。  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>設定圖層上所有元素的顯示屬性  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。  
  
3.  按一下 PolygonLayer1 上的向下箭頭，然後按一下 **[多邊形屬性]**。 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     **[地圖多邊形屬性]** 對話方塊隨即開啟。 此對話方塊中設定的顯示選項會先套用至圖層上的所有多邊形，然後才會套用規則為主的顯示選項。  
  
4.  在 [填滿] 索引標籤上，確認填滿樣式是 [實心]。 漸層和模式會套用至所有色彩。  
  
6.  在 [色彩] 中，選取 [淺鋼青]。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  預覽報表。  
  
沒有相關資料的郡會顯示為灰藍色。 只有包含相關分析資料的郡會具有您所指定色彩規則中的 [紅色] 到 [綠色] 等色彩。  
  
## <a name="CustomPoint"></a>7.加入自訂點  
若要表示尚未建立的新商店，在本節中，您會指定一個點並使用 [星形] 標記類型。  
  
1.  切換至 [設計] 檢視。  
  
2.  按兩下地圖來顯示 **[地圖圖層]** 窗格。 在工具列上，按一下 **加入圖層**![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")，然後按一下 **點圖層**。    
  
    新的點圖層便會加入至地圖中。 根據預設，點圖層的空間資料類型為 **[內嵌]**。  
  
3.  按一下 PointLayer2 上的箭號 > [新增點]。  
  
4.  將指標移到地圖檢視區上。 游標會變更為十字形狀。  
  
5.  按一下地圖上您要加入點的位置。 在本教學課程中，按一下歐奈達郡內的位置。 以圓形標示的點就會新增至圖層中您所按的點。 根據預設，系統會選取點。  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  以滑鼠右鍵按一下您新增的點，然後按一下 [內嵌點屬性]。  
  
7.  選取 [覆寫此圖層的點選項]。 對話方塊中會出現一個額外的頁面。 您在此處設定的值，其優先順序高於圖層或色彩規則的顯示選項。  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  在 [標記] 索引標籤上，選取 [星形] 作為 [標記類型]。  

10. 將 [標記大小] 變更為 [18pt]。
  
3.  在 [標籤] 索引標籤的 [標籤文字] 中，輸入 **New Store**。  
  
5.  在 **[位置]**中，按一下 **[上方]**。  

13. 在 [字型] 索引標籤上，使字型大小成為 [10pt] 和 [粗體]。

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  預覽報表。  
  
標籤會出現在商店位置上方。  

![report-builder-map-custom-point-new-store](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8.置中與縮放地圖   
在本節中，您會學習如何變更地圖中心，以及變更縮放層級的另一種方式。  
 
1.  切換至 [設計] 檢視。  

1.  選取地圖，然後以滑鼠右鍵按一下並按一下 [檢視區屬性]。  
  
2.  在 [置中與縮放] 索引標籤，確定已選取 [設定檢視置中與縮放層級]。  

4. 將 [縮放層級 (百分比)] 設為 [125]。
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  按一下地圖，並拖曳以將它置中於您想要的位置。  
  
6.  您也可以使用滑鼠滾輪變更縮放層級。  
  
7.  預覽報表。  
  
在 [設計] 檢視中，顯示介面和檢視上的地圖是以範例資料為基礎。 在呈現的報表中，地圖檢視會在您指定的檢視上置中。  
  
## <a name="Title"></a>9.加入報表標題  
  
1.  切換至 [設計] 檢視。
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入 **紐約商店的銷售額** ，然後按一下文字方塊外部。  
  
這個標題就會顯示在報表的頂端。 沒有定義任何頁首時，位於報表主體頂端的項目就相當於報表頁首。  
  
## <a name="Save"></a>10.儲存報表  
  
1.  在設計檢視或預覽中，在 [檔案] 功能表 > [另存新檔]。
 
3.  在 **[名稱]**中輸入 **紐約的商店銷售額**。  

3. 將它儲存到本機電腦上，或 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 伺服器。
  
4. 按一下 **[儲存]**。 

如果您將它儲存到報表伺服器，您可以在該處檢視。

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>後續步驟  
以上總結如何將地圖加入至報表的逐步解說。  
  
如需詳細資訊，請參閱[地圖 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md)  
[SQL Server 2016 的報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  


