---
title: 安裝 Reporting Services 原生模式報表伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9bfbae24063bfa3daa7fbafd1004125e826f6886
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851863"
---
# <a name="install-reporting-services-native-mode-report-server"></a>安裝 Reporting Services 原生模式報表伺服器
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式報表伺服器可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈或命令列安裝。 在安裝精靈中，您也可以選擇 1) 安裝檔案並以預設值設定伺服器，或 2) 僅安裝檔案但不要由安裝精靈設定伺服器。 本主題檢閱 *「原生模式的預設組態」* (Default Configuration for Native Mode)，其中安裝程式會安裝及設定報表伺服器執行個體。 當安裝程式完成之後，報表伺服器會執行及備妥使用。 原生模式報表伺服器會當做獨立的應用程式伺服器來執行。 原生模式為預設伺服器模式。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
##  <a name="bkmk_top"></a> 本主題內容  
  
-   [什麼是預設組態？](#bkmk_whatisdefaultconfiguration)  
  
-   [何時安裝原生模式預設組態](#bkmk_whentoinstalldefaultconfig)  
  
-   [需求](#bkmk_requirements)  
  
-   [預設 URL 保留項目](#bkmk_defaultURLreservations)  
  
-   [使用 SQL Server 安裝精靈安裝原生模式](#bkmk_installwithwizard)  
  
-   [使用命令列安裝原生模式](#bkmk_commandline)  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> 什麼是預設組態？  
 當您選取原生模式的預設組態選項時，安裝程式會安裝下列 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
-   報表伺服器服務 (包含報表伺服器 Web 服務、背景處理應用程式及報表管理員)。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令列公用程式 (rsconfig.exe、rskeymgmt.exe 及 rs.exe)  
  
 此選項不會套用到類似 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的共用功能；如果您想要安裝這些功能，必須將其指定為個別項目。  
  
 安裝程式會針對原生模式報表伺服器安裝設定以下項目：  
  
-   報表伺服器服務的服務帳戶。  
  
-   報表伺服器 Web 服務 URL。  
  
-   報表管理員 URL。  
  
-   報表伺服器資料庫。  
  
-   報表伺服器資料庫的服務帳戶存取。  
  
-   報表伺服器資料庫的 DSN 連接。  
  
 安裝程式不會設定自動執行帳戶、報表伺服器電子郵件、備份加密金鑰或向外延展部署。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定這些屬性。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> 何時安裝原生模式預設組態  
 預設組態會在作業狀態下安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，好讓您可以在安裝程式完成之後立刻使用報表伺服器。 當您想要儲存步驟時，請指定這個模式，其方式是刪除您原本必須在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具內執行的任何必要組態工作。  
  
 安裝預設組態並不保證報表伺服器可在安裝程式完成之後運作。 當此服務啟動時，預設 URL 可能無法註冊。 請務必要測試您的安裝，以確認此服務可如預期般啟動及執行。  
  
##  <a name="bkmk_requirements"></a> 需求  
 預設組態選項會使用預設值來設定讓報表伺服器運作所需的核心設定， 它的需求如下：  
  
-   您的硬體應符合執行 Microsoft SQL Server 的最低和軟體需求。 如需詳細資訊，請參閱＜ [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)＞。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須一起安裝在相同的執行個體中。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體會主控安裝程式所建立及設定的報表伺服器資料庫。  
  
-   用來執行安裝程式的使用者帳戶必須是本機管理員群組的成員，而且擁有在主控報表伺服器資料庫之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上存取和建立資料庫的權限。  
  
-   安裝程式必須能夠使用預設值，以保留可提供報表伺服器和報表管理員之存取的 URL。 這些值包括連接埠 80、一個強式萬用字元，以及採用 **ReportServer_\<***instance_name***>** 和 **Reports_\<***instance_name***>** 格式的虛擬目錄名稱。  
  
-   安裝程式必須能夠使用預設值，以建立報表伺服器資料庫。 這些值為 **ReportServer** 和 **ReportServerTempDB**。 如果您現有的資料庫是來自之前的安裝，安裝程式將會被封鎖，因為它無法在原生模式的預設組態中設定報表伺服器。 您必須重新命名、移動或刪除這些資料庫，才能解除封鎖安裝程式。  
  
 如果您的電腦未能滿足預設安裝的所有需求，就必須在僅限檔案模式中安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，然後在安裝程式完成之後使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來進行設定。  
  
 不要只是為了讓預設安裝能夠繼續就嘗試重新設定電腦， 這樣做可能需要好幾個小時的工作，讓原本可從安裝選項獲得的省時優點消失殆盡。 最佳的解決方案是在僅限檔案模式中安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，然後設定報表伺服器使用特定值。  
  
##  <a name="bkmk_defaultURLreservations"></a> 預設 URL 保留項目  
 URL 保留項目是由前置詞、主機名稱、通訊埠和虛擬目錄所組成：  
  
|部分|描述|  
|----------|-----------------|  
|Prefix|預設前置詞是 HTTP。 如果您之前安裝了安全通訊端層 (SSL) 憑證，安裝程式將會嘗試建立使用 HTTPS 前置詞的 URL 保留項目。|  
|主機名稱|預設主機名稱是強式萬用字元 (+)， 它會指定報表伺服器會接受任何主機名稱解析為電腦，包括 http:// 來指定連接埠上的任何 HTTP 要求\<電腦名稱 > / reportserver， http://localhost/reportserver，或 http://\<IPAddress > /reportserver。|  
|通訊埠|預設連接埠是 80。 請注意，如果您使用通訊埠 80 以外的任何通訊埠，當您在瀏覽器視窗中開啟 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 應用程式時，就必須明確將此通訊埠加入 URL 中。|  
|虛擬目錄|根據預設，系統會使用 Reportserver_< 格式建立虛擬目錄\<*instance_name*> 針對報表伺服器 Web 服務和 reports_<\<*instance_name*>報表管理員。 如果是報表伺服器 Web 服務，預設虛擬目錄會是 **reportserver**。 如果是報表管理員，預設虛擬目錄則為 **reports**。|  
  
 完整 URL 字串可能出現的範例如下：  
  
-   http://+:80/reportserver，提供報表伺服器的存取權。  
  
-   http://+:80/reports提供存取至報表管理員。  
  
##  <a name="bkmk_installwithwizard"></a> 使用 SQL Server 安裝精靈安裝原生模式  
 下列清單描述您在 SQL Server 安裝精靈中選取的  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 專屬步驟和選項。 此清單不會描述您在安裝精靈中看見的每一個頁面，而是只有屬於原生模式安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相關頁面。  
  
1.  在 **[安裝程式角色]** 頁面上，選取 **[SQL Server 功能安裝]**。  
  
     ![適用於安裝程式角色的 SQL Server 功能安裝](../../../2014/sql-server/install/media/rs-setuprole.gif "適用於安裝程式角色的 SQL Server 功能安裝")  
  
2.  在 **[特徵選取]** 頁面上，選取下列選項：  
  
    -   **[Database Engine Services]**(除非已安裝資料庫引擎執行個體)。  
  
    -   **Reporting Services 原生**。  
  
    -   **[管理工具 - 基本]**。 管理工具並非必要，但建議您使用這些工具，除非您安裝了其他管理工具。 預設組態選項會產生可運作的報表伺服器，但您可能想要在日後變更組態選項。 某些選項 (像是 [我的報表]) 是透過 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 加以管理。  
  
     ![特徵選取中的 SSRS 原生模式選取](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "特徵選取中的 SSRS 原生模式選取")  
  
3.  如果您打算使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能，就需要在 **[伺服器組態]** 頁面上確認 SQL Server Agent 是否設定為 **[自動]** 啟動類型。  
  
4.  在 **[Reporting Services 組態]** 頁面上選取 **[安裝和設定]**。  
  
     ![SSRS 原生模式設定](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "SSRS 原生模式設定")  
  
5.  SQL Server 安裝精靈完成後，請利用下列基本步驟驗證預設的原生模式安裝。  
  
    -   開啟 [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員]，並確認能夠連接到報表伺服器。  
  
    -   以系統管理權限開啟瀏覽器，並連接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理員，例如 `http://loclahost/Reports`。  
  
    -   以系統管理權限開啟瀏覽器，並連接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器頁面。 例如，  `http://loclahost/ReportServer`  
  
 如需詳細資訊，請參閱下列兩個主題的＜原生＞一節：  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [針對 Reporting Services 安裝進行疑難排解](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
##  <a name="bkmk_commandline"></a> 使用命令列安裝原生模式  
 下列範例包含 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務，因為它是預設組態所需。  
  
```  
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS"   
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK   
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
 如需詳細資訊和範例，請參閱 <<c0> [ 命令提示字元安裝的 Reporting Services SharePoint 模式和原生模式](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md)和[從命令提示字元安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解 Reporting Services 安裝](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [僅限檔案安裝 &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
 [初始化報表伺服器 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [在原生模式報表伺服器上設定 SSL 連接](../security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server 2014 快速入門安裝](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
