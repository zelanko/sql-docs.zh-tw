---
title: 受控實例上的主機資料庫 |Microsoft Docs
description: 描述如何在受控實例上設定 MDS 資料庫。
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
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b4ca791a1a0ce46929f4d409d234f8dbc7efdec3
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794905"
---
# <a name="host-database-on-managed-instance"></a>受控實例上的主機資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本文涵蓋如何設定受控實例上的 MDS 資料庫。
  
## <a name="preparation"></a>準備

我們需要完成準備中的下列步驟。
- 完成建立和設定的受控實例。 包含虛擬網路和點對站 VPN。
- 完成 web 應用程式電腦設定。
  - 包含安裝點對站 VPN。
  - 安裝角色和功能。

**資料庫端:**

1. 建立 Azure SQL Database 受控實例包含虛擬網路。 [入門建立 Azure SQL Database 受控實例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. 設定點對站連線。 [使用原生 Azure 憑證驗證設定 VNet 的點對站連線:Azure 入口網站](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. 使用 SQL Database 受控實例來設定 Azure Active Directory 驗證。 [使用 SQL 設定及管理 Azure Active Directory 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**Web 應用程式電腦端:**

1. 安裝點對站連線憑證和 VPN, 以確保電腦可以存取 SQL Database 受控實例。 [使用原生 Azure 憑證驗證設定 VNet 的點對站連線:Azure 入口網站](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. 安裝角色和功能。 需要下列功能。

- 角色

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- 特色：

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>安裝和設定[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web 應用程式

我們需要完成下列步驟, 才能安裝和[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]設定。

1. 安裝 SQL Server 2019 包含[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]功能。
2. 在管理實例上建立資料庫。[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]
3. 建立和設定的[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]web 應用程式。
  
**安裝 SQL Server 2019**

您可以使用 [SQL Server 安裝程式安裝精靈] 或命令提示[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]字元來安裝。

1. 按兩下 Setup.exe，並遵循安裝精靈中的步驟。

2. 選取[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] [共用功能] 底下的 [特徵選取] 頁面。
隨即安裝 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]、組件、Windows PowerShell 嵌入式管理單元，以及 Web 應用程式與服務的資料夾和檔案。

    ![mds-SQLServer2019-Config-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "mds-SQLServer2019-Config-MI_SQLFeatureSelection")  

**設定資料庫和網站**

1. 連接 Windows Azure 虛擬網路, 以確保您可以連接到受控實例。

    ![mds-SQLServer2019-Config-MI-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "mds-SQLServer2019-Config-MI_P2SVPNConnect")  

2. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]啟動。 然後按一下左窗格中的 [**資料庫**設定]。

3. 按一下 [**建立資料庫**], 然後按一下 [**建立資料庫**嚮導] 中的 [下一步]。

4. 在 [**資料庫伺服器**] 頁面上, 填入**SQL Server 實例**並選取**驗證類型**, 然後按一下 [**測試連接**], 確認您可以使用您所提供之驗證類型的認證來連接到資料庫。處於. 按 [下一步]。

   > [!NOTE]
   > - 受控實例的 SQL Server 實例, 例如 "xxxxxxx.xxxxxxx.database.windows.net"
   > - 針對受控實例, 我們支援「 **SQL Server 帳戶**」和「**目前使用者-Active Directory 整合**」驗證類型。
   > - 當您選取 [**目前使用者-Active Directory 整合**] 做為 [驗證類型] 時, [**使用者名稱**] 方塊會是唯讀的, 並顯示登入電腦的 Windows 使用者帳戶名稱。 如果您在 Azure 虛擬機器[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (VM) 上執行 SQL Server 2019, [**使用者名稱**] 方塊會顯示 vm 的 vm 名稱和本機系統管理員帳戶的使用者名稱。

    請確定您的驗證封裝含受控實例的「 **sysadmin** 」規則。
![mds-SQLServer2019-Config-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "mds-SQLServer2019-Config-MI_CreateDBConnect")  

5. 在 [資料庫名稱] 欄位中輸入名稱。 (選擇性) 若要選取 Windows 定序，請清除 [SQL Server 預設定序] 核取方塊，然後按一下一或多個可用選項 (例如 [區分大小寫])。 按一下 [下一步]。

    ![mds-SQLServer2019-Config-MI-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "mds-SQLServer2019-Config-MI_CreatedDBName")  

6. 在 [**使用者名稱**] 欄位中, 指定將成為預設超級使用者[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]之使用者的 Windows 帳戶。 進階使用者具有所有功能區域的存取權，並可新增、刪除及更新所有模型。

    ![mds-SQLServer2019-Config-MI-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "mds-SQLServer2019-Config-MI_createDBUserName")

7. 按一下 **「下一步」** 檢視 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 資料庫的設定摘要，然後按一下 **「下一步」** 建立資料庫。 [進度和完成] 頁面隨即出現。

8. 建立和設定資料庫時，請按一下 [完成]。

    如需有關 [**建立資料庫]** 中之設定的詳細資訊, 請參閱[ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] create&#41;database wizard Configuration Manager](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)。

9. 在的 [**資料庫**設定] 頁面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]上, 按一下 [**選取資料庫**]。

10. 按一下 **[連線]** , [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]選取您在步驟8中建立的資料庫, 然後按一下 **[確定]** 。

    ![mds-SQLServer2019-Config-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-Config-MI_connectDBName")

11. 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中，按一下左窗格的 [Web 組態]。

12. 在 [網站] 清單方塊中，按一下 [預設的網站]，然後按一下 [建立] 以建立 Web 應用程式。
![mds-SQLServer2019-Config-MI-WebConfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "mds-SQLServer2019-Config-MI_WebConfiguration")

   > [!NOTE] 
   > 當您選取 [預設的網站] 時，必須建立 Web 應用程式。 如果您選取清單方塊中的 [建立新網站]，即會自動建立應用程式。

    

13. 在 [**應用程式集**區] 區段中, 輸入不同的使用者名稱, 輸入密碼, 然後按一下 [確定]。
![mds-SQLServer2019-Config-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "mds-SQLServer2019-Config-MI_CreateWebApplication")

   > [!NOTE]
   > 您需要確保使用者可以使用您剛建立的 Active Directory 整合式驗證來存取資料庫。 或者, 您稍後需要變更 web.config 中的連接。

    

14. 如需 [**建立 web 應用程式**] 對話方塊的詳細資訊, 請參閱[ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] &#41;Configuration Manager 的 [建立 web 應用程式]](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)對話方塊。

15. 在 [ web 設定] 頁面的 [ **web 應用程式**] 方塊中, 按一下您已建立的應用程式, 然後按一下 [**將應用程式與資料庫產生關聯**] 區段中的 [**選取**]。

16. 按一下 **「連接」** ，並選取您想要與 Web 應用程式產生關聯的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 資料庫，然後按一下 **「確定」** 。

    您已完成網站的設定程序。 [ **Web**設定] 頁面現在會顯示您選取的網站、您建立的 Web 應用[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]程式, 以及與應用程式相關聯的資料庫。

    ![mds-SQLServer2019-Config-MI-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "mds-SQLServer2019-Config-MI_WebConfigSelectDB")

17. 按一下 **[套用]** 。 [組態完成] 訊息方塊隨即顯示。 按一下訊息方塊中的 [確定]，以啟動 Web 應用程式。 網站位址是 http://server 名稱/web 應用程式/。

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>在 Web 應用程式上連接受控實例資料庫的其他驗證類型

我們可以在 C:\Program Files\Microsoft SQL Server\150\Master Data Services\webapplication。底下取得 web.config 檔案 **。** 我們可以修改 connectionString 以變更其他驗證類型, 以連接受控實例資料庫。

預設驗證類型為「**Active Directory 整合**」, 以下是範例連接字串。

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

我們也支援 Active Directory 密碼驗證和 SQL Server 驗證, 以下是範例連接字串。

Active Directory 密碼驗證

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

SQL Server 驗證

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>升級[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]與資料庫版本

**更新[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

安裝 SQL Server 2019**累計更新** [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]時, 將會自動更新。

**升級資料庫版本**

如果您在安裝 SQL Server 2019**累積更新**後收到「用戶端版本與資料庫版本不相容」的問題, 則需要升級資料庫版本。

![mds-SQLServer2019-Config-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "mds-SQLServer2019-Config-MI_UpgradeDBPage")

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]啟動。 然後按一下左窗格中的 [**資料庫**設定]。

2. 在的 [**資料庫**設定] 頁面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]上, 按一下 [**選取資料庫**]。

3. 按一下 **[連接]** , [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]選取您與 web 應用程式相關聯的資料庫, 然後按一下 **[確定]** 。

    ![mds-SQLServer2019-Config-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-Config-MI_ConnectDBName")

4. 按一下 [**升級資料庫 ...** ] 按鈕

    ![mds-SQLServer2019-Config-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "mds-SQLServer2019-Config-MI_SelectUpgradeDB")

5. 在 [升級資料庫] 中, 按一下 [**歡迎使用**] 頁面上的 **[下一步]** 按鈕和**升級審核**頁面。

    ![mds-SQLServer2019-Config-MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "mds-SQLServer2019-Config-MI_UpgradeDBWizard")

6. 當所有工作都完成時, 按一下 **[完成]** 按鈕。

## <a name="see-also"></a>另請參閱

 [Master Data Services 資料庫](../master-data-services/master-data-services-database.md)[主資料管理員 Web 應用程式](../master-data-services/master-data-manager-web-application.md)[[資料庫設定&#40;]&#41;頁面 Master Data Services 組態管理員](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)[Master Data Services &#40;MDS&#41;的新功能](../master-data-services/what-s-new-in-master-data-services-mds.md)
