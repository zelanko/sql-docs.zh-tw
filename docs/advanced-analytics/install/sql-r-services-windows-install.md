---
title: 安裝 SQL Server 2016 R 服務 (資料庫內)
description: 將 R 程式設計語言支援新增至 Windows 上 SQL Server 2016 R 服務上的資料庫引擎。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 61dd49191e85d9fd4685904ae01b72d754d43318
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715814"
---
# <a name="install-sql-server-2016-r-services"></a>安裝 SQL Server 2016 R 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝和設定**SQL Server 2016 R Services**。 如果您有 SQL Server 2016, 請安裝此功能, 以在 SQL Server 中啟用 R 程式碼的執行。

在 SQL Server 2017 中, 會在[Machine Learning 服務](../r/r-server-standalone.md)中提供 R 整合, 以反映 Python 的新增。 如果您想要 R 整合並擁有 SQL Server 2017 安裝媒體, 請參閱[安裝 SQL Server Machine Learning 服務](sql-machine-learning-services-windows-install.md)以新增功能。 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>預先安裝檢查清單

+ 需要資料庫引擎實例。 您不能只安裝 R, 雖然您可以將它累加地新增至現有的實例。

+ 針對商務持續性, R 服務支援[Always On 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。 您必須在每個節點上安裝 R Services 和設定封裝。

+ 請勿在容錯移轉叢集上安裝 R Services。 用於隔離 R 進程的安全性機制, 與 Windows Server 容錯移轉叢集環境不相容。

+ 請勿在網域控制站上安裝 R Services。 安裝程式的 R Services 部分將會失敗。

+ 請勿在執行同資料庫實例的同一部電腦上安裝**共用功能** >  **R Server (獨立式)** 。 

  與其他 R 和 Python 版本並存安裝是可行的, 因為 SQL Server 實例會使用自己的開放原始碼 R 和 Anaconda 散發套件複本。 不過, 在 SQL Server 外的 SQL Server 電腦上執行使用 R 和 Python 的程式碼, 可能會導致各種問題:
    
  + 您可以使用不同的程式庫和不同的可執行檔, 並取得不同的結果, 而不是在 SQL Server 中執行。
  + 在外部程式庫中執行的 R 和 Python 腳本無法由 SQL Server 管理, 因而導致資源競爭。
  
如果您使用任何較舊版本的革新分析開發環境或 RevoScaleR 套件, 或如果您已安裝 SQL Server 2016 的任何發行前版本, 您必須將它們卸載。 不支援執行舊版和較新版本的 RevoScaleR 和其他專屬套件。 如需移除舊版的說明, 請參閱[SQL Server Machine Learning 服務的升級和安裝常見問題](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安裝完成之後, 請務必完成本文中所述的其他後續設定步驟。 這些步驟包括啟用 SQL Server 使用外部腳本, 以及新增 SQL Server 代表您執行 R 作業所需的帳戶。 設定變更通常需要重新開機實例, 或重新開機啟動列服務。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2016 的安裝程式。

2. 在 [**安裝**] 索引標籤上, 選取 [**新增 SQL Server 獨立安裝或將功能加入至現有安裝**]。
    
   ![安裝 R Services (資料庫內)](media/2016-setup-installation-rsvcs.png "開始使用 R Services 安裝 database engine")
   
3. 在 [**特徵選取**] 頁面上, 選取下列選項:

   - 選取 [**資料庫引擎服務**]。 在使用機器學習服務的每個實例中, 都需要有資料庫引擎。
   - 選取 **[R Services (資料庫內)** ]。 安裝 R 的資料庫內使用支援。
    
     ![R Services 功能選取](media/2016setup-rsvcs-features.png "針對資料庫內的 R 服務選取這些功能")

    > [!IMPORTANT]
    > 請勿同時安裝 R Server 和 R Services。 您通常會安裝 R Server (獨立式) 來建立環境, 讓資料科學家或開發人員用來連接到 SQL Server 和部署 R 解決方案。 因此，不需要在相同的電腦上同時安裝 R Server 和 R Services。

4.  在 [**同意安裝 Microsoft R Open** ] 頁面上, 按一下 [**接受**]。
  
    需要此授權合約才能下載 Microsoft R Open, 其中包含開放原始碼 R 基底套件和工具的散發, 以及來自 Microsoft R 開發小組的增強型 R 套件和連線提供者。
  
5. 在您接受授權合約之後, 就會在準備安裝程式時短暫暫停。 當按鈕變成可用時, 請按 **[下一步]** 。

6. 在 [**準備安裝**] 頁面上, 確認包含下列專案, 然後選取 [**安裝**]。

   + Database Engine 服務
   + R Services (資料庫內)

    請注意儲存設定檔之路徑`..\Setup Bootstrap\Log`底下的資料夾位置。 當安裝程式完成時, 您可以在摘要檔案中檢查已安裝的元件。

7. 在安裝程式完成之後, 如果您被指示重新開機電腦, 請立即執行此動作。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)＞。

## <a name="set-environment-variables"></a>設定環境變數

僅適用于 R 功能整合, 您應該設定**MKL_CBWR**環境變數, 以確保從 Intel 數學核心程式庫 (MKL) 計算的[輸出一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

1. 在 [控制台] 中, 按一下 [**系統及安全性** > **系統** > ] [系統**設定** > ] [**環境變數**]。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為`MKL_CBWR`
  + 將變數值設定為`AUTO`

此步驟需要重新開機伺服器。 如果您即將啟用腳本執行, 您可以在重新開機前保留, 直到完成所有設定工作為止。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>啟用腳本執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以從這個頁面下載並安裝適當的版本:[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > 您也可以試用[Azure Data Studio](../../azure-data-studio/what-is.md)的預覽版本, 其支援 SQL Server 的系統管理工作和查詢。
  
2. 連接到您安裝 Machine Learning Services 的實例, 按一下 [追加**查詢**] 以開啟查詢視窗, 然後執行下列命令:

   ```sql
   sp_configure
   ```
    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為功能預設是關閉的。 系統管理員必須明確地啟用此功能, 才能執行 R 或 Python 腳本。
     
3. 若要啟用外部腳本功能, 請執行下列語句:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新啟動服務

當安裝完成時, 請重新開機資料庫引擎, 然後繼續進行下一步, 啟用腳本執行。

重新開機服務也會自動重新開機[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]相關的服務。

您可以使用 SSMS 中實例的右鍵 [**重新開機**] 命令, 或使用 [控制台] 中的 [**服務**] 面板, 或使用 [ [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)] 來重新開機服務。

## <a name="verify-installation"></a>確認安裝

使用[自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)檢查實例的安裝狀態。

請使用下列步驟來確認用來啟動外部腳本的所有元件都在執行中。

1. 在 SQL Server Management Studio 中, 開啟新的查詢視窗, 然後執行下列命令:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。

2. 開啟 [**服務**] 面板或 SQL Server 組態管理員, 並確認**SQL Server Launchpad 服務**正在執行。 針對每個已安裝 R 或 Python 的資料庫引擎實例, 您應該會有一個服務。 如需服務的詳細資訊, 請參閱擴充性[架構](../concepts/extensibility-framework.md)。

7. 如果啟動控制板正在執行, 您應該能夠執行簡單的 R, 以確認外部腳本執行時間可以與 SQL Server 通訊。 

    在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]開啟新的**查詢**視窗, 然後執行如下所示的腳本:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    當第一次載入外部腳本執行時間時, 腳本可能需要一些時間才能執行。 結果應該如下所示:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累計更新套用至資料庫引擎和機器學習服務元件。

在連線到網際網路的裝置上, 累積更新通常會透過 Windows Update 套用, 但您也可以使用下列步驟來進行受控制的更新。 當您套用資料庫引擎的更新時, 安裝程式會提取您在相同實例上安裝之 R 程式庫的累計更新。 

在中斷連線的伺服器上, 需要額外的步驟。 如需詳細資訊, 請參閱[在沒有網際網路存取的電腦上安裝 > 套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 從已安裝的基準實例開始:SQL Server 2016 初始版本, SQL Server 2016 SP 1, 或 SQL Server 2016 SP 2。

2. 移至累計更新清單:[SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 選取最新的累計更新。 可執行檔會自動下載並解壓縮。

4. 執行安裝程式。 接受授權條款, 然後在 [特徵選取] 頁面上, 檢查已套用累積更新的功能。 您應該會看到針對目前實例安裝的每項功能, 包括 R 服務。 安裝程式會下載更新所有功能所需的封包檔。

5. 繼續執行嚮導, 並接受 R 散發的授權條款。 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>其他組態

如果外部腳本驗證步驟成功, 您可以從 SQL Server Management Studio、Visual Studio Code 或任何其他可將 T-sql 語句傳送至伺服器的用戶端執行 Python 命令。

如果您在執行命令時遇到錯誤, 請參閱本節中的其他設定步驟。 您可能需要對服務或資料庫進行其他適當的設定。

在實例層級, 其他設定可能包括:

* [SQL Server Machine Learning 服務的防火牆設定](../../advanced-analytics/security/firewall-configuration.md)
* [啟用其他網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連線](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [管理磁片配額](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas), 以避免外部腳本執行耗盡磁碟空間的工作

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

在資料庫上, 您可能需要下列設定更新:

* [授與使用者 SQL Server Machine Learning 服務的許可權](../../advanced-analytics/security/user-permission.md)
* [新增 SQLRUserGroup 作為資料庫使用者](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> 並非所有列出的變更都是必要的, 而且可能不需要。 需求取決於您已安裝 SQL Server 的安全性架構, 以及您希望使用者如何連接到資料庫並執行外部腳本。 您可以在這裡找到其他疑難排解秘訣:[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>建議的優化

現在您已有所有工作, 您可能也會想要優化伺服器以支援機器學習服務, 或安裝預先定型模型。

### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您認為您可能會大量使用 R, 或預期有許多使用者同時執行腳本, 您可以增加指派給啟動列服務的背景工作帳戶數目。 如需詳細資訊, 請參閱[修改 SQL Server Machine Learning 服務的使用者帳戶集](../administration/modify-user-account-pool.md)區。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>優化伺服器以進行外部腳本執行

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式的預設設定是針對資料庫引擎支援的各種服務優化伺服器的平衡, 其中可能包括解壓縮、轉換和載入 (ETL) 程式、報告、審核, 以及使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料的應用程式。 因此, 在預設設定下, 您可能會發現機器學習服務的資源有時候會受到限制或節流, 特別是在需要大量記憶體的作業中。

若要確保機器學習作業的優先順序和適當地設定資源, 建議您使用 SQL Server Resource Governor 來設定外部資源集區。 您也可能想要變更配置給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎的記憶體數量, 或增加[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]在服務下執行的帳戶數目。

- 若要設定用來管理外部資源的資源集區, 請參閱[建立外部資源集](../../t-sql/statements/create-external-resource-pool-transact-sql.md)區。
  
- 若要變更為資料庫保留的記憶體數量, 請參閱[伺服器記憶體設定選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以啟動[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]的 R 帳戶數目, 請參閱[修改機器學習服務的使用者帳戶集](../administration/modify-user-account-pool.md)區。

如果您使用的是 Standard Edition, 而且沒有 Resource Governor, 您可以使用動態管理檢視 (Dmv) 和擴充事件, 以及 Windows 事件監視, 協助管理 R 所使用的伺服器資源。如需詳細資訊, 請參閱[監視和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他 R 套件

您為 SQL Server 建立的 R 解決方案可以呼叫基本的 R 函式、與 SQL Server 一起安裝之專屬套件的函式, 以及與 SQL Server 所安裝的開放原始碼 R 版本相容的協力廠商 R 套件。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您在電腦上個別安裝 R, 或如果您已將套件安裝至使用者程式庫, 則無法從 T-sql 使用這些套件。

安裝和管理 R 套件的程式在 SQL Server 2016 和 SQL Server 2017 中有所不同。 在 SQL Server 2016 中, 資料庫管理員必須安裝使用者需要的 R 套件。 在 SQL Server 2017 中, 您可以將使用者群組設定為在每個資料庫層級上共用封裝, 或設定資料庫角色以讓使用者安裝自己的封裝。 如需詳細資訊, 請參閱[安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例, 並瞭解 R 如何與 SQL Server 搭配運作的基本概念。 如需下一個步驟, 請參閱下列連結:

+ [教學課程：在 T-sql 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用于 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看以真實世界案例為基礎的機器學習範例, 請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。