---
title: 將 SQL Server Reporting Services 報表檢視器網頁組件部署至 SharePoint 頁面 | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.suite: pro-bi
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9106f0b63831920b1a685b92ed5d2d82db41622e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265627"
---
# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>將 SQL Server Reporting Services 報表檢視器網頁組件部署至 SharePoint 頁面

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

報表檢視器網頁組件是自訂的網頁組件，可用於檢視 SharePoint 網站中的 SQL Server Reporting Services (原生模式) 報表。 您可以在使用網頁組件來檢視、巡覽、列印並匯出報表伺服器的報表。 報表檢視器網頁組件與 SQL Server Reporting Services 報表伺服器或 Power BI 報表伺服器所處理的報表定義 (.rdl) 檔建立關聯。 此報表檢視器網頁組件不能搭配 Power BI 報表伺服器中裝載的 Power BI 報表使用。

使用下列指示手動部署解決方案套件，將報表檢視器網頁組件新增至 SharePoint Server 2013 或 SharePoint Server 2016 環境。 部署解決方案是設定網頁組件的必要步驟。

**報表檢視器網頁組件是獨立的解決方案套件，與 SQL Server Reporting Services 的 SharePoint 整合模式未建立關聯。**

## <a name="requirements"></a>需求

> [!IMPORTANT]
> 如果您已經設定 Reporting Services SharePoint 整合模式，則目前無法安裝此網頁組件。
>

**支援的 SharePoint 伺服器版本：**
* SharePoint Server 2016
* SharePoint Server 2013

**支援的 Reporting Services 版本：**  
* SQL Server 2008 Reporting Services (原生模式) 及更新版本。
* Power BI 報表伺服器

## <a name="download-the-report-viewer-web-part-solution-package"></a>下載報表檢視器網頁組件解決方案套件

Microsoft 下載中心提供報表檢視器網頁組件。

[下載報表檢視器網頁組件解決方案套件](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>重新部署伺服器陣列解決方案

本節說明如何在 SharePoint 伺服器陣列中部署解決方案套件。 這個工作只需要執行一次。

1. 在 SharePoint 伺服器上，使用 [以系統管理員身分執行] 選項開啟 SharePoint 管理介面。

2. 執行 [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) 以新增伺服器陣列解決方案。

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。

3. 執行 [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) Cmdlet 以部署伺服器陣列解決方案。

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>啟用功能

1. 在 SharePoint 網站中，選取左上方的**齒輪**圖示，然後選取 [網站設定]。

    ![從齒輪圖示開啟網站設定。](media/sharepoint-site-settings.png)

    根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示通常只要輸入 *http://<computer name>* 即可存取 SharePoint 網站來開啟根網站集合。

3. 在 [網站集合管理] 中選取 [網站集合功能]。

4. 向下捲動網頁，直到您找到**報表檢視器網頁組件**功能。

5. 選取 [啟用]。

    ![啟動報表檢視器網頁組件功能](media/web-part-activiate-feature.png)

6. 開啟每個網站並按一下 [網站動作]，為其他網站集合重複執行。

(選擇性) 您也可以使用 [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx) Cmdlet，在所有網站上使用 PowerShell 啟用此功能。

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>移除解決方案

雖然 SharePoint 管理中心可以撤銷解決方案，但是除非有以系統方式排除安裝或修補程式的部署問題，否則不需要撤銷 **ReportViewerWebPart.wsp** 檔案。

1. 在 SharePoint 管理中心的 [系統設定] 中，選取 [管理伺服器陣列方案]。

2. 選取 **ReportViewerWebPart.wsp**。

3. 選取 [撤銷方案]。

### <a name="remove-the-web-part-from-site-settings"></a>移除網站設定中的網頁組件

撤銷解決方案不會從 SharePoint 網站中的網頁組件清單中移除報表檢視器網頁組件。 若要移除報表檢視器網頁組件，請執行下列作業。

1. 在 SharePoint 網站中，選取左上方的**齒輪**圖示，然後選取 [網站設定]。

    ![從齒輪圖示開啟網站設定。](media/sharepoint-site-settings.png)

    根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示通常只要輸入 *http://<computer name>* 即可存取 SharePoint 網站來開啟根網站集合。

2. 在**網站設計工具庫**下選取 [網頁組件]。

3. 選取 **ReportViewerNativeMode.dwp** 旁邊的**編輯圖示**。 它可能不會列在第一頁結果中。

4. 選取 [刪除項目]。

    ![編輯和刪除報表檢視器原生模式網頁組件](media/report-viewer-native-mode-edit-delete.png)

您可嘗試使用 PowerShell 刪除網頁組件，但此做法沒有直接命令。 如需指令碼範例，請參閱 [How to delete web parts from the web part Gallery](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f) (如何刪除網頁組件庫的網頁組件)。

## <a name="supported-languages"></a>支援的語言

網頁組件支援下列語言：

* 英文 (en)
* 德文 (de)
* 西班牙文 (sp)
* 法文 (fr)
* 義大利文 (it)
* 日文 (ja)
* 韓文 (ko)
* 葡萄牙文 (pt)
* 俄文 (ru)
* 中文 (簡體 - zh-HANS 與 zh-CHS)
* 中文 (繁體 - zh-HANS 與 zh-CHT)

## <a name="troubleshoot"></a>疑難排解

* 在您已設定 SharePoint 整合模式時解除安裝 SSRS 時發生錯誤：

    Install-SPRSService: [A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService 無法轉換成 [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService。 類型 A 源自 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll' 位置之 'Default' 內容中的 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'。 類型 B 源自 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll' 位置之 'Default' 內容中的 'Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'。
    
    解決方案：
    1. 移除報表檢視器網頁組件
    2. 解除安裝 SSRS
    3. 重新安裝報表檢視器網頁組件

* 在您已設定 SharePoint 整合模式時嘗試升級 SharePoint 時發生錯誤：

    無法載入檔案或組件 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' 或其相依性的其中之一。 系統找不到指定的檔案。 00000000-0000-0000-0000-000000000000
    
    解決方案：
    1. 移除報表檢視器網頁組件
    2. 解除安裝 SSRS
    3. 重新安裝報表檢視器網頁組件

## <a name="next-steps"></a>後續步驟

部署並啟動報表檢視器網頁組件後，您可以將網頁組件新增至 SharePoint 網頁。 如需詳細資訊，請參閱[將報表檢視器網頁組件新增到 SharePoint 頁面](add-report-viewer-web-part-to-page.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
