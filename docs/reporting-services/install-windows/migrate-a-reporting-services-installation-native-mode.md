---
title: 移轉 Reporting Services 安裝 (原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- manual Reporting Services migrations
- Report Server Windows service
- custom Reporting Services installations
- automatic Reporting Services migrations
- Reporting Services, upgrades
- upgrading Reporting Services
- migrating Reporting Services
ms.assetid: a6fc56c1-c504-438d-a2b0-5ed29c24e7d6
caps.latest.revision: 54
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7a1104ea9d5e26731ad22be5ab0645d2e8773a08
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37975265"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>移轉 Reporting Services 安裝 (原生模式)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

本主題提供將下列其中一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式部署的支援版本移轉到新 SQL Server Reporting Services 執行個體的逐步指示：  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  

如需遷移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式部署的資訊，請參閱 [遷移 Reporting Services 安裝 &#40;SharePoint 模式&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)。  
  
 移轉的定義是將應用程式資料檔案移至新的 SQL Server 執行個體。 以下是您必須移轉安裝的常見原因：  
  
-   您有大規模的部署或執行時間需求。  
  
-   您要變更安裝的硬體或拓撲。  
  
-   您遇到封鎖升級的問題。

## <a name="bkmk_nativemode_migration_overview"></a> 原生模式移轉概觀

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的移轉程序包括手動和自動步驟。 下列工做為報表伺服器的部分移轉作業：  
  
-   備份資料庫、應用程式和組態檔。  
  
-   備份加密金鑰。  
  
-   安裝新的 SQL Server 執行個體。 如果您使用相同的硬體，只要是支援的版本，就可以將 SQL Server 與現有的安裝並存安裝。  
  
    > [!TIP]  
    >  並存安裝可能會要求您將 SQL Server 安裝為具名執行個體。  
  
-   將報表伺服器資料庫和其他應用程式檔案，從現有的安裝移至新的 SQL Server 安裝。  
  
-   將任何自訂應用程式檔案移至新的安裝。  
  
-   設定報表伺服器。  
  
-   編輯 **RSReportServer.config** 以便包含先前安裝的任何自訂設定。  
  
-   或者，請針對新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows 服務群組設定自訂的存取控制清單 (ACL)。  
  
-   當您確認新的執行個體可完全運作之後，請移除未使用的應用程式和工具。  
  
 裝載報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本有一些限制。 如果您重複使用先前安裝中所建立的報表伺服器資料庫，請檢閱下列主題。  
  
-   [建立報表伺服器資料庫](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
##  <a name="bkmk_fixed_database_name"></a> 固定資料庫名稱  
 您無法重新命名報表伺服器資料庫。 資料庫的識別會在建立資料庫時，記錄於報表伺服器預存程序中。 重新命名報表伺服器的主要或暫存資料庫將會在程序執行時造成錯誤發生，使得報表伺服器安裝失效。  
  
 如果現有安裝的資料庫名稱不適用於新的安裝，您應該考慮建立新的資料庫並讓它使用此名稱，然後使用以下清單中的技術，載入現有的應用程式資料：  
  
-   撰寫呼叫報表伺服器 Web 服務 SOAP 方法的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 指令碼，以便在資料庫之間複製資料。 您可以使用 RS.exe 公用程式執行此指令碼。 如需這種方法的詳細資訊，請參閱 [指令碼與 PowerShell 搭配 Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)。  
  
-   撰寫可呼叫 WMI 提供者的程式碼，以便在資料庫之間複製資料。 如需這種方法的詳細資訊，請參閱 [存取 Reporting Services WMI 提供者](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)。  
  
-   如果您只有少量的項目，可以從報表設計師、模型設計師和報表產生器將報表、報表模型和共用資料來源重新發行到新的報表伺服器。 您必須重新建立角色指派、訂閱、共用排程、報表快照集排程、您在報表或其他項目上設定的自訂屬性、模型項目安全性，以及您在報表伺服器上設定的屬性。 您將會遺失報表記錄和報表執行記錄資料。  
  
##  <a name="bkmk_before_you_start"></a> 開始之前  
 即使您正在移轉而非升級安裝，請考慮在現有的安裝上執行 Upgrade Advisor，以便協助您識別可能會影響移轉的任何問題。 如果您正在移轉尚未安裝或設定的報表伺服器，這個步驟便特別有用。 透過執行升級建議程式，您可以找出新 SQL Server 安裝可能不支援的自訂設定。  
  
 此外，您應留意 SQL Server Reporting Services 中的數項重要變更，因為這些變更將會影響您移轉安裝的方式：
 
- 新的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 已取代報表管理員。
  
- 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始，IIS 不再是必要元件。 如果您要將報表伺服器安裝移轉至新的電腦，就不需要加入 Web 伺服器角色。 此外，設定 URL 和驗證的步驟與舊版有所不同，而且診斷和疑難排解問題的技巧與工具也不一樣。  
  
- 報表伺服器 Web 服務、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]和報表伺服器 Windows 服務執行時使用相同的帳戶。 這三個應用程式會從 RSReportServer.config 檔案讀取組態設定。 
  
- [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 和 SQL Server Management Studio 已設計成移除重複的功能。 每個工具都支援不同組的工作。
  
- [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本都不支援 ISAPI 篩選器。 如果您使用 ISAPI 篩選器，則必須在移轉之前重新設計報表方案。  
  
- [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本都不支援 IP 位址限制。 如果您使用 IP 位址限制，則必須在移轉之前重新設計報表方案，或使用防火牆、路由器或網路位址轉譯 (NAT) 之類的技術來設定受限不得存取報表伺服器的位址。  
  
- [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本都不支援用戶端安全通訊端層 (SSL) 憑證。 如果您使用用戶端 SSL 憑證，則必須在移轉之前重新設計報表方案。  
  
- 如果您使用 Windows 整合式驗證以外的驗證類型，則必須在 `<AuthenticationTypes>` RSReportServer.config **檔案中，以受支援的驗證類型更新** 元素。 受支援的驗證類型為 NTLM、Kerberos、Negotiate 和 Basic。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本都不支援匿名、.NET Passport 和摘要式驗證。  
  
- 如果您在報表環境中使用自訂的階層式樣式表，則這些樣式表不會移轉。 您必須以手動方式移動它們以進行遷移。  
  
如需 SQL Server Reporting Services 中變更的詳細資訊，請參閱升級建議程式文件和 [Reporting Services 的新功能](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。  

## <a name="bkmk_backup"></a> 備份檔案和資料

 安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的新執行個體之前，請務必備份目前安裝中的所有檔案。  
  
1.  備份報表伺服器資料庫的加密金鑰。 這個步驟對於移轉是否成功很重要。 之後在移轉程序中，您必須針對報表伺服器還原此金鑰，以便重新取得加密資料的存取權。 若要備份金鑰，請使用 Reporting Services 組態管理員。  
  
2.  使用備份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的任何支援方法來備份報表伺服器資料庫。 如需詳細資訊，請參閱[將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md) 中有關如何備份報表伺服器資料庫的指示。  
  
3.  備份報表伺服器組態檔。 要備份的檔案包括：  
  
    1.  RSReportServer.config  
  
    2.  Rswebapplication.config  
  
    3.  Rssvrpolicy.config  
  
    4.  Rsmgrpolicy.config  
  
    5.  Reportingservicesservice.exe.config  
  
    6.  報表伺服器 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式的 Web.config。  
  
    7.  [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 的 Machine.config (如果您針對報表伺服器作業修改過它的話)。  

## <a name="bkmk_install_ssrs"></a> 安裝 SQL Server Reporting Services

 在僅限檔案模式下，安裝新的報表伺服器執行個體，如此您就可以將它設定為使用非預設值。 若為命令列安裝，請使用 **FilesOnly** 引數。 在 [安裝精靈] 中，選取 [安裝但不設定] 選項。  
  
 按一下下列其中一個連結，即可檢視有關如何安裝新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]執行個體的指示：  
  
-   [從安裝精靈安裝 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  

## <a name="bkmk_move_database"></a> 移動報表伺服器資料庫

 報表伺服器資料庫包含已發行的報表、模型、共用資料來源、排程、資源、訂閱，以及資料夾。 此外，它也包含系統和項目屬性，以及存取報表伺服器內容的權限。  
  
 如果您的移轉包含使用不同的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，就必須將報表伺服器資料庫移至新的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 如果您使用的是相同的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，請跳至 [移動自訂組件或延伸模組](#bkmk_move_custom)一節。  
  
 若要移動報表伺服器資料庫，請執行下列動作：  
  
1.  選擇要使用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 SQL Server Reporting Services 需要您使用下列其中一個版本來裝載報表伺服器資料庫：  
  
    -   SQL Server 2016  
  
    -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    -   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
2.  啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
3.  如果 **從未主控過報表伺服器資料庫，請在系統資料庫中建立** RSExecRole [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 如需詳細資訊，請參閱 [建立 RSExecRole](../../reporting-services/security/create-the-rsexecrole.md)。  
  
4.  遵循[將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md) 中的指示。  
  
 請記住，報表伺服器資料庫和暫存資料庫彼此相依，而且必須一起移動。 請勿複製資料庫；複製並不會將所有的安全性設定傳送到新的安裝。 請勿針對排程的報表伺服器作業移動 SQL Server Agent 作業。 報表伺服器會自動重新建立這些作業。  

## <a name="bkmk_move_custom"></a> 移動自訂組件或延伸模組

 如果安裝包含自訂報表項目、組件或延伸模組，您就必須重新部署自訂元件。 如果您不要使用自訂元件，請跳至 [設定報表伺服器](#bkmk_configure_reportserver)。  
  
 若要重新部署自訂元件，請執行下列動作：  
  
1.  判斷組件是否受到支援或需要重新編譯：

    -  自訂安全性延伸模組必須使用 [IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx) 介面重新撰寫。
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的自訂轉譯延伸模組必須使用轉譯物件模型 (ROM) 重新撰寫。  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本都不支援 HTML 3.2 和 HTML OWC 轉譯器。  
  
    -   其他自訂組件應該不需要重新編譯。  
  
2.  將組件移至新的報表伺服器 \bin 資料夾。 在 SQL Server 中，報表伺服器二進位檔位於預設報表伺服器執行個體的下列位置：  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3.  修改組態檔，以便加入自訂元件的項目。 這些項目會因您所使用的組件類型而不同。 如需有關放置檔案和加入組態項目之位置的指示，請參閱下列主題：  
  
    1.  [部署自訂組件](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2.  [如何：部署自訂報表項目](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3.  [部署資料處理延伸模組](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4.  [部署傳遞延伸模組](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5.  [部署轉譯延伸模組](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6.  [實作安全性延伸模組](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="bkmk_configure_reportserver"></a> 設定報表伺服器

 設定報表伺服器 Web 服務和入口網站的 URL，然後設定報表伺服器資料庫的連線。  
  
 如果您正在移轉向外延展部署，請將所有的報表伺服器節點設為離線，然後一次移轉一個伺服器。 在移轉第一個報表伺服器且該伺服器成功連線至報表伺服器資料庫之後，報表伺服器資料庫的版本就會自動升級為 SQL Server 資料庫版本。  
  
> [!IMPORTANT]  
>  如果向外延展部署中有任何報表伺服器是在線上且尚未移轉，則這些伺服器可能會遭遇 rsInvalidReportServerDatabase 例外狀況，因為它們在連接至已升級版本時使用的是舊版的結構描述。  
  
> [!NOTE]  
>  如果您遷移的報表伺服器是設定為向外延展部署的共用資料庫，必須在設定報表伺服器服務之前，從 **ReportServer** 資料庫中的 **Keys** 資料表刪除所有舊的加密金鑰。 如果未移除金鑰，移轉後的報表伺服器會嘗試在向外延展部署模式中初始化。 如需詳細資訊，請參閱[新增和移除向外延展部署的加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) 和[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。  
>   
>  您無法利用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來刪除向外延展金鑰， 而是必須使用 SQL Server Management Studio，從 **ReportServer** 資料庫中的 **Keys** 資料表刪除舊金鑰。 請刪除 Keys 資料表中的所有資料列。 這麼做將會清除資料表，使其僅用於還原對稱金鑰，其步驟如下所示。  
>   
>  刪除金鑰之前，建議您先備份對稱加密金鑰。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來備份金鑰。 請開啟 [組態管理員]，然後按一下 [加密金鑰] 索引標籤，再按一下 [備份] 按鈕。 您也可以編寫 WMI 指令碼命令，備份加密金鑰。 如需 WMI 的詳細資訊，請參閱 [BackupEncryptionKey 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)。  
  
1.  啟動 Reporting Services 組態管理員，並連接到您剛才安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  設定報表伺服器和入口網站的 URL。 如需詳細資訊，請參閱[設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
3.  設定報表伺服器資料庫，並且從先前安裝中選取現有的報表伺服器資料庫。 在成功設定後，報表伺服器服務就會重新啟動，而在建立報表伺服器資料庫的連線之後，資料庫就會自動升級為 SQL Server Reporting Services。 如需如何執行您用來建立或選取報表伺服器資料庫之 [變更資料庫精靈] 的詳細資訊，請參閱[建立原生模式報表伺服器資料庫](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
4.  還原加密金鑰。 若要針對已經在報表伺服器資料庫中之預先存在的連接字串和認證啟用可回復加密，這個步驟就是必要的。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
5.  如果您在新的電腦上安裝報表伺服器，而且正在使用 Windows 防火牆，請確定報表伺服器所接聽的 TCP 通訊埠是開啟的。 此通訊埠依預設為 80。 如需詳細資訊，請參閱 [設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
6.  如果您想要在本機管理您的原生模式報表伺服器，則必須設定作業系統，允許透過入口網站進行本機管理。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  

## <a name="bkmk_copy_custom_config"></a> 將自訂組態設定複製到 RSReportServer.config 檔案

如果您在先前安裝中修改了 RSReportServer.config 檔案或 RSWebApplication.config 檔案，就應該在新的 RSReportServer.config 檔案中進行相同的修改。 下列清單將摘要列出一些您可能會修改先前組態檔的原因，並且提供有關如何在 SQL Server 2016 中設定相同設定的其他資訊連結。  
  
|自訂|[資訊]|  
|-------------------|-----------------|  
|含有自訂設定的報表伺服器電子郵件傳遞|[電子郵件設定 - Reporting Services 原生模式](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。|  
|裝置資訊設定|[在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="bkmk_windowsservice_group"></a> Windows 服務群組和安全性 ACL

 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 中有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows 服務群組這個服務群組，會用來為跟著 QL Server Reporting Services 安裝的所有登錄機碼、檔案和資料夾建立安全性 ACL。 這個 Windows 群組名稱會以格式 SQLServerReportServerUser$\<computer_name>$\<instance_name> 顯示。  

## <a name="bkmk_verify"></a> 驗證您的部署

1.  開啟瀏覽器並輸入 URL 位址，以測試報表伺服器和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 虛擬目錄。 如需詳細資訊，請參閱 [驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)。  
  
2.  測試報表，並確認其包含您預期的資料。 檢閱資料來源資訊，查看是否仍然有指定資料來源連接資訊。 雖然報表伺服器會在處理和轉譯報表時使用報表物件模型，但不會以新的報表定義語言元素取代 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 若要深入了解現有報表如何在新版報表伺服器上執行，請參閱[升級報表](../../reporting-services/install-windows/upgrade-reports.md)。  

## <a name="bkmk_remove_unused"></a> 移除未使用的程式和檔案

一旦將報表伺服器成功移轉至新執行個體，您就可以執行下列步驟，以移除不再需要的程式和檔案。  
  
1.  如果您不再需要舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，請解除安裝它。 這個步驟不會刪除下列項目，但如果您不再需要它們，可以用手動方式加以移除：  
  
    -   舊的報表伺服器資料庫  
  
    -   RsExec 角色  
  
    -   報表伺服器服務帳戶  
  
    -   報表伺服器 Web 服務的應用程式集區  
  
    -   報表管理員和報表伺服器的虛擬目錄  
  
    -   報表伺服器記錄檔案  
  
2.  如果您不再需這部電腦上的 IIS，請移除它。

## <a name="next-steps"></a>後續步驟

[移轉 Reporting Services 安裝](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)   
[報表伺服器資料庫](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Reporting Services 回溯相容性](../../reporting-services/reporting-services-backward-compatibility.md)   
[Reporting Services 組態管理員](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
