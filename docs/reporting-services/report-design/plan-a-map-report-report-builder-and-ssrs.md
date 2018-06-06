---
title: 規劃地圖報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0e70da5054e3a5211f98dffedcf9eafff7c4b3b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="plan-a-map-report-report-builder-and-ssrs"></a>規劃地圖報表 (報表產生器及 SSRS)
良好的報表會呈現具備行動力或洞察能力的資訊。 若要針對地理背景呈現分析資料 (例如銷售總計或人口統計)，您可以將地圖加入 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中。 一個地圖可以包含多個圖層，而每個圖層都會顯示由特定類型之空間資料所定義的地圖元素：表示位置的點、表示路線的線條，或表示區域的多邊形。 您可以讓您的分析資料與每個圖層上的地圖元素產生關聯。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> 指定地圖的用途  
 良好的報表設計會提供可協助使用者採取行動來處理問題的資訊。 若要建立實用、容易理解的地圖顯示，請決定您希望地圖協助回答的問題。 例如，您可以在地圖上視覺化下列類型的資料來識別市場商機：  
  
-   每個商店的相對銷售額。  
  
-   依客戶人口統計，根據相對於商店位置的客戶位置分類的銷售額。  
  
-   依銷售領域的相關銷售額或其他財務資料。  
  
-   跨多個商店之不同折扣策略的相關銷售額。  
  
 在您識別地圖顯示的用途之後，必須分析您所需的資料。 分析資料來自報表資料集。 位置資料來自您必須指定的空間資料來源。  
  
##  <a name="Data"></a> 指定空間資料與分析資料  
 您必須指定所需的空間資料與分析資料。  
  
 分析資料來自報表資料集、隨附在來自地圖庫之地圖的範例資料，或隨附在 ESRI 形狀檔之空間資料的分析資料。  
  
 空間資料包含三種形式：點、線條和多邊形。  
  
-   **點：** 點會指定位置，例如，商店、餐廳或會議中心所在的城市或地址。 對於您想要顯示在地圖上的每個位置，您必須提供該位置的空間資料。 將點加入至地圖之後，您可以顯示點位置的標記以及改變標記類型、大小與色彩。  
  
-   **線條：** 線條會指定路徑或路線，例如，傳遞路線或飛行路徑。 將線條加入至地圖之後，您可以更改線條色彩與線條寬度。  
  
-   **多邊形：** 多邊形會指定區域，例如，區域、領域、國家 (地區)、州、省、縣、城市，或城市、郵遞區號、電話交換機或人口普查區所涵蓋的區域。 將多邊形加入至地圖之後，除了顯示外框之外，您還可以顯示多邊形區域中心點的標記。  
  
 識別您所需要的空間資料之後，您必須尋找該資料的來源。  
  
### <a name="find-a-source-for-spatial-data"></a>尋找空間資料的來源  
 若要尋找地圖中所使用的空間資料，您可以使用下列來源：  
  
-   ESRI 形狀檔，包括您可以在網際網路上搜尋到之公開提供的形狀檔。  
  
-   來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 空間資料來源的空間資料。  
  
-   來自地圖厙中之報表的地圖。  
  
-   將空間資料當作 ESRI 形狀檔或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 空間資料提供的協力廠商網站。  
  
-   提供地圖檢視之背景的 Bing 地圖底圖。 若要在地圖中顯示圖格，必須將報表伺服器設定為支援 Bing Maps Web 服務。  
  
 如需詳細資訊，請參閱＜哪裡可以取得 ESRI 形狀檔？＞ 在[地圖精靈與地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md) 中。  
  
 空間資料可能是政治敏感的內容，也可能受著作權保護。 查閱空間資料來源的使用條款與隱私權聲明，了解如何在報表中使用空間資料。  
  
 在您找到所需的資料之後，可以將該資料內嵌在報表定義中，或在處理報表時動態擷取該資料。 如需詳細資訊，請參閱本主題稍後的＜ [平衡報表定義大小與報表處理時間](#Embedding) ＞。  
  
### <a name="determine-the-spatial-data-and-the-spatial-data-match-fields"></a>決定空間資料與空間資料符合欄位  
 若要在地圖上顯示分析資料，以及更改大小、色彩或標記類型，您必須指定讓空間資料和分析資料產生關聯的欄位。  
  
 空間資料必須包含下列欄位：  
  
-   **Spatial data.** 包含定義每個點、線條或多邊形之座標組的空間資料欄位。  
  
-   **符合欄位：** 唯一識別每個空間資料欄位的一個或多個欄位。 例如，對於商店位置點，您可能會使用商店的名稱。 如果商店名稱在空間資料中不是唯一的，您可以加入城市名稱以及商店名稱。  
  
 若要讓空間資料與分析資料產生關聯，請使用符合欄位。  
  
### <a name="determine-the-analytical-data-and-the-analytical-data-match-fields"></a>決定分析資料與分析資料符合欄位  
 識別空間資料之後，您必須識別分析資料。 分析資料可能是來自下列來源：  
  
-   現有的報表資料集。 系統會將欄位指定為簡單的欄位運算式，例如，[Sales] 或 =Fields!Sales.Value。  
  
-   空間資料來源所提供的資料欄位。 系統會將欄位指定為開頭為 #，後面緊接著空間資料來源中之欄位名稱的關鍵字。  
  
 接著，您必須決定符合欄位的名稱：  
  
-   符合欄位： 一個或多個欄位，會指定與空間資料符合欄位相同資訊以建立空間資料與分析資料之間的關聯性。 符合欄位應該符合資料類型與格式。  
  
 當您已經識別空間資料來源、空間資料、分析資料來源、分析資料，以及符合欄位之後，您就可以決定要加入至您報表之地圖的類型。  
  
##  <a name="MapType"></a> 選擇地圖類型  
 當您執行「地圖精靈」時，您會將地圖和第一個地圖圖層加入至報表。 此精靈可讓您將下列其中一個類型的地圖加入至報表中：  
  
-   顯示沒有相關分析資料之位置的基本地圖。  
  
-   包含一個與每個地圖元素相關之分析值的地圖，例如，每個商店位置的銷售總額。  
  
-   包含一個以上與地圖元素相關之分析值的地圖，例如，客戶數目與每個商店位置的銷售總額。  
  
 下表描述每一個地圖類型。 所有地圖類型都可以讓您選取控制調色盤、框線樣式與字型的主題，而且會顯示標籤。  
  
|精靈圖示|圖層樣式|圖層類型|描述及選項|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../../reporting-services/report-design/media/rs-maptype-polygon-basic.gif "rs_MapType_Polygon_Basic")|基本地圖|多邊形|僅顯示區域的地圖，例如銷售領域。<br /><br /> 選項：依調色盤更改色彩或使用單一色彩。 調色盤是預先定義的一組色彩。 當調色盤中的所有色彩都經過指派之後，就會指派色彩的陰影。|  
|![rs_MapType_Polygon_ColorAnalytical](../../reporting-services/report-design/media/rs-maptype-polygon-coloranalytical.gif "rs_MapType_Polygon_ColorAnalytical")|色彩分析地圖|多邊形|透過更改色彩顯示分析資料的地圖，例如，依地區顯示的銷售資料。|  
|![rs_MapType_Polygon_Bubble](../../reporting-services/report-design/media/rs-maptype-polygon-bubble.gif "rs_MapType_Polygon_Bubble")|泡泡地圖|多邊形|透過更改在區域上置中的泡泡大小來顯示分析資料的地圖，例如，依地區顯示的銷售資料。<br /><br /> 選項：根據另一個分析欄位更改區域色彩，然後指定色彩規則。|  
|![rs_MapType_Line_Basic](../../reporting-services/report-design/media/rs-maptype-line-basic.gif "rs_MapType_Line_Basic")|基本線條地圖|行|僅顯示線條的地圖，例如傳遞路線。<br /><br /> 選項：依調色盤更改色彩或使用單一色彩。|  
|![rs_MapType_Line_Analytical](../../reporting-services/report-design/media/rs-maptype-line-analytical.gif "rs_MapType_Line_Analytical")|分析線條地圖|線條|更改線條色彩與寬度的地圖，例如，已傳遞的封裝數目以及依路線顯示的準時度量資訊。<br /><br /> 選項：依某個分析欄位更改線條寬度、依另一個分析欄位更改線條色彩，然後指定色彩規則。|  
|![rs_MapType_Marker_Basic](../../reporting-services/report-design/media/rs-maptype-marker-basic.gif "rs_MapType_Marker_Basic")|基本標記地圖|點|顯示每個位置之標記的地圖，例如城市。<br /><br /> 選項：依調色盤更改色彩或使用單一色彩，然後變更標記樣式。|  
|![rs_MapType_Marker_Bubble](../../reporting-services/report-design/media/rs-maptype-marker-bubble.gif "rs_MapType_Marker_Bubble")|泡泡標記地圖|點|針對每個位置顯示泡泡，並依某個分析資料欄位更改泡泡大小的地圖，例如，依城市顯示的銷售資料。<br /><br /> 選項：根據另一個分析欄位更改泡泡色彩，然後指定色彩規則。|  
|![rs_MapType_Marker_Analytical](../../reporting-services/report-design/media/rs-maptype-marker-analytical.gif "rs_MapType_Marker_Analytical")|分析標記地圖|點|在每個位置顯示標記，並根據分析資料更改標記色彩、大小與類型的地圖，例如，最暢銷的產品、收益範圍與折扣策略。<br /><br /> 選項：依某個分析欄位更改標記類型、依另一個分析欄位更改標記大小，依第三個分析欄位更改標記色彩，然後指定色彩規則。|  
  
 使用「地圖精靈」加入地圖之後，您可以使用「圖層精靈」建立其他圖層或變更圖層的選項。 如需精靈的詳細資訊，請參閱[地圖精靈和地圖圖層精靈 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)。  
  
 您可以針對每個圖層分別自訂顯示或資料選項。 如需在執行精靈後自訂地圖的詳細資訊，請參閱 [自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)中。  
  
##  <a name="Legend"></a> 規劃圖例  
 為協助您的使用者解譯地圖，您可以加入多個地圖圖例、色階，以及距離標尺。 當您設計地圖時，規劃您希望圖例顯示的位置。 您可以指定有關每個圖例的下列資訊：  
  
-   **圖例位置。** 例如，圖例可以顯示檢視區內部或外部，以及相對於檢視區的 12 個離散位置。  
  
-   **圖例樣式：** 例如，您可以指定字型樣式、框線樣式、分隔線與填滿屬性。  
  
-   **圖例標題。** 例如，您可以指定標題文字，以及個別控制要顯示地圖圖例的標題還是色階。  
  
-   **地圖圖例配置。** 例如，地圖圖例可以顯示為高的資料表或寬的資料表。  
  
 系統會根據您為每個圖層設定的規則選項，在報表處理期間自動建立圖例的內容。  
  
 根據預設，所有圖層都會將規則結果顯示在第一個地圖圖例中。 您可以建立多個圖例，然後針對每個規則，指派要用來顯示結果的圖例。  
  
 如需詳細資訊，請參閱[使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md) 和[變更地圖圖例、色階與相關的規則 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)。  
  
##  <a name="Embedding"></a> 平衡報表定義大小與報表處理時間  
 對於地圖而言，良好的報表設計會要求您平衡控制報表效能與報表定義大小的選項。 以空間資料或 Bing 地圖底圖為基礎的地圖元素可以是靜態的，而且內嵌在報表定義中，或者是動態的，而且在每次處理報表時建立。 您必須評估靜態或動態地圖資料的權衡得失，並找出適合您狀況的平衡點。 請考量下列資訊再做決定：  
  
-   內嵌的地圖元素可能會大幅增加報表定義的大小，但是會減少檢視報表中之地圖所需的時間。 您的報表伺服器可能有需要處理的大小限制。  
  
-   報表定義會指定可以處理之空間資料點的數目限制以及個別的值 (指定可包含在報表定義中之地圖元素的數目)。  
  
-   動態地圖元素會減少報表定義的大小，但是會增加處理及呈現地圖所需的時間。  
  
-   當空間資料的來源位於您的電腦上，則地圖元素永遠會內嵌在報表定義中。 其中包括來自地圖庫的空間資料，或是已經安裝在本機的 ESRI 形狀檔。  
  
 若要使用動態空間資料，空間資料來源必須位在報表伺服器上。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中設計報表時，可以將空間資料來源加入至專案中，然後與報表定義一起發行至報表伺服器。 如果您要使用報表產生器設計報表，必須先將空間資料上傳至報表伺服器，然後在精靈或圖層屬性中，指定地圖圖層之空間資料的來源。  
  
## <a name="see-also"></a>另請參閱  
 [自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [教學課程：地圖報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-map-report-report-builder.md)   
 [地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [報表疑難排解：地圖報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
