---
title: 安裝 SQL Server 2016 R Services （資料庫內）-SQL Server 機器學習服務
description: 新增 R 程式設計語言支援，可在 Windows 上 SQL Server 2016 R Services 上的資料庫引擎。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0cfe6b67217521f829f7b4745d42283e70a411fe
ms.sourcegitcommit: 32a55df1275ad169bb1457243dc8caa8b48b206f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/28/2019
ms.locfileid: "55147026"
---
# <a name="install-sql-server-2016-r-services"></a>安裝 SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何安裝和設定**SQL Server 2016 R Services**。 如果您有 SQL Server 2016 時，安裝此功能以啟用 SQL Server 中的 R 程式碼執行。

在 SQL Server 2017 中，提供 R 整合[Machine Learning 服務](../r/r-server-standalone.md)，反映的 Python。 如果您的 R 整合，並讓 SQL Server 2017 安裝媒體，請參閱[安裝 SQL Server 2017 Machine Learning 服務](sql-machine-learning-services-windows-install.md)新增功能。 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>預先安裝檢查清單

+ 需要資料庫引擎執行個體。 雖然您可以將它以累加方式加入現有的執行個體，您無法安裝只是 R。

+ 業務續航力[Always On 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)R Services 的支援。 您必須安裝 R Services，並設定封裝，每個節點上。

+ 請勿在容錯移轉叢集上安裝 R Services。 用來隔離 R 程序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝 R Services。 R Services 的部分安裝程式將會失敗。

+ 未安裝**共用功能** > **R Server （獨立式）** 同一部電腦上執行的資料庫執行個體。 

  與其他版本的 R 和 Python 的並排顯示安裝可能會因為 SQL Server 執行個體會使用自己的開放原始碼 R 和 Anaconda 散發套件。 不過，執行 SQL Server 外部的 SQL Server 電腦使用 R 和 Python 程式碼可能會導致各種問題：
    
  + 您使用不同的程式庫和其他可執行檔，並比您在 SQL Server 中執行時，取得不同的結果。
  + 執行外部程式庫中的 R 和 Python 指令碼不受 SQL Server，導致資源爭用。
  
如果您使用任何舊版 Revolution Analytics 開發環境或 RevoScaleR 套件，或您已安裝任何發行前版本的 SQL Server 2016，您就必須將它們解除安裝。 不支援執行舊版和新版的 RevoScaleR 與其他專屬的套件版本。 移除舊版的協助，請參閱[升級和安裝常見問題集，SQL Server Machine Learning 服務的](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安裝程式完成之後，請務必完成本文中所述的其他後續設定步驟。 這些步驟包括啟用 SQL Server 以使用外部指令碼，以及新增 SQL Server，來代替您執行 R 作業所需的帳戶。 組態變更通常需要重新啟動的執行個體或重新啟動 Launchpad 服務。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2016 安裝精靈。

2. 在 **安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入到現有安裝**。
    
   ![安裝 R Services (In-database)](media/2016-setup-installation-rsvcs.png "開始使用 R 服務的資料庫引擎安裝")
   
3. 在 **特徵選取**頁面上，選取下列選項：

   - 選取  **Database Engine Services**。 使用機器學習服務的每個執行個體中只需要 database engine。
   - 選取  **R Services （資料庫）**。 安裝支援的資料庫中使用。
    
     ![R Services 的特徵選取](media/2016setup-rsvcs-features.png "選取這些功能的 R Services 資料庫")

    > [!IMPORTANT]
    > 請勿安裝 R Server 和 R 服務的方法，在相同的時間。 您通常會安裝 R Server （獨立式），以建立環境的資料科學家或開發人員用來連接到 SQL Server，並部署 R 解決方案。 因此，不需要在相同的電腦上同時安裝 R Server 和 R Services。

4.  在 **同意安裝 Microsoft R Open**頁面上，按一下**接受**。
  
    此授權合約，才能下載 Microsoft R Open，其中包含開放原始碼 R 基底套件和工具，以及增強型的 R 套件和 Microsoft R 開發小組的連線提供者的散發套件。
  
5. 您接受授權合約之後，會短暫的暫停時，安裝程式已準備好。 按一下 [**下一步]** 時按鈕會變成可用。

6. 在 **安裝準備就緒**頁面上，確認下列項目都包含在內，然後選取**安裝**。

   + Database Engine 服務
   + R Services (資料庫內)

    記下的資料夾路徑下的位置`..\Setup Bootstrap\Log`儲存組態檔。 安裝完成時，您可以檢閱 摘要檔中已安裝的元件。

7. 安裝程式完成，如果系統指示您重新啟動電腦之後, 請現在登出。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)＞。

## <a name="set-environment-variables"></a>設定環境變數

您應該設定 R 功能整合只**MKL_CBWR**環境變數，以[確保一致的輸出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)從 Intel 數學核心程式庫 (MKL) 計算。

1. 在控制台中，按一下**系統及安全性** > **System** > **進階系統設定** >  **環境變數**。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為 `MKL_CBWR`
  + 若要設定變數值 `AUTO`

此步驟需要重新啟動伺服器。 如果您要啟用指令碼執行，您可以延後重新啟動後的所有組態工作完成前。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>啟用指令碼執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以下載並安裝適當版本，從這個頁面：[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > 您也可以試試預覽版[Azure Data Studio](../../azure-data-studio/what-is.md)，其支援的系統管理工作和 SQL Server 查詢。
  
2. 連接到您安裝 Machine Learning 服務的執行個體，請按一下**新的查詢**開啟查詢視窗中，並執行下列命令：

   ```sql
   sp_configure
   ```
    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為預設關閉的功能。 您可以執行 R 或 Python 指令碼之前，此功能，必須明確啟用由系統管理員。
     
3. 若要啟用外部指令碼的功能，請執行下列陳述式：
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新啟動服務

安裝完成後，重新啟動 database engine，再繼續下一步，啟用指令碼執行。

重新啟動服務時，也會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

您可以重新啟動服務，使用滑鼠右鍵**重新啟動**命令，在 SSMS 中，或使用之執行個體**Services**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>確認安裝

檢查安裝狀態的執行個體[自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

使用下列步驟，確認用來啟動外部指令碼的所有元件正在都執行。

1. 在 SQL Server Management Studio 中，開啟新的查詢視窗中，並執行下列命令：
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。

2. 開啟**Services**面板或 SQL Server 組態管理員，並確認**SQL Server Launchpad 服務**正在執行。 您應該有一項服務，每個資料庫引擎執行個體具有 R 或 Python 安裝。 如需有關服務的詳細資訊，請參閱[Extensibility framework](../concepts/extensibility-framework.md)。

7. 如果 Launchpad 正在執行，您應該能夠執行簡單的 R，以確認外部指令碼的執行階段可與 SQL Server 通訊。 

    開啟新**查詢** 視窗中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行指令碼，如下所示：
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    若要執行，第一次載入外部指令碼執行階段時，可能有點需要指令碼。 結果應該類似這樣：

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累積更新套用至 database engine 和機器學習服務元件。

在連線網際網路的裝置，通常透過 Windows Update 套用累計更新，但您也可以使用下列步驟，針對受控制的更新。 當您套用資料庫引擎的更新時，安裝程式會提取您在相同的執行個體安裝的 R 程式庫的累計更新。 

在中斷連線的伺服器，則需要額外的步驟。 如需詳細資訊，請參閱 <<c0> [ 在沒有網際網路存取的電腦上安裝 > 套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 開始使用已安裝的基準執行個體：SQL Server 2016 的最初發行版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2。

2. 請移至累計更新清單：[SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 選取最新的累積更新。 可執行檔會下載並自動擷取。

4. 執行安裝程式。 接受授權條款，並在 特徵選取 頁面中，檢閱 ，套用累計更新的功能。 您應該會看到針對目前的執行個體，包括 R Services 安裝的每項功能。 安裝程式下載封包檔需要更新所有功能。

5. 繼續執行精靈，並接受 R 散發的授權條款。 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>其他組態

如果外部指令碼驗證步驟成功，您可以從 SQL Server Management Studio、 Visual Studio Code 中或任何其他用戶端可以傳送至伺服器的 T-SQL 陳述式來執行 Python 命令。

如果執行命令時，您會收到錯誤，請檢閱本節中的其他設定步驟。 您可能需要對服務或資料庫中的其他適當的組態。

執行個體層級，可能包括額外的設定：

* [SQL Server Machine Learning 服務的防火牆設定](../../advanced-analytics/security/firewall-configuration.md)
* [啟用額外的網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

在資料庫上，您可能需要將下列的組態更新：

* [SQL Server Machine Learning 服務的權限授與使用者](../../advanced-analytics/security/user-permission.md)
* [新增 SQLRUserGroup 作為資料庫使用者](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> 並非所有列出的變更是必要的而且沒有任何可能需要。 需求取決於您的安全性結構描述，您可在此安裝 SQL Server，和您預期使用者會連線到資料庫並執行外部指令碼的方式。 其他疑難排解提示可以在這裡找到：[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>建議的最佳化

既然您已使用的所有項目，您也可以在最佳化的伺服器，以支援機器學習服務，或安裝預先定型的模型。

### <a name="add-more-worker-accounts"></a>新增更多的背景工作帳戶

如果您認為您可能會經常使用 R，或如果您預期有許多使用者同時執行指令碼，您可以增加指派給 Launchpad 服務的工作者帳戶數目。 如需詳細資訊，請參閱 <<c0> [ 修改 SQL Server Machine Learning 服務的使用者帳戶集區](../administration/modify-user-account-pool.md)。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>最佳化執行外部指令碼伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式為了最佳化伺服器的平衡，針對各種服務所支援的資料庫引擎，其中可能包括擷取、 轉換和載入 (ETL) 程序、 報告、 稽核和使用應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。 因此，如果在預設設定下，您可能會發現適用於 machine learning 資源，有時限制或進行節流處理，尤其是需要大量記憶體的作業。

若要確保機器學習服務工作，優先處理且獲得適當的資源，我們建議您使用 SQL Server 資源管理員，來設定外部資源集區。 您也可以變更配置的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database engine、 或增加下執行的帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

- 若要設定資源集區來管理外部的資源，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更的資料庫保留的記憶體數量，請參閱[伺服器記憶體組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以啟動的 R 帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，請參閱 <<c2> [ 修改機器學習服務的使用者帳戶集區](../administration/modify-user-account-pool.md)。

如果您使用 Standard Edition，而且沒有資源管理員，您可以使用動態管理檢視 (Dmv) 和擴充的事件，以及 Windows 事件監視，以協助您管理伺服器資源所使用的。如需詳細資訊，請參閱 <<c0> [ 監視和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他 R 套件

建立適用於 SQL Server 的 R 解決方案，可以呼叫基本 R 函式，函式與 SQL Server 一起安裝的專屬套件與第三方 R 套件開放原始碼 R 的 SQL Server 安裝的版本相容。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您有 R 的強大功能的個別安裝的電腦上，或如果您將套件安裝到使用者程式庫，您將無法使用 T-SQL 的那些套件。

安裝和管理 R 套件的程序是 SQL Server 2016 和 SQL Server 2017 中的不同。 在 SQL Server 2016 中，資料庫管理員必須安裝使用者所需的 R 套件。 在 SQL Server 2017 中，您可以設定使用者群組，共用每個資料庫層級上的封裝，或設定資料庫角色，以讓使用者安裝自己的封裝。 如需詳細資訊，請參閱 <<c0> [ 安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。