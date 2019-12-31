---
title: 規劃 Reporting Services 和 Power View 瀏覽器支援 (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: cd3a3e268e09e882b4e38eee6a620843fcc21a23
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241195"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>規劃 Reporting Services 和 Power View 瀏覽器支援 (Reporting Services 2014)
  在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，您會使用網頁瀏覽器來檢視報表和執行報表管理員。 並非所有瀏覽器都支援所有報表功能。 本主題說明報表管理員管理功能「檢視報表」(Visual Studio 中的報表檢視器控制項) 的支援和需求。 本主題也概述受支援的瀏覽器、驗證需求和指令碼需求的功能可用性。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SharePoint 模式 |[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]原生模式  
  
 **本主題內容：**  
  
- [Power View 瀏覽器案例](#bkmk_powerview)  
  
- [報表管理員瀏覽器需求 (原生模式)](#bkmk_reportmanager)  
  
- [檢視報表的瀏覽器需求](#bkmk_reportviewer)  
  
- [驗證需求](#bkmk_authentication)  
  
- [Visual Studio 中 ReportViewer Web 服務器控制項的瀏覽器支援](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a>Power View 瀏覽器案例

 支援的瀏覽器和 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 支援的瀏覽器版本清單取決於開啟的文件類型。 Excel 2013 活頁簿和「**rdlx**」檔案使用不同的元件。  
  
|文件類型|環境|瀏覽器支援|  
|-------------------|-----------------|---------------------|  
|Power View 報表 (.RDLX)|**Sharepoint Server：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sharepoint 整合模式和 Power View web 應用程式。|請參閱[Sharepoint Server 上的 Power View 和 Reporting Services Sharepoint 整合模式](#bkmk_powerview_on_SSRS)。|  
|具有 Power View 工作表的 Excel 2013 活頁簿|**SharePoint Server：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]在 Excel Services 中。<br /><br /> **SharePoint Online （Office 365）：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]在 Excel Web 應用程式上。|請參閱[Excel Services 上的 Power View 或 SharePoint Online 上的 Excel Web 應用程式](#bkmk_powerview_on_ExcelServices)。|  
  
###  <a name="bkmk_powerview_on_SSRS"></a>SharePoint Server 和 Reporting Services SharePoint 整合模式上的 Power View  
 下表摘要說明當使用者在具有 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 服務應用程式並已安裝及設定 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] for SharePoint 增益集的 SharePoint 伺服器陣列中開啟 Power View 報表 (.RDLX) 時，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援的瀏覽器版本。  
  
- 此表格適用於 SharePoint 2010 和 SharePoint 2013。  
  
- 如需 SharePoint 2013 瀏覽器支援的詳細資訊，請參閱[在 sharepoint 2013 中規劃瀏覽器支援](https://technet.microsoft.com//library/cc263526\(office.15\).aspx)（https://technet.microsoft.com/library/cc263526(office.15).aspx)。  
  
- 如需 SharePoint 2010 瀏覽器支援的詳細資訊，請參閱[計畫瀏覽器支援（SharePoint Server 2010）](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) （https://technet.microsoft.com/library/cc263526(office.14).aspx)。  
  
|**瀏覽器**|**Windows 8 和8。1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 10 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 9**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|  
|**Internet Explorer 8**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|  
|**Mozilla Firefox （最新的公開發行版）**|32 位元|32 位元|32 位元|32 位元|32 位元|不支援|  
|**Apple Safari （最新的公開發行版）**|不支援|不支援|不支援|不支援|不支援|32 位元、64 位元|  
  
> [!NOTE]  
> 「32 位元」是指瀏覽器，不是作業系統。 例如，您可以在 64 位元 Windows 7 上使用 32 位元 Internet Explorer 9。  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Internet Explorer 中的 InPrivate 瀏覽功能

 
  [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 不支援 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 和 Internet Explorer 9 中的 InPrivate 瀏覽功能。 如需有關 InPrivate 瀏覽的詳細資訊，請參閱[什麼是 Inprivate 流覽？](https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a>在 Excel Services 或 SharePoint Online 上的 Excel Web 應用程式上 Power View

 下表摘要說明當使用者在執行 Excel Services 的 SharePoint Server 上開啟具有 Power View 工作表的 Excel 2013 活頁簿時， [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 支援的瀏覽器版本：  
  
-   如需 SharePoint 2013 瀏覽器支援的詳細資訊，請參閱[在 sharepoint 2013 中規劃瀏覽器支援](https://technet.microsoft.com/library/cc263526\(office.15\).aspx)（https://technet.microsoft.com/library/cc263526(office.15).aspx)。  
  
|**瀏覽器**|**Windows 8 和8。1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 10 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 9**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|  
|**Internet Explorer 8**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|  
|**Mozilla Firefox （最新的公開發行版）**|32 位元|32 位元|32 位元|32 位元|32 位元|32 位元、64 位元|  
|**Apple Safari （最新的公開發行版）**|不支援|不支援|不支援|不支援|不支援|32 位元、64 位元|  
|**Google Chrome （最新的公開發行版）**|32-位 **（\*）** 用於限定時間|32-位 **（\*）** 用於限定時間|32-位 **（\*）** 用於限定時間|32-位 **（\*）** 用於限定時間|32-位 **（\*）** 用於限定時間|不支援|  
  
 **（\*）** Chrome 將停止支援 Silverlight 所使用的 Netscape 外掛程式 API （NPAPI）。 Power View 會視 Silverlight 而定。  如需詳細資訊，請參閱＜ [NPAPI 的最後倒數計時](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html)＞。  
  
##  <a name="bkmk_reportmanager"></a>報表管理員瀏覽器需求（原生模式）

 以下是目前支援的瀏覽器清單，您可以使用這些瀏覽器執行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式報表管理員，以管理報表和報表伺服器。  
  
|[瀏覽器]|  
|-------------|  
|Internet Explorer 7 (含) 以後版本，而且必須啟用指令碼。|  
|Mozilla FireFox （最新的公開發行版）|  
|Apple Safari （最新的公開發行版）|  
|Google Chrome （最新的公開發行版）|  
  
##  <a name="bkmk_reportviewer"></a>查看報表的瀏覽器需求

 以下是報表檢視器目前支援的瀏覽器和功能清單。 報表檢視器支援從 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表管理員和 SharePoint 文件庫檢視報表。  
  
|**瀏覽器**|**Windows 8 和8。1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|**適用於 iPad 的 iOS 6-7**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|不支援|不支援|  
|**Internet Explorer 10 (適用於桌上型電腦)**|32 位元、64 位元|32 位元、64 位元|32 位元、64 位元|不支援|不支援|不支援|不支援|  
|**Internet Explorer 9**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 8**|不支援|32 位元、64 位元|不支援|32 位元、64 位元|32 位元、64 位元|不支援|不支援|  
|**Internet Explorer 7**|不支援|不支援|不支援|不支援|32 位元、64 位元|不支援|不支援|  
|**Mozilla Firefox （最新的公開發行版）**|32 位元|32 位元|32 位元|32 位元|32 位元|不支援|不支援|  
|**Apple Safari （最新的公開發行版）**|不支援|不支援|不支援|不支援|不支援|32 位元、64 位元|支援有限的功能<sup>（1）</sup>|  
|**Google Chrome （最新的公開發行版）**|32 位元|32 位元|32 位元|32 位元|32 位元|不支援|不支援|  
  
 **<sup>（1）</sup>** 支援下列功能：  
  
- 匯出至 PDF 和 TIFF 格式。  
  
- 在 iOS 裝置的 Apple Safari 中，以互動方式檢視報表。 功能支援包括展開/摺疊、參數窗格以及互動式排序。  
  
- 如需詳細資訊，請參閱[在 Microsoft Surface 裝置和 Apple IOS 裝置上觀看 Reporting Services 報表](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md)。  
  
 **注意**如果您要從 Macintosh 電腦存取報表伺服器，建議您使用 Safari。 如果您使用與[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的 SharePoint 產品，請參閱[規劃瀏覽器支援（Windows SharePoint Services）](https://go.microsoft.com/fwlink/?LinkId=183583)。  
  
### <a name="url-access-for-viewing-reports"></a>檢視報表的 URL 存取

 若要直接檢視報表，而不是透過報表管理員檢視報表，您可以使用 URL 存取來連結報表和報表檢視器。 URL 存取支援各種不同的瀏覽器。  
  
 如需有關 URL 存取的詳細資訊，請參閱下列主題：  
  
- [URL 存取參數參考](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a>驗證需求

 瀏覽器可支援必須由報表伺服器處理的特定驗證配置，用戶端要求才會成功。 下表將識別 Windows 作業系統上執行之每個瀏覽器所支援的預設驗證類型。  
  
|**瀏覽器類型**|**支援**|**瀏覽器預設值**|**伺服器預設值**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|交涉、Kerberos、NTLM、基本|交涉|可以。 搭配 Internet Explorer 使用預設驗證設定。|  
|**Firefox**|NTLM，基本|NTLM|可以。 搭配 Firefox 使用預設驗證設定。|  
|**Safari**|基本|基本|可以。 搭配 Safari 使用預設驗證設定。|  
|**Chrome**|交涉、NTLM、基本|已交涉|可以。 預設驗證設定適用於 Chrome。|  
  
### <a name="script-requirements"></a>指令碼需求

 若要使用報表檢視器，請設定瀏覽器來執行指令碼。  
  
 如果指令碼功能未啟用，當您開啟報表時，會看到類似下列的錯誤訊息：  
  
- **您的瀏覽器不支援腳本，或已設定為不允許腳本執行。按一下這裡以不搭配腳本來觀看這份報表**。  
  
 如果您選擇檢視不含指令碼支援的報表，報表會以 HTML 轉譯，且不含報表檢視器功能 (例如，報表工具列和文件引導模式)。  
  
> [!NOTE]  
> 報表工具列屬於 HTML 檢視器元件的一部分。 根據預設，此工具列會出現在瀏覽器視窗中轉譯的每個報表上方。 報表檢視器會提供一些功能，包括搜尋報表中的資訊、捲動至特定頁面以及調整頁面大小以供檢視等功能。 如需有關報表工具列或 HTML 檢視器的詳細資訊，請參閱＜ [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md)＞。  
  
##  <a name="bkmk_controls"></a>Visual Studio 中 ReportViewer Web 服務器控制項的瀏覽器支援

 ReportViewer Web 伺服器控制項是用來將報表功能內嵌在 ASP.NET Web 應用程式內。 這些控制項隨附在 Visual Studio 中，而且支援與本主題所述之其他元件不同的瀏覽器和瀏覽器版本。 用來檢視應用程式的瀏覽器類型會決定您可以在應用程式中提供的 ReportViewer 功能種類。 請使用本主題提供的資料表來判斷哪些支援的瀏覽器受限於報表功能限制，以及支援的平台。  
  
 由於支援的瀏覽器具有轉譯引擎的差異，所以某些進階報表功能可能會以不同的方式顯示在不同的瀏覽器中。  例如，文字旋轉。  
  
### <a name="scripting-requirements"></a>指令碼需求

 請使用已啟用指令碼支援的瀏覽器。 如果瀏覽器無法執行指令碼，您便無法檢視報表。  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>使用 ReportViewer Web 伺服器控制項檢視報表的瀏覽器需求

 互動式報表功能的支援會因瀏覽器類型而異。 下列支援矩陣顯示哪些瀏覽器類型在哪些平台上受到支援 (受限於 [注意] 資料行中所提的條件約束)。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**瀏覽器**|**Windows 8**和**Windows 8.1**|**Windows 7**|**Windows Server 2012**和**2012 R2**|**Windows Server 2008**和**2008 R2**|**Windows Server 2003**|**Mac OS X 10.6-10。9**|**附註**|  
|**Internet Explorer 11 （適用于桌上型電腦）**|是|是|是|不支援|不支援|不支援|Internet Explorer 支援完整的 ReportViewer 功能集合。|  
|**Internet Explorer 10 (適用於桌上型電腦)**|是|是|是|不支援|不支援|不支援|Internet Explorer 支援完整的 ReportViewer 功能集合。|  
|**Internet Explorer 9**|不支援|是|不支援|是|是|是|Internet Explorer 支援完整的 ReportViewer 功能集合。|  
|**Internet Explorer 8.0**|不支援|是|不支援|是|是<sup>1</sup>|不支援|Internet Explorer 支援完整的 ReportViewer 功能集合。 <sup>sha-1</sup>|  
|**Internet Explorer 7.0**|不支援|是|不支援|是|是<sup>1</sup>|不支援|Internet Explorer 支援完整的 ReportViewer 功能集合。 <sup>sha-1</sup>|  
|**Firefox （最新的公開發行版）**|是|是|是|是|是|不支援|不支援列印和縮放。|  
|**Safari （最新的公開發行版）**|不支援|不支援|不支援|不支援|不支援|是|不支援列印和縮放。<br /><br /> 此瀏覽器已停用在參數化報表上選取日期所用的日曆控制項。 使用者必須手動輸入他們想要在參數提示區域中使用的日期。|  
|**Chrome （最新的公開發行版）**|是|是|是|是|是|不支援|不支援列印和縮放。|  
  
 <sup>1</sup>在標準模式中，Internet Explorer 7.0 和8.0 不會在報表中顯示斜線。 如果您在報表中使用斜線，請將 ASP.NET 頁面設定為可在 Internet Explorer 中的 quirks 模式下執行。 若要這麼做，請\<尋找！ASP.NET 網頁中的 DOCTYPE> 標記。 或者，如果您使用主版頁面，您可以在 .master 檔案中尋找此標記。 此標記的外觀如下：  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 取代\<！使用下列標記的 DOCTYPE> 標記：  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 如需 Internet Explorer 相容性模式的詳細資訊，請參閱[定義檔相容性](https://go.microsoft.com/fwlink/?LinkId=180380)（https://go.microsoft.com/fwlink/?LinkId=180380)。  
  
 如需使用 ReportViewer 控制項的詳細資訊，請參閱[部署報表和 ReportViewer 控制項](https://msdn.microsoft.com/library/ms251723.aspx)（https://msdn.microsoft.com/library/ms251723.aspx)。  
  
## <a name="next-steps"></a>接下來的步驟

 [Reporting Services 工具](tools/reporting-services-tools.md)[報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [HTML 檢視器和報告工具列](html-viewer-and-the-report-toolbar.md)
