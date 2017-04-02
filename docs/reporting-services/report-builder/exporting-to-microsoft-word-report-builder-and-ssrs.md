---
title: "匯出至 Microsoft Word (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0cd8ae26-4682-4473-8f15-af084951defd
caps.latest.revision: 23
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 23
---
# 匯出至 Microsoft Word (報表產生器及 SSRS)
  Word 轉譯延伸模組會將分頁報表轉譯成 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 格式 (.docx)。 此格式為 Office Open XML。  
  
 此轉譯器會產生 **application/vnd.openxmlformats-officedocument.wordprocessingml.document** 內容類型的檔案，而檔案的副檔名為 .docx。  
  
 如需如何匯出至 Word 的詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。  
  
 將報表匯出至 Word 文件之後，您可以變更報表的內容，並設計文件樣式的報表，例如郵件標籤、訂購單或套印信件。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItemsWord"></a> Word 中的報表項目  
 匯出到 Word 的報表會顯示為代表報表主體的巢狀資料表。 系統會將 Tablix 資料區轉譯為巢狀資料表，以反映報表中資料區的結構。 文字方塊與矩形會分別轉譯為資料表內的資料格。 文字方塊值則會顯示在資料格內。  
  
 影像、圖表、資料橫條、走勢圖、地圖、指標與量測計會分別轉譯為資料表資料格內的靜態影像。 系統會轉譯這些報表項目的超連結與鑽研連結。 不支援可以在圖表內按一下的地圖和區域。  
  
 在 Word 中不會轉譯新聞稿樣式資料行的報表。 也不會轉譯報表主體與頁面背景影像和色彩。  
  
##  <a name="Pagination"></a> 分頁  
 在 Word 中開啟報表後，Word 會根據頁面大小，再次為整個報表分頁。 分頁可能會使分頁符號插入到您不想加入的位置，而且在某些情況下，可能會讓匯出的報表在資料列中有兩個接續的分頁符號，或者加入了空白頁。 您可以調整頁面邊界，藉以嘗試變更 Word 的分頁。  
  
 此轉譯器僅支援邏輯分頁符號。  
  
### 調整頁面大小  
 報表在進行轉譯時，Word 頁面高度與寬度會透過下列 RDL 屬性設定：紙張大小高度和寬度、頁面的左右邊界，以及頁面的上下邊界。  
  
### 頁寬  
 Word 支援的頁寬最多可達 22 英吋。 如果報表的寬度大於 22 英吋，轉譯器仍然會轉譯該報表，不過，Word 在列印配置檢視或閱讀版面配置檢視時，將不會顯示報表內容。 若要檢視資料，切換到標準檢視或 Web 版面配置檢視。 在這些檢視下，Word 會減少空白字元的總數，藉以顯示更多的報表內容。  
  
 進行轉譯時，報表會成長為所需的寬度 (最多 22 英吋)，才能顯示內容。 報表的寬度下限是以 [屬性] 窗格中的 RDL Width 屬性為基礎。  
  
##  <a name="DocumentProperties"></a> 文件屬性  
 Word 轉譯器會將下列中繼資料寫入到 DOCX 檔。  
  
|報表元素屬性|說明|  
|-------------------------------|-----------------|  
|Report Title (report title)|Title|  
|Report.Author|作者|  
|Report.Description|註解|  
  
##  <a name="ReportHeadersFooters"></a> 頁首和頁尾  
 系統會將頁首和頁尾轉譯為 Word 中的頁首和頁尾區域。 如果表示報表頁面總數的報表頁碼或運算式出現在頁首或頁尾中，它們會轉譯成 Word 欄位，讓正確的頁碼顯示在轉譯的報表中。 如果是在報表中設定頁首或頁尾高度，Word 就無法支援這個設定。 在某些情況下，PrintOnFirstPage 屬性可以指定是否在報表第一頁列印頁首和頁尾文字。 如果轉譯的報表有多頁，而且每頁只包含一個單一區段，則您可以將 PrintOnFirstPage 設為 False，就會隱藏第一頁上的文字，否則，不管 PrintOnFirstPage 屬性的值為何，都會列印文字。  
  
 當報表匯出至 Word 時，Word 轉譯器會嘗試剖析頁首和頁尾的所有運算式。 許多形式的運算式都可以成功剖析，而且預期的值會出現在所有報表頁面上的頁首和頁尾。  
  
 不過，當頁首或頁尾包含在不同報表頁面上評估為不同值的複雜運算式時，相同的值可能會顯示在所有報表頁面上。 下列兩個運算式中的頁碼不會在匯出的報表中遞增。 頁碼在所有報表頁面上會轉譯為相同的值。  
  
-   `="Page: " + Globals!PageNumber.ToString + " of " + Globals!TotalPages.ToString`  
  
-   `=Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
 發生這種情形的原因是，Word 轉譯器剖析分頁相關之欄位 (例如 **PageNumber** 和 **TotalPages** ) 的報表時，只處理簡單參考，但不處理函數呼叫。 在此例中，運算式呼叫 **ToString** 函數。 下列兩個運算式是對等的，當您在報表產生器或報表設計師中預覽報表，或在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站或 SharePoint 文件庫中轉譯發行的報表時，這兩個運算式都會正確轉譯。 不過，Word 轉譯器只會成功剖析第二個運算式，轉譯正確的頁碼。  
  
-   **複雜運算式：**  運算式為 `="Average Sales " & Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
-   **具有文字往返的運算式：** 文字 **Average Sales**、運算式  `=Avg(Fields!YTDPurchase.Value, "Sales)`、文字 **Page Number**和運算式 `=Globals!PageNumber`  
  
 為避免這個問題，當您在頁尾和頁首中使用運算式時，請使用多個文字往返來代替一個複雜運算式。 下列兩個運算式是對等的。 第一個是複雜運算式，而第二個使用文字往返。 Word 轉譯器僅成功剖析第二個運算式。  
  
##  <a name="Interactivity"></a> 互動性  
 Word 中支援某些互動元素。 下列是特定行為的描述。  
  
### 顯示與隱藏  
 Word 轉譯器會根據轉譯時的狀態，轉譯報表項目。 如果報表項目的狀態為隱藏，就不會在 Word 文件中轉譯報表項目。 如果報表項目的狀態為顯示，則會在 Word 文件中轉譯報表項目。 但是，Word 不支援切換功能。  
  
### 文件引導模式  
 如果有任何文件引導模式標籤存在於報表中，它們在個別的報表項目和群組上，會轉譯為 Word 目錄 (TOC) 標籤。 文件引導模式標籤會當做 TOC 標籤的標籤文字使用。 目標連結會放置在其上有設定標籤的項目附近。 當系統沒有在 Word 文件中為您建立 TOC 時，您可以使用在報表中轉譯的文件引導模式標籤來建立自己的 TOC。  
  
### 超連結與鑽研連結  
 系統會將文字方塊和影像報表項目上的超連結與鑽研連結轉譯為 Word 文件中的超連結。 當您按一下超連結時，預設的網頁瀏覽器會開啟並導覽至 URL。 當您按一下鑽研超連結時，則會存取原始報表伺服器。  
  
### 互動式排序  
 報表內容會根據它們目前在報表資料區域內排序的方式，進行轉譯。 Word 不支援互動式排序。 報表經過轉譯之後，就可以在 Word 中套用資料表排序。  
  
### 書籤  
 報表中的書籤會轉譯為 Word 書籤。 而書籤連結會轉譯為超連結，以連接文件內的書籤標籤。 書籤標籤的長度必須少於 40 個字元。 在書籤標籤中可以使用的唯一特殊字元是底線 (_)。 不支援的特殊字元會從書籤標籤名稱移除，而且，如果名稱的長度大於 40 個字元，該名稱就會遭到截斷。 如果報表有重複的書籤名稱，這些書籤不會在 Word 中進行轉譯。  
  
##  <a name="WordStyleRendering"></a> Word 樣式轉譯  
 以下簡短描述如何在 Word 中轉譯樣式。  
  
### 調色盤  
 在報表中轉譯的色彩會轉譯到 Word 文件中。  
  
### 框線  
 報表項目的框線 (除了頁面框線) 會轉譯為 Word 資料表資料格框線。  
  
##  <a name="SquigglyLines"></a> 匯出之報表中的曲線  
 在 Word 中匯出並檢視時，報表資料或常數可能會加上紅色或綠色曲線的底線。 紅色曲線表示拼寫錯誤。 綠色曲線表示文法錯誤。 當報表包含不符合 Word 中所指定編輯語言校訂 (拼字和文法) 的字詞時，就會發生這種情形。 例如，如果報表是以西班牙文版的 Word 轉譯，則英文報表資料行的標頭可能會加上紅色曲線的底線。 報表中察覺的拼字錯誤會比察覺的文法錯誤更為常見，因為報表通常只包含簡短的文字，而不是完整的句子或段落。  
  
 報表中出現的曲線暗示報表有錯誤，但也可能不是錯誤。 您可以藉由變更報表的校訂語言來移除曲線。 若要變更校訂語言，請選取報表的內容，然後為該內容指定適當的語言。 您可以選取全部或部分內容。 在 Word 中，語言選項 [設定校訂語言] 位於 [校閱] 索引標籤的 [語言] 區域中。 更新內容之後，需要重新儲存文件。  
  
 根據您 Office 程式的語言版本而定，您所選擇語言的校訂工具 (如字典) 會隨程式提供，或是在您購買的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 語言套件中提供。  
  
 下列主題提供有關設定 Office 和 Word 選項的其他資訊。  
  
-   在 Word 的 [Microsoft Office 語言喜好設定] 或 [Word 選項] 對話方塊中變更編輯語言。 如需詳細資訊，請參閱＜ [在 Office 程式中啟用使用其他語言的功能](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1)＞。  
  
-   加入 Office 語言套件，然後變更編輯語言。 如需詳細資訊，請參閱[在 Office 程式中啟用使用其他語言的功能](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1)和 [Office 語言選項](http://office.microsoft.com/language/)。  
  
> [!NOTE]  
>  您在 Word 的 [Microsoft Office 語言喜好設定] 或 [Word 選項] 對話方塊中變更編輯語言時，變更會套用至所有 Office 程式。  
  
##  <a name="WordLimitations"></a> Word 限制  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]會套用下列限制：  
  
-   Word 資料表最多支援 63 個資料行。 如果您的報表有超過 63 個資料行，而且您嘗試進行轉譯，Word 就會分割資料表。 其他資料行的位置在報表主體中顯示之 63 個資料行的旁邊。 因此，報表資料行可能不會如預期般對齊。  
  
-   Word 支援的頁寬最多可達 22 英吋，而頁高可達 22 英吋。 如果您的內容寬度超過 22 英吋，有些資料可能就不會顯示在 [整頁模式] 檢視中。  
  
-   Word 會忽略頁首及頁尾的高度設定。  
  
-   報表匯出後，Word 會為報表再次分頁。 這可能會將額外的分頁符號加入到轉譯的報表中。  
  
-   雖然您在 Tablix (資料表、矩陣或清單) 中，將靜態標頭資料列的 RepeatOnNewPage 屬性設定為 **True**，但是 Word 不會在第二頁之後重複標頭資料列。 您可以在報表中定義明確的分頁符號，以強制標頭資料列出現在新的頁面上。 不過，Word 會將自己的分頁套用到匯出至 Word 的已轉譯報表，因此，結果可能會不同，而且標頭資料列可能不會如預期般重複。 靜態標頭資料列是包含資料行標題的資料列。  
  
-   文字方塊會在其內含不中斷空格時成長。  
  
-   當文字匯出到 Word 時，如果文字的某些字型中有使用字型裝飾，則可能會在轉譯報表中產生非預期或遺漏的圖像。  
  
##  <a name="WordBenefits"></a> 使用 Word 轉譯器的優點  
 除了讓 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx 檔案的新功能可供匯出的報表使用之外，匯出的報表 *.docx 檔案通常較小。 使用 Word 轉譯器所匯出的報表通常比使用 Word 2003 轉譯器所匯出的相同報表小得多。  
  
## 匯出之報表的回溯相容性  
 您可以選取 Word 相容模式及設定相容選項。 Word 轉譯器會以開啟的相容模式來建立文件。 以關閉的相容模式重新儲存文件，可能會影響文件配置。  
  
 如果您關閉相容模式，然後重新儲存報表，報表配置可能會以非預期的方式變更。  
  
##  <a name="AvailabilityWord"></a> Word 2003 轉譯器  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 (.doc) 轉譯延伸模組已被取代。 如需詳細資訊，請參閱 [SQL Server 2016 中 SQL Server Reporting Services 已被取代的功能](../Topic/Deprecated%20Features%20in%20SQL%20Server%20Reporting%20Services%20in%20SQL%20Server%202016.md)。  
  
 Word 轉譯器與已安裝 Word、Excel 和 PowerPoint 之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 相容性套件的 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 相容。 如需詳細資訊，請參閱 [Microsoft Office Word、Excel 及 PowerPoint 檔案格式相容性套件](http://go.microsoft.com/fwlink/?LinkID=205622)。  
  
 與 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 相容的舊版 Word 轉譯延伸模組已重新命名為 Word 2003。 根據預設，只能使用 Word 轉譯延伸模組。 您必須更新 Reporting Services 組態檔，才能使用 Word 2003 轉譯延伸模組。 Word 2003 轉譯器會產生 **application/vnd.ms-word** 內容類型的檔案，而檔案的副檔名為 .doc。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，預設的 Word 轉譯器是可轉譯為 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 格式 (.docx) 的版本。 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站和 SharePoint 清單的 [匯出] 功能表中，這就是 [Word] 選項。 只與 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 相容的舊版現在已命名為 Word 2003，而且使用該名稱列於功能表上。 根據預設，系統不會顯示 **[Word 2003]** 功能表選項，但是管理員可以透過更新 RSReportServer 組態檔，顯示此選項。 若要使用 Word 2003 轉譯器，從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 匯出報表，請更新 RSReportDesigner 組態檔。 不過，讓 Word 2003 轉譯器顯示並不適用於所有案例。 因為 RSReportServer 組態檔位於報表伺服器上，所以您從中匯出報表的工具或產品必須連接至報表伺服器，以便讀取組態檔。 如果您在中斷連接或本機模式中使用工具或產品，讓 Word 2003 轉譯器顯示就沒有任何作用。 **[Word 2003]** 功能表選項會維持無法使用的狀態。 如果您在 RSReportDesigner 組態檔中，讓 Word 2003 轉譯器顯示，就一定可以在 **報表預覽中使用** [Word 2003] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 功能表選項。  
  
 在下列案例中， **[Word 2003]** 功能表選項永不顯示：  
  
-   報表產生器處於中斷連接模式，而且您在報表產生器中預覽報表。  
  
-   報表檢視器 Web 組件處於本機模式，而且 SharePoint 伺服陣列並未與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器整合。 如需詳細資訊，請參閱[比較報表檢視器中的本機模式與連接模式報表 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local mode vs. connected mode reports in the report viewer.md)  
  
 如果 **[Word 2003]** 轉譯器設定為顯示，在下列案例中，您就可以同時使用 **[Word]** 和 **[Word 2003]** 功能表選項：  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站 (當 Reporting Services 是以原生模式安裝時)。  
  
-   SharePoint 網站 (當 Reporting Services 是以 SharePoint 整合模式安裝時)。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和預覽報表。  
  
-   報表產生器已連接至報表伺服器。  
  
-   報表檢視器 Web 組件處於遠端模式。  
  
 下列 XML 顯示 RSReportServer 和 RSReportDesigner 組態檔中這兩個 Word 轉譯延伸模組的元素：  
  
 `<Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>`  
  
 `<Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>`  
  
 WORDOPENXML 延伸模組會定義 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx 檔案的 Word 轉譯器。 WORD 延伸模組會定義 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 版本。 `Visible = “false”` 表示隱藏 Word 2003 轉譯器。 如需詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)和 [RSReportDesigner 組態檔](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。  
  
### Word 與 Word 2003 轉譯器之間的差異  
 透過 Word 或 Word 2003 轉譯器所轉譯的報表通常無法用肉眼分辨。 不過，您可能會注意到 Word 或 Word 2003 這兩個格式之間的小差異。  
  
##  <a name="DeviceInfo"></a> 裝置資訊設定  
 您可以變更此轉譯器的某些預設值，例如，省略超連結和鑽研連結或是在進行轉譯時，展開忽略原始的項目狀態而切換的所有項目，方法是，變更裝置資訊設定。 如需詳細資訊，請參閱 [Word Device Information Settings](../../reporting-services/word-device-information-settings.md)。  
  
## 請參閱＜  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive functionality - different report rendering extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  