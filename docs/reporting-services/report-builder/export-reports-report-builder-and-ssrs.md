---
title: "匯出報表 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
caps.latest.revision: 23
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: db9a6cef14a145c8546a0f47a71bf83a358d483c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---

# <a name="export-reports-report-builder-and-ssrs"></a>匯出報表 (報表產生器及 SSRS)

  您可以將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表匯出成另一種檔案格式 (例如 PowerPoint、Image、PDF、 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]或 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] )，或是透過產生 Atom 服務文件，並且列出報表中所提供與 Atom 相符的資料摘要，藉此匯出報表。 您可以從報表產生器、報表設計師 ([!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]) 或報表伺服器匯出報表。  
  
 匯出報表來執行下列操作：  
  
-   **在其他應用程式中處理報表資料。** 例如，您可以將報表匯出到 Excel，然後在 Excel 中繼續處理資料。  
  
-   **以不同的格式列印報表。** 例如，您可以將報表匯出為 PDF 檔案格式，然後列印報表。  
  
-   **將報表複本儲存為其他檔案類型。** 例如，您可以將報表匯出為 Word 並儲存，以建立報表的複本。  
  
-   **使用報表資料做為應用程式中的資料摘要。** 例如，您可以產生符合 Atom 的資料摘要的 Power Pivot 或 Power BI 中，可以使用，並使用 Power Pivot 或 Power BI 中的資料。 如需詳細資訊，請參閱[從報表產生資料摘要](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)  
  
-   當您設定訂閱或透過電子郵件傳遞報表時，或者，如果您想要儲存報表伺服器上提供的報表時，在報表伺服器上轉譯報表很有用。 如需詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供許多轉譯延伸模組，可支援將報表匯出為常用的檔案格式。 轉譯延伸模組支援軟分頁 (例如 Word 或 Excel)、手動分頁 (例如 PDF 或 TIFF)，或是僅限資料 (例如 CSV 或與 Atom 相符的 XML) 的檔案格式。  
  
 當您將報表匯出為不同格式時，報表分頁可能會受到影響。 當您預覽報表時，其實是檢視遵循軟分頁規則的 HTML 轉譯延伸模組所轉譯的報表。 當您將報表匯出為不同的檔案格式 (例如 Adobe Acrobat (PDF)) 時，分頁是根據實體頁面大小而定，並且遵循手動分頁規則。 這些頁面也可以利用您加入到報表的邏輯分頁符號來分隔，但是頁面的實際長度會根據您所使用的轉譯器類型而有所不同。 若要變更報表的分頁，您必須了解所選擇的轉譯延伸模組的分頁行為。 您可能需要針對此轉譯延伸模組調整報表配置的設計。 如需詳細資訊，請參閱[頁面配置和轉譯](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="bkmk_export_from_rb"></a> 從報表產生器匯出報表

1.  執行或預覽報表。  
  
2.  在功能區上按一下 **[匯出]**。  
  
     ![報表產生器匯出](../../reporting-services/report-builder/media/ssrb-export.png "產生器匯出報表")  
  
3.  選取要使用的格式。  
  
     [另存新檔] 對話方塊隨即開啟。 依預設，檔案名稱就是您匯出之報表的名稱。 您可以選擇變更檔案名稱。  
  
##  <a name="bkmk_export_from_rm"></a> 從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站匯出報表  
  
1.  從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站的 [首頁] 上，巡覽至您要匯出的報表。  
  
2.  按一下報表來轉譯和預覽報表。  
  
3.  在 [報表檢視器] 工具列上，按一下 [匯出] 下拉式箭頭。  
  
     ![Reporting Services web 入口網站匯出](../../reporting-services/report-builder/media/ssrsportal-export.png "Reporting Services web 入口網站匯出")  
  
4.  選取要使用的格式。  
  
5.  按一下 **[匯出]**。 隨即出現對話方塊，詢問您是要開啟還是儲存檔案。  
  
6.  若要以選取的匯出格式檢視報表，按一下 **[開啟]**。  
  
     \- 或 -  
  
     若要以選取的匯出格式立即儲存報表，按一下 **[儲存]**。  
  
     使用與您選擇之格式相關聯的應用程式，顯示或儲存報表。 如果您按一下 **[儲存]**，系統會提示您儲存報表的位置。  
  
##  <a name="bkmk_export_from_sharepoint"></a> 從 SharePoint 文件庫匯出報表  
  
1.  預覽報表。  
  
2.  在工具列上，按一下 **[動作]**，指向 **[匯出]**，然後選取您要使用的格式。  
  
     隨即開啟 **[檔案下載]** 對話方塊。  
  
3.  若要以選取的匯出格式檢視報表，按一下 **[開啟]**。  
  
     \- 或 -  
  
     若要以選取的匯出格式立即儲存報表，按一下 **[儲存]**。  
  
     使用與您選擇之格式相關聯的應用程式，顯示或儲存報表。 如果您按一下 **[儲存]**，系統會提示您儲存報表的位置。  
  
     您可以選擇變更匯出之報表的檔案名稱。  
  
     **注意** ：如果因為您沒有與此檔案類型相關聯的程式而無法以您所選擇的格式開啟報表，系統將會提示您儲存匯出的報表，或在線上尋找一個程式來開啟該報表。  
  
##  <a name="RendererTypes"></a> 轉譯延伸模組類型  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 轉譯延伸模組有三種類型：  
  
-   **資料轉譯器延伸模組** ：資料轉譯延伸模組會移除報表的所有格式設定和配置資訊，並且只顯示資料。 產生的檔案可用於將原始報表資料匯入到其他檔案類型 (例如，Excel)、其他資料庫、XML 資料訊息，或是自訂應用程式。 資料轉譯器不支援分頁符號。  
  
     支援下列資料轉譯延伸模組：CSV、XML 及 Atom。  
  
-   **非強制分頁轉譯器延伸模組** ：非強制分頁轉譯延伸模組會維持報表配置和格式設定。 產生的檔案最適合使用螢幕檢視與傳遞，例如，使用網頁或 **ReportViewer** 控制項。  
  
     以下為支援的軟分頁轉譯延伸模組： [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 和網頁封存 (MHTML)。  
  
-   **強制分頁轉譯延伸模組** ：強制分頁轉譯器延伸模組會維持報表配置和格式設定。 所產生的檔案最適合一致的列印結果，或者以書本格式線上檢視報表。  
  
     以下為支援的手動分頁轉譯延伸模組：TIFF 和 PDF。  
  
##  <a name="ExportFormats"></a> 可在檢視報表時匯出的格式  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供轉譯延伸模組，可將報表轉譯成各種不同格式。 您應該針對所選的檔案格式進行報表設計最佳化。  下表列出您可以從使用者介面匯出的格式。  有一些額外格式可以與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱搭配使用，或者，從 URL 存取匯出時也會有一些額外格式。  請參閱本主題中的 [匯出報表的其他方式](#OtherWaysExportingReports)一節。  
  
|格式|轉譯延伸模組類型|說明|  
|------------|------------------------------|-----------------|  
|Acrobat (PDF) 檔案|手動分頁|PDF 轉譯延伸模組會將報表轉譯成可在 Adobe Acrobat 與支援 PDF 1.3 之其他協力廠商 PDF 檢視器中開啟的檔案。 雖然 PDF 1.3 與 Adobe Acrobat 4.0 和更新版本相容，但是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 只支援 Adobe Acrobat 6 或更新版本。 轉譯延伸模組不需要 Adobe 軟體就能轉譯報表。 不過，必須使用 PDF 檢視器 (例如 Adobe Acrobat) 才能檢視或列印 PDF 格式的報表。<br /><br /> 如需詳細資訊，請參閱[匯出至 PDF 檔案](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)。|  
|Atom|資料|Atom 轉譯延伸模組會從報表產生與 Atom 相符的資料摘要。 資料摘要讀取與交換應用程式，例如 Power Pivot 或 Power BI 中，可以取用符合 Atom 的資料摘要。<br /><br /> 輸出結果為 Atom 服務文件，其中會列出可從報表取得的資料摘要。 針對報表中的每一個資料區，至少會建立一個資料摘要。 根據資料區的類型以及該資料區顯示的資料而定，可能會產生多個資料摘要。<br /><br /> 如需詳細資訊，請參閱[從報表產生資料摘要](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)。|  
|CSV|資料|逗號分隔值 (CSV) 轉譯延伸模組會將報表從多數應用程式都可輕易讀取與交換的標準化純文字格式報表，轉譯為扁平化表示的資料。<br /><br /> 如需詳細資訊，請參閱[匯出至 CSV 檔案](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)。|  
|EXCELOPENXML|軟分頁|檢閱報表時，在匯出功能表中顯示為 "Excel"。 Excel 轉譯延伸模組會將報表轉譯成與 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2013 相容的 Excel 文件 (.xlsx)。  如需詳細資訊，請參閱[匯出至 Microsoft Excel](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。|  
|PowerPoint|手動分頁|PowerPoint 轉譯擴充功能會將報表轉譯成與 PowerPoint 2013 相容的 PowerPoint 文件 (.pptx)。|  
|TIFF 檔案|手動分頁|影像轉譯延伸模組會將報表轉譯成點陣圖或中繼檔。 依預設，影像轉譯延伸模組會產生報表的 TIFF 檔，可在多個頁面中檢視。 當用戶端接收到影像時，可以在影像檢視器中顯示和列印影像。<br /><br /> 影像轉譯延伸模組可產生 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]支援的任何格式檔案：BMP、EMF、EMFPlus、GIF、JPEG、PNG 和 TIFF。<br /><br /> 如需詳細資訊，請參閱[匯出至影像檔](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)。|  
|網頁封存|軟分頁|HTML 轉譯延伸模組會轉譯 HTML 格式的報表。 轉譯延伸模組也可產生完整的 HTML 頁面，或內嵌在其他 HTML 頁面中的 HTML 片段。 所有 HTML 均以 UTF-8 編碼產生。<br /><br /> HTML 轉譯延伸模組是在報表產生器中預覽以及瀏覽器中檢視之報表的預設轉譯延伸模組，包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站中執行時。<br /><br /> 如需詳細資訊，請參閱[轉譯為 HTML](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)。|  
|WORDOPENXML|軟分頁|檢閱報表時，在匯出功能表中顯示為 "Word"。 Word 轉譯延伸模組會將報表轉譯成與 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2013 相容的 Word 文件 (.docx)。  如需詳細資訊，請參閱[匯出至 Microsoft Word](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)。|  
|XML|資料|XML 轉譯延伸模組會傳回 XML 格式的報表。 報表 XML 的結構描述為報表特有的，且僅包含資料。 XML 轉譯延伸模組不會轉譯配置資訊，也不會維持分頁。 此延伸模組所產生的 XML 可以匯入資料庫中 (當做 XML 資料訊息使用)，或傳送到自訂應用程式。<br/><br/> 如需詳細資訊，請參閱[匯出至 XML](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)。|  
  
##  <a name="GeneratingDataFeedsFromReport"></a> 從報表產生資料摘要  
 若要從報表產生資料摘要，請在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站中執行報表，然後按一下入口網站工具列上的 **產生資料摘要** 圖示。 系統會提示您選擇要儲存還是開啟檔案。 如果您選擇 **[開啟]**，Atom 服務文件會在與 .atomsvc 副檔名相關聯的應用程式中開啟。 如果您選擇 **[儲存]**，文件會儲存為 .atomsvc 檔。 根據預設，檔案的名稱會是報表的名稱。 您可以將名稱變更為更有意義的名稱。  
  
 將 Atom 服務文件儲存到您的電腦上。 之後您可以將文件上傳到報表伺服器或是其他伺服器，以供其他人使用。 如需詳細資訊，請參閱[從報表產生資料摘要](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)和[從報表產生資料摘要](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)。  
  
##  <a name="Troubleshooting"></a> 匯出的報表疑難排解  
 在您將報表匯出成另一種格式後，有時報表看起來會跟原來不一樣，或是未能依照您希望的方式運作。 發生這種情況的原因是，轉譯器可能套用了某些規則和限制。 當您建立報表時，可以考量許多限制來加以對付。 您可能需要在報表中使用稍微不同的配置、小心對齊報表內的項目、將報表頁尾限制為單行文字等等。  
  
 若您的報表包含具有阿拉伯數字的 Unicode 文字，或是包含阿拉伯日期，則當您使用下列格式之一將報表匯出或列印報表時，會無法正確轉譯日期與數字。  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   影像/TIFF  
  
 若您將報表匯出為 HTML，可正確轉譯日期與數字。  
  
 與特定轉譯器相關的主題將敘述每種轉譯器轉譯報表項目和資料區的方式，以及其限制與解決方案。  
  
-   [匯出至 CSV 檔案 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [匯出至 Microsoft Word &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [轉譯為 HTML &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)  
  
-   [匯出至 PDF 檔案 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [匯出至影像檔 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [匯出至 XML &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了額外的功能，可協助您建立在其他格式中正常運作的報表。 在 Tablix 資料區 (資料表、矩陣和清單)、群組和矩形上的分頁符號，可讓您更充分掌控報表的分頁。 以分頁符號隔開的報表頁面，可以有不同的頁面名稱，以及重設頁碼編排方式。 頁面名稱和頁碼可以透過運用運算式，以動態方式在報表執行時更新。 如需詳細資訊，請參閱[Reporting Services 中的分頁](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
 此外，您還可以使用內建的全域 RenderFormat，針對不同的轉譯器依條件套用不同的報表配置。 如需詳細資訊，請參閱[Built-in Globals and Users References](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)

##  <a name="OtherWaysExportingReports"></a> 匯出報表的其他方式  
 匯出報表是在您於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站或報表產生器中開啟報表時，視需要而執行的工作。 如果您想要使匯出作業自動化 (例如，依重複執行的排程，以特定檔案類型將報表匯出至共用資料夾)，請建立訂閱，將報表傳遞至共用資料夾。 如需詳細資訊，請參閱＜ [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)＞。  
  
 在報告工具中預覽的報表或在瀏覽器應用程式 (例如 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站) 中開啟的報表，一律會先以 HTML 格式轉譯。 您無法指定不同的轉譯延伸模組做為檢視的預設值。 不過，您可以建立訂閱，以您要的轉譯格式產生報表，然後傳遞至電子郵件收件匣或共用資料夾。 如需詳細資訊，請參閱 [建立及管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) 和 [建立、修改和刪除資料驅動訂閱](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)。  
  
 您也可以透過指定轉譯延伸模組做為 URL 參數的 URL 存取報表，並且直接將報表轉譯成指定的格式，而不需先轉譯為 HTML。 下列範例會以 Excel 格式轉譯報表：  
  
```  
http://<Report Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 而下列會從具名執行個體轉譯 PowerPoint 報表︰  
  
```  
http://<Report Server Name/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 如需詳細資訊，請參閱 [Export a Report Using URL Access](../../reporting-services/export-a-report-using-url-access.md)。  

## <a name="next-steps"></a>後續的步驟

[控制分頁符號、標題、資料行和資料列 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
[尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
[列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
[儲存報表 &#40;報表產生器&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

