---
title: "升級及安裝常見問題集 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 47
---
# 升級及安裝常見問題集 (SQL Server R Services)
  本主題提供安裝常見問題及從 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 預覽版本升級問題的解答。  
  
 如果您是第一次安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，請依照以下描述的程序來安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 R 元件：[安裝 SQL Server R Services &#40;資料庫內&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  

   
## <a name="important-changes-from-pre-releae-versions"></a>發行前版本的重要變更  
 如已安裝任何 SQL Server 2016 發行前版本，或者要使用 SQL Server 2016 公用版本發行前的安裝指示，請務必知道，安裝程序和發行前版本和 RTM 版本完全不同。 這些變更包括 SQL Server 安裝精靈的可用選項和後置安裝步驟。 
   
> [!WARNING] 不支援任何 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 發行前版本的新安裝。 建議您儘快升級。  
+ 如已安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] CTP3、CTP3.1、CTP3.2、RC0 或 RC1，您必須重新執行設定後續安裝指令碼以解除安裝舊版的 R 元件和 R Services。 
+ 設定後續安裝指令碼僅供協助客戶解除安裝發行前版本。  安裝任何較新版本時，請勿執行指令碼。

## <a name="how-to-uninstall-previous-versions-of-r-services"></a>如何解除安裝舊版的 R Services

請務必以正確的順序解除安裝舊版的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 及其相關的 R 元件。

### <a name="1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>1.先執行指令碼來取消註冊 Windows 使用者群組和元件，再解除安裝舊版元件。
如已安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 發行前版本，您必須先執行具有 `/uninstall` 引數的指令碼 `RegisteREext.exe`。

如此一來，您可以取消註冊舊的元件，並移除與 Launchpad 相關聯的 Windows 使用者群組。 如果不這麼做，您無法為安裝的任何新執行個體建立所需的 Windows 使用者群組。
  
例如，如已在預設執行個體上安裝 R Services，請從指令碼安裝的目錄執行此命令︰  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
如已在具名執行個體上安裝 R Services，請在 *INSTANCE:* 之後指定執行個體名稱。  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

您可能需要執行多次指令碼，才能移除所有的元件。

> [!NOTE]
> 此指令碼的預設位置不盡相同，取決於您安裝的發行前版本。 如果嘗試執行錯誤的指令碼版本，可能會發生錯誤。 
> 
>  + 如有 CTP 3.1、3.2 或 3.3，您必須先從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=723194)下載更新版的安裝後組態指令碼，才能解除安裝元件。 更新的指令碼支援取消舊元件的註冊。 按一下連結並選取 [另存新檔]  ，將指令碼儲存至本機資料夾。 重新命名現有的指令碼，然後將新的指令碼複製到執行指令碼所在的資料夾。 
>  + 針對 RC0，已安裝正確的指令碼檔案，且位於此資料夾中︰`C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64`  
>  + 發行版本 (13.0.1601.5 或更新版本) 安裝或設定元件不需要任何指令碼。 指令碼應僅用於移除舊元件。 


### <a name="2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>2.解除安裝任何舊版的 Revolution Enterprise 工具，包括與 CTP 版本一起安裝的元件。

R 元件的解除安裝順序很重要。 一律先解除安裝 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]。 再解除安裝 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]。  

 如果您不小心先解除安裝 R Open，然後在嘗試解除安裝 Revolution R 企業版時發生錯誤，一種解決方法是重新安裝 Revolution R Open 或 Microsoft R Open，然後以正確的順序解決這兩個元件。  

### <a name="3-uninstall-any-other-version-of-microsoft-r-open"></a>3.解除安裝任何其他版本的 Microsoft R Open。

最後，解除安裝所有其他版本的 Microsoft R Open。
 
### <a name="4-upgrade-sql-server"></a>4.升級 SQL Server  
  
解除安裝所有發行前版本元件後，重新啟動電腦。 這是 SQL Server 安裝程式的需求，如不完成重新啟動將無法繼續進行更新的安裝。     

這麼做之後，請執行 SQL Server 安裝程式，並依照這些指示安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]：[安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
無須額外的元件；R 封裝和連線套件均由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝。 


## <a name="upgrading-r-components"></a>升級 R 元件

因為已發行 SQL Server 2016 的 Hotfix 或增強功能，如果您的執行個體已包含 R Services 功能，R 元件也會升級或更新。 

不過，當升級或修補未連線到網際網路的伺服器時，您必須先手動下載 R 元件的更新版本，再開始重新整理。 如需詳細資訊，請參閱[安裝沒有網際網路存取的 R 元件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。

## <a name="problems-uninstalling-older-versions-of-r"></a>解除安裝舊版 R 的問題  
在某些情況下，解除安裝程序無法完整移除舊版的 Revolution R Open 或 Revolution R Enterprise。  
  
 如果移除較舊版本有問題，您也可以編輯登錄來移除相關的索引鍵。  
  
 開啟 Windows 登錄並找到此機碼︰`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。  
  
 如有下列任一項目，且索引鍵只包含單一值 `sEstimatedSize2`，請予以刪除：  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2 版)  
  
-   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1 版)  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0 版)  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0 版)  


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>自動安裝需要新的 R 元件授權合約  
 如果使用命令列升級已安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體，您必須修改命令列以使用新的授權合約參數 */IACCEPTROPENLICENSEAGREEMENT*。 
 
 未能使用正確引數可能會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝失敗。  
  
## <a name="after-running-setup-includersqlproductnametokenrsqlproductnamemdmd-is-still-not-enabled"></a>執行安裝程式之後，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 仍未啟用。  
 即使安裝，仍預設停用支援執行外部指令碼的功能。 這是設計用於減少介面區域。  
  
 若要啟用 R 指令碼，系統管理員可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中執行下列陳述式：  
  
1.  在要使用 R 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體中執行此陳述式。  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  重新啟動執行個體。  
  
3.  重新啟動執行個體之後，請開啟 **SQL Server 組態管理員**或**服務**面板，並確認 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務正在執行。  

> [!TIP] 若要安裝預先設定的 R Services 執行個體，請使用包含已啟用 R Services 之 Enterprises Edition 的 Azure 虛擬機器映像。 如需詳細資訊，請參閱[在 Azure 虛擬機器上安裝 SQL Server R Services](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。
 

## <a name="setup-of-includersqlproductnametokenrsqlproductnamemdmd-not-available-in-a-failover-cluster"></a>容錯移轉叢集不提供 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的安裝程式  
 目前，無法在容錯移轉叢集上安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。  
    
 不過，您可以將 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝在使用 AlwaysOn 且屬於可用性群組的獨立電腦上。 如需在 AlwaysOn 可用性群組中使用 R Services 的詳細資訊，請參閱 [Always On 可用性群組︰互通性](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)。  

另一個選項是在不同的 SQL Server 執行個體上安裝複本，以執行 R 指令碼。 可以使用複寫或記錄傳送來建立複本。
 
## <a name="launchpad-service-cannot-be-started"></a>無法啟動 Launchpad 服務  

有幾個問題會妨礙 LaunchPad 啟動。
+ **未啟用 8.3 標記法**。  若要安裝 R Services (資料庫內)，功能安裝所在的磁碟機必須支援使用 **8.3** 標記法建立短檔名。  8.3 檔案名稱也稱為短檔名，用於與舊版 Microsoft Windows 相容之長檔名的舊名或替代檔名。 

  如果您要安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的磁碟區不支援短檔名，從 SQL Server 啟動 R 的處理程序可能無法找出正確的可執行檔，且 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 也不會啟動。  
  
   因應措施是，您應該在 SQL Server 及 R Services 安裝所在的磁碟區上啟用 8.3 標記法。 然後，您必須在 R Services 組態檔中提供工作目錄的簡短名稱。 

    1. 若要啟用 8.3 標記法，請執行 **fsutil** 公用程式配合 *8dot3name* 引數，如下所示︰[fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。
    2. 啟用 8.3 標記法後，開啟檔案 RLauncher.config。 在預設安裝中，RLauncher.config 檔案位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn。
    3. 記錄 WORKING_DIRECTORY 屬性。
    4. 使用 fsutil 公用程式搭配 *file* 引數來指定 WORKING_DIRECTORY 中指定的資料夾簡短檔案路徑。
    5. 編輯組態檔以使用 WORKING_DIRECTORY 的簡短名稱。   
     
或者，您可以為 WORKING_DIRECTORY 指定不同的目錄，其具有與 8.3 標記法相容的路徑。     
   
   > [!NOTE] 未來版本會移除此限制。 
 
+ **執行 Launchpad 的帳戶已經變更，或已移除必要的權限。** 依預設，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 在啟動時會使用下列帳戶，其由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝程式設定，以擁有所有的必要權限︰NT Service\MSSQLLaunchpad。

  因此，如果您將不同的帳戶指派給 Launchpad，或 SQL Server 電腦上的原則移除了權限，帳戶可能沒有必要的權限，而您可能會看到此錯誤︰*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登入失敗︰未授與使用者這個電腦所要求的登入類型。*

  若要將必要權限授予新的服務帳戶，請使用**本機安全性原則**應用程式並更新帳戶權限以包含這些權限︰
  + 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
  + 略過跨越檢查 (SeChangeNotifyPrivilege)
  + 以服務登入 (SeServiceLogonRight)
  + 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

  如需執行 SQL Server 服務權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。
  
## <a name="side-by-side-installation-not-supported"></a>不支援並存安裝  
 請勿使用其他的 R 版本，或其他來自 Revolution Analytics 的版本建立並存安裝。  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>SQL Server 當地語系化版本的 R 元件離線安裝 
如果您要在無法存取網際網路的電腦上安裝 R Services，您必須額外採取兩個步驟︰您必須將 R 元件安裝程式下載到本機資料夾，再執行 SQL Server 安裝程式；而且您必須編輯安裝程式檔案，以確保已安裝正確的語言。 

R 元件所用的語言識別碼必須和要安裝的 SQL Server 安裝程式語言相同，否則 [下一步] 按鈕會停用，而您無法完成安裝。

如需詳細資訊，請參閱[安裝沒有網際網路存取的 R 元件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>無法啟動 R 指令碼的執行階段
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 建立 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 執行 R 作業所使用的 Windows 使用者群組。 此使用者群組必須能夠登入執行 R Services 的執行個體，才能代表使用 Windows 整合式驗證的遠端使用者來執行 R。
  
 在不具此權限之 Windows 的 R 使用者 (**SQLRUsers**) 群組環境中，您可能會看到下列錯誤：  
  
-   嘗試執行 R 指令碼時：  
  
     *無法啟動 'R' 指令碼的執行階段。請檢查 'R' 執行階段的組態。*  
  
     *發生外部指令碼錯誤。無法啟動執行階段。*  
  
-   [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務產生錯誤：  
  
     *無法將啟動器 RLauncher.dll 初始化*  
  
     *未註冊任何啟動器 dll！*  
  
-   安全性記錄檔指出帳戶 NT SERVICE\MSSQLLAUNCHPAD 無法登入。  
  
如需如何授與此使用者群組必要權限的資訊，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 

> [!NOTE]
> 
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，則不適用這項限制。 

  
## <a name="remote-execution-via-odbc"></a>透過 ODBC 的遠端執行   
 如果您使用資料科學工作站，並連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦以使用 **RevoScaleR** 函數來執行 R 命令，在使用將資料寫入伺服器的 ODBC 呼叫時，可能會發生錯誤。 
 
 原因與上一節所述相同︰R Services 在安裝期間，會建立一組用於執行 R 工作的背景工作帳戶。 不過，如果這些帳戶無法連接到伺服器，就無法代表您執行 ODBC 呼叫。 
 
 請注意，如果您使用 SQL 登入從遠端工作站執行 R 指令碼，即不適用這項限制，因為 SQL 登入認證會明確地從 R 用戶端傳遞至 SQL Server 執行個體，再到 ODBC。
  
若要啟用隱含的驗證，您必須授與此群組背景工作帳戶權限，如下所示︰  
    
1. 在您要執行 R 程式碼的執行個體上，將 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開啟為系統管理員。 

2. 執行下列指令碼。 如已變更預設值，以及電腦和執行個體名稱，請務必編輯使用者群組名稱。
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

如需使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI 執行此作業的詳細資訊及使用步驟，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。

    
## <a name="errors-during-setup-because-r-components-cannot-be-installed"></a>因為無法安裝 R 元件，所以安裝期間發生錯誤。  
 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝 R Services (資料庫內) 時，當您在包含 Microsoft R Open 授權條款的頁面上按一下 [接受] 時，且已安裝其他元件時，安裝程式應該會找到元件，然後開始安裝。 不過，在這些情況下，元件仍可能安裝失敗︰  
  
-   您要執行離線安裝，但無法下載元件。  
  
     [安裝沒有網際網路存取的 R 元件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
-   您要使用此選項來檢查更新，因為找不到正確版本的元件，更新服務會傳回錯誤。  
  
  這是 RC3 中已修正的已知問題。  
  
 
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>將 R Server (獨立式) 升級至 RC3，需要使用 RC2 安裝公用程式來解除安裝。
 Microsoft R Server (獨立式) 第一次推出是在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2。 若要升級至 Microsoft R Server RC3 版本，您必須先使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 安裝程式來解除安裝，然後再使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3 安裝程式重新安裝。  
  
1.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式解除安裝 R Server (獨立式) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2。  
  
2.  將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升級到 RC3 並選取安裝 R Services (資料庫內) 的選項。 這會將 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的執行個體升級至 RC3，而不需要任何其他額外設定。  
  
3.  再次執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3 安裝程式並安裝 Microsoft R Server (獨立式)。  

升級至 RTM 版本的 Microsoft R Server 時，不需要此因應措施。

## <a name="see-also"></a>另請參閱  
 [開始使用 SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [開始使用 Microsoft R Server &#40;獨立式&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  