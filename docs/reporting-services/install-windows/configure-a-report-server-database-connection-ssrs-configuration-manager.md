---
title: "設定報表伺服器資料庫連線 (SSRS 設定管理員) | Microsoft Docs"
ms.custom: 
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: 8339048088fd686b2b9065cad760179229901d9f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="configure-a-report-server-database-connection--ssrs-configuration-manager"></a>設定報表伺服器資料庫連接 (SSRS 組態管理員)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

每個報表伺服器執行個體都必須連接至儲存伺服器所管理之報表、報表模型、共用資料來源、資源和中繼資料的報表伺服器資料庫。 如果您要安裝預設組態，您可以在報表伺服器安裝期間建立初始連接。 在大部分的情況下，您將利用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，在安裝程式完成之後設定連接。 您可以隨時修改連接，以變更帳戶類型或重設認證。 如需如何建立資料庫及設定連線的逐步指示，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。

 您必須在下列情況下設定報表伺服器資料庫連接：  
  
-   設定報表伺服器以供第一次使用。  
  
-   設定報表伺服器來使用其他的報表伺服器資料庫。  
  
-   變更用於資料庫連接的使用者帳戶或密碼。 帳戶資訊若是儲存在 RSReportServer.config 檔案中，您只需要更新資料庫連接。 如果您是使用服務帳戶進行連接 (這會使用 Windows 整合式安全性做為認證類型)，則不會儲存密碼，因此不必更新連接資訊。 如需變更帳戶的詳細資訊，請參閱 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
-   設定報表伺服器向外延展部署。 若要設定向外延展部署，您必須建立到報表伺服器資料庫的多個連接。 如需如何執行此多步驟作業的詳細資訊，請參閱[設定原生模式報表伺服器向外延展部署 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
## <a name="how-reporting-services-connects-to-the-database-engine"></a>Reporting Services 如何連接到 Database Engine  
 報表伺服器對報表伺服器資料庫的存取會視認證與連接資訊，以及針對使用該資料庫之報表伺服器執行個體有效的加密金鑰而定。 必須要有有效的加密金鑰，才能儲存和擷取機密資料。 當您第一次設定資料庫時，會自動建立加密金鑰。 建立金鑰之後，如果您變更報表伺服器服務識別，則必須更新金鑰。 如需使用加密金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。  
  
 報表伺服器資料庫為內部元件，只能由報表伺服器存取。 您為報表伺服器資料庫指定的認證和連接資訊是報表伺服器所專用。 要求報表的使用者不需要資料庫權限或是報表伺服器資料庫的資料庫登入。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用 **System.Data.SqlClient** 連接到主控報表伺服器資料庫的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 如果您要使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的本機執行個體，報表伺服器將會使用共用記憶體建立連接。 如果您要使用報表伺服器資料庫的遠端資料庫伺服器，您可能必須根據您使用的版本來啟用遠端連接。 如果您正在使用 Enterprise Edition，預設會啟用 TCP/IP 的遠端連接。  
  
 若要確認此執行個體可接受遠端連線，請依序按一下 [開始]、[所有程式]、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 [組態工具]，再按一下 [SQL Server 組態管理員]，然後確認每一個服務都已啟用 TCP/IP 通訊協定。  
  
 當您啟用遠端連接時，也會啟用用戶端和伺服器通訊協定。 若要確認通訊協定已啟用，請依序按一下 **[開始]**、 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[組態工具]**、 **[SQL Server 組態管理員]**、 **[SQL Server 網路組態]**，再按一下 **[MSSQLSERVER 的通訊協定]**。 如需詳細資訊，請參閱《 [線上叢書》中的](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) 啟用或停用伺服器網路通訊協定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="defining-a-report-server-database-connection"></a>定義報表伺服器資料庫連接  
 若要設定連接，您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員或 **rsconfig** 命令列公用程式。 報表伺服器需要下列連接資訊：  
  
-   主控報表伺服器資料庫之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的名稱。  
  
-   報表伺服器資料庫的名稱。 第一次建立連接時，您可以建立新的報表伺服器資料庫或選取現有的資料庫。 如需詳細資訊，請參閱《 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)。  
  
-   認證類型。 您可以使用服務帳戶、Windows 網域帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。  
  
-   使用者名稱和密碼 (只有使用 Windows 網域帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入時才需要)。  
  
 您提供的認證必須被授與對報表伺服器資料庫的存取權。 如果您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，會自動執行此步驟。 如需有關存取資料庫所需權限的詳細資訊，請參閱此主題中的＜資料庫權限＞一節。  
  
### <a name="storing-database-connection-information"></a>儲存資料庫連接資訊  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會儲存及加密下列 RSreportserver.config 設定中的連接資訊。 您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具或 rsconfig 公用程式來建立這些設定的加密值。  
  
 不過，並不是每種連接類型都需要設定所有的值， 如果您利用預設值設定連線 (也就是利用服務帳戶來進行連線)，則 \<**LogonUser**>、\<**LogonDomain**> 和 \<**LogonCred**> 將是空的，如下所示：  
  
```  
<Dsn></Dsn>  
<ConnectionType></ConnectionType>  
<LogonUser></LogonUser>  
<LogonDomain></LogonDomain>  
<LogonCred></LogonCred>  
```  
  
 當您設定連接來使用特定的 Windows 帳戶或資料庫登入時，如果您後續又變更該帳戶或登入，請務必記得更新所儲存的值。  
  
### <a name="choosing-a-credential-type"></a>選擇認證類型  
 在報表伺服器資料庫的連接中，您可以使用三種認證類型：  
  
-   使用報表伺服器服務帳戶的 Windows 整合式安全性。 由於報表伺服器會實作為單一服務，所以只有用來執行此服務的帳戶才需要資料庫存取權。  
  
-   Windows 使用者帳戶。 如果報表伺服器和報表伺服器資料庫安裝在相同電腦上，您可以使用本機帳戶。 否則，您必須使用網域帳戶。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
> [!NOTE]  
>  自訂驗證延伸模組不能用來連接到報表伺服器資料庫。 自訂驗證延伸模組只能用於驗證報表伺服器的主體。 它們對於報表伺服器資料庫的連接，或者提供報表內容之外部資料來源的連接，不會有任何影響。  
  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體設定為 Windows 驗證，而且與報表伺服器電腦位於相同的網域或信任網域中，您可以設定此連接使用透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來當做連接屬性管理的服務帳戶或網域使用者帳戶。 如果資料庫伺服器位於不同的網域，或者您使用的是工作群組安全性，您就必須設定此連接使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。 在此情況下，請務必為此連接加密。  
  
##### <a name="using-service-accounts-and-integrated-security"></a>使用服務帳戶和整合式安全性  
 您可以使用 Windows 整合式安全性，以透過報表伺服器服務帳戶進行連接。 此帳戶會被授與報表伺服器資料庫的登入權限。 如果您以預設的組態安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，這是安裝程式選擇的預設認證類型。  
  
 此服務帳戶是信任帳戶，可提供管理報表伺服器資料庫連接的低維護方法。 由於此服務帳戶會使用 Windows 整合式安全性進行連接，因此不需要儲存認證。 但是，如果您接著變更服務帳戶密碼或識別 (例如，從內建帳戶切換到網域帳戶)，請務必使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具進行變更。 此工具會自動更新資料庫權限，以使用修訂過的帳戶資訊。 如需詳細資訊，請參閱《 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
 如果將資料庫連接設定為使用此服務帳戶，則當報表伺服器資料庫位於遠端電腦上時，該帳戶必須具有網路權限。 如果報表伺服器資料庫位於不同的網域、在防火牆後面，或者您使用的是工作群組安全性而非網域安全性，則請勿使用服務帳戶。 您應該改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者帳戶。  
  
##### <a name="using-a-domain-user-account"></a>使用網域使用者帳戶  
 您可以針對與報表伺服器資料庫的報表伺服器連接指定 Windows 使用者帳戶。 如果您使用本機或網域帳戶，則每當您變更密碼或帳戶時，您必須更新報表伺服器資料庫連接。 請一定要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來更新此連接。  
  
##### <a name="using-a-sql-server-login"></a>使用 SQL Server 登入  
 您可以指定單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，以連接到報表伺服器資料庫。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，而報表伺服器資料庫位於遠端電腦上，請利用 IPSec 來保護伺服器之間資料傳輸的安全。 如果您使用資料庫登入，則每當您變更密碼或帳戶時，您必須更新報表伺服器資料庫連接。  
  
### <a name="database-permissions"></a>資料庫權限  
 用來連接到報表伺服器資料庫的帳戶被授與下列角色：  
  
-   **ReportServer** 資料庫的 **public** 和 **RSExecRole** 角色。  
  
-   **master** 、 **msdb**和 **ReportServerTempDB**資料庫的 **RSExecRole** 角色。  
  
 當您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具建立或修改此連接時，會自動授與這些權限。 如果您使用 rsconfig 公用程式，並且為連接指定不同的帳戶，則必須針對該新帳戶更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中，建立將會更新報表伺服器之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的指令碼檔案。  
  
### <a name="verifying-the-database-name"></a>確認資料庫名稱  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，以判斷特定報表伺服器執行個體使用了哪一個報表伺服器資料庫。 若要尋找名稱，請連接到報表伺服器執行個體，然後開啟 [資料庫安裝] 頁面。  
  
## <a name="using-a-different-report-server-database-or-moving-a-report-server-database"></a>使用不同的報表伺服器資料庫，或移動報表伺服器資料庫  
 您可以變更連接資訊，來設定報表伺服器執行個體使用不同的報表伺服器資料庫。 通常，需要切換資料庫的狀況會發生在部署實際報表伺服器的時候。 通常，實際伺服器首展的時候，就會從測試報表伺服器資料庫切換到實際報表伺服器資料庫。您也可以將報表伺服器資料庫移到另一部電腦。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) 升級和移轉 Reporting Services [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="configuring-multiple-reports-servers-to-use-the-same-report-server-database"></a>設定多個報表伺服器使用同一個報表伺服器資料庫  
 您可以設定多個報表伺服器，使用同一個報表伺服器資料庫。 這個部署組態稱為向外延展部署。 如果您想要在伺服器叢集中執行多部報表伺服器，此組態為必要條件。 但是，如果您想要分割服務應用程式，或是測試新報表伺服器執行個體的安裝和設定，將它與現有的報表伺服器安裝做比較，也可以使用這個組態。 如需詳細資訊，請參閱[設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  

## <a name="next-steps"></a>後續的步驟

[建立報表伺服器資料庫](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
[管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[設定報表伺服器服務帳戶](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
