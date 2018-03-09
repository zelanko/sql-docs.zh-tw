---
title: "新增、變更或刪除地圖或地圖圖層 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.maplayerproperties.general.f1
- "10526"
- sql13.rtp.rptdesigner.mappolygonlayerproperties.general.f1
- "10529"
- "10525"
- "10535"
- sql13.rtp.rptdesigner.mappointlayerproperties.general.f1
- sql13.rtp.rptdesigner.shared.layerfilters.f1
- sql13.rtp.rptdesigner.maplinelayerproperties.general.f1
- "10524"
- sql13.rtp.rptdesigner.maptilelayerproperties.general.f1
- "10532"
- sql13.rtp.rptdesigner.maplayerproperties.analyticaldata.f1
- "10528"
- "10527"
- sql13.rtp.rptdesigner.shared.layervisibility.f1
ms.assetid: 6e89815e-187e-45bf-bf63-3d5c4a246360
caps.latest.revision: "15"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0bb98e926d7c06a216ef5230af9fd9a113d451dc
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs"></a>加入、變更或刪除地圖或地圖圖層 (報表產生器及 SSRS)
  地圖是圖層的集合。 將地圖加入至 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表時，您會定義第一個圖層。 您可以使用地圖圖層精靈建立其他圖層。  
  
 加入、移除或變更圖層選項的一個最簡單的方法，就是使用地圖圖層精靈。 您也可以從 [地圖] 窗格手動變更選項。 若要顯示 [地圖] 窗格，按一下報表設計介面上的地圖。 下圖顯示此窗格的幾個部分：  
  
 ![rsMapLayerZone](../../reporting-services/report-design/media/rsmaplayerzone.gif "rsMapLayerZone")  
  
 地圖圖層是以它們顯示在 [地圖] 窗格中的順序，由下而上繪製。 在上圖中，圖格圖層會最先繪製，而多邊形圖層則是最後繪製。 稍後繪製的圖層可能會隱藏圖層上先前繪製的地圖元素。 您可以使用 [地圖] 窗格工具列上的方向鍵來變更圖層的順序。 若要顯示或隱藏圖層，請切換可見性圖示。 您可以在 [圖層資料] 屬性對話方塊的 [可見性] 頁面上，變更圖層的透明度。  
  
 下表顯示 [地圖] 窗格的工具列圖示。  
  
|符號|描述|使用時機|  
|------------|-----------------|-----------------|  
|![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")|地圖圖層精靈|若要使用精靈加入圖層，按一下 [新增圖層精靈]。|  
|![rs_IconMapAddLayer](../../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")|加入圖層|若要手動加入圖層，按一下 [加入圖層]，然後按一下要加入之地圖圖層的類型。|  
|![rs_IconMapPolygonLayer](../../reporting-services/report-design/media/rs-iconmappolygonlayer.gif "rs_IconMapPolygonLayer")|多邊形圖層|加入地圖圖層，此圖層會顯示以多組多邊形座標為基礎的區域或形狀。|  
|![rs_IconMapLineLayer](../../reporting-services/report-design/media/rs-iconmaplinelayer.gif "rs_IconMapLineLayer")|線條圖層|加入地圖圖層，此圖層會顯示以多組線條座標為基礎的路徑或路線。|  
|![rs_IconMapPointLayer](../../reporting-services/report-design/media/rs-iconmappointlayer.gif "rs_IconMapPointLayer")|點圖層|加入地圖圖層，此圖層會顯示以多組點座標為基礎的位置。|  
|![rs_IconMapTileLayer](../../reporting-services/report-design/media/rs-iconmaptilelayer.gif "rs_IconMapTileLayer")|影像分割圖層|加入地圖圖層，此圖層會顯示對應至檢視區所定義之目前地圖檢視區域的 Bing 地圖底圖。|  
  
 [地圖] 窗格的底部為地圖檢視區域。 若要變更地圖的置中或縮放選項，請使用方向鍵調整檢視置中，並使用滑動軸調整縮放層級。  
  
 如需圖層的詳細資訊，請參閱 [地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="AddLayer"></a> 從地圖圖層精靈加入圖層  
  
-   從功能區中，按一下 [插入] 功能表上的 [地圖]，然後按一下 [地圖精靈]。 此精靈可讓您將圖層加入至現有的地圖。 地圖精靈與地圖圖層精靈的大部分精靈頁面都相同。  
  
     如需詳細資訊，請參閱 [地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)。  
  
##  <a name="ChangeLayer"></a> 使用地圖圖層精靈來變更圖層的選項  
  
-   執行地圖圖層精靈。 這個精靈可讓您變更您使用地圖圖層精靈所建立的圖層選項。 在 [地圖] 窗格中，以滑鼠右鍵按一下此圖層，然後在工具列上按一下圖層精靈按鈕 (![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"))。  
  
     如需詳細資訊，請參閱 [地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)。  
  
##  <a name="AddVectorLayer"></a> 從 [圖層] 窗格工具列加入點、線條或多邊形圖層  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  在工具列上，按一下 [新增圖層] 按鈕，然後從下拉式清單中按一下您要新增的圖層類型：[點]、[線條] 或 [多邊形]。  
  
    > [!NOTE]  
    >  雖然您可以手動加入地圖圖層並加以設定，我們建議您最好使用地圖圖層精靈來新增圖層。 若要在 [地圖] 窗格工具列啟動精露，請以滑鼠右鍵按一下圖層精靈按鈕 (![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"))。  
  
3.  以滑鼠右鍵按一下圖層，然後按一下 [圖層資料]。  
  
4.  在 [使用以下來源的空間資料] 中，選取空間資料的來源。 這些選項會隨著您選取的項目而不同。  
  
     如果您想要從此圖層上的報表視覺化分析資料，請執行下列操作：  
  
    1.  按一下 **[分析資料]**。  
  
    2.  在 [分析資料集] 中，按一下其中包含分析資料與符合欄位之資料集的名稱，來建立分析資料與空間資料之間的關聯性。  
  
    3.  按一下 **[加入]**。  
  
    4.  從空間資料集輸入符合欄位的名稱。  
  
    5.  從分析資料集輸入符合欄位的名稱。  
  
     如需連結空間和分析資料的詳細資訊，請參閱[自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="FilterAnalyticalData"></a> 篩選圖層的分析資料  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下 [地圖] 窗格中的圖層，然後按一下 [圖層資料]。  
  
3.  按一下 **[篩選]**。  
  
4.  定義篩選方程式，以限制用於地圖顯示的分析資料。 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
##  <a name="PointProperties"></a> 控制點圖層或多邊形中心點的點屬性  
  
1.  選取 [地圖點屬性] 對話方塊上的 [一般] 來變更下列地圖元素的標籤、工具提示和標記類型選項：  
  
    -   點圖層上的所有動態或內嵌的點。 點的色彩規則、大小規則與標記類型規則會覆寫這些選項。 若要覆寫特定內嵌點的選項，請使用 [地圖內嵌點屬性對話方塊、標記](http://msdn.microsoft.com/library/3c5eb1c5-d40a-424f-aa7c-43b112f42dec) 頁面。  
  
    -   在多邊形圖層上，所有動態或內嵌之多邊形的中心點。 中心點的色彩規則、大小規則與標記類型規則會覆寫這些選項。 若要覆寫特定中心點的選項，請使用 [地圖內嵌點屬性對話方塊、標記](http://msdn.microsoft.com/library/3c5eb1c5-d40a-424f-aa7c-43b112f42dec) 頁面。  
  
##  <a name="Embedded"></a> 將內嵌資料指定為空間資料的來源  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下圖層，然後按一下 [圖層資料]。  
  
3.  在 [使用以下來源的空間資料] 中，選取 [內嵌在報表中的資料]。  
  
4.  若要從現有的報表載入地圖項目，或以 ESRI 檔案為基礎建立地圖項目，按一下 [瀏覽]，並指向該檔案，然後按一下 [開啟]。 地圖元素便會內嵌在此報表定義中。 您所指向的空間資料必須符合圖層類型。 例如，若是點圖層，您必須指向指定點座標組的空間資料。  
  
5.  在 [空間] 欄位中，指定包含空間資料之欄位的名稱。 您可能需要從空間資料來源決定此名稱。  
  
    > [!NOTE]  
    >  如果您不知道欄位的名稱，而且您已經瀏覽到 ESRI 形狀檔，請使用 [連結到 ESRI 形狀檔 (.shp)] 選項來代替此選項。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ESRI"></a> 將 ESRI 形狀檔指定為空間資料的來源  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下圖層，然後按一下 [圖層資料]。  
  
3.  在 [使用以下來源的空間資料] 中，選取 [連結到 ESRI 形狀檔 (.shp)]。  
  
4.  在 [檔案名稱] 中，鍵入 ESRI 形狀檔的位置，或按一下 [瀏覽] 以選取 ESRI 形狀檔。  
  
    > [!NOTE]  
    >  如果此形狀檔在您的本機電腦上，空間資料會內嵌在報表定義中。 若要在處理報表時動態擷取資料，您必須將 ESRI .shp 檔及其支援檔案 .dbf 上傳至報表伺服器。 如需詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件](http://go.microsoft.com/fwlink/?linkid=121312) 的＜如何：上傳檔案或報表 (報表管理員)＞。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="DatasetField"></a> 將報表資料集欄位指定為空間資料的來源  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下圖層，然後按一下 [圖層資料]。  
  
3.  在 [使用以下來源的空間資料] 中，選取 [資料集中的空間欄位]。  
  
4.  在 [資料集名稱] 中，按一下報表內包含所需空間資料之資料集的名稱。  
  
5.  在 [空間欄位名稱] 中，按一下資料集內包含空間資料的欄位名稱。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TileLayer"></a> 若要加入圖格圖層  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  在工具列上，按一下 [加入圖層] 按鈕，然後從下拉式清單中按一下 [圖格圖層]。  
  
    > [!NOTE]  
    >  如需有關在報表中使用 Bing 地圖底圖的詳細資訊，請參閱 [其他使用規定](http://go.microsoft.com/fwlink/?LinkId=151371)。  
  
3.  以滑鼠右鍵按一下 [圖層] 窗格中的圖格圖層，然後按一下 [圖格屬性]。  
  
4.  在 [圖格選項] 中，選取圖格樣式。 如果可以使用 Bing 地圖底圖，設計介面上的圖層會更新成您選取的樣式。  
  
    > [!NOTE]  
    >  當您在「地圖精靈」或「地圖圖層精靈」中加入多邊形、線條或點圖層時，也可以加入影像分割圖層。 在 [選擇空間資料及地圖檢視選項] 頁面上，選取 [Add a Bing Maps background for this map view (加入此地圖檢視的 Bing Maps 背景)] 選項。  
  
##  <a name="DrawingOrder"></a> 變更圖層的繪圖順序  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  按一下 [圖層] 窗格中的圖層，即可選取它。  
  
3.  在 [圖層] 窗格工具列上，按一下向上鍵或向下鍵來變更每個圖層的繪圖順序。  
  
##  <a name="Transparency"></a> 變更多邊形、線條或點圖層的透明度  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下圖層，然後按一下 [圖層資料]。  
  
3.  按一下 **[可見性]**。  
  
4.  在 [透明度選項] 中，輸入表示透明度百分比的值，例如 **40**。 透明度百分比為零 (0) 表示圖層是不透明的。 透明度百分比為 100，則表示您在報表中看不到圖層。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TileTransparency"></a> 變更圖格圖層的透明度  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  以滑鼠右鍵按一下圖層，然後按一下 [圖格屬性]。  
  
3.  按一下 **[可見性]**。  
  
4.  在 [透明度選項] 中，輸入表示透明度百分比的值，例如 **40**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Secure"></a> 為圖格圖層指定安全連接  
  
1.  按一下地圖，直到 [圖層] 窗格出現為止。  
  
2.  在 [圖層] 窗格中按一下圖格圖層，即可選取它。 [屬性] 窗格會顯示圖格圖層屬性。  
  
3.  在 [屬性] 窗格中，將 UseSecureConnection 設定為 **True**。  
  
 Bing Maps Web 服務的連接將會使用 HTTP SSL (安全通訊端層) 服務來擷取這個圖層的 Bing 地圖底圖。  
  
##  <a name="Language"></a> 為圖格標籤指定語言  
  
1.  根據預設，如果是顯示標籤的圖格樣式，語言是由報表產生器的預設地區設定所決定。 您可以透過以下方式來自訂圖格標籤的語言設定。  
  
    -   按一下檢視區外部的地圖，即可選取該地圖。 在 [屬性] 窗格中，針對 TileLanguage 屬性從下拉式清單中選取文化特性值。  
  
    -   按一下報表背景，即可選取報表。 在 [屬性] 窗格中，針對 Language 屬性從下拉式清單中選取文化特性值。  
  
     設定圖格標籤語言的優先順序如下：報表屬性 Language、報表產生器的預設地區設定，以及地圖屬性 TileLanguage。  
  
##  <a name="ConditionalHide"></a> 根據檢視區縮放層級，有條件地隱藏圖層  
  
1.  設定 [可見性] 選項來控制地圖圖層的顯示。  
  
    -   在 [地圖圖層] 窗格中，以滑鼠右鍵按一下圖層選取此圖層，然後按一下 [地圖圖層] 工具列上的 [屬性]，開啟 [地圖圖層屬性]。  
  
    -   按一下 **[可見性]**。  
  
    -   在 [圖層可見性] 中，選取 [根據縮放值顯示或隱藏]。  
  
    -   輸入顯示圖層時的最小和最大縮放值。  
  
    -   選擇性。 輸入透明度的值。  
  
     您也可以有條件地隱藏圖層。 如需詳細資訊，請參閱[隱藏項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [報表疑難排解：地圖報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
