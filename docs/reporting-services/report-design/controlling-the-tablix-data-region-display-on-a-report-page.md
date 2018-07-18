---
title: 控制報表頁面上的 Tablix 資料區顯示 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f81c48cc-f038-4f57-988d-e9a3cbb46424
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05ebc27d8ca5ac641819e01c0e9cf3e5cbc27457
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022005"
---
# <a name="controlling-the-tablix-data-region-display-on-a-report-page"></a>控制報表頁面上的 Tablix 資料區顯示
請了解您可在資料表、矩陣或清單資料區之 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中設定的屬性，以變更它在您檢視報表時的顯示方式。  
   
## <a name="controlling-the-appearance-of-data"></a>控制資料的外觀  
資料表、矩陣和清單資料區都是 *Tablix* 資料區的範例。 下列功能有助於控制 Tablix 資料區的外觀：  
  
-   **格式化資料。** 若要格式化資料表、矩陣或清單中的資料，請在資料格中設定文字方塊的格式屬性。 您可以同時設定多個資料格的屬性。 若要格式化圖表中的資料，設定數列的格式屬性。 如需詳細資訊，請參閱[格式化報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md) 和[格式化圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)。  
  
-   **撰寫運算式**。 如需詳細資訊，請參閱[報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md) 和[運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)。  
  
-   **控制排序次序**。 若要控制排序次序，您可以針對資料區定義排序運算式。 若要控制與群組相關聯之資料列和資料行的排序次序，您可以針對群組 (包括詳細資料群組) 定義排序運算式。 您也可以加入互動式排序按鈕，讓使用者排序 Tablix 資料區或其群組。 如需詳細資訊，請參閱[在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
-   **沒有資料時顯示訊息**。 報表資料集在執行階段沒有資料存在時，您可以撰寫自己要顯示的訊息來取代資料區。 如需詳細資訊，請參閱[在資料區域中設定沒有資料的訊息 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)。  
  
-   **有條件地隱藏資料**。 若要有條件地控制要顯示或隱藏一個資料區域或部分資料區域，您可以將 Hidden 屬性設定為 **True** 或設定為運算式。 運算式可以包含報表參數的參考。 您也可以指定切換項目，讓使用者可以決定顯示詳細資料。 如需詳細資訊，請參閱[向下鑽研動作 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)。  
  
-   **合併資料格。** 資料表內多個連續的資料格可以組合成單一資料格。 這稱為資料行範圍或資料格合併。 資料格只能水平或垂直合併。 當您合併資料格時，只會保留第一個資料格的資料。 其他儲存格中的資料則會移除。 合併的資料格可以分割成原始資料行。 如需詳細資訊，請參閱[在資料區中合併資料格 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="controlling-tablix-data-region-position-and-expansion-on-a-page"></a>控制頁面上的 Tablix 資料區域位置和展開  
 下列功能有助於控制 Tablix 資料區顯示在轉譯報表中的方式：  
  
-   **控制 Tablix 資料區相對於其他報表項目的位置**。 Tablix 資料區可以放置在報表設計介面的其他報表項目上方、旁邊或下方。 在執行階段， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會針對為連結之資料集擷取的資料，在需要時展開 Tablix 資料區，並在需要時將對等報表項目移到一旁。 若要錨定其他報表項目旁的 Tablix，請讓報表項目成為對等，並調整其相對位置。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
-   **變更展開方向**。 若要控制 Tablix 資料區跨頁面從左至右 (LTR) 或從右至左 (RTL) 展開，請使用可透過 [屬性] 視窗存取的 Direction 屬性。 如需詳細資訊，請參閱[轉譯資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-data-regions-report-builder-and-ssrs.md)。  
  
## <a name="controlling-how-a-tablix-data-region-renders-on-a-page"></a>控制 Tablix 資料區在頁面上轉譯的方式  
 下列清單將描述您可以協助控制 Tablix 資料區如何在報表中顯示的方式：  
  
-   **控制分頁**。 若要控制顯示在每個報表頁面上的資料量，您可以針對資料區域設定分頁符號。 您也可以針對群組設定分頁符號。 分頁符號可以透過減少需要在每個頁面上處理的資料量來影響視需要轉譯的效能。 如需詳細資訊，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md) 和[新增分頁符號 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)。  
  
-   **在資料列標頭的任何一端顯示資料**。 您不一定要將資料列標頭顯示在 Tablix 資料區的旁邊。 您可以在資料行之間移動資料列標頭，使資料的資料行出現在資料列標頭之前。 若要這樣做，請修改矩陣的 GroupsBeforeRowHeaders 屬性。 您可以透過 [屬性] 視窗存取這個屬性。 這個屬性的值是整數；例如，2 這個值會先顯示資料區域資料行的兩個群組執行個體，然後才顯示包含資料列標頭的資料行。  
  
## <a name="controlling-how-tablix-row-and-column-groups-render"></a>控制 Tablix 資料列和資料行群組轉譯的方式  
 控制 Tablix 資料區群組轉譯的方式主要取決於群組結構。 Tablix 資料區可以有四個區域，如下圖所示：  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 資料列群組區域和資料行群組區域包含群組頁首。 當 Tablix 資料區具有群組頁首時，您就可以透過在 **[Tablix 屬性]** 對話方塊的 **[一般]** 頁面上設定屬性，來控制資料列和資料行重複的方式。  
  
 如果 Tablix 資料區只有 Tablix 主體區域，就沒有任何群組頁首。 只有靜態和動態 Tablix 成員存在。 相對於 Tablix 資料列或資料行群組，靜態成員會顯示一次。 動態成員則會針對每個唯一的群組值重複一次。 例如，在顯示銷售訂單的 Tablix 資料區中，銷售訂單中的資料行名稱可以顯示在靜態資料列成員上。 銷售訂單中的每一行都會顯示在動態資料列成員上。  
  
 您可以透過在 [屬性] 窗格中設定屬性，協助控制 Tablix 成員轉譯的方式。 如需詳細資訊，請參閱[群組窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md) 中的＜進階模式＞。  
  
 下列清單將描述您可以協助控制 Tablix 資料區如何在報表中顯示的方式：  
  
-   **在多個頁面上重複資料列與資料行標頭**。您可以在每個會用到 tablix 資料區域的頁面上，顯示資料列與資料行標頭。 如需詳細資訊，請參閱[在多個頁面上顯示資料列和資料行標頭 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)。  
  
-   **捲動時保留檢視中的資料列和資料行標頭**。 您可以控制在使用瀏覽器捲動報表時，是否要保留檢視中的資料列和資料行標頭。 如需詳細資訊，請參閱[在報表中捲動時將標頭保持可見 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)。  
  
 如需將報表匯出成不同格式如何影響 Tablix 資料區在頁面上轉譯之方式的詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [控制分頁符號、標題、資料行和資料列 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [建立矩陣](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [使用清單建立發票和表單](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
