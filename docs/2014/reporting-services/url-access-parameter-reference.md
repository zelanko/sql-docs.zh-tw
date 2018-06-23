---
title: URL 存取參數參考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 8ff6bcb77e9bd703091398357fcef37876a7c247
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035595"
---
# <a name="url-access-parameter-reference"></a>URL 存取參數參考
  您可以使用下列參數當做 URL 的一部分，以設定報表的外觀及操作。 本章節中將列出最常用的參數。 參數會區分大小寫，而且如果是導向至報表伺服器，則以參數前置字元 *rs:* 開頭，如果是導向至 HTML 檢視器，則以 *rc:* 開頭。 您也可以指定裝置或轉譯延伸模組特定的參數。 如需有關裝置特定參數的詳細資訊，請參閱[在 URL 中指定裝置資訊設定](specify-device-information-settings-in-a-url.md)。  
  
> [!IMPORTANT]  
>  請務必讓 URL 包含 `_vti_bin` Proxy 語法，以便透過 SharePoint 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP Proxy 路由傳送要求。 此 Proxy 會將某些內容加入至 HTTP 要求，也就是確保針對 SharePoint 模式報表伺服器正確執行報表所需的內容。 如需範例，請參閱[存取報表伺服器項目使用 URL 存取](access-report-server-items-using-url-access.md)。  
>   
>  如需有關在 URL 中包含報表參數的詳細資訊與範例，請參閱＜ [Pass a Report Parameter Within a URL](pass-a-report-parameter-within-a-url.md)＞。  
  
## <a name="html-viewer-commands-rc"></a>HTML 檢視器命令 (rc:)  
 下表描述 URL 存取參數前置詞為*rc:* ，可用來以 HTML 檢視器為目標。  
  
|參數|描述|值|  
|---------------|-----------------|------------|  
|*工具列*|顯示或隱藏工具列。<br /><br /> **\*\* 重要\* \***  *rc:Toolbar* = `false`無法運作，而不是網域名稱，為目標上裝載報表 URL 存取字串，可用的 IP 位址SharePoint 網站。|如果這個參數的值為 `false`，則會忽略所有剩餘的選項。 如果您省略這個參數，工具列就會自動顯示以轉譯支援該參數的格式。 此參數的預設值是`true`。<br /><br /> `true` <br /> `false`|  
|*參數*|顯示或隱藏工具列的參數區。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Parameters=Collapsed`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Parameters=Collapsed`|如果將這個參數設定為 `true`，工具列的參數區就會顯示。 如果將這個參數設定為 `false`，參數區就不會顯示，且無法由使用者顯示。 如果將這個參數設定為 `Collapsed` 的值，參數區就不會顯示，但可以由使用者切換顯示。 此參數的預設值為 `true`。 有效值為：<br /><br /> `true` <br /> `false` <br /> `Collapsed`|  
|*顯示比例*|將報表縮放值設定為整數百分比或字串常數。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Zoom=Page Width`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Zoom=Page Width`|標準字串值包括 `Page Width` 和 `Whole Page`。 Internet Explorer 5.0 之前的舊版 Internet Explorer 和所有非[!INCLUDE[msCoName](../includes/msconame-md.md)] 瀏覽器都會忽略這個參數。 此參數的預設值為 `100`。|  
|*區段*|設定要顯示報表中的哪一頁。<br /><br /> `Native` 顯示報表的第 2 頁的模式範例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:Section=2`<br /><br /> `SharePoint` 顯示報表的第 2 頁的模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Section=2`|任何大於報表中頁數的值都會顯示最後一頁。 任何小於 `0` 的值都會顯示報表的第 1 頁。 此參數的預設值為 `1`。|  
|*FindString*|在報表中搜尋特定文字集。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales&rc:FindString=Mountain-400`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:FindString=Mountain-400`||  
|*StartFind*|指定要搜尋的最後一部分。<br /><br /> `Native` 搜尋第一個出現的"mountain-400"文字在 Product Catalog 範例報表第一頁開始，並終止於頁面 5 的模式範例：<br /><br /> `http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400`|此參數的預設值是報表的最後一頁。|  
|*EndFind*|設定要在搜尋中使用的最後一頁的頁碼。 例如，值為`5`表示要搜尋的最後一頁報表的第 5 頁。 將此參數搭配 *StartFind* 參數使用。 請參閱上述範例中的為*StartFind* 。|預設值為目前頁面的頁碼。|  
|*FallbackPage*|設定在搜尋或文件引導模式選取項目失敗時所顯示頁面的頁碼。|預設值為目前頁面的頁碼。|  
|*GetImage*|取得 HTML 檢視器使用者介面的特定圖示。||  
|*圖示*|取得特定轉譯延伸模組的圖示。||  
|*樣式表*|指定要套用至 HTML 檢視器的樣式表。||  
|裝置資訊設定|指定裝置資訊設定的形式`rc:tag=value`，其中*標記*特定裝置資訊設定到目前使用的轉譯延伸模組的名稱 (請參閱的描述*格式化*參數)。 例如，您可以利用 IMAGE 轉譯延伸模組的 *OutputFormat* 裝置資訊設定，使用下列 URL 存取字串的參數將報表轉譯為 JPEG 影像： `…&rs:Format=IMAGE&rc:OutputFormat=JPEG`。 如需所有延伸模組特定裝置資訊設定的詳細資訊，請參閱[轉譯延伸模組的裝置資訊設定 &#40;Reporting Services&#41;](device-information-settings-for-rendering-extensions-reporting-services.md)。||  
  
## <a name="report-server-commands-rs"></a>報表伺服器命令 (rs:)  
 下表描述 URL 存取參數前置詞為*rs:* ，而且可用來針對報表伺服器。  
  
|參數|描述|  
|---------------|-----------------|  
|*Command*|目錄項目上所執行的動作，視其項目類型而定。 預設值取決於 URL 存取字串中所參考目錄項目的類型。 有效值為：<br /><br /> `ListChildren` 和`GetChildren`顯示資料夾的內容。 資料夾項目會顯示在一般項目導覽頁中。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`|  
||`Render` 轉譯指定的報表。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`|  
||`GetSharedDatasetDefinition` 顯示與共用資料集相關聯的 XML 定義。 共用資料集屬性 (包括查詢、資料集參數、預設值、資料集篩選，以及定序和大小寫區分等資料選項) 是儲存於定義中。 您必須對共用資料集具有 [讀取報表定義]  權限，才能使用這個值。<br /><br /> `Native` 模式範例：<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
||`GetDataSourceContents` 指定共用的資料來源的屬性顯示為 XML。 如果您的瀏覽器支援 XML，而且如果您是使用已驗證的使用者`Read Contents`權限的資料來源，資料來源定義會顯示。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`|  
||`GetResourceContents` 轉譯資源並在 HTML 網頁中顯示如果資源與瀏覽器不相容。 否則，系統會提示您開啟檔案或資源，或是將其儲存至磁碟。<br /><br /> `Native` 模式範例：<br /><br /> `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`<br /><br /> `SharePoint` 模式範例：<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`|  
||`GetComponentDefinition` 顯示與已發行的報表項目相關聯的 XML 定義。 您必須擁有`Read Contents`已發行的報表項目上的權限，才能使用這個值。|  
|*格式*|指定用於轉譯報表的格式。 常見的值包括 `ATOM`、`HTML4.0`、`MHTML`、`IMAGE`、`EXCEL`、`WORD`、`CSV`、`PDF` 和 `XML`。 預設值是 `HTML4.0`。 如需詳細資訊，請參閱 [Export a Report Using URL Access](export-a-report-using-url-access.md)。<br /><br /> 例如，直接從 `Native` 模式報表伺服器取得報表的 PDF 副本。<br /><br /> `http://myrshost/ReportServer?/myreport&rs:Format=PDF`<br /><br /> 例如在`SharePoint`模式。<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF`|  
|*ParameterLanguage*|提供 URL 所傳遞參數的語言，這與瀏覽器語言無關。 預設值是瀏覽器語言。 此值可以是文化特性值，例如 `en-us` 或 `de-de.`。<br /><br /> 例如在 `Native` 模式下，覆寫瀏覽器語言及指定文化特性值 de-DE。<br /><br /> `http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE`|  
|*快照式*|根據報表記錄快照集來轉譯報表。 如需詳細資訊，請參閱[轉譯報表記錄快照集使用 URL 存取](render-a-report-history-snapshot-using-url-access.md)。<br /><br /> 例如在 `Native` 模式下，擷取日期為 2003-04-07 且時間戳記為 13:40:02 的報表記錄快照集。<br /><br /> `http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02`|  
|*PersistStreams*|轉譯單一永續性資料流中的報表。 這個參數是由影像轉譯器用來傳輸轉譯的報表，一次一個區塊。 在 URL 存取字串中使用這個參數後，以 *GetNextStream* 參數使用相同的 URL 存取字串，而不用 *PersistStreams* 參數，以取得永續性資料流中的下一個區塊。 這個 URL 命令最後會傳回 0 個位元組資料流，表示永續性資料流結尾。 預設值是 `false`。|  
|*GetNextStream*|取得使用 *PersistStreams* 參數存取的永續性資料流中的下一個資料區塊。 如需詳細資訊，請參閱 *PersistStreams*的描述。 預設值是 `false`。|  
|*工作階段識別碼*|指定用戶端應用程式和報表伺服器之間已建立的使用中報表工作階段。 此參數的值是設定為工作階段識別碼。<br /><br /> 您可以將工作階段識別碼指定為 Cookie 或是 URL 的一部分。 當將報表伺服器設定成不使用工作階段 Cookie 時，第一個沒有指定工作階段識別碼的要求，會導致使用某個工作階段識別碼來進行重新導向。 如需有關報表伺服器工作階段的詳細資訊，請參閱[Identifying Execution State](report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)。|  
|*ClearSession*|`true` 的值會指示報表伺服器從報表工作階段移除報表。 所有和已驗證的使用者相關聯的報表執行個體，都會從報表工作階段移除。 (報表執行個體定義為：使用不同的報表參數值多次執行相同的報表)。預設值是 `false`。|  
|*ResetSession*|`true` 的值會指示報表伺服器透過移除與所有報表快照集的報表工作階段關聯，重設報表工作階段。 預設值是 `false`。|  
|*ShowHideToggle*|切換該報表區段的顯示和隱藏狀態。 指定正整數以表示要切換的區段。|  
  
## <a name="report-viewer-web-part-commands-rv"></a>報表檢視器 Web 組件命令 (rv:)  
 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 保留報表參數名稱，而這些名稱在與 SharePoint 整合時，用於以報表檢視器 Web 組件為目標。 這些參數名稱都使用 *rv:* 做為字首。 報表檢視器 Web 組件也接受 *rs:ParameterLanguage* 參數。  
  
|參數|動作|  
|---------------|------------|  
|*工具列*|控制報表檢視器 Web 組件的工具列顯示。 預設值是 `Full`。 其值可能是：<br /><br /> `Full`：顯示完整的工具列。<br /><br /> `Navigation`：只在工具列中顯示分頁。<br /><br /> `None`：不顯示工具列。<br /><br /> <br /><br /> 例如，在 `SharePoint` 模式中，只在工具列中顯示分頁。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation`|  
|*HeaderArea*|控制報表檢視器 Web 組件的標頭顯示。 預設值是 `Full`。 其值可能是：<br /><br /> `Full`：顯示完整的標頭。<br /><br /> `BreadCrumbsOnly`： 只顯示蹤跡導覽來通知的使用者的應用程式中的標頭中。<br /><br /> `None`：不顯示標頭。<br /><br /> <br /><br /> 例如，在 `SharePoint` 模式中，只在標頭中顯示階層連結導覽。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly`|  
|*DocMapAreaWidth*|控制參數區在報表檢視器 Web 組件中的顯示寬度 (以像素為單位)。 預設值與報表檢視器 Web 組件的預設值相同。 其值必須為非負整數。|  
|*AsyncRender*|控制是否要以非同步方式轉譯報表。 預設值是`true`，指定以非同步方式轉譯報表。 此值必須為 `true` 或 `false` 的布林值。|  
|*ParamMode*|控制報表檢視器 Web 組件的參數提示區域在整頁檢視中的顯示方式。  預設值是 `Full`。 有效值為：<br /><br /> `Full`： 顯示參數提示區域。<br /><br /> `Collapsed`： 摺疊參數提示區域。<br /><br /> `Hidden`： 隱藏參數提示區域。<br /><br /> 例如，在 `SharePoint` 模式中，摺疊參數提示區域。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed`|  
|*DocMapMode*|控制報表檢視器 Web 組件的文件引導模式區域在整頁檢視中的顯示方式。 預設值是 `Full`。 有效值為：<br /><br /> `Full`：顯示文件引導模式區域。<br /><br /> `Collapsed`： 摺疊文件引導模式區域。<br /><br /> `Hidden`： 隱藏文件引導模式區域。|  
|*DockToolBar*|控制報表檢視器 Web 組件工具列是否停駐在頂部或底部。 有效值為`Top`和`Bottom`。 預設值是 `Top`。<br /><br /> <br /><br /> 例如，在 `SharePoint` 模式中，將工具列停駐在底部。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom`|  
|*ToolBarItemsDisplayMode*|控制要顯示的工具列項目。 這是位元列舉值。 若要包含工具列項目，請將項目的值加入總值。 例如：針對沒有動作功能表，請使用 rv:ToolBarItemsDisplayMode=63 (或 0x3F)，這就是 1+2+4+8+16+ 32；僅針對動作功能表項目，請使用 rv:ToolBarItemsDisplayMode=960 (或 0x3C0)。  預設值是`-1`，其中包括所有工具列項目。 有效值為：<br /><br /> 1 (0x1)：[上一步] 按鈕<br /><br /> 2 (0x2)：文字搜尋控制項<br /><br /> 4 (0x4)：頁面導覽控制項<br /><br /> 8 (0x8)：[重新整理] 按鈕<br /><br /> 16 (0x10)：[顯示比例] 清單方塊<br /><br /> 32 (0x20)：[Atom 摘要] 按鈕<br /><br /> 64 (0x40)：[動作] 中的 [列印] 功能表選項<br /><br /> 128 (0x80)：[動作] 中的 [匯出] 子功能表<br /><br /> 256 (0x100：[動作] 中的 [用報表產生器開啟] 功能表選項<br /><br /> 512 (0x200：[動作] 中的 [訂閱] 功能表選項<br /><br /> 1024 (0x400：[動作] 中的 [新資料警示] 功能表選項<br /><br /> 例如，在`SharePoint`模式，只顯示**回**按鈕、 文字搜尋控制項、 頁面導覽控制項和**重新整理** 按鈕。<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15`|  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](url-access-ssrs.md)  
  
  