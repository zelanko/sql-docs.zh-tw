---
title: 地圖精靈與地圖圖層精靈 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapandlayerwizard.f1
- "10542"
- MICROSOFT.REPORTDESIGNER.MAPLAYER.NAME
ms.assetid: 48cbe18b-1290-4107-8a1c-ec6acd71f73b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f005ac1a727b375d7c0796a9f30bfed388dccfbd
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290756"
---
# <a name="map-wizard-and-map-layer-wizard-report-builder-and-ssrs"></a>地圖精靈與地圖圖層精靈 (報表產生器及 SSRS)
  地圖精靈與地圖圖層精靈會將建立地圖、加入地圖圖層，或變更現有圖層上之地圖圖層選項的程序自動化。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 在您將地圖加入至報表，或將地圖圖層加入至地圖之前，您必須擁有下列資訊：  
  
-   **空間資料來源：** 提供空間資料 (例如，包含空間資料之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體和資料庫的名稱，或環境系統研究協會 (Environmental Systems Research Institute, Inc.，ESRI) 形狀檔的名稱) 之來源的位置或連接。(ESRI) 形狀檔。  
  
-   **Spatial data.** 來自空間資料來源，包含指定位置之座標位置組的欄位。  
  
-   **分析資料：** 用於改變地圖顯示 (如商店的年度銷售量) 的分析資料。  
  
-   **符合欄位：** 定義空間資料與分析資料之間關聯性的符合欄位，例如，區域和城市的名稱以唯一識別每個城市。  
  
 以下各節提供有關在「地圖精靈」與「地圖圖層精靈」中指定之選項的資訊。  
  
##  <a name="BackToTop"></a> 地圖精靈與地圖圖層精靈頁面  
 若要開啟「地圖精靈」，請進行下列其中一個動作：  
  
-   當您第一次開啟報表產生器時，請在設計介面的中央按一下 **[地圖]** 精靈圖示。  
  
-   在 **[插入]** 索引標籤上，按一下 **[地圖]**，然後按一下 **[地圖精靈]**。  
  
 若要開啟「地圖圖層精靈」，請進行下列動作：  
  
-   按一下地圖以顯示 [地圖] 窗格，然後在工具列上，按一下 **[新增圖層精靈]** 按鈕。  
  
 針對對應的說明內容，按一下精靈頁面的標題。 您看到的頁面會根據您選擇的地圖類型、空間資料來源及分析資料來源而有所不同。  
  
1.  [選擇空間資料的來源](#SpatialDataSource)。 空間資料可能來自地圖庫、環境系統研究協會 (Environmental Systems Research Institute, Inc.，ESRI) 形狀檔，或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 關聯式資料庫中的空間資料。  
  
    -   [何謂空間資料？](#SpatialData)  
  
    -   [何謂地圖庫？](#MapGallery)  
  
    -   [何謂 ESRI 形狀檔？](#Shapefile)  
  
    -   [哪裡可以取得 ESRI 形狀檔？](#GetShapefiles)  
  
    -   [何謂 SQL Server 空間查詢？](#SqlServerSpatial)  
  
2.  [選擇空間資料及地圖檢視選項](#MapView)。 設定地圖檢視、地圖解析度，指定是否要在報表中內嵌空間資料，以及指定是否要包含 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing 地圖底圖的圖格背景。  
  
    -   [何謂地圖檢視或檢視區？](#Viewport)  
  
    -   [何謂地圖解析度或最佳化？](#Resolution)  
  
    -   [內嵌的空間資料用途為何？](#Embed)  
  
    -   [何謂 Bing 地圖底圖背景？](#Tiles)  
  
3.  [選擇地圖視覺效果](#Visualization)。 選擇要建立之地圖的類型。  
  
    -   [基本地圖、泡泡地圖與分析地圖之間的差異為何？](#MapType)  
  
    -   **選擇地圖視覺效果：多邊形**  
  
    -   **選擇地圖視覺效果：程式行**  
  
    -   **選擇地圖視覺效果：點**  
  
4.  **選擇與資料來源的連接**。 選擇資料來源連接，或建立一個外部資料來源的連接，其中包含要顯示在地圖上的分析資料。  
  
5.  **設計查詢**。 建立指定分析資料的查詢。  
  
6.  [選擇分析資料集](#AnalyticalData)。 指定分析資料的資料來源。  
  
    -   [空間資料和分析資料之間的差異為何？](#Diff)  
  
7.  [指定空間與分析資料的比對欄位](#SpecifyMatchFields)。 建立空間資料與分析資料之間的關聯性，讓地圖元素的外觀可以隨著資料變化。  
  
    -   [何謂符合欄位？](#MatchFields)  
  
8.  [選擇色彩主題和資料視覺效果](#ThemeandVisualization)。 若要指定如何根據地圖背景視覺化資料，請指定地圖主題、要視覺化的欄位，以及要改變的項目：色彩、大小和/或標記類型。  
  
    -   [主題的用途為何？](#Theme)  
  
    -   [地圖預覽中的圖例和標尺用途為何？](#Legends)  
  
    -   [何謂規則？](#Rules)  
  
 在您加入地圖或地圖圖層並預覽報表之後，可以變更您在精靈中設定的地圖和地圖圖層選項。 如需詳細資訊，請參閱[自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
 如需地圖的詳細資訊，請參閱 [地圖 &#40;報表產生器及 SSRS&#41;](maps-report-builder-and-ssrs.md)。 若要將地圖加入至報表的逐步指示，請參閱[教學課程：地圖報表&#40;報表產生器&#41;](../tutorial-map-report-report-builder.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="SpatialDataSource"></a> 選擇空間資料的來源  
 在此頁面上，指定空間資料來源以及要包含的空間資料。 空間資料可能來自地圖庫、ESRI 形狀檔，或指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或更新版本資料庫之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 空間資料的資料集查詢。  
  
 您可以在每個圖層上使用空間資料的相同來源或不同來源，但是您必須指定每次您加入圖層時的來源。 當空間資料來自地圖庫或 ESRI 形狀檔時，空間資料來源不是個別的報表項目， 因此不會出現在 [報表資料] 窗格中。  
  
###  <a name="SpatialData"></a> 何謂空間資料？  
 空間資料包含可定義地理或幾何元素的座標軸。 在地圖中，空間資料會定義 *「地圖元素」*(Map Element)：定義區域或形狀的多邊形、定義路線或路徑的線條，以及定義標記或圖釘的點。 空間資料會以二進位格式儲存在資料來源中，並指定為座標位置組。 例如，點是 X 和 Y 座標 (X Y)、線條是兩組座標位置 ((X1 Y1), (X2 Y2))、多邊形是四組以上的座標位置，其中第一組和最後一組座標位置相同 ((X1 Y1), (X2 Y2), (X3 Y3), (X1 Y1))。  
  
 如需詳細資訊，請參閱您使用之空間資料類型的文件集。  
  
###  <a name="MapGallery"></a> What is the map gallery?  
 地圖庫包含的地圖來自報表撰寫環境之地圖庫資料夾中的報表。 地圖庫中的地圖可讓您快速開始將地圖加入至報表中。 地圖庫中預先定義的地圖是由地圖提供者所提供。  
  
> [!NOTE]  
>  這個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 地圖功能會使用美國人口普查局 ([http://www.census.gov/](http://www.census.gov/)) 提供的 TIGER/Line Shapefiles 資料。 TIGER/Line 形狀檔是 Census MAF/TIGER 資料庫中選定地理和製圖資訊的擷取內容。 TIGER/Line 形狀檔是由美國人口普查局所免費提供。 如需有關 TIGER/Line Shapefile 的詳細資訊，請參閱 [http://www.census.gov/geo/www/tiger](http://www.census.gov/geo/www/tiger) \(英文\)。 TIGER/Line 形狀檔中的界限資訊只能當做統計資料收集和表格製作的用途，其統計用途的描述和指定並不構成司法權或擁有權利的判定，也不屬於法律上的土地描述。 Census TIGER 和 TIGER/Line 是美國人口普查局的註冊商標。  
  
 若要擴充地圖庫，您可以從地圖庫目錄加入或移除報表，也可以加入資料夾來組織地圖。 如需詳細資訊，請參閱 [地圖 &#40;報表產生器及 SSRS&#41;](maps-report-builder-and-ssrs.md)。  
  
###  <a name="Shapefile"></a> What is an ESRI shapefile?  
 ESRI 形狀檔是一組檔案，其中包含符合 Environmental Systems Research Institute, Inc. (ESRI) 形狀檔空間資料格式的資料。 這組檔案通常包括內含空間資料的 \<檔名>.shp 檔案以及支援檔案 \<檔名>。  
  
 當您將形狀檔指定為您本機電腦上的空間資料來源時，會將空間資料自動內嵌至報表中。 若要以動態方式使用 ESRI 檔案中的空間資料，您必須執行下列操作：  
  
 在報表產生器中，將 .shp 檔和 .dbf 檔同時上傳至報表伺服器上的相同資料夾，然後連結至 .shp 檔做為空間資料來源。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的報表設計師中，將 .shp 檔和 .dbf 檔同時加入至報表專案，然後將 .shp 檔案的名稱指定為空間資料來源。  
  
###  <a name="GetShapefiles"></a> 哪裡可以取得 ESRI 形狀檔？  
 ESRI 形狀檔可上網取得。 如需詳細資訊，請參閱 [尋找地圖的 ESRI 形狀檔](https://go.microsoft.com/fwlink/?linkid=178814)。  
  
###  <a name="SqlServerSpatial"></a> 何謂 SQL Server 空間查詢？  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 空間查詢是一種資料集查詢，可以指定來自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 關聯式資料庫之 SQLGeometry 或 SQLGeography 資料類型的資料。  
  
> [!NOTE]  
>  當您在精靈中定義資料來源時，您會在 [設計查詢] 頁面看到不同的查詢設計工具，端視您所連接的資料來源類型而定。 如需詳細資訊，請參閱[查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)。  
  
 當您在查詢設計工具中執行查詢時，結果集會顯示一個資料行，其中包含顯示為文字的空間資料。 例如，一個資料列可能包含單一點的空間資料，而下一個資料列則可能包含定義一組點的空間資料。 每個資料列都會變成一個地圖元素。 您可以將每個地圖元素的顯示變更為個別的單位。  
  
 如需詳細資訊，請參閱《 [SQL Server 線上叢書](https://go.microsoft.com/fwlink/?linkid=120955)》中的＜空間資料的類型＞。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="MapView"></a> 選擇空間資料及地圖檢視選項  
 在此頁面上，您可以設定下列選項：  
  
-   針對您在前一個精靈頁面選取的空間資料，設定檢視置中與縮放層級。 您設定的檢視會套用至整個地圖。  
  
-   設定地圖解析度。  
  
-   指定是否將空間資料內嵌至報表中。  
  
-   針對內嵌的資料，指定要包含所有資料還是只包含目前檢視中的資料。  
  
-   指定是否要包含 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing 地圖底圖背景。  
  
###  <a name="Viewport"></a> 何謂地圖檢視或檢視區？  
 地圖檢視區會針對報表中的所有圖層定義要顯示的地圖區域。  
  
 根據預設，色階與距離標尺會出現在檢視區內部，而地圖圖例則出現在檢視區外部。 您可以在完成精靈後，變更檢視區的這些選項。  
  
###  <a name="Resolution"></a> 何謂地圖解析度和最佳化？  
 當您針對表示線條或多邊形的空間資料變更解析度時，就是在指定您希望繪製地圖的詳細程度。 例如，針對某個地區的空中鳥瞰圖，您需要將資料粒度降低到地球表面區域的一百公尺，還是一英哩的解析度就已經足夠？  
  
 當空間資料內嵌在報表中時，如果解析度較高，會增加以該解析度繪製細節所需之元素的數目。 當空間資料沒有內嵌在報表中時，如果解析度較高，則會增加每次檢視報表時報表處理器以該解析度計算地圖線條所需的時間。  
  
 當您降低解析度時，報表處理器會套用演算法來減少繪製地圖元素所需的點數。 解析度越低，顯示地圖元素所需的資料越少，而且顯示效能也越好。  
  
 當您調整滑動軸時，精靈窗格中的預覽資料會更新來表示生效。 將地圖加入至報表之後，您可以變更地圖檢視區選項來調整此值。  
  
###  <a name="Embed"></a> 內嵌的空間資料用途為何？  
 當您將地圖元素或 Bing 地圖底圖內嵌到報表中時，空間資料會儲存在報表定義中。  
  
 包含地圖的報表可以使用空間資料或是 Bing 地圖底圖 (在報表處理時或在設計階段動態擷取，然後內嵌到報表定義中)。 內嵌的地圖元素可能會大幅增加報表定義的大小，但是會減少在報表中檢視地圖所需的時間。 動態地圖元素會減少報表定義的大小，但是會增加處理及檢視地圖所需的時間。  
  
 良好的報表設計會要求您評估靜態或動態地圖資料的權衡得失，並找出適合您狀況的平衡點。 一般而言，資料越多，表示報表定義和編譯的報表在報表伺服器上需要的儲存空間越多，處理的時間也越長。 永遠的最佳做法是，裁剪空間資料以及限制其他報表資料，就能夠只包含報表需要的資料。  
  
###  <a name="Tiles"></a> 何謂 Bing 地圖底圖背景？  
 若要將地理影像背景加入至您的地圖，請選取 Bing 地圖底圖背景選項。 報表處理器會從 Bing Map Web 服務下載圖格，供您在此精靈頁面指定的地圖區域與解析度使用。 您可以指定下列其中一種圖格類型：  
  
-   **路段圖：** 以白色背影顯示路段圖樣式。  
  
-   **空照圖：** 只顯示空照圖檢視。 在此模式下不會顯示任何文字。  
  
-   **混合：** 顯示 **[路段圖]** 和 **[空照圖]** 檢視的組合。  
  
 如需有關圖格的詳細資訊，請參閱＜ [Bing 地圖底圖系統](https://go.microsoft.com/fwlink/?LinkId=147315)＞。 如需有關在報表中使用 Bing 地圖底圖的詳細資訊，請參閱 [其他使用規定](https://go.microsoft.com/fwlink/?LinkId=151371) 和 [隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=151372)。  
  
 若要在設計檢視下查看圖格背景，您必須能夠存取網際網路。 若要從報表伺服器上的報表查看預覽中的圖格背景，則必須將報表伺服器設定為支援 Bing 地圖底圖。 如需詳細資訊，請參閱[報表疑難排解：將報表對應&#40;報表產生器及 SSRS&#41; ](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)及 < 規劃地圖 」 中[Reporting Services 文件](https://go.microsoft.com/fwlink/?linkid=121312)SQL Server 線上叢書 》 中。  
  
 如需自訂圖格圖層之其他方式的詳細資訊，請參閱[加入、變更或刪除地圖或地圖圖層 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="Visualization"></a> 選擇地圖視覺效果  
 在此頁面上，選擇要加入至報表之地圖或地圖圖層的類型。 第一次執行精靈時，您會將地圖和第一個地圖圖層加入至報表中。 一個地圖可以包含多個地圖圖層。 每個地圖圖層都會顯示一個特定的空間資料類型：多邊形、線條或點。  
  
 您選擇的地圖類型取決於您要將地圖和資料用於何種用途。  
  
###  <a name="MapType"></a> 基本地圖、泡泡地圖與分析地圖之間的差異為何？  
 **[基本地圖]** 僅顯示位置。 您可以使用陰影改變地圖區域的色彩，但是色彩並不表示分析資料值。  
  
 **[泡泡地圖]** 會將單一分析資料彙總的相對值傳達為泡泡大小，例如，商店銷售量。 您可以針對多邊形或點建立泡泡地圖。 若是多邊形，設定多邊形中心點屬性；若是點，則設定標記屬性。  
  
 **[分析地圖]** 會針對每個地圖元素傳達一個或多個分析資料彙總的相對值。 例如，商店銷售量當做標記大小、產品類別目錄的收益範圍當做標記色彩，而最暢銷的產品當做標記類型。  
  
 如需詳細資訊，請參閱 [規劃地圖報表 &#40;報表產生器及 SSRS&#41;](plan-a-map-report-report-builder-and-ssrs.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="AnalyticalData"></a> 選擇分析資料集  
 在此頁面上，指定取得要顯示在此地圖圖層上之分析資料的位置。  
  
 若要根據地圖背景顯示報表資料或任何分析資料，您必須指定資料的位置以及該資料與空間資料的關係。 您的資料可能來自現有的報表資料集，或來自您建立查詢所依據的新資料集。 現有的分析資料可能會包含在內含空間資料的 ESRI 形狀檔中。  
  
###  <a name="Diff"></a> 空間資料和分析資料之間的差異為何？  
 空間資料由指定點、線條和多邊形的座標位置組所組成。 地圖元素以空間資料為基礎。  
  
 分析資料是您想要用來改變地圖外觀的數值或類別資料。 分析資料可能來自報表資料集，也可能隨附在來自地圖庫或 ESRI 形狀檔之地圖的空間資料中。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="SpecifyMatchFields"></a> 指定符合欄位  
 在此頁面上，建立空間資料與分析資料間的關聯性。  
  
###  <a name="MatchFields"></a> 何謂符合欄位？  
 符合欄位可讓報表處理器建立分析資料與空間資料間的關聯性。 符合欄位會在分析資料內指定唯一的值。 例如，商店名稱在資料內可能不是唯一的，因此您可以同時指定城市和商店名稱。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
##  <a name="ThemeandVisualization"></a> 選擇色彩主題和資料視覺效果  
 在此頁面上，指定如何根據地圖背景、地圖主題、要視覺化的欄位，以及要改變的項目 (色彩、大小和/或標記類型) 視覺化資料。  
  
###  <a name="Theme"></a> 主題的用途為何？  
 您所選擇的主題會設定色彩、框線與字型的預設值。 您可以在完成精靈後變更這些選項。  
  
###  <a name="Legends"></a> 地圖預覽中的圖例和標尺用途為何？  
 圖例可協助使用者解譯顯示在地圖上的資料。 一個地圖會提供一個色彩範圍、一個距離標尺，以及一個圖例。  
  
-   **色彩範圍。** 色彩範圍會顯示有刻度的色彩列，為報表處理器依據您為圖層所指定的規則所決定的資料間隔，提供指引。  
  
-   **距離標尺：** 距離標尺會在地圖上提供距離單位的指引。 距離單位是根據地圖投射與顯示比例層級自動決定。  
  
-   **圖例** 圖例會提供指引，以協助解譯地圖上色彩、大小及標記類型的意義。 根據預設，所有圖層的所有規則都會在第一個圖例中顯示資料間隔。 您可以自訂此圖例並在將地圖加入至報表中之後加入圖例。  
  
###  <a name="Rules"></a> 何謂規則？  
 規則是報表處理器用來將分析資料分為不同範圍的計算方法。 您可以針對每個圖層指定不同的規則。 您可以指定的規則類型取決於圖層上的空間資料類型：  
  
-   **多邊形：** 您可以指定色彩規則。  
  
-   **多邊形的中心點：** 您可以指定色彩、大小與標記類型規則。  
  
-   **線條：** 您可以指定色彩和寬度規則。  
  
-   **點：** 您可以指定色彩、大小與標記類型規則。  
  
 報表處理器會套用您所設定的規則，並自動決定要顯示在圖例中之項目的清單。 根據預設，所有圖層的所有規則結果都會顯示在第一個圖例中。 您可以在完成精靈後調整這個設定。 如需詳細資訊，請參閱 [使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#BackToTop)  
  
## <a name="see-also"></a>另請參閱  
 [報表疑難排解：地圖報表 &#40;報表產生器及 SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [規劃地圖報表 &#40;報表產生器及 SSRS&#41;](plan-a-map-report-report-builder-and-ssrs.md)   
 [地圖 &#40;報表產生器及 SSRS&#41;](maps-report-builder-and-ssrs.md)  
  
  
