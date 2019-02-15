---
title: 頁面配置和轉譯 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f14a144bcdfbfd65d7ea3e99d9ac03d7b2ee0f1d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294426"
---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>頁面配置和轉譯 (報表產生器及 SSRS)
  當您撰寫報表時，最好了解 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 轉譯器的行為以確保經過轉譯的報表看起來是您想要的方式，包括頁面配置與分頁。 您也可能想要確認經過轉譯的報表是否符合您或組織常用的紙張大小。  
  
 當您在報表管理員或是報表產生器或報表設計師的預覽窗格中檢視報表時，報表會先透過 HTML 轉譯器進行轉譯。 接著，您可以將報表匯出為不同的格式，例如 Excel 或逗點分隔檔 (CSV)。 然後，匯出的報表可以在 Excel 中進行進一步的分析，或是當做可以匯入與使用 CSV 資料檔之應用程式的資料來源使用。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含一組轉譯器，可將報表輸出成不同的格式。 轉譯報表時，每個轉譯器都有套用規則。 當您將報表匯出為不同的檔案格式 (特別是針對轉譯器，例如，根據實際頁面大小使用分頁的 Adobe Acrobat (PDF) 轉譯器) 時，您可能需要變更報表的配置，讓匯出的報表在套用轉譯規則之後的外觀和列印都正確無誤。  
  
 讓匯出的報表得到最佳效果通常是一個反覆的程序。您會在報表產生器或報表設計師中撰寫並預覽報表、將報表匯出至慣用的格式、檢閱匯出的報表，然後針對報表進行變更。  
  
 本主題提供 Reporting Services 轉譯延伸模組及其使用方式的相關資訊。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="PageLayout"></a> 頁面配置] 和 [報表項目  
 報表項目是指與不同類型的報表資料相關聯的配置元素。 資料表、矩陣、清單、圖表和量測計都是資料區報表項目，每一個都會連結到報表資料集。 處理報表時，資料區會展開到報表頁面的下方，以便顯示資料。 其他報表項目會連結到單一項目，並顯示單一項目。 **[影像]** 報表項目會連結到圖片。 **[文字方塊]** 報表項目包含類似標題或運算式的簡單文字，其中可以包含內建欄位、報表參數或資料集欄位的參考。 **[線條]** 和 **[矩形]** 報表項目則提供了報表頁面上的簡單圖形化元素。 **[矩形]** 也可以是其他報表項目的容器。 報表可以包含子報表。  
  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]時，您可以將報表項目放在設計介面上的任何地方。 您可以使用貼齊格線和調整大小的控點，以互動方式放置、展開及收縮報表項目的最初形狀。 您可以並排不同組的資料來放置資料區，甚至是不同格式的相同資料。 當您將報表項目放在設計介面上時，它會有預設的大小和形狀，而且與所有其他報表項目之間具有初始關聯性。 您可以交互放置許多報表項目，以便建立更複雜的報表設計。 例如，在資料表資料格中放置圖表或影像、在資料表資料格中放置資料表，以及在矩形中放置多個影像。 除了提供您想要讓報表呈現的組織和外觀以外，在矩形等容器中放置報表項目也有助於控制報表項目顯示在報表頁面上的方式。  
  
 報表可以合併多個頁面，每一個頁面上都有重複的頁首和頁尾。 報表可以包含類似影像和線條的圖形元素，也可以有多種字型、色彩和樣式 (可以根據運算式)。  
  
##  <a name="ReportSections"></a> 報表區段  
 報表是由三個主要區段所組成：選擇性頁首、選擇性頁尾和報表主體。 報表頁首和頁尾不是報表的個別區段，而是由放置於報表主體上方和底部的報表項目所組成。 頁首和頁尾會在每個報表頁面的上方和底部重複相同的內容。 您可以將影像、文字方塊和線條放在頁首和頁尾中。 您也可以將所有類型的報表項目都放在報表主體中。  
  
 您可以在報表項目上設定屬性，即可一開始在頁面上隱藏或顯示這些項目。 您可以在資料列或資料行或是資料區的群組上設定可見性屬性，並提供切換按鈕讓使用者以互動方式顯示或隱藏報表資料。 您可以使用運算式 (包括了根據報表參數的運算式) 來設定可見性或初始可見性。  
  
 當處理報表時，報表資料會結合報表配置元素，而已結合的資料則會傳送到報表轉譯器。 此轉譯器遵循報表項目展開的預先定義規則，而且可決定每個頁面所容納的資料量。 若要設計容易閱讀的報表，並針對您打算使用的轉譯器最佳化此報表，您應該了解用於控制 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中之分頁的規則。 如需詳細資訊，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
##  <a name="RenderingExtensions"></a> 轉譯器  
 Reporting Services 包含一組轉譯器 (也稱為轉譯延伸模組)，您可以使用這組轉譯器將報表匯出為不同的格式。 轉譯器有三種類型：  
  
-   **資料轉譯器** ：資料轉譯器會從報表移除所有格式與版面配置資訊，而僅顯示資料。 所產生的檔案可用於將原始報表資料匯入到其他檔案類型 (例如，Excel)、其他資料庫、XML 資料訊息，或是自訂應用程式。 可用的資料轉譯器是：CSV 和 XML。  
  
    > [!NOTE]  
    >  雖然它不提供直接匯出為不同格式的功能，但是 Atom 轉譯會從報表產生資料檔。  
  
-   **軟分頁轉譯器** ：軟分頁轉譯器會維持報表的版面配置和格式。 所產生的檔案最適合使用螢幕檢視與傳遞，例如，使用網頁。 可用的軟分頁符號轉譯器是：[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word、 網頁封存 (MHTML)，和 HTML。  
  
-   **手動分頁轉譯器** ：手動分頁轉譯器會維持報表的版面配置和格式。 所產生的檔案最適合一致的列印結果，或者以書本格式線上檢視報表。 可用的手動分頁符號轉譯器支援：TIFF 和 PDF。  
  
 當您在報表產生器或報表設計師中預覽報表，或在報表管理員中執行報表時，報表一定會先以 HTML 轉譯。 在執行報表後，您可以將它匯出為其他的檔案格式。 如需詳細資訊，請參閱 <<c0> [ 匯出的報表&#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)。</c0>  
  
  
  
##  <a name="RenderingBehaviors"></a> 轉譯行為  
 根據所選取的轉譯器，當轉譯報表時，系統會套用某些規則。 將報表項目全部容納在一頁的方式，取決於下列因素的組合：  
  
-   轉譯規則。  
  
-   報表項目的寬度和高度。  
  
-   報表主體的大小。  
  
-   頁面的寬度和高度。  
  
-   用於分頁的轉譯器特定支援。  
  
 例如，轉譯為 HTML 和 MHTML 格式的報表會針對各種長度的頁面，提供最佳的電腦螢幕檢視效果。  
  
 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)。  
  
  
  
##  <a name="Pagination"></a> 分頁  
 分頁指的是報表內的頁數，以及如何在這些頁面上排列報表項目。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的分頁會根據您用於檢視和傳遞報表的轉譯延伸模組，以及您設定報表使用的分頁符號和保持在一起的選項而有所不同。  
  
 若要為使用者成功設計容易閱讀的報表，並針對計畫用於傳遞報表的轉譯器最佳化該報表，您必須了解用於控制 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中之分頁的規則。 使用資料與軟分頁轉譯延伸模組匯出的報表通常不會受到分頁影響。 當您使用資料轉譯延伸模組時，報表會以 XML 或 CSV 格式轉譯為表格式資料列集。 為確保匯出的報表資料可以使用，您應該了解從報表套用至已轉譯之扁平化表格式資料列集的規則。  
  
 當您使用軟分頁轉譯延伸模組 (例如，HTML 轉譯延伸模組) 時，您可能想要知道報表列印後的外觀，同時也想知道使用 PDF 之類的手動分頁轉譯器的效果如何。 在建立或更新報表期間，您可以在報表產生器和報表設計師中預覽並匯出該報表。  
  
 手動分頁轉譯器對於報表版面配置與實際頁面大小擁有最大的影響力。 若要深入了解，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節列出的程序可以為您逐步示範如何在報表中使用分頁。  
  
-   [加入分頁符號 &#40;報表產生器及 SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md)  
  
-   [在多個頁面上顯示資料列和資料行標頭 &#40;報表產生器及 SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [加入或移除頁首或頁尾 &#40;報表產生器及 SSRS&#41;](add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [在報表中捲動時將標頭保持可見 &#40;報表產生器及 SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [顯示頁碼或其他報表屬性 &#40;報表產生器及 SSRS&#41;](display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [隱藏第一頁或最後一頁的頁首或頁尾 &#40;報表產生器及 SSRS&#41;](hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
  
  
##  <a name="InThisSection"></a> 本節內容  
 下列主題提供有關頁面配置與轉譯的其他資訊。  
  
 [頁首和頁尾 &#40;報表產生器及 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)  
 提供有關如何在報表中使用頁首與頁尾，以及如何使用頁首與頁尾控制分頁的資訊。  
  
 [控制分頁符號、標題、資料行和資料列 &#40;報表產生器及 SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 提供有關使用分頁符號的資訊。  
  
  
  
## <a name="see-also"></a>另請參閱  
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
