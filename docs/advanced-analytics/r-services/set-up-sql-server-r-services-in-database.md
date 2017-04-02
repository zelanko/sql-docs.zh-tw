---
title: "設定 SQL Server R 服務 (資料庫內) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "安裝 SQL Server R 服務"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# 設定 SQL Server R 服務 (資料庫內)
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和更新版本中，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈安裝與 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相關的所有元件。  
 
 
 完成安裝程式後，可能需要一些額外的步驟來啟用 R Services 功能以設定帳戶，並授與使用者特定資料庫的權限。   
  
如果在完成安裝之後，遇到資料庫存取的問題，或需要解除安裝舊版，請參閱[升級和安裝常見問題集 &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。  

> [!NOTE]
> 若要安裝 R Services (資料庫內)，安裝功能所在的磁碟機必須支援使用 8.3 標記法來建立短檔名。 否則，可能無法啟動從 SQL Server 啟動 R 的處理程序。 請務必先啟用磁碟區上的 8.3 標記法，再安裝 R Services。 未來版本會移除此限制。

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a> 步驟 1：在 SQL Server 2016 或更新版本上安裝 R Services (資料庫內)  
   
  
1.  執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
    如需如何執行自動安裝的資訊，請參閱 [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md)。  
  
2.  在 [安裝]  索引標籤上，按一下 [新增 SQL Server 獨立安裝或將功能加入至現有安裝] 。  
  
    > [!NOTE]  
    >  您無法在容錯移轉叢集上安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 不過，您可以將 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝在使用 AlwaysOn 且屬於可用性群組的獨立電腦上。 如需在 AlwaysOn 可用性群組中使用 R Services 的詳細資訊，請參閱 [Always On 可用性群組︰互通性](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)。  
  
3.  在 [特徵選取]  頁面上，選取下列選項：  
  
    -   **Database Engine 服務**  
  
         需要資料庫引擎的至少一個執行個體才能使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 您可以使用預設或具名執行個體。  
  
    -   **R Services (資料庫內)**  
  
         此選項會設定 R 作業所使用的資料庫服務，並安裝支援外部指令碼和處理序的擴充功能。  
    > [!NOTE]
    > 
    > 如果您需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行 R 程式碼，請務必安裝 **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]**。 
    > 
    > 相反地，Microsoft R Server (獨立式) 是可讓您在不執行 SQL Server 的 Windows 電腦上使用縮放 R 程式庫的選項。 我們建議您在用於 R 開發的膝上型電腦或另一部電腦上安裝 Microsoft R Server (獨立式)，以建立稍後可以部署到執行 R Services (資料庫內) 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 R 解決方案。
 
  
4.  在 [同意安裝 Microsoft R Open] 頁面上，按一下 [接受]。  
  
     需有本授權合約才能下載 Microsoft R Open，其中包含開放原始碼 R 基底套件和工具的散發，以及來自 Revolution Analytics 的增強型 R 套件和連接提供者。  
  
    > [!NOTE]  
    >  如果您使用的電腦無法存取網際網路，此時可以暫停步驟以分別下載安裝程式，如下所述︰[安裝沒有網際網路存取的 R 元件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。  
  
     按一下 [接受]，等到 [下一步] 按鈕變成使用中，再按一下 [下一步]。  
  
5.  在 [準備安裝] 頁面上，確認包含這些選項，然後按一下 [安裝]。  
  
     **功能**  
  
     Database Engine Services  
  
     R 服務 (資料庫內)  
  
6.  安裝完成時，重新啟動電腦。   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a> 步驟 2︰啟用 R Services 並確認本機 R 指令碼執行是否運作  
  
  
1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果未安裝，您可以重新執行 SQL Server 安裝精靈以開啟下載連結並安裝它。  
  
2. 連接到已安裝 R Services (資料庫內) 的執行個體，執行下列命令明確啟用 R Services 功能；否則，即使已在安裝時安裝功能，也無法叫用 R 指令碼。  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 SQL Server 服務。 這也會自動重新啟動相關的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務。 您可以使用控制台的 [服務] 窗格，或使用 SQL Server 組態管理員，重新啟動服務。  
  
9. 取得 SQL Server 服務之後，請執行下列命令來確認已啟用 R 功能，並檢查 *run_value* 設為 1：  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   (選擇性) 開啟 [服務] 窗格，並確認執行個體的 Launchpad 服務執行中。 每個執行個體都擁有自己的 Launchpad 服務。
   
10. 現在，您應該能夠執行簡單的 R 指令碼，如下面的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 所示：  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **結果**  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  如果您需要存取 SQL Server 資料，或從遠端資料科學用戶端執行 R 命令，則需要一些額外的步驟。 下列步驟會詳細說明這些額外的需求。
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a> 步驟 3︰為 Launchpad 帳戶啟用隱含的驗證  
   
  
在安裝期間建立了 20 個新的 Windows 使用者帳戶，以在 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務的安全性權杖下執行工作。 當使用者從外部用戶端傳送 R 指令碼時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會啟用可用的背景工作者帳戶、比對呼叫使用者的身分識別，然後代表使用者執行 R 指令碼。 這是新的資料庫引擎服務，其支援安全執行外部指令碼，稱之為「隱含的驗證」。 

您可以在 Windows 使用者群組 **SQLRUserGroup** 中，檢視這些帳戶。  如果您需要從遠端資料科學用戶端執行 R 指令碼並使用 Windows 驗證，這些背景工作者帳戶必須有代表您登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的權限。  
  
1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [物件總管] 中，展開 [安全性]，以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。  
2. 在 [登入 - 新增] 對話方塊中，按一下 [搜尋]。  
3. 按一下 [物件類型]，然後選取 [群組]。 取消選取其他所有項目。  
4. 在 [輸入要選取的物件名稱] 中輸入 *SQLRUserGroup*，按一下 [檢查名稱]。  
5. 與執行個體的 Launchpad 服務相關聯的本機群組名稱，應該解析為類似 *instancename\SQLRUserGroup*。 按一下 **[確定]**。  
6. 依預設，登入指派給**公用**角色，並有連接到資料庫引擎的權限。 
7. 按一下 **[確定]**。  
  
> [!NOTE] 如果您在 SQL Server 的計算內容中使用 SQL 登入來執行 R 指令碼，就不需要這個額外步驟。
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>步驟 4︰授與非系統管理員使用者 R 指令碼的權限  
  
如果您已自行安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並在自己的執行個體中執行 R 指令碼，您通常是以系統管理員身分執行指令碼，並因此取得不同作業和資料庫中所有資料的隱含權限，以及視需要安裝新 R 套件的能力。  
  
不過，企業案例中的大部分使用者，包括使用 SQL 登入存取資料庫的人員，並沒有這類的提高權限。 因此，針對每位要執行外部指令碼的使用者，您必須授與每個會在使用 R 的資料庫中執行 R 指令碼的使用者權限。   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] 需要安裝協助嗎？ 不確定是否執行了所有步驟嗎？
>
> 請使用這些自訂報表檢查 R Services 的安裝狀態。 如需詳細資訊，請參閱[使用自訂報表監視 R Services](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)。    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a> 選擇性修改  
  
本節描述您可以在執行個體或資料科學用戶端組態中執行的其他變更，以支援執行 R 指令碼。
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>修改 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 使用的背景工作帳戶數目
  
如果您認為自己會經常使用 R，或預期會有許多使用者同時執行指令碼，您可以增加指派給 Launchpad 服務的背景工作者帳戶數目。 如需詳細資訊，請參閱[修改 SQL Server R Services 的使用者帳戶集區](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>視需要提供 R 使用者其他資料庫的登入、讀取、寫入或 DDL 權限。  
  
在執行 R 指令碼時，使用者帳戶可能需要讀取其他資料庫的資料、建立新的資料表儲存結果，以及將資料寫入資料表。 
     
針對每位要執行 R 指令碼的使用者，請確認使用者帳戶擁有特定資料庫的 **db_datareader**、**db_datawriter** 或 **db_ddladmin** 權限。   
       
例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 SQL 登入 *MySQLLogin* 在 *RSamples* 資料庫中執行 T-SQL 查詢的權限。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
如需每個角色中所包含之權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源  
  
如果您在資料科學用戶端電腦上建立 R 解決方案，且必須連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦當作計算內容，您可以使用 SQL 登入或整合式的 Windows 驗證。  
  
如果您使用 SQL 登入，請確定此登入擁有您要讀取資料之資料庫的適當權限。 您可以新增 *Connect to* 和 *SELECT* 權限，或新增 **db_datareader** 角色的登入權限來執行此作業。 如果您需要建立物件，您會需要 **DDL_admin** 權限。  若要將資料儲存至資料表，請新增 **db_datawriter** 角色的登入權限。  
  
如果您使用 Windows 驗證，您必須在資料科學用戶端上設定 ODBC 資料來源，此用戶端會指定該執行個體名稱和其他連接資訊。  
  
如需詳細資訊，請參閱[使用 ODBC 資料來源管理員](http://windows.microsoft.com/windows/using-odbc-data-source-administrator)。  
  
### <a name="optimize-the-server-for-r"></a>最佳化 R 伺服器  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的預設設定是為了最佳化伺服器的平衡，處理資料庫引擎支援的各種服務，可能包含 ETL 程序、報表、稽核和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的應用程式。 因此，在預設設定下，您可能會發現受限或節流的 R 作業資源，尤其是需要大量記憶體的作業。  
  
 為確保 R 工作優先處理且獲得適當的資源，建議您使用資源管理員設定 R 作業特定的外部資源集區。 您也可能想要變更配置到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎的記憶體數量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務下所執行的帳戶數目。  
  
-   設定資源集區以便管理外部資源  
  
     [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   變更保留給資料庫引擎的記憶體數量  
  
     [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   變更 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 可以啟動的 R 帳戶數目  
  
     [修改 SQL Server R 服務的使用者帳戶集區](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>取得 R 原始碼 (選擇性)  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包括散佈開放原始碼 R 基底套件。  
  
或者按一下這些連結之一，立即開始下載已修改的 GPL/LGPL 原始程式碼。 原始程式碼會在符合 GNU 通用公共授權時提供，但不需要安裝或使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。  
  
-   與 RC2 相容︰下載封存檔 [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 
  
-   與 RC3 相容︰下載封存檔 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 

-   與 RTM 相容︰下載封存檔 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771)
  
## <a name="troubleshooting"></a>疑難排解  
 遇到問題嗎？ 安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 發行前版本時，請參閱這份常見問題。  
  
 [升級及安裝常見問題集 &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [設定資料科學用戶端](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [建立獨立式 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  