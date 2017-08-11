---
title: "啟用和停用 reporting Services 的用戶端列印 |Microsoft 文件"
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
helpviewer_keywords:
- pdf
- viewer
- reportviewer
- toolbar
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ee650a09b57ae92abda378fea6fc780b550fbac4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---

# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>啟用和停用 Reporting Services 的用戶端列印功能

  報表檢視器工具列上的 [列印] 按鈕使用可攜式文件格式 (PDF)，提供用戶端在瀏覽器中檢視之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表的列印。 新的遠端列印體驗使用包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 PDF 轉譯延伸模組，以將報表轉譯為 PDF 模式。 您可以下載 .PDF 格式的報表，或如果您已安裝可檢視 .PDF 檔案的應用程式，列印按鈕會顯示列印對話方塊，提供頁面常用設定項目，例如頁面大小方向及 .PDF 檔案的預覽。 雖然依預設會啟用用戶端列印，但如果您不想提供此功能，也可以停用它。  
  
 舊版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 ActiveX 控制項，它必須從報表伺服器下載至用戶端電腦。 如果您將報表伺服器升級至 SQL Server 2016 列印控制項不會移除從報表伺服器或用戶端電腦。  

##  <a name="bkmk_clientside_printexpereince"></a> 列印體驗  
 當您按一下列印![htmlviewer_print](../../reporting-services/report-server/media/htmlviewer-print.png "htmlviewer_print")按鈕的報表檢視器工具列上，經驗會根據項目而有所不同。PDF 檢視應用程式會安裝在用戶端電腦以及您使用瀏覽器。   您可以下載 PDF 檔案，或從對話方塊設定列印選項，取決於用戶端電腦。  
  
 ![報表工具列](../../reporting-services/media/ssrs-htmlviewer-toolbar.png "報表工具列")  
  
|||  
|-|-|  
|第一個對話方塊在所有瀏覽器中都相同，並且允許您變更基本版面配置屬性，例如方向。 當您按一下 [列印] ，其體驗會依您使用的瀏覽器而稍有不同。|![ssrs_pdfprint_chrome1](../../reporting-services/report-server/media/ssrs-pdfprint-chrome1.png "ssrs_pdfprint_chrome1")|  
|在 Chrome 中，會開啟詳細的瀏覽器列印對話方塊。   您可以變更列印設定、列印和開啟作業系統列印對話方塊。|![ssrs_pdfprint_chrome2](../../reporting-services/report-server/media/ssrs-pdfprint-chrome2.png "ssrs_pdfprint_chrome2") ![ssrs_pdfprint_chrome3.png](../../reporting-services/report-server/media/ssrs-pdfprint-chrome3-png.png "ssrs_pdfprint_chrome3.png")|  
|如果您已安裝 PDF 閱讀程式應用程式，列印按鈕將會開啟 PDF 檔案的預覽視窗，您可以儲存或列印。||  
|如果您沒有安裝 PDF 閱讀程式應用程式，則會有兩種使用者體驗：<br /><br /> 報表將自動轉譯，並使用您的瀏覽器下載程序下載 PDF 檔案。   **注意：** 報表越複雜，則您按下 [列印]  到您看見瀏覽器下載通知之間的延遲就越久。 您也可以按一下 [按一下這裡以檢視報表 PDF。] 強制再次下載。<br /><br /> 按一下 [按一下這裡以檢視報表 PDF。] 強制下載 PDF。|![ssrs_pdfprint_firefox2](../../reporting-services/report-server/media/ssrs-pdfprint-firefox2.png "ssrs_pdfprint_firefox2")|  
  
##  <a name="bkmk_troubleshoot_clientsideprinting"></a> 疑難排解用戶端列印功能  
 如果報表檢視器工具列上的列印按鈕已停用，請確認下列項目：  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中報表伺服器的用戶端列印功能已停用。 請參閱本主題中的  [啟用及停用用戶端列印功能](#bkmk_enable) 一節。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] PDF 轉譯延伸模組已停用。 檢閱 `<Extension Name="PDF"` rsreportserver.config **檔案的** 區段。  
  
-   您正在比較模式中檢視報告，該模式使用舊的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] HTML4 轉譯引擎。 PDF 列印體驗需要 HTML 5 轉譯引擎。  按一下工具列上的 [嘗試預覽]  按鈕。  
  
     ![ssrs_html5_switch2html5](../../reporting-services/report-server/media/ssrs-html5-switch2html5.png "ssrs_html5_switch2html5")  
  
##  <a name="bkmk_enable"></a> 啟用及停用用戶端列印功能  
 報表伺服器管理員可以選擇將報表伺服器系統屬性 **EnableClientPrinting** 設定為 **false**，來停用遠端列印功能。 這樣會停用由該伺服器管理的所有報表的用戶端列印功能。 依預設， **EnableClientPrinting** 設定為 **true**。 您可以採用下列方式來停用用戶端列印：  
  
-   針對 **原生模式報表伺服器**：  
  
    1.  使用系統管理權限來啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    2.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，連接到報表伺服器執行個體。  
  
    3.  報表伺服器節點，以滑鼠右鍵按一下，然後按一下 **屬性**。 如果 **[屬性]** 選項已停用，請確認您已使用系統管理權限來啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    4.  按一下 **[進階]**。  
  
    5.  選取 **EnableClientPrinting**中報表伺服器的用戶端列印功能已停用。  
  
    6.  設為 True 或 False 然後按一下 [確定] 。  
  
         ![ssrs_ssmsproperties_clientprinting](../../reporting-services/report-server/media/ssrs-ssmsproperties-clientprinting.png "ssrs_ssmsproperties_clientprinting")  
  
-   針對 **SharePoint 模式報表伺服器**：  
  
    1.  在 SharePoint 管理中心內，按一下 **[應用程式管理]**。  
  
    2.  按一下 **[管理服務應用程式]**。  
  
    3.  按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱，然後按一下 SharePoint 功能區中的 **[管理]** 。  
  
    4.  按一下 **[系統設定]**。  
  
    5.  選取 **[啟用用戶端列印]**。 **[啟用用戶端列印]** 選項位於靠近頁面底部的位置。  
  
    6.  按一下 **[確定]**。  
  
-   撰寫指令碼或程式碼，將報表伺服器系統屬性 **EnableClientPrinting** 設定為 **false.**。  
  
 下列範例指令碼說明停用用戶端列印功能的方法之一。 編譯後執行下列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 程式碼，將 **EnableClientPrinting** 屬性設定為 **[False]**。 執行程式碼之後，請重新啟動 IIS。  
  
### <a name="sample-script"></a>範例指令碼  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

