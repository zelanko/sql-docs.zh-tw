---
title: Reporting Services 組態管理員 (原生模式) | Microsoft Docs
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6d485289efaff3fe319ed7643132ba0e485221f
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276960"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 組態管理員 (原生模式)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式安裝。 如果您是利用僅限檔案安裝選項來安裝報表伺服器，就必須利用組態管理員來設定伺服器，才能使用該伺服器。 如果您使用預設組態安裝選項來安裝報表伺服器，則可以使用組態管理員來驗證或修改在安裝過程中所指定的設定。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員可用於設定本機或遠端報表伺服器執行個體。

> [!NOTE]
> 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版開始， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員並非設計成管理 SharePoint 模式的報表伺服器。 SharePoint 模式是使用 SharePoint 管理中心和 PowerShell 指令碼來管理並設定。  
  
##  <a name="bkmk_scenarios"></a> 使用 Reporting Services 組態管理員的案例  
 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員執行下列工作：  
  
-   設定報表伺服器服務帳戶。 此帳戶一開始是在安裝過程中設定，但是如果您更新密碼或想要使用其他帳戶，則可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來修改。  
  
-   建立並設定 URL。 報表伺服器與 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 是透過 URL 存取的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式。 報表伺服器 URL 可存取報表伺服器的 SOAP 端點。 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL 是用來開啟 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 。您可以為每個應用程式設定單一 URL 或多個 URL。  
  
-   建立和設定報表伺服器資料庫。 報表伺服器是需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫做為內部儲存的無狀態伺服器。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來建立及設定報表伺服器資料庫的連接。 您也可以選取已經包含您要使用之內容的現有報表伺服器資料庫。  
  
-   設定原生模式向外延展部署。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援部署拓撲，可讓多個報表伺服器執行個體使用單一的共用報表伺服器資料庫。 若要部署報表伺服器向外延展部署，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，將每個報表伺服器連接到共用報表伺服器資料庫。  
  
-   備份、還原或取代用於加密已儲存之連接字串和認證的對稱金鑰。 如果您要變更服務帳戶，或將報表伺服器資料庫移到另一部電腦，您必須先備份對稱金鑰。  
  
-   設定自動執行帳戶。 在排程作業期間或沒有使用者認證時，此帳戶用於遠端連接。  
  
-   設定報表伺服器電子郵件。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含報表伺服器電子郵件傳遞延伸模組，可使用簡易郵件傳送通訊協定 (SMTP) 將報表或報表處理通知傳遞到電子郵件信箱中。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員指定要使用您網路上的哪個 SMTP 伺服器或閘道傳遞電子郵件。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員不會協助您管理報表伺服器內容、啟用其他功能，或授與伺服器的存取權。 完整部署需要您也使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來啟用其他功能或修改預設值，並使用入口網站來授與使用者對伺服器的存取權。

##  <a name="bkmk_requirements"></a> 需求

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員為特定版本所專用。 隨著這個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本一起安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員無法用來設定舊版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 如果您在相同電腦上並存執行舊版和新版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，就必須使用每一個版本所隨附的 Reporting Service 組態管理員來設定每一個執行個體。  

若要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，您必須：

- 在裝載要設定之報表伺服器的電腦上，擁有本機系統管理員權限。 如果要設定遠端電腦，則同樣必須擁有該電腦的本機系統管理員權限。

- 您必須擁有在用來主控報表伺服器資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 上，建立資料庫的權限。

- 進行設定的報表伺服器必須啟用並執行 Windows Management Instrumentation (WMI) 服務。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會使用報表伺服器 WMI 提供者來連接本機與遠端報表伺服器。 如果要設定遠端報表伺服器，該電腦必須允許遠端 WMI 存取。 如需詳細資訊，請參閱 [設定報表伺服器來進行遠端管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)。  

- 在您可以連接及設定遠端報表伺服器執行個體之前，您必須先啟用要通過 Windows 防火牆傳遞的 Windows Management Instrumentation (WMI) 呼叫。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) 設定報表伺服器來進行遠端管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

當您安裝 SQL Server Reporting Services 時，會自動安裝 Reporting Services 組態管理員。

##  <a name="bkmk_start_configuration_manager"></a> 啟動 Reporting Services 組態管理員

1.  請使用下列適合您的 Microsoft Windows 版本的步驟：

    - 在 Windows 的 [開始] 畫面上，鍵入 **Reporting** ，然後從搜尋結果中選取 [Reporting Services 組態管理員] 。

    - 選取 [開始]，然後依序指向 [所有程式] 和 [[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]，再指向 [組態工具]。

         如果您想要從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定報表伺服器執行個體，請開啟該版本的程式資料夾。 例如，指向 [ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ] 而不是 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] ]，以開啟 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 伺服器元件的組態工具。

         選取 [Reporting Services 組態管理員]。

2. **[Reporting Services 組態連接]** 對話方塊隨即出現，可讓您選取所要設定的報表伺服器執行個體。 選取 [連接]。

3. 在 **[伺服器名稱]** 中，指定安裝報表伺服器執行個體的電腦名稱。 預設會出現本機電腦的名稱，但是如果您想要連接到遠端電腦上所安裝的報表伺服器，也可以輸入遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。

4. 如果您指定遠端電腦，請選取 [尋找] 來建立連線。

5. 在 **Report Server 在stance**中，選取您要設定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。 只有這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的報表伺服器執行個體會顯示在清單中。 您不能設定舊版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。

6. 選取 [連接]。

## <a name="next-steps"></a>後續步驟

[入口網站](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
[設定報表伺服器資料庫連線](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)   
[設定和管理報表伺服器](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
