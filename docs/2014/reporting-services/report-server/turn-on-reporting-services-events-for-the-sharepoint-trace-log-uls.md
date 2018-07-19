---
title: 開啟 SharePoint 追蹤記錄檔的 Reporting Services 事件 (ULS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 81110ef6-4289-405c-a931-e7e9f49e69ba
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8b278a5e71b3954e8d296fd9dc7644b33b99aae9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244328"
---
# <a name="turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls"></a>Turn on Reporting Services events for the SharePoint trace log (ULS)
  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，SharePoint 模式的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 伺服器可以將 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 事件寫入 SharePoint 統一記錄服務 (ULS) 追蹤記錄。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定類別目錄。  
  
 本主題內容：  
  
-   [一般 ULS 記錄建議](#bkmk_general)  
  
-   [開啟和關閉 Reporting Services 類別目錄中的 Reporting Services 事件](#bkmk_turnon)  
  
-   [建議組態](#bkmk_recommended)  
  
-   [讀取記錄項目](#bkmk_readentries)  
  
-   [SQL Server Reporting Services 事件清單](#bkmk_list)  
  
-   [利用 PowerShell 檢視記錄檔](#bkmk_powershell)  
  
-   [追蹤記錄位置](#bkmk_trace)  
  
##  <a name="bkmk_general"></a> 一般 ULS 記錄建議  
 下表將針對監視 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 環境，列出建議的事件類別目錄和層級。 記錄事件時，每個項目都會包含記錄事件的時間、處理序名稱，以及執行緒識別碼。  
  
|類別目錄|層級|描述|  
|--------------|-----------|-----------------|  
|[資料庫]|「詳細資訊」|記錄涉及資料庫存取權的事件。|  
|一般|「詳細資訊」|記錄涉及下列項目之存取權的事件：<br /><br /> [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 網頁<br /><br /> 報表檢視器 HTTP 處理常式<br /><br /> 報表存取 (.rdl 檔)<br /><br /> 資料來源 (.rsds 檔)<br /><br /> SharePoint 網站的 URL (.smdl 檔)|  
|Office Server 一般|Exception|記錄登入失敗。|  
|拓撲|Verbose|記錄目前的使用者資訊。|  
|Web 組件|「詳細資訊」|記錄涉及報表檢視器 Web 組件之存取權的事件。|  
  
##  <a name="bkmk_turnon"></a> 開啟和關閉 Reporting Services 類別目錄中的 Reporting Services 事件  
  
1.  在 SharePoint 管理中心內  
  
2.  按一下 **[監視]**。  
  
3.  按一下 **[報表]** 群組中的 **[設定診斷記錄]** 。  
  
4.  在類別目錄清單中找到 **[SQL Server Reporting Services]** 。  
  
5.  按一下加號 (+) 展開 **[SQL Server Reporting Services]** 之下的子類別目錄。  
  
6.  選取要加入至追蹤記錄的子類別目錄。  
  
7.  在類別目錄清單的底部，選取 **[回報至追蹤記錄的最低緊急事件]** 的事件等級。 選取 **[無]** 停用追蹤。  
  
> [!NOTE]  
>  **不支援** [回報至追蹤記錄的最低緊急事件] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]選項。 已忽略此選項。  
  
##  <a name="bkmk_recommended"></a> 建議組態  
 建議您使用下列記錄選項做為標準組態：  
  
-   **HTTP 重新導向程式**  
  
-   **SOAP 用戶端 Proxy**  
  
-   如果您遇到組態設定方面的問題，請加入 **[組態頁面]**。  
  
 您可以使用下列 PowerShell 指令程式來檢閱所有目前伺服器陣列診斷記錄設定：  
  
```  
Get-SPDiagnosticConfig  
```  
  
##  <a name="bkmk_readentries"></a> 讀取記錄項目  
 記錄中的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 項目會以下列方式格式化。  
  
1.  **產品：SQL Server Reporting Services**  
  
2.  **類別目錄：** 與伺服器相關的事件其名稱開頭會有 "Report Server" 字元。 例如 "Report Server Alerting Runtime"，這些事件會記錄到報表伺服器記錄檔。  
  
3.  **類別目錄：** 與 Web 前端元件相關或從中進行通訊的事件不會包含 "Report Server"。 例如 "Service Application Proxy"、"Report Server Alerting Runtime"。 WFE 項目會包含 CorrelationID，但伺服器項目不會包含。  
  
##  <a name="bkmk_list"></a> SQL Server Reporting Services 事件清單  
 下表為 SQL Server Reporting Services 類別目錄中事件的清單：  
  
|區域名稱|描述或範例項目|  
|---------------|-----------------------------------|  
|[組態頁面]||  
|HTTP 重新導向程式||  
|本機模式處理||  
|本機模式轉譯||  
|SOAP 用戶端 Proxy||  
|UI 頁面||  
|Power View|已寫入 **LogClientTraceEvents** API 中的記錄項目。 這些項目來自於用戶端應用程式，包括[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，一項功能[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]增益集[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition。<br /><br /> 所有來自於 LogClientTraceEvents API 的記錄項目都會記錄在 “SQL Server Reporting Services” 的 **類別目錄** 和 “Power View” 的 **區域** 之下。<br /><br /> 使用 “Power View” 的區域所記錄的項目內容是由用戶端應用程式所決定。|  
|報表伺服器警示執行階段||  
|報表伺服器應用程式定義域管理員||  
|報表伺服器緩衝回應||  
|報表伺服器快取||  
|報表伺服器目錄||  
|報表伺服器區塊||  
|報表伺服器清除||  
|報表伺服器組態管理員|範例項目：<br /><br /> MediumUsing 報表伺服器內部 URL http://localhost:80/ReportServer。<br /><br /> UnexpectedMissing 或是無效的 ExtendedProtectionLevel 設定|  
|報表伺服器密碼編譯||  
|報表伺服器資料延伸模組||  
|報表伺服器資料庫輪詢||  
|報表伺服器預設值||  
|報表伺服器電子郵件延伸模組||  
|報表伺服器 Excel 轉譯器||  
|報表伺服器延伸模組 Factory||  
|報表伺服器 HTTP 執行階段||  
|報表伺服器影像轉譯器||  
|報表伺服器記憶體監控||  
|報表伺服器通知||  
|報表伺服器處理||  
|報表伺服器提供者||  
|報表伺服器轉譯||  
|報表伺服器報表預覽||  
|報表伺服器資源公用程式|範例項目：<br /><br /> MediumReporting Services 啟動 SKU：評估版<br /><br /> MediumEvaluation 複本：剩下 180 天|  
|報表伺服器執行工作||  
|報表伺服器執行要求||  
|報表伺服器排程||  
|報表伺服器安全性||  
|報表伺服器服務控制器||  
|報表伺服器工作階段||  
|報表伺服器訂閱||  
|報表伺服器 WCF 執行階段||  
|報表伺服器 Web 服務||  
|服務應用程式 Proxy||  
|共用服務|範例項目：<br /><br /> MediumUpdating ReportingWebServiceApplication<br /><br /> MediumGranting 對內容資料庫的存取。<br /><br /> ReportingWebServiceApplication 的 MediumProvisioning 執行個體<br /><br /> ReportingWebServiceApplication 的 MediumProcessing 服務帳戶變更<br /><br /> MediumSetting 資料庫權限。|  
  
##  <a name="bkmk_powershell"></a> 利用 PowerShell 檢視記錄檔  
 ![PowerShell 相關內容](../media/rs-powershellicon.jpg "PowerShell 相關內容")您可以使用 PowerShell 從 ULS 記錄檔傳回 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 相關事件的清單。 從 SharePoint 2010 管理命令介面輸入下列命令，從包含 "**sql server reporting services**" 的 ULS 記錄檔 UESQL11SPOINT-20110606-1530.log 傳回已篩選過的資料列清單：  
  
```  
Get-content -path "C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS\UESQL11SPOINT-20110606-1530.log" | select-string "sql server reporting services”  
```  
  
 您可以下載多種可用來讀取 ULS 記錄的工具。 例如， [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com/) 或 [SharePoint ULS 記錄檢視器](http://ulsviewer.codeplex.com/workitem/list/basic)。 兩者都在 CodePlex 上提供。  
  
 如需有關如何使用 PowerShell 來檢視記錄資料的詳細資訊，請參閱 [檢視診斷記錄 (SharePoint Server 2010)](http://technet.microsoft.com/library/ff463595.aspx)  
  
##  <a name="bkmk_trace"></a> 追蹤記錄位置  
 追蹤記錄檔通常位於 **c:\Program Files\Common files\Microsoft Shared\Web Server Extensions\14\logs** 資料夾中，但是您可以從 SharePoint 管理中心的 **[診斷記錄]** 頁面中驗證或變更此路徑。  
  
 如需詳細資訊以及在 SharePoint 2010 管理中心內設定 SharePoint 伺服器之診斷記錄的步驟，請參閱 [設定診斷記錄設定 (Windows SharePoint Services)](http://go.microsoft.com/fwlink/?LinkID=114423)。  
  
  
