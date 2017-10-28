---
title: "連接到 Management Studio 中的報表伺服器 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttors.connectionproperties.f1
- sql13.swb.connecttors.login.f1
- sql13.swb.connection.login.reportserver.f1
helpviewer_keywords:
- report servers [Reporting Services], connections
- connections [Reporting Services], report server
- registering report servers
- report servers [Reporting Services], registering
- Connect to Server dialog box, Reporting Services
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 0bc7925f72d59170a24f4a82d1c1a73e618a97a0
ms.openlocfilehash: f59854e37e292d03cf7d57443e3aa4b899a21a11
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="connect-to-a-report-server-in-management-studio"></a>連接至 Management Studio 中的報表伺服器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 提供物件總管，可讓您連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系列中的任何伺服器並以圖形方式瀏覽其內容。 若為 Reporting Services，您可以使用 [物件總管] 來進行下列作業：  
  
-   啟用報表伺服器功能。  
  
-   設定伺服器預設值並設定角色定義。  
  
-   管理正在執行的作業。  
  
-   管理作業排程。  
  
 您可以連接至原生模式報表伺服器或以 SharePoint 整合模式執行的報表伺服器。 連接語法以及您可以執行的作業類型會因報表伺服器的伺服器模式和您的權限而不同。 如果您無法連接至報表伺服器或執行特定工作，可能是您沒有足夠的權限，或是指定的報表伺服器名稱不正確。 如需有關權限和連接語法的詳細資訊，請參閱本主題結尾的表格。  
  
 請注意，您無法使用 [物件總管] 來檢視或管理報表伺服器內容。 內容管理是透過報表管理員 (如果報表伺服器以原生模式執行的話) 或 SharePoint 網站 (如果報表伺服器以 SharePoint 整合模式執行的話) 執行的。  
  
 [物件總管] 可讓您在同一個工作空間內開啟多個伺服器執行個體的連接，只要這些伺服器都在相同的伺服器群組中註冊即可。 您必須先註冊報表伺服器，然後才能在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中連接至該伺服器。 如果報表伺服器已經註冊，您就可以略過此步驟。 本主題的結尾會提供註冊報表伺服器的指示。  
  
### <a name="to-connect-to-a-native-mode-report-server"></a>連接至原生模式報表伺服器  
  
1.  如果 [物件總管] 尚未開啟，請在 [檢視] 功能表中選取它。  
  
2.  按一下**連接**來檢視伺服器類型的清單，然後選取**Reporting Services**。  
  
3.  在**連接到伺服器**對話方塊方塊中，輸入報表伺服器執行個體的名稱。 報表伺服器執行個體名稱以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱為基礎。 根據預設，本機報表伺服器執行個體的執行個體名稱就是電腦名稱。 如果您將報表伺服器安裝成具名執行個體時，使用此語法來指定伺服器： *\<伺服器名稱 > [\\< instancename\>]*。  
  
4.  選取驗證類型。 如果您要使用 Windows 驗證，就必須使用您的認證進行連接。 如果您選取了 [基本驗證] 或 [表單驗證]，請輸入帳戶和密碼。  
  
5.  按一下 **[連接]**。 報表伺服器就會出現在 [物件總管] 中。  
  
6.  以滑鼠右鍵按一下伺服器節點，設定伺服器屬性和伺服器預設值。 如需詳細資訊，請參閱[設定報表伺服器屬性 &#40;Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### <a name="to-connect-to-a-sharepoint-integrated-mode-report-server"></a>連接至 SharePoint 整合模式報表伺服器  
  
1.  如果 [物件總管] 尚未開啟，請在 [檢視] 功能表中選取它。  
  
2.  按一下 [連接到檢視的伺服器類型] 清單，然後選取**Reporting Services**。  
  
3.  在 [連接到伺服器] 對話方塊中，輸入 SharePoint 網站的 URL。 下列範例說明語法： `http://<web server>/sites/<site>`。  
  
4.  選取驗證類型。 如果您要使用 Windows 驗證，就必須使用您的認證進行連接。 如果您選取了 [基本驗證] 或 [表單驗證]，請輸入帳戶和密碼。  
  
5.  按一下 **[連接]**。 報表伺服器就會出現在 [物件總管] 中。  
  
6.  以滑鼠右鍵按一下伺服器節點，設定伺服器屬性和伺服器預設值。 如需詳細資訊，請參閱[設定報表伺服器屬性 &#40;Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### <a name="to-register-a-report-server"></a>若要註冊報表伺服器  
  
1.  如果您無法連接至報表伺服器，就表示您沒有存取伺服器的權限或者必須註冊伺服器。 若要註冊的伺服器，請按一下**已註冊的伺服器**檢視 功能表上  
  
2.  按一下 [Reporting Services] 圖示。  
  
3.  以滑鼠右鍵按一下**Reporting Services**，指向 **新增**，然後按一下 **伺服器註冊**。 **新增伺服器註冊**對話方塊隨即出現。  
  
4.  如**伺服器名稱**，輸入的值。 您必須指定的值會因伺服器模式而不同：  
  
    -   若為原生模式報表伺服器，請輸入報表伺服器執行個體的名稱。 報表伺服器執行個體名稱以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱為基礎。 根據預設，本機報表伺服器執行個體的執行個體名稱就是電腦名稱。 如果您將報表伺服器安裝成具名執行個體時，使用此語法來指定伺服器： *\<伺服器名稱 > [\\< instancename\>]*。  
  
    -   若為以 SharePoint 整合模式執行的報表伺服器，要連接的伺服器就是與報表伺服器連接的 SharePoint 網站。 連接至 SharePoint 網站是必要的，如此您才能夠檢視控制報表伺服器內容和作業之存取權的權限等級。 您可以在網站集合中指定任何網站。 下列範例說明語法： `http://mysharepointsite`。  
  
5.  對於 [驗證]，請選取要用於存取 Web 伺服器的驗證模式。 您必須選擇報表伺服器正在使用的驗證模式。  
  
    -   如果您使用預設的安全性，請選擇**Windows 驗證**。  
  
    -   如果您安裝並部署了自訂安全性延伸模組時，選擇**表單驗證**。  
  
    -   如果您將報表伺服器設定為使用基本驗證，請選擇**基本驗證**。  
  
    -   如果報表伺服器設定為 SharePoint 整合模式中，選擇  **Windows 驗證**。  
  
6.  按一下**測試**驗證的連線。  
  
7.  出現提示時，按一下**確定**，然後按一下 **儲存**。  
  
## <a name="connection-syntax-and-permissions"></a>連接語法和權限  
 下表將摘要列出執行特定作業所需的連接語法、作業和權限。  
  
 當您指定[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的伺服器類型為**連接到伺服器**對話方塊中，您可以指定報表伺服器名稱或 Web 服務的端點。  
  
|連接至|工作|Permissions|  
|----------------|-----------|-----------------|  
|原生模式報表伺服器 (當做預設或具名執行個體連接)：<br /><br /> \<伺服器名稱 >\<_ 執行個體 ><br /><br /> 報表伺服器的連接是透過報表伺服器 WMI 提供者建立的。|檢視和設定伺服器屬性與預設值。<br /><br /> 檢視和取消作業。<br /><br /> 建立和管理共用排程。<br /><br /> 建立、修改或刪除角色定義。|指派給系統管理員角色。|  
|原生模式報表伺服器 (透過報表伺服器 Web 服務的端點，當做預設或具名執行個體連接)：<br /><br /> `http://<servername>/reportserver`<br /><br /> 指定報表伺服器的 URL 會提供連接至報表伺服器的替代方式。|檢視和設定伺服器屬性與預設值。<br /><br /> 檢視和取消作業。<br /><br /> 建立和管理共用排程。<br /><br /> 建立、修改或刪除角色定義。|指派給系統管理員角色。|  
|SharePoint 整合模式報表伺服器 (透過 SharePoint 網站連接)：<br /><br /> `http://<webserver>/<SharePointSite>`|檢視和設定伺服器屬性與預設值。<br /><br /> 檢視和取消作業。<br /><br /> 建立和管理針對您所連接之網站定義的共用排程。<br /><br /> 檢視針對您所連接之網站定義的權限等級。|您所連接之 SharePoint 網站的完整控制權限等級。|  
|SharePoint 整合模式報表伺服器 (透過報表伺服器執行個體的名稱連接)：<br /><br /> \<伺服器名稱 >\<_ 執行個體 >|檢視和設定伺服器屬性與預設值。<br /><br /> 檢視和取消作業。|與報表伺服器整合之 SharePoint 網站的完整控制權限等級。<br /><br /> 請注意，當您連接至報表伺服器而非 SharePoint 網站時，您可以執行的工作數目會大幅減少。 這是因為報表伺服器只能傳回在報表伺服器資料庫 (而非 SharePoint 組態和內容資料庫) 中儲存或管理的應用程式資料。|  
  
## <a name="see-also"></a>請參閱＜  
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [在 SQL Server Management Studio &#40; reporting ServicesSSRS &#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  

