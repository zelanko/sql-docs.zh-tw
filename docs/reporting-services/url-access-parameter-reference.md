---
title: URL 存取參數參考 | Microsoft Docs
description: 您可以在 URL 中使用本文的參數，以設定 Reporting Services 報表的外觀與風格。
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ac67de4831d1785f17029bc6c68fa6f7d8aeb16
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77147378"
---
# <a name="url-access-parameter-reference"></a>URL 存取參數參考

  您可以在 URL 中使用下列參數，以設定 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 報表的外觀與風格。 本章節中將列出最常用的參數。 參數會區分大小寫，而且如果是導向至報表伺服器，則以參數前置字元 *rs:* 開頭，如果是導向至 HTML 檢視器，則以 *rc:* 開頭。 您也可以指定裝置或轉譯延伸模組特定的參數。 如需裝置特定參數的詳細資訊，請參閱[在 URL 中指定裝置資訊設定](../reporting-services/specify-device-information-settings-in-a-url.md)。
  
> [!IMPORTANT]  
>  對 SharePoint 模式報表伺服器而言，URL 要包含 `_vti_bin` Proxy 語法，才能透過 SharePoint 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP Proxy 路由傳送要求。 此 Proxy 會將確保正確執行 SharePoint 模式報表伺服器報表所需的內容來新增至 HTTP 要求。 如需範例，請參閱[使用 URL 存取權存取報表伺服器項目](../reporting-services/access-report-server-items-using-url-access.md)。
> 
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  

##  <a name="html-viewer-commands-rc"></a><a name="bkmk_htmlviewer"></a> HTML 檢視器命令 (rc:)
 - HTML 檢視器命令的使用對象是 HTML 檢視器，其前置詞為 *rc:* ：
  
-   **Toolbar**：顯示或隱藏工具列。 如果這個參數的值為 **false**，則會忽略所有剩餘的選項。 如果您省略這個參數，工具列就會自動顯示以轉譯支援該參數的格式。 這個參數的預設值為 **true**。
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** 不適用於不使用網域名稱，而使用 IP 位址指出 SharePoint 網站所託管報表的 URL 存取字串。
  
-   **參數**：顯示或隱藏工具列的參數區。 如果將這個參數設定為 **true**，工具列的參數區就會顯示。 如果將這個參數設定為 **false**，參數區就不會顯示，且無法由使用者顯示。 如果將這個參數值設定為 **Collapsed**，參數區就不會顯示，但使用者可以切換顯示。 此參數的預設值為 **true**。  
  
     例如，在原生模式中：
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     例如，在 SharePoint 模式中：
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   **Zoom**：將報表縮放值設定為整數百分比或字串常數。 標準字串值包括 **Page Width** 和 **Whole Page**。 Internet Explorer 5.0 之前的舊版 Internet Explorer 和所有非[!INCLUDE[msCoName](../includes/msconame-md.md)] 瀏覽器都會忽略這個參數。 此參數的預設值為 **100**。
  
     例如，在原生模式中：
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     例如，在 SharePoint 模式中：
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   **Section**：設定要顯示報表中的哪一頁。 任何大於報表頁數的值都會顯示最後一頁。 任何小於 **0** 的值都會顯示為報表第 1 頁。 此參數的預設值為 **1**。
  
     例如在原生模式下，顯示報表的第 2 頁：
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     例如在 SharePoint 模式下，顯示報表的第 2 頁：
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   **FindString**：在報表中搜尋特定文字集。
  
     例如，在原生模式中：
  
    ```  
    https://myrshost/reportserver?/Sales&rc:FindString=Mountain-400  
    ```  
  
     例如，在 SharePoint 模式中：
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:FindString=Mountain-400  
    ```  
  
-   **StartFind**：指定要搜尋的最後一部分。 此參數的預設值是報表的最後一頁。  
  
     例如在原生模式下，於 Product Catalog 範例報表中，搜尋第 1 頁到第 5 頁中第一個出現的 "Mountain-400" 文字：
  
    ```  
    https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   **EndFind**：設定要在搜尋中使用的最後一頁的頁碼。 例如， **5** 的值指出要搜尋的最後一頁為報表的第 5 頁。 預設值為目前頁面的頁碼。 將此參數搭配 *StartFind* 參數使用。 請參閱上一個範例。
  
-   **FallbackPage**：設定在搜尋或文件引導模式選取項目失敗時所顯示頁面的頁碼。 預設值為目前頁面的頁碼。
  
-   **GetImage**：取得 HTML 檢視器使用者介面的特定圖示。
  
-   **Icon**：取得特定轉譯延伸模組的圖示。
  
-   **Stylesheet**：指定要套用至 HTML 檢視器的樣式表。
  
-   **裝置資訊設定**：以 `rc:tag=value` 格式指定裝置資訊設定，其中 *tag* 是目前專用於轉譯延伸模組的特定裝置資訊設定名稱。 (請參閱 *Format* 參數的描述。)例如，您可以利用 IMAGE 轉譯延伸模組的 *OutputFormat* 裝置資訊設定，使用下列 URL 存取字串的參數將報表轉譯為 JPEG 影像：`...&rs:Format=IMAGE&rc:OutputFormat=JPEG`。 如需所有延伸模組特定裝置資訊設定的詳細資訊，請參閱[轉譯延伸模組的裝置資訊設定 &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)。
  
##  <a name="report-server-commands-rs"></a><a name="bkmk_reportserver"></a> 報表伺服器命令 (rs:)
 報表伺服器命令前面會加上 *rs:* ，而且用來針對下列報表伺服器︰
  
-   **命令**：目錄項目上所執行的動作，視其項目類型而定。 預設值取決於 URL 存取字串中所參考目錄項目的類型。 有效值為：
  
    -   **ListChildren** 和 **GetChildren**：顯示資料夾的內容。 資料夾項目會顯示在一般項目導覽頁中。
  
         例如，在原生模式中：
  
        ```  
        https://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         例如，原生模式中的具名執行個體：
  
        ```  
        https://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         例如，在 SharePoint 模式中：
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Render**：報表會在瀏覽器中轉譯，方便您檢視。
  
         例如，在原生模式中：
  
        ```  
        https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         例如，在 SharePoint 模式中：
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition**：顯示與共用資料集建立關聯的 XML 定義。 共用資料集屬性 (包括查詢、資料集參數、預設值、資料集篩選，以及定序和大小寫區分等資料選項) 是儲存於定義中。 您必須對共用資料集具有 [讀取報表定義]  權限，才能使用這個值。
  
         例如，在原生模式中：
  
        ```  
        https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents**：將所指定共用資料來源的屬性顯示為 XML。 如果瀏覽器支援 XML，且您是具有資料來源 **Read Contents** 權限的已驗證使用者，則會顯示資料來源定義。
  
         例如，在原生模式中：
  
        ```  
        https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         例如，在 SharePoint 模式中：
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents**：如果資源與瀏覽器不相容，請轉譯資源並使用 HTML 頁面顯示。 否則，系統會提示您開啟檔案或資源，或將其儲存至磁碟。  
  
         例如，在原生模式中：
  
        ```  
        https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         例如，在 SharePoint 模式中：
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition**：顯示與已發佈報表項目建立關聯的 XML 定義。 您必須在已發行報表項目上具有 **「讀取內容」** 權限，才能使用這個值。
  
-   **Format**︰指定用於轉譯並檢視報表的格式。 常見的值包括：
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL** (適用於 .xls)
    
    -   **EXCELOPENXML** (適用於 .xlsx)
  
    -   **WORD** (適用於 .doc)
    
    -   **WORDOPENXML** (適用於 .docx)
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     預設值是 **HTML5**秒。 如需詳細資訊，請參閱[使用 URL 存取匯出報表](../reporting-services/export-a-report-using-url-access.md)。
  
     如需完整清單，請參閱報表伺服器 rsreportserver.config 檔案的 **\<轉譯>** 延伸模組區段。 如需在何處尋找檔案的資訊，請參閱 [RsReportServer.config 組態檔](../reporting-services/report-server/rsreportserver-config-configuration-file.md)。
  
     例如，直接從原生模式報表伺服器取得報表的 PDF 副本。
  
    ```  
    https://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     例如，直接從 SharePoint 模式報表伺服器取得報表的 PDF 複本：
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   **ParameterLanguage**：提供 URL 所傳遞參數的語言，這與瀏覽器語言無關。 預設值是瀏覽器語言。 此值可以是文化特性值，例如 **en-us** 或 **de-de**。
  
     例如，在原生模式下，若要覆寫瀏覽器語言及指定文化特性值 de-DE：
  
    ```  
    https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   **快照集**：根據報表記錄快照集來轉譯報表。 如需詳細資訊，請參閱[使用 URL 存取轉譯報表記錄快照集](../reporting-services/render-a-report-history-snapshot-using-url-access.md)。
  
     例如，在原生模式下，擷取日期為 2003-04-07 且時間戳記為 13:40:02 的報表記錄快照集：
  
    ```  
    https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   **PersistStreams**：轉譯單一永續性資料流中的報表。 這個參數是由影像轉譯器用來傳輸轉譯的報表，一次一個區塊。 在 URL 存取字串中使用這個參數後，以 *GetNextStream* 參數使用相同的 URL 存取字串，而不用 *PersistStreams* 參數，以取得永續性資料流中的下一個區塊。 這個 URL 命令最後會傳回 0 個位元組資料流，表示永續性資料流結尾。 預設值為 **false**。
  
-   **GetNextStream**：取得使用 *PersistStreams* 參數存取的永續性資料流中下一個資料區塊。 如需詳細資訊，請參閱 *PersistStreams*的描述。 預設值為 **false**。
  
-   **SessionID**：指定用戶端應用程式和報表伺服器之間已建立的使用中報表工作階段。 此參數的值是設定為工作階段識別碼。
  
     您可以將工作階段識別碼指定為 Cookie 或是 URL 的一部分。 當將報表伺服器設定成不使用工作階段 Cookie 時，第一個沒有指定工作階段識別碼的要求，會導致使用某個工作階段識別碼來進行重新導向。 如需報表伺服器工作階段的詳細資訊，請參閱[識別執行狀態](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)。
  
-   **ClearSession**：**true** 的值會指示報表伺服器從報表工作階段移除報表。 所有和已驗證的使用者相關聯的報表執行個體，都會從報表工作階段移除。 (報表執行個體的定義：使用不同報表參數值執行多次的相同一份報表)。預設值為 **false**。
  
-   **ResetSession**：**true** 的值會指示報表伺服器透過移除與所有報表快照集的報表工作階段關聯，重設報表工作階段。 預設值為 **false**。
  
-   **ShowHideToggle**：切換該報表區段的顯示和隱藏狀態。 指定正整數以表示要切換的區段。
  
##  <a name="report-viewer-web-part-commands-rv"></a><a name="bkmk_webpart"></a> 報表檢視器網頁組件命令 (rv:)
 下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 保留報表參數名稱用於將與 SharePoint 整合的報表檢視器網頁組件指定為目標。 這些參數名稱都使用 *rv:* 做為字首。 報表檢視器網頁組件也接受 *rs:ParameterLanguage* 參數。
  
-   **Toolbar**：控制報表檢視器網頁組件的工具列顯示。 預設值是 **Full**秒。 值可以是：
  
    -   **完整**：顯示完整的工具列。
  
    -   **Navigation**：只在工具列中顯示分頁。
  
    -   **無**：不顯示工具列。
  
     例如，在 SharePoint 模式中，只在工具列中顯示分頁：
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   **HeaderArea**：控制報表檢視器網頁組件的標頭顯示。 預設值是 **Full**秒。 值可以是：
  
    -   **完整**：顯示完整的標頭。
  
    -   **BreadCrumbsOnly**：只在標頭中顯示軌跡瀏覽，以通知使用者其在應用程式中的所在位置。
  
    -   **無**：不顯示標頭。
  
     例如，在 SharePoint 模式中，只在標頭中顯示軌跡瀏覽：
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   **DocMapAreaWidth**：控制參數區在報表檢視器網頁組件中的顯示寬度 (以像素為單位)。 預設值與報表檢視器網頁組件的預設值相同。 其值必須為非負整數。
  
-   **AsyncRender**：控制是否要以非同步方式轉譯報表。 預設值為 **true**，此值指定以非同步方式轉譯報表。 此值必須為 **true** 或 **false**的布林值。
  
-   **ParamMode**：控制報表檢視器網頁組件的參數提示區域，在整頁檢視中的顯示方式。 預設值是 **Full**秒。 有效值為：
  
    -   **完整**：顯示參數提示區域。
  
    -   **Collapsed**：摺疊參數提示區域。
  
    -   **Hidden**：隱藏參數提示區域。
  
     例如，在 SharePoint 模式中，摺疊參數提示區域：
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   **DocMapMode**：控制報表檢視器網頁組件的文件引導模式區域，在整頁檢視中的顯示方式。 預設值是 **Full**秒。 有效值為：
  
    -   **完整**：顯示文件引導模式區域。
  
    -   **Collapsed**：摺疊文件引導模式區域。
  
    -   **Hidden**：隱藏文件引導模式區域。
  
-   **DockToolBar**：控制報表檢視器網頁組件工具列停駐在頂部或底部。 有效值為 **Top** 和 **Bottom**。 預設值是 **Top**秒。
  
     例如，在 SharePoint 模式中，將工具列停駐在底部：
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   **ToolBarItemsDisplayMode**：控制要顯示的工具列項目。 這是位元列舉值。 若要包含工具列項目，請將項目的值新增總值。 例如，若無 [動作]  功能表，請使用 *rv:ToolBarItemsDisplayMode=63* (或 0x3F)，即 1+2+4+8+16+32。 僅限 [動作]  功能表項目，請使用 *rv:ToolBarItemsDisplayMode=960* (或 0x3C0)。 預設值是 **-1**，其中包含所有的工具列項目。 有效值為：
  
    -   **1 (0x1)** ：[上一步]  按鈕  
  
    -   **2 (0x2)** ：文字搜尋控制項  
  
    -   **4 (0x4)** ：頁面導覽控制項  
  
    -   **8 (0x8)** ：[重新整理]  按鈕  
  
    -   **16 (0x10)** ：[縮放]  清單方塊  
  
    -   **32 (0x20)** ：[Atom 摘要]  按鈕  
  
    -   **64 (0x40)** ：[動作]  中的 [列印]  功能表選項  
  
    -   **128 (0x80)** ：[動作]  中的 [匯出]  子功能表  
  
    -   **256 (0x100)** ：[動作]  中的 [用報表產生器開啟]  功能表選項  
  
    -   **512 (0x200)** ：[動作]  中的 [訂閱]  功能表選項  
  
    -   **1024 (0x400)** ：[動作]  中的 [新資料警示]  功能表選項  
  
     例如，在 SharePoint 模式中，只顯示 [上一步]  按鈕、文字搜尋控制項、頁面導覽控制項和 [重新整理]  按鈕：
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>另請參閱
 - [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)
 - [使用 URL 存取匯出報表](../reporting-services/export-a-report-using-url-access.md)
  
  
