---
title: 建立原生模式報表伺服器資料庫 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- databases [Reporting Services], creating
ms.assetid: 81b9f4ad-800b-4688-8b47-a5a83dc8ff10
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8ff6878b05138bb1ad4c23e57699dd896ab7b441
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198820"
---
# <a name="create-a-native-mode-report-server-database--ssrs-configuration-manager"></a>建立原生模式報表伺服器資料庫 (SSRS 組態管理員)
  原生模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫進行內部儲存。 資料庫是必要元件，它是用來儲存已發行的報表、模型、共用資料來源、工作階段資料、資源和伺服器中繼資料。  
  
 若要建立報表伺服器資料庫或是變更連接字串或認證，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員中 [資料庫] 頁面上的選項。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="when-to-create-or-configure-the-report-server-databases"></a>何時建立或設定報表伺服器資料庫  
 如果您在僅限檔案模式中安裝了報表伺服器，您就必須建立及設定報表伺服器資料庫。  
  
 如果您已安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]預設組態中的原生模式，報表伺服器資料庫建立和安裝報表伺服器執行個體時自動設定。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來檢視或修改安裝程式為您進行的設定。  
  
##  <a name="rsdbrequirements"></a> 開始之前  
 建立或設定報表伺服器資料庫是多重步驟的程序。 在您建立報表伺服器資料庫之前，請考慮您要如何指定以下項目：  
  
 選取資料庫伺服器  
 檢閱支援的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本，以及[建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md) 主題中受支援的版本。  
  
 啟用 TCP/IP 連接  
 針對 [!INCLUDE[ssDE](../../includes/ssde-md.md)]啟用 TCP/IP 連接。 某些版本的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 依預設並不會啟用 TCP/IP。 本主題將提供指示。  
  
 為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開啟通訊埠  
 對遠端伺服器而言，如果您正在使用防火牆軟體，您必須開啟 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽的通訊埠。  
  
 決定報表伺服器認證  
 決定報表伺服器將如何連接到報表伺服器資料庫。 認證類型包括網域使用者帳戶、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者帳戶或報表伺服器服務帳戶。  
  
 這些認證會加密並儲存於 RSReportServer.config 檔案中。 報表伺服器會將這些認證用於對報表伺服器資料庫的進行中連接。 如果您想要使用 Windows 使用者帳戶或資料庫使用者帳戶，請務必指定已經存在的帳戶。 雖然 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員將會建立登入並設定必要的權限，但是它不會為您建立帳戶。 如需詳細資訊，請參閱[設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 決定報表伺服器語言  
 選擇要為報表伺服器指定的語言。 當使用者使用不同語言版本的瀏覽器連接到伺服器時，預先定義的角色名稱、描述和 [我的報表] 資料夾並不會以不同的語言顯示。  
  
 檢查認證來建立並提供資料庫  
 確認您的帳戶認證有權在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上建立資料庫。 這些認證會用於單次連接，以建立報表伺服器資料庫和 **RSExecRole**。 如果登入尚未存在，將會針對報表伺服器所使用的帳戶來建立資料庫使用者登入，以連接到資料庫。 您可以在登入所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶之下連接，或者也可以輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。  
  
### <a name="to-enable-access-to-a-remote-report-server-database"></a>啟用對遠端報表伺服器資料庫的存取  
  
1.  如果您正在使用遠端 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，請登入資料庫伺服器，以確認或啟用 TCP/IP 連接。  
  
2.  依序指向 **[開始]**、 **[所有程式]**、 **[Microsoft SQL Server]**、 **[組態工具]**，然後按一下 **[SQL Server 組態管理員]**。  
  
3.  開啟 **[SQL Server 網路組態]**。  
  
4.  選取執行個體。  
  
5.  以滑鼠右鍵按一下 **[TCP/IP]** ，然後按一下 **[已啟用]**。  
  
6.  重新啟動服務。  
  
7.  開啟防火牆軟體，並開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽的通訊埠。 如果是預設執行個體，這對於 TCP/IP 連接通常是通訊埠 1433。 如需詳細資訊，請參閱《 [線上叢書》的](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) 設定用於 Database Engine 存取的 Windows 防火牆 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="to-create-a-local-report-server-database"></a>若要建立本機報表伺服器資料庫  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並連接到您正在建立資料庫的報表伺服器執行個體。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在 [資料庫] 頁面上，按一下 **[變更資料庫]**。  
  
3.  按一下 **[建立新的報表伺服器資料庫]**，再按 **[下一步]**。  
  
4.  連接到將用來建立及主控報表伺服器資料庫的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體：  
  
    1.  輸入您想要使用的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。 此精靈將會顯示本機 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，它會當做預設執行個體 (如果有的話) 來執行。 否則，您必須輸入要使用的伺服器和執行個體。 具名執行個體會依照以下格式來指定：\<伺服器名稱>\\<執行個體名稱\>。  
  
    2.  輸入用於與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之單次連接的認證，以便建立報表伺服器資料庫。 如需有關如何使用這些認證的詳細資訊，請參閱本主題的「 [在開始之前](#rsdbrequirements) 」。  
  
    3.  按一下 **[測試連接]** 可驗證與伺服器的連接。  
  
    4.  按 [下一步] 。  
  
5.  指定用來建立資料庫的屬性。 如需有關如何使用這些屬性的詳細資訊，請參閱本主題的「 [在開始之前](#rsdbrequirements) 」。  
  
    1.  輸入報表伺服器資料庫的名稱。 會伴隨主要資料庫，建立一個暫存資料庫。 請考慮使用描述性名稱來協助您記住資料庫的使用方式。 請注意，您所指定的名稱將會在資料庫的存留期間使用。 當您建立報表伺服器資料庫之後，就無法重新命名了。  
  
    2.  選取您希望角色定義和 [我的報表] 所顯示的語言。  
  
    3.  報表伺服器模式一律設定為 **[原生]**。  
  
    4.  按 [下一步] 。  
  
6.  指定報表伺服器用來連接到報表伺服器資料庫的認證。  
  
    1.  指定驗證類型：  
  
         使用已經定義的 **資料庫登入，選取要連接的** [資料庫認證] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果報表伺服器位於不同網域、非信任網域或防火牆後面的電腦上，則建議使用資料庫認證。  
  
         如果您具有最低權限的網域使用者帳戶，而該帳戶具有登入電腦和資料庫伺服器的權限，請選取 **[Windows 認證]** 。  
  
         如果您希望報表伺服器使用它的服務帳戶進行連接，請選取 **[服務認證]** 。 有了這個選項，伺服器就會使用整合式安全性來進行連接；認證並不會加密或儲存起來。  
  
    2.  按 [下一步] 。  
  
7.  檢閱 [摘要] 頁面上的資訊，以確認設定都正確無誤，然後按 **[下一步]**。  
  
8.  按一下報表伺服器 URL 頁面或報表管理員 URL 頁面上的 URL 來確認連接。 必須有定義 URL，這項測試才有效。 如果報表伺服器資料庫連接有效，您將會在瀏覽器視窗中看到報表伺服器資料夾階層或報表管理員。 如需詳細資訊，請參閱 < [Verify a Reporting Services Installation](verify-a-reporting-services-installation.md)在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器資料庫連接&#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [資料庫&#40;SSRS 原生模式&#41;](../../sql-server/install/database-ssrs-native-mode.md)   
 [管理 Reporting Services 原生模式報表伺服器](../report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
