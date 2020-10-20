---
title: 在受控實例上裝載資料庫
description: 瞭解如何建立並設定 Master Data Services (MDS) 資料庫，並將其裝載于 Azure SQL 受控執行個體上。
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 671ae0d9578c81d56c3324f73a4240152594dd49
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194430"
---
# <a name="host-an-mds-database-on-a-managed-instance"></a>在受控實例上裝載 MDS 資料庫

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  本文涵蓋如何在受控實例上設定 Master Data Services (MDS) 資料庫。
  
## <a name="preparation"></a>準備

若要準備，您必須建立並設定 Azure SQL 受控執行個體，並設定您的 web 應用程式電腦。

### <a name="create-and-configure-the-database"></a>建立和設定資料庫

1. 使用虛擬網路建立受控實例。 請參閱 [快速入門：建立 SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance-get-started) 以取得詳細資料。

1. 設定點對站連線。 如需相關指示，請參閱 [使用原生 Azure 憑證驗證設定 VNet 的點對站連線： Azure 入口網站](/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 。

1. 設定 SQL 受控執行個體的 Azure Active Directory 驗證。 如需詳細資訊，請參閱 [設定及管理 SQL 的 Azure Active Directory 驗證](/azure/sql-database/sql-database-aad-authentication-configure) 。

### <a name="configure-web-application-machine"></a>設定 web 應用程式電腦

1. 安裝點對站連線憑證和 VPN，以確保機器可以存取受控實例。 如需相關指示，請參閱 [使用原生 Azure 憑證驗證設定 VNet 的點對站連線： Azure 入口網站](/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 。

1. 安裝下列角色和功能：
   - 角色：
     - Internet Information Services
     - Web 管理工具
     - IIS 管理主控台
     - World Wide Web 服務
     - 應用程式開發
     - .NET 擴充性 3.5
     - .NET 擴充性 4.5
     - ASP.NET 3.5
     - ASP.NET 4.5
     - ISAPI 擴充功能
     - ISAPI 篩選
     - 一般 HTTP 功能
     - 預設文件
     - 目錄瀏覽
     - HTTP 錯誤
     - 靜態內容
     - 健康情況及診斷
     - HTTP 記錄
     - 要求監視器
     - 效能
     - 靜態內容壓縮
     - 安全性
     - 要求篩選
     - Windows 驗證
       > [!NOTE]
       > 不要安裝 WebDAV 發行

   - 功能：
     - .NET Framework 3.5 (包括 .NET 2.0 和 3.0)
     - .NET Framework 4.5 進階服務
     - ASP.NET 4.5
     - WCF Services
     - HTTP 啟用 (必要) 
     - TCP 連接埠共用
     - Windows 處理序啟用服務
     - 處理序模型
     - .NET 環境
     - 設定 API
     - 動態內容壓縮

## <a name="install-and-configure-an-mds-web-application"></a>安裝和設定 MDS web 應用程式

接下來，您要安裝和設定 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 。

### <a name="install-sql-server-2019"></a>安裝 SQL Server 2019

您可以使用 SQL Server 安裝程式安裝精靈或命令提示字元來安裝 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 。

1. 開啟 `Setup.exe` ，並遵循安裝精靈中的步驟。

2. 在 [功能選擇]**** 頁面中，選取 [共用功能]**** 底下的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]。
此動作會安裝：
   - [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]
   - 組件
   - Windows PowerShell 嵌入式管理單元
   - Web 應用程式和服務的資料夾和檔案。

   ![mds-SQLServer2019-Config-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "mds-SQLServer2019-Config-MI_SQLFeatureSelection")  

### <a name="set-up-the-database-and-website"></a>設定資料庫和網站

1. 連接 Azure 虛擬網路，以確保您可以連線到受控實例。

   ![mds-SQLServer2019-Config-MI-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "mds-SQLServer2019-Config-MI_P2SVPNConnect")

1. 開啟 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ，然後選取左窗格中的 [ **資料庫** 設定]。

1. 選取 [ **建立資料庫** ] 以開啟 [ **建立資料庫]**。 選取 [下一步] 。

1. 在 [ **資料庫伺服器** ] 頁面上，完成 [ **SQL Server 實例** ] 欄位，然後選擇 [ **驗證類型**]。 選取 [ **測試連接** ] 以確認您可以使用您的認證，透過所選的驗證類型連線到資料庫。 選取 [下一步] 。

   > [!NOTE]
   > - SQL Server 實例看起來會像這樣 `xxxxxxx.xxxxxxx.database.windows.net` 。
   > - 針對受控實例，請選擇 [ **SQL Server 帳戶]** 和 [ **目前使用者-Active Directory 整合式]** 驗證類型。
   > - 如果您選取 [ **目前使用者-Active Directory 整合** 為驗證類型，[ **使用者名稱** ] 欄位會是唯讀的，並顯示目前已登入的 Windows 使用者帳戶。 如果您是 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 在 Azure 虛擬機器上執行 SQL Server 2019 (vm) ，[ **使用者名稱** ] 欄位會顯示 vm 的 vm 名稱，以及 vm 上本機系統管理員帳戶的使用者名稱。

   您的驗證必須包含受控實例的「 **系統管理員** 」規則。

   ![mds-SQLServer2019-Config-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "mds-SQLServer2019-Config-MI_CreateDBConnect")  

1. 在 [資料庫名稱]**** 欄位中輸入名稱。 （選擇性）若要選取 Windows 定序，請清除 [ **SQL Server 預設定序]** 核取方塊，然後選取一或多個可用的選項。 例如，區分 **大小寫**。 選取 [下一步] 。

   ![mds-SQLServer2019-Config-MI-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "mds-SQLServer2019-Config-MI_CreatedDBName")

1. 在 [ **使用者名稱** ] 欄位中，指定預設超級使用者的 Windows 帳戶 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 。 超級使用者可以存取所有功能區域，而且可以新增、刪除及更新所有模型。

   ![mds-SQLServer2019-Config-MI-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "mds-SQLServer2019-Config-MI_createDBUserName")

1. 選取 [ **下一步]** 以查看資料庫設定的摘要 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 。 再次選取  **[下一步]** 以建立資料庫。 您將會看到 [ **進度] 和 [完成]** 頁面。

1. 建立並設定資料庫之後，請選取 **[完成]**。

   如需有關 [ **建立資料庫嚮導]** 中設定的詳細資訊，請參閱 [建立資料庫嚮導 &#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)。

1. 在的 [ **資料庫** 設定] 頁面上 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ，選擇 [ **選取資料庫**]。

1. 選取 [ **連接]**，選擇 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 資料庫，然後選取 **[確定]**。

   ![mds-SQLServer2019-Config-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-Config-MI_connectDBName")

1. 在中 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ，選取左窗格中的 [ **Web** 設定]。

1. 在 [ **網站** ] 清單方塊中，選擇 [ **預設的網站**]，然後選取 [ **建立** ] 以建立 Web 應用程式。

   ![mds-SQLServer2019-Config-MI-WebConfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "mds-SQLServer2019-Config-MI_WebConfiguration")

   > [!NOTE]
   > 如果您選取 [ **預設**的網站]，就必須另外建立 web 應用程式。 如果您在清單方塊中選擇 [ **建立新網站** ]，則會自動建立應用程式。

1. 在 [ **應用程式集** 區] 區段中，輸入不同的使用者名稱，輸入密碼，然後選取 **[確定]**。

   ![mds-SQLServer2019-Config-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "mds-SQLServer2019-Config-MI_CreateWebApplication")

   > [!NOTE]
   > 請確定使用者可以使用您最近建立的 Active Directory 整合式驗證來存取資料庫。 或者，您可以在稍後變更連接 `web.config` 。

   如需 [ **建立 Web 應用程式** ] 對話方塊的詳細資訊，請參閱 [&#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;的 [建立 web 應用程式] ](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)對話方塊。

1. 在 [web**應用程式**] 視窗的 [ **web**設定] 窗格中，選取您已建立的應用程式，然後選擇 [**將應用程式與資料庫建立關聯**] 區段中的 [**選取**]。

1. 選取 [ **連接]** ，然後選擇 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 您要與 web 應用程式產生關聯的資料庫。 選取 [確定]  。

   您已完成網站的設定。 [ **Web** 設定] 頁面現在會顯示您所選取的網站、您建立的 Web 應用程式，以及 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 與應用程式相關聯的資料庫。

   ![mds-SQLServer2019-Config-MI-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "mds-SQLServer2019-Config-MI_WebConfigSelectDB")

1. 選取 [套用]。 您會看到設定 **完成** 訊息。 在訊息方塊中選取 **[確定]** ，以啟動 web 應用程式。 網址為 `http://server name/web application/` 。

## <a name="configure-authentication"></a>設定驗證

若要將受控實例資料庫連接至 web 應用程式，您需要變更其他驗證類型。

尋找 `web.config` 下的檔案 `C:\Program Files\Microsoft SQL Server\150\Master Data Services\WebApplication` 。 修改 connectionString 以變更其他驗證類型以連接到受控實例資料庫。

預設驗證類型 `Active Directory Integrated` 如下列範例連接字串所示：

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
   ```

MDS 也支援 Active Directory 密碼驗證和 SQL Server 驗證，如下列範例連接字串所示：

- Active Directory 密碼驗證

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
   ```

- SQL Server 驗證

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
   ```

## <a name="upgrade-ssmdsshort_md-and-sql-database-version"></a>升級 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 和 SQL Database 版本

### <a name="upgrade-ssmdsshort_md"></a>升級 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]

安裝 **SQL Server 2019 累積更新**。 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 將會自動更新。

### <a name="upgrade-sql-server"></a>升級 SQL Server

您可能會收到錯誤： `The client version is incompatible with the database version` 安裝 **SQL Server 2019 累積更新**之後。
![mds-SQLServer2019-Config-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "mds-SQLServer2019-Config-MI_UpgradeDBPage")

若要修正此問題，您需要升級資料庫版本：

1. 開啟 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ，然後選取左窗格中的 [  **資料庫** 設定]。

1. 在的 [ **資料庫** 設定] 頁面上 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ，選擇 [ **選取資料庫**]。

1. 選擇 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 您與 web 應用程式相關聯的資料庫。 選取 **[連接**]，然後選取 **[確定]**。

   ![mds-SQLServer2019-Config-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-Config-MI_ConnectDBName")

1. 選取 **升級資料庫 ...** .

   ![mds-SQLServer2019-Config-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "mds-SQLServer2019-Config-MI_SelectUpgradeDB")

1. 在 [升級資料庫] 嚮導的 [**歡迎使用**] 頁面上，選取 [**下一步]** ，然後在 [**升級審核**] 頁面

   ![mds-SQLServer2019-Config-MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "mds-SQLServer2019-Config-MI_UpgradeDBWizard")

1. 當所有工作都完成之後，請選取 **[完成]** 。

## <a name="see-also"></a>另請參閱

- [Master Data Services 資料庫](../master-data-services/master-data-services-database.md)
- [主資料管理員 Web 應用程式](../master-data-services/master-data-manager-web-application.md)
- [資料庫組態頁面 &#40;Master Data Services 組態管理員&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)
- [Master Data Services &#40;MDS&#41; 的新功能](../master-data-services/what-s-new-in-master-data-services-mds.md)