---
title: "部署 SharePoint 網站上的 SQL Server Reporting Services 報表檢視器 web 組件 |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a75ad193204e17e1d053aa4e00adba5f551d684b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---

# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>部署 SharePoint 網站上的 SQL Server Reporting Services 報表檢視器 web 組件

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

報表檢視器 web 組件是可用來檢視 SharePoint 網站中的 SQL Server Reporting Services （原生模式） 報表的自訂 web 組件。 您可以使用 web 組件來檢視、 導覽、 列印並匯出報表的報表伺服器上。 報表檢視器 web 組件都與 SQL Server Reporting Services 報表伺服器或 Power BI 報表伺服器所處理的報表定義 (.rdl) 檔案。 此報表檢視器 web 組件不能與 Power BI 報表伺服器中主控的 Power BI 報表。

使用下列指示手動部署方案套件，將報表檢視器 web 組件加入至 SharePoint Server 2013 或 SharePoint Server 2016 的環境。 部署方案是設定網頁組件的必要的步驟。

**報表檢視器 web 組件是獨立的方案套件，並不是相關聯的 SQL Server Reporting Services SharePoint 整合模式。**

## <a name="requirements"></a>需求

**支援 SharePoint Server 版本：**  
* SharePoint Server 2016
* SharePoint Server 2013

**支援 Reporting Services 版本：**  
* SQL Server 2008 Reporting Services （原生模式） 及更新版本。
* Power BI 報表伺服器

## <a name="download-the-report-viewer-web-part-solution-package"></a>下載報表檢視器 web 組件的方案套件

Microsoft Download Center 上可用的報表檢視器 web 組件。

[下載報表檢視器 web 組件的方案套件](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>部署伺服器陣列方案

本節說明如何在 SharePoint 伺服器陣列中部署方案套件。 這個工作只需要執行一次。

1. 在 SharePoint 伺服器上，開啟 SharePoint 管理命令介面，使用**系統管理員身分執行**選項。

2. 執行[Add-spsolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx)加入伺服器陣列方案。

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。

3. 執行[Install-spsolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx)指令程式來部署伺服器陣列方案。

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>啟用功能

1. 在 SharePoint 網站中，選取**齒輪**圖示在左上方和選取 **站台設定*。

    ![站台設定，從齒輪圖示。](media/sharepoint-site-settings.png)

    根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示您通常可以存取 SharePoint 網站輸入*http://<computer name>* 以開啟根網站集合。

3. 在**網站集合管理**，選取**網站集合功能**。

4. 網頁向下捲動直到您找到**報表檢視器 web 組件**功能。

5. 選取**啟動**。

    ![啟用報表檢視器 web 組件功能](media/web-part-activiate-feature.png)

6. 開啟每個站台，然後按一下 [網站動作] 中，以重複其他網站集合。

（選擇性） 您也可以以 PowerShell 使用的所有站台上啟用此功能[Enable-spfeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet。

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>移除解決方案

雖然 SharePoint 管理中心內會提供方案撤銷，但是您不需要撤銷**ReportViewerWebPart.wsp**檔案，除非您有系統地排除安裝或修補程式部署問題。

1. 在 SharePoint 管理中心中**系統設定**，選取**管理伺服器陣列方案**。

2. 選取**ReportViewerWebPart.wsp**。

3. 選取撤銷方案。

### <a name="remove-the-web-part-from-site-settings"></a>移除站台設定 web 組件

撤銷方案不會移除報表檢視器 web 組件的 SharePoint 網站中的 web 組件清單。 若要移除報表檢視器 web 組件，執行下列作業。

1. 在 SharePoint 網站中，選取**齒輪**圖示在左上方和選取 **站台設定*。

    ![站台設定，從齒輪圖示。](media/sharepoint-site-settings.png)

    根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示您通常可以存取 SharePoint 網站輸入*http://<computer name>* 以開啟根網站集合。

2. 在下**Web 設計工具庫**，選取**web 組件**。

3. 選取**編輯圖示**旁**ReportViewerNativeMode.dwp**。 它可能不會列在結果的第一頁中。

4. 選取**刪除項目**。

    ![編輯和刪除原生模式的報表檢視器 web 組件](media/report-viewer-native-mode-edit-delete.png)

使用 PowerShell，嘗試進行刪除 web 組件，但不是它的直接命令。 如需指令碼的範例，請參閱[如何從 web 組件庫中刪除 web 組件](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)。

## <a name="supported-languages"></a>支援的語言

Web 組件支援下列語言：

* 英文 (en)
* 德文 (de)
* 西班牙文 (sp)
* 法文 (fr)
* 義大利文 （它）
* 日文 (ja)
* 韓文 (ko)
* 葡萄牙文 (pt)
* 俄文 (ru)
* 中文 （簡體-zh-chs 和 HANS 和 ZH-CHS）
* 中文 （繁體-zh-chs 和 HANT 和 zh-chs 和 ZH-CHT）

## <a name="next-steps"></a>後續的步驟

之後的報表檢視器 web 組件已部署和 activiated，您可以加入至 SharePoint 網頁的 web 組件。 如需詳細資訊，請參閱[加入報表檢視器 web 組件至 SharePoint 網頁](add-report-viewer-web-part-to-page.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

