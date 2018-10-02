---
title: 報表設計檢視 (報表產生器) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: da0c23b3fcc746fa2ad8614f88ce539386e71b6e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775316"
---
# <a name="report-design-view-report-builder"></a>報表設計檢視 (報表產生器)
  [報表產生器] 視窗的設計目的是要協助您輕鬆地組織報表資源和快速地建立所需的編頁報表。 設計介面位於視窗中央，並且具有功能區和窗格。 設計介面是您可以加入和組織報表項目的位置。 本文所說明的窗格可用來加入、選取並組織報表資源，以及變更報表項目屬性。  
  
 ![報表產生器設計檢視](../../reporting-services/report-builder/media/ssrb-designview.png "報表產生器設計檢視")  
  
1.  功能區  
  
2.  [參數窗格](#Ribbon)  
  
3.  [報表組件庫](#ReptPartGallery)  
  
4.  [屬性窗格](#PropertiesPane)  
  
5.  [報表設計介面](#RptDesignSurface)  
  
6.  [報表資料窗格](#ReptDataPane)  
  
7.  [群組窗格](#GroupPane)  
  
8.  目前報表狀態列  
  
##  <a name="Ribbon"></a> 參數窗格  
 您可以使用報表參數控制報表資料、將相關的報表連接在一起，以及變更報表呈現方式。 [參數] 窗格提供報表參數的彈性配置。  
  
 請深入閱讀 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
  
##  <a name="RptDesignSurface"></a> 報表設計介面  
 報表產生器的設計介面是設計報表時的主要工作區域。 若要在報表中放置資料區域、子報表、文字方塊、影像、矩形和線條等報表項目，可以將這些項目從功能區或報表組件庫加入設計介面中。 您可以從這裡對報表項目加入群組、運算式、參數、篩選、動作、可見性和格式。  
  
 也可以變更下列項目：  
  
-   報表主體屬性 (例如框線和填滿色彩)，方法是以滑鼠右鍵按一下設計介面上任何報表項目外部的白色區域，然後按一下 [主體屬性]。  
  
-   頁首和頁尾的屬性 (例如框線和填滿色彩)，方法是以滑鼠右鍵按一下設計介面上頁首或頁尾區域任何報表項目外部的白色區域，然後按一下 [頁首屬性] 或 [頁尾屬性]。  
  
-   報表本身的屬性 (例如版面設定)，方法是以滑鼠右鍵按一下設計介面周圍的灰色區域，然後按一下 [報表屬性]。  
  
-   報表項目的屬性，方法是以滑鼠右鍵按一下這些項目，然後按一下 [屬性]。  
  
 如需如何使用鍵盤在設計介面上操作項目的資訊，請參閱[鍵盤快速鍵 &#40;報表產生器&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
### <a name="design-surface-size-and-print-area"></a>設計介面大小和列印區域  
 設計介面大小可能與您指定來列印報表的頁面大小列印區域不同。 變更設計介面的大小無法變更報表的列印區域。 無論您為報表所設定的列印區域大小為何，完整的設計區域大小都不會變更。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
> [!TIP]  
>  若要顯示尺規，請在 [檢視] 索引標籤上選取 [尺規] 核取方塊。  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 在 [報表資料] 窗格中，您可以定義報表所需的報表資料和報表資源，然後再設計報表配置。 例如，您可以將資料來源、資料集、導出欄位、報表參數和影像加入至 [報表資料] 窗格。  
  
 當您將項目加入至 [報表資料] 窗格之後，只需要將欄位拖曳到設計介面上的報表項目，就可以控制資料要出現在報表中的位置。  
  
> [!TIP]  
>  如果您將欄位從 [報表資料] 窗格直接拖曳到報表設計介面，而不是將它放置在像是資料表或圖表等資料區域中，當您執行報表時，就只會看到該欄位中資料的第一個值。  
  
 您也可以將內建欄位從 [報表資料] 窗格拖曳到設計介面上。 進行轉譯時，這些欄位會提供有關報表的資訊，例如報表名稱、報表中的總頁數，以及目前的頁碼。  
  
 當您將某個項目加入到報表設計介面時，會自動將一些項目加入到 [報表資料] 窗格。 例如，如果從 [報表組件庫] 加入報表組件，由於報表組件是資料區域，資料集就會自動加入到 [報表資料] 窗格。 如需詳細資訊，請參閱 [報表產生器中的報表組件和資料集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)。 此外，如果將影像內嵌在報表中，它也會加入到 [報表資料] 窗格中的 [影像] 資料夾。  
  
> [!NOTE]  
>  您可以使用 [新增] 按鈕，將新的項目新增至 [報表資料] 窗格。 您可以從相同的資料來源或其他資料來源，將多個資料集加入至報表。 您可以從報表伺服器加入共用資料集。 若要從相同的資料來源新增新的資料集，請以滑鼠右鍵按一下資料來源，然後按一下 [新增資料集]。  
  
 如需 [報表資料] 窗格中項目的詳細資訊，請參閱下列主題：  
  
-   [內建的全域和使用者參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [影像 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)  
  
-   [資料連接、資料來源及連接字串 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
-   [報表內嵌資料集和共用資料集 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [資料集欄位集合 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> 報表組件庫  
 建立報表最簡單的方式，就是在報表伺服器或整合到 SharePoint 網站的報表伺服器找到現有的報表組件，如資料表和圖表。  
  
 按一下 [插入] 索引標籤上的 [報表組件] 以開啟 [報表組件庫]。 您可以在這裡搜尋報表組件，以加入報表中。 您可以依下列方式篩選報表組件：報表組件的全部或部分名稱、建立者、上次修改報表組件者、上次修改時間、儲存位置，或報表組件的類型。 例如，您可以依其中一個同事，搜尋上星期建立的所有圖表。  
  
> [!NOTE]  
>  若要檢視報表組件庫，則需要連接到伺服器。  
  
 您可以以縮圖或清單方式檢視搜尋結果，並依名稱、建立和修改日期，以及建立者來排序搜尋結果。 如需詳細資訊，請參閱[報表組件 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
  
##  <a name="PropertiesPane"></a> 屬性窗格 (報表產生器)  
 報表中的每個項目 (包括資料區域、影像、文字方塊和報表主體本身) 都具有相關聯的屬性。 例如，文字方塊的 BorderColor 屬性會顯示文字方塊框線的色彩值，而報表的 PageSize 屬性會顯示報表的頁面大小。  
  
 這些屬性會顯示在 [屬性] 窗格中。 窗格中的屬性會因您所選取的報表項目而有所不同。  
  
 若要查看 [屬性] 窗格，請在 [檢視] 索引標籤的 [顯示/隱藏] 群組中，按一下 [屬性]。  
  
### <a name="changing-property-values"></a>變更屬性值  
 在報表產生器中，您可以用許多方式來變更報表項目的屬性：  
  
-   按一下功能區上的按鈕和清單。  
  
-   變更對話方塊內的設定。  
  
-   變更 [屬性] 窗格內的屬性值。  
  
 對話方塊和功能區會提供最常用的屬性。  
  
 根據屬性而定，您可以從下拉式清單中選取屬性值、輸入值，或按一下 `<Expression>` 來建立運算式。  
  
### <a name="changing-the-properties-pane-view"></a>變更屬性窗格檢視  
 根據預設，顯示在 [屬性] 窗格中的屬性會組織成一些廣泛的類別目錄，例如 [動作]、[框線]、[填滿]、[字型] 和 [一般]。 每個類別目錄都具有一組相關聯的屬性。 例如，下列屬性列於 [字型] 類別目錄中：[Color]、[FontFamily]、[FontSize]、[FontStyle]、[FontWeight]、[LineHeight] 和 [TextDecoration]。 如果您想要，也可以依字母順序排列此窗格中所列的所有屬性。 這樣做會移除這些類別目錄並按照字母順序列出所有屬性，不論類別目錄為何。  
  
 [屬性] 窗格的窗格頂端具有三個按鈕：[類別目錄]、[按字母排列] 和 [屬性頁]。 按一下 [類別目錄] 和 [按字母排列] 按鈕，即可在 [屬性] 窗格檢視之間切換。 按一下 [屬性頁] 按鈕，即可開啟選取之報表項目的 [屬性] 對話方塊。  
  
  
##  <a name="GroupPane"></a> 群組窗格 (報表產生器)  
 群組的用途在於將報表資料組織為視覺階層以及計算總計。 您可以在設計介面和 [群組] 窗格中檢視資料區域內的資料列和資料行群組。 [群組] 窗格具有兩個窗格：[資料列群組] 和 [資料行群組]。 當您選取某個資料區域時，[群組] 窗格就會將該資料區域內的所有群組顯示成階層式清單：子群組會以縮排方式顯示在其父群組底下。  
  
 ![報表產生器的資料列群組](../../reporting-services/report-builder/media/ssrb-rowgroups.png "報表產生器的資料列群組")  
  
 您可以從 [報表資料] 窗格中拖曳欄位，然後將這些欄位放置在設計介面或 [群組] 窗格中，藉以建立群組。 在 [群組] 窗格中，您可以加入父群組、相鄰群組和子群組、變更群組屬性，以及刪除群組。  
  
 雖然系統預設會顯示 [群組] 窗格，但是您可以清除 [檢視] 索引標籤上的 [群組窗格] 核取方塊，藉以關閉此窗格。[群組] 窗格不適用於 [圖表] 或 [量測計] 資料區。  
  
 如需詳細資訊，請參閱[群組窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md) 和[了解群組 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
  
##  <a name="RunMode"></a> 在執行模式中預覽報表  
 在報表設計檢視中，您使用的不是實際資料，而是欄位名稱或運算式所指示之資料的表示。 當您想要查看顯示在所設計之報表內容中的實際資料時，可以執行報表來預覽顯示在報表配置中之基礎資料庫的資料。 在設計與執行報表之間切換，可讓您調整其設計並且立即查看結果。 若要預覽報表，請在功能區的 [檢視] 群組中，按一下 [執行]。  
  
 當您按一下 [執行] 時，報表產生器就會連線至報表資料來源、在電腦上快取資料、結合資料和配置，然後在 HTML 檢視器中轉譯報表。 在您繼續設計報表時，可以視需要不斷執行報表。 當您對報表感到滿意時，就可以將報表儲存至報表伺服器，具有適當權限的其他個人可以在其中檢視您的報表。  
   
 請深入閱讀 [在報表產生器中預覽報表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)。  
  
### <a name="running-a-report-with-parameters"></a>使用參數執行報表  
 當您執行報表時，系統會自動處理報表。 如果報表包含參數，所有參數都必須具有預設值，然後報表才能自動執行。 如果某個參數沒有預設值，當您執行報表時，就必須選擇該參數的值，然後按一下 [執行] 索引標籤上的 [檢視報表]。如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
### <a name="print-preview"></a>預覽列印  
 當您在執行模式中預覽報表時，它就類似於以 HTML 產生的報表。 這個預覽並不是 HTML，不過報表的配置及分頁與 HTML 的輸出相似。 您可以切換到預覽列印模式，以變更檢視來顯示列印的報表。 按一下 [執行] 索引標籤上的 [預覽列印] 按鈕。所顯示的報表就如同在實際頁面上所看到的。 這個檢視與影像和 PDF 轉譯延伸模組所產生的輸出類似。 預覽列印並不是影像或 PDF 檔案，不過報表的配置及分頁與這些格式的輸出相似。  
  
  
## <a name="see-also"></a>另請參閱  
 [尋找、檢視和管理報表 &#40;報表產生器和 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [SQL Server 2016 的報表產生器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  
  
