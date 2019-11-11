---
title: 在 Windows 上安裝
description: 此文章章解釋如何在 Windows 上安裝 SQL Server 機器學習服務。 您可以使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 8d51c147cfe5895356f8af270f62443643caa8f1
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727649"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-windows"></a>在 Windows 上安裝 SQL Server 機器學習服務 (Python 和 R)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章章解釋如何在 Windows 上安裝 SQL Server 機器學習服務。 您可以使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

+ 需要資料庫引擎執行個體。 您無法只安裝 R 或 Python 功能，雖然您可以藉由累加方式將其新增至現有的執行個體。

+ 針對商務持續性，機器學習服務支援 [AlwaysOn 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。 您必須在每個節點上都安裝機器學習服務，並設定套件。

+ SQL Server 2017 中的容錯移轉叢集上*不支援*安裝機器學習服務。 不過，SQL Server 2019 *支援*。 
 
+ 請勿在網域控制站上安裝機器學習服務。 安裝程式的機器學習服務部分將會失敗。

+ 不要在執行資料庫內執行個體的同一部電腦上安裝 [共用功能]   > [Machine Learning 伺服器 (獨立式)]  。 獨立伺服器會爭用相同資源，而損害這兩個安裝的效能。

+ 支援與其他 R 和 Python 版本並存安裝，但不建議這麼做。 支援的原因，是因為 SQL Server 執行個體使用自己的開放原始碼 R 和 Anaconda 散發套件副本。 但不建議您這樣做，因為在 SQL Server 外的 SQL Server 電腦上執行使用 R 和 Python 的程式碼，可能會導致各種問題：
    
  + 與在 SQL Server 中執行時相比，您可以使用不同的程式庫和不同的可執行檔，並取得不同的結果。
  + 在外部程式庫中執行的 R 和 Python 指令碼無法由 SQL Server 管理，因而導致資源競爭。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
+ 根據預設，系統會在 SQL Server 巨量資料叢集上安裝機器學習服務。 如果您使用的是巨量資料叢集，就不需要依照此文章中的步驟。 如需詳細資訊，請參閱[在巨量資料叢集上使用機器學習服務 (Python 和 R)](../../big-data-cluster/machine-learning-services.md)。
::: moniker-end

> [!IMPORTANT]
> 安裝完成之後，請務必完成此文章中所述的設定後步驟。 這些步驟包括讓 SQL Server 使用外部指令碼，以及新增 SQL Server 代替您執行 R 和 Python 作業所需的帳戶。 設定變更通常需要重新啟動執行個體，或重新啟動啟動控制板服務。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 的安裝精靈。
  
1. 在 [安裝]  索引標籤上，選取 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]  。

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![新的 SQL Server 獨立安裝](media/2017setup-installation-page-mlsvcs.png)
   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![新的 SQL Server 獨立安裝](media/2019setup-installation-page-mlsvcs.png)
   ::: moniker-end

1. 在 [特徵選取]  頁面上，選取下列選項：

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

   - **Database Engine 服務**
     
     若要搭配 SQL Server 使用 R 和 Python，您必須安裝資料庫引擎的執行個體。 您可以使用預設或具名執行個體。

   - **Machine Learning Services (資料庫內)**
     
     此選項會安裝支援 R 和 Python 指令碼執行的資料庫服務。

   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

   - **Database Engine 服務**
     
     若要搭配 SQL Server 使用 R、Python 和 Java，您必須安裝資料庫引擎的執行個體。 您可以使用預設或具名執行個體。

   - **Machine Learning Services (資料庫內)**
     
     此選項會安裝支援 R、Python 和 Java 指令碼執行的資料庫服務。

   ::: moniker-end

   - **R**
     
     核取此選項可新增 Microsoft R 套件、解譯器和開放原始碼 R。 
     
   - **Python**
     
     核取此選項可新增 Microsoft Python 套件、Python 3.5 可執行檔，以及從 Anaconda 散發套件選取程式庫。
     
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   - **Java**
     
     核取此選項以安裝 SQL 隨附的開放式 JRE，或提供不同版本的 JDK 或 JRE 的位置。
   ::: moniker-end
   
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![R 和 Python 的功能選項](media/2017setup-features-page-mls-rpy.PNG "適用於 R 和 Python 的安裝選項")
   ::: moniker-end
   
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![R、Python 的功能選項](media/2019setup-features-page-mls-rpy.png "適用於 R、Python 和 Java 的安裝選項")
   ::: moniker-end
   
   > [!NOTE]
   > 
   > 請勿選取 [Machine Learning 伺服器 (獨立式)]  的選項。 在**共用功能**下安裝 Machine Learning Server 的選項，旨在不同的電腦上使用。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

4. 在 [同意安裝 Microsoft R Open]  頁面上，選取 [接受]  ，然後 [下一步]  。 本授權合約涵蓋 Microsoft R Open，其中包含開放原始碼 R 基底套件和工具的散發套件，以及來自 Microsoft 開發小組的增強型 R 套件和連接提供者。

1. 在 [同意安裝 Python]  頁面上，選取 [接受]  ，然後 [下一步]  。 Python 開放原始碼授權合約也涵蓋 Anaconda 和相關工具，以及 Microsoft 開發小組的一些新 Python 程式庫。

   > [!NOTE]
   >  如果您使用的電腦無法存取網際網路，您可以在此時暫停安裝，以分別下載安裝程式。 如需詳細資訊，請參閱[在沒有網際網路存取的情況下安裝機器學習元件](../install/sql-ml-component-install-without-internet-access.md)。

1. 在 [準備安裝]  頁面上，確認包含這些選項，然後選取 [安裝]  。
  
   + Database Engine 服務
   + Machine Learning 服務 (資料庫內)
   + R 或 Python，或兩者

   請注意組態檔儲存所在資料夾 (路徑 `..\Setup Bootstrap\Log` 底下) 的位置。 當安裝程式完成時，您可以在摘要檔案中檢閱已安裝的元件。

1. 在安裝程式完成之後，如果系統要求您重新啟動電腦，請立即重新啟動。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)＞。

::: moniker-end

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

1. 在 [同意安裝 Microsoft R Open]  頁面上，選取 [接受]  ，然後 [下一步]  。 本授權合約涵蓋 Microsoft R Open，其中包含開放原始碼 R 基底套件和工具的散發套件，以及來自 Microsoft 開發小組的增強型 R 套件和連接提供者。

1. 在 [同意安裝 Python]  頁面上，選取 [接受]  ，然後 [下一步]  。 Python 開放原始碼授權合約也涵蓋 Anaconda 和相關工具，以及 Microsoft 開發小組的一些新 Python 程式庫。

1. 在 [Java 安裝位置]  頁面上，您可以安裝 SQL 隨附的開放 JRE 版本，也可以提供您自己安裝 JDK 或 JRE 的位置。 然後選取 [下一步]  。

   > [!NOTE]
   >  如果您使用的電腦無法存取網際網路，您可以在此時暫停安裝，以分別下載安裝程式。 如需詳細資訊，請參閱[在沒有網際網路存取的情況下安裝機器學習元件](../install/sql-ml-component-install-without-internet-access.md)。

1. 在 [準備安裝]  頁面上，確認包含這些選項，然後選取 [安裝]  。
  
   + Database Engine 服務
   + Machine Learning 服務 (資料庫內)
   + R、Python 和/或 Java

   請注意組態檔儲存所在資料夾 (路徑 `..\Setup Bootstrap\Log` 底下) 的位置。 當安裝程式完成時，您可以在摘要檔案中檢閱已安裝的元件。

1. 在安裝程式完成之後，如果系統要求您重新啟動電腦，請立即重新啟動。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)＞。

::: moniker-end

## <a name="set-environment-variables"></a>設定環境變數

僅針對 R 功能整合，您應該設定 **MKL_CBWR** 環境變數，以確保來自 Intel Math Kernel Library (MKL) 計算的輸出[會保持一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) \(英文\)。

1. 在 [控制台] 中，按一下 [系統及安全性]   > [系統]   > [進階系統設定]   > [環境變數]  。

2. 建立新的使用者或系統變數。 

   + 將變數名稱設定為 `MKL_CBWR`
   + 將變數值設定為 `AUTO`

此步驟需要重新啟動伺服器。 如果您即將啟用指令碼執行，則可以推遲重新啟動，直到完成所有設定工作為止。

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>啟用指令碼執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以從這個頁面下載並安裝適當的版本：[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > 您也可以使用 [Azure Data Studio](../../azure-data-studio/what-is.md)，它支援針對 SQL Server 的系統管理工作與查詢。
  
2. 連線到您安裝機器學習服務的執行個體，按一下 [新增查詢]  開啟查詢視窗，然後執行下列命令：

    ```sql
    sp_configure
    ```

    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為該功能預設是關閉的。 系統管理員必須明確地啟用該功能，您才能執行 R 或 Python 指令碼。
    
3.  若要啟用外部指令碼功能，請執行下列陳述式：
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果您已針對 R 語言啟用該功能，請不要再次執行 Python 的重新設定。 基礎擴充性平台支援這兩種語言。

## <a name="restart-the-service"></a>重新啟動服務

當安裝完成時，請先重新啟動資料庫引擎，然後再繼續執行下一步，以啟用指令碼執行。

重新啟動服務也會自動重新啟動相關的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務。

您可以針對 SSMS 中的執行個體，使用滑鼠右鍵按一下 [重新啟動]  命令，或使用 [控制台] 中的 [服務]  面板，或使用 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)來重新啟動服務。

## <a name="verify-installation"></a>確認安裝

在[自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)或安裝程式記錄中，檢查執行個體的安裝狀態。

使用下列步驟確認用於啟動外部指令碼的所有元件都正在執行。

1. 在 SQL Server Management Studio 中，開啟新的 [查詢] 視窗，並執行下列命令︰
    
   ```sql
   EXECUTE sp_configure  'external scripts enabled'
   ```

   **run_value** 現在應該設定為 1。
    
2. 開啟 [服務]  面板或 SQL Server 組態管理員，並確認 **SQL Server Launchpad 服務**正在執行。 您應該為每個安裝 R 或 Python 的資料庫引擎執行個體都提供一個服務。 如需服務的詳細資訊，請參閱[擴充性架構](../concepts/extensibility-framework.md)。 
   
3. 如果啟動控制板正在執行，您應該能夠執行簡單 R 和 Python 指令碼，以確認外部指令碼執行階段可以與 SQL Server 通訊。

   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟新的 [查詢]  視窗，然後執行如下所示的指令碼：
   
   + 適用於 R
   
     ```sql
     EXEC sp_execute_external_script  @language =N'R',
     @script=N'
     OutputDataSet <- InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
     
   + 適用於 Python
     
     ```sql
     EXEC sp_execute_external_script  @language =N'Python',
     @script=N'
     OutputDataSet = InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
   
   **結果**

   第一次載入外部指令碼執行階段時，該指令碼可能需要一些時間才能執行。 結果應該類似這樣：

   | hello |
   |----|
   | 1|

> [!NOTE]
> 根據設計，不會傳回 Python 指令碼中使用的資料行或標題。 若要為您的輸出新增資料行名稱，您必須指定傳回資料集的結構描述。 若要這麼做，請使用預存程序的 WITH RESULTS 參數、命名資料行，並指定 SQL 資料類型。
> 
> 例如，您可以加入下面這一行來產生任意的資料行名稱：`WITH RESULT SETS ((Col1 AS int))`

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
<!-- There are no updates yet available for 2019, and there's no 2019 update list site. When updates become available, add 2019 information to this section. -->

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累積更新套用至資料庫引擎和機器學習元件。

在連線到網際網路的裝置上，累積更新通常會透過 Windows Update 套用，但您也可以使用下列步驟來進行受控制的更新。 當您套用資料庫引擎的更新時，安裝程式會針對您安裝在相同執行個體上的任何 R 或 Python 功能提取累積更新。 

在中斷連線的伺服器上，需要額外的步驟。 如需詳細資訊，請參閱[在沒有網際網路存取的電腦上安裝 > 套用累積更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 從已經安裝的基準執行個體開始：SQL Server 2017 初始版本

2. 移至累積更新清單：[SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/) \(英文\)

3. 選取最新的累積更新。 可執行檔會自動下載並解壓縮。

4. 執行安裝程式。 接受授權條款，然後在 [特徵選取] 頁面上，檢閱已套用累積更新的功能。 您應該會看到針對目前執行個體安裝的每個功能，包括機器學習功能。 安裝程式會下載更新所有功能所需的 CAB 檔案。

   ![已安裝功能的摘要](media/cumulative-update-feature-selection.png)

5. 繼續執行精靈，並接受 R 和 Python 散發套件的授權條款。 

::: moniker-end

## <a name="additional-configuration"></a>其他組態

如果外部指令碼驗證步驟成功，您就可以從 SQL Server Management Studio、Visual Studio Code，或任何可以將 T-SQL 陳述式傳送到伺服器的其他用戶端來執行 R 或 Python 命令。

如果您在執行命令時遇到錯誤，請檢閱此節中的其他設定步驟。 您可能需要對服務或資料庫進行其他適當的設定。

在執行個體層級，其他設定可能包括：

* [SQL Server 機器學習服務的防火牆設定](../../advanced-analytics/security/firewall-configuration.md)
* [啟用其他網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連線](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [為 SQLRUserGroup 建立登入](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [管理磁碟配額](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)，以避免外部指令碼執行耗盡磁碟空間的工作

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
在 Windows 上的 SQL Server 2019 中，隔離機制已經變更。 這會影響 **SQLRUserGroup**、防火牆規則、檔案權限，以及隱含驗證。 如需詳細資訊，請參閱[機器學習服務的隔離變更](sql-server-machine-learning-services-2019.md)。
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

在資料庫上，您可能需要下列設定更新：

* [授與使用者 SQL Server 機器學習服務的權限](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> 是否需要其他設定取決於您的安全性架構、SQL Server 的安裝位置，以及預期使用者如何連線至資料庫並執行外部指令碼。

## <a name="suggested-optimizations"></a>建議的最佳化

既然一切正常，您可能還需要最佳化伺服器以支援機器學習，或安裝預先定型模型。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您預期會有許多使用者同時執行指令碼，您可以增加指派給 Launchpad 服務的背景工作者帳戶數目。 如需詳細資訊，請參閱[在 SQL Server 機器學習服務中調整外部指令碼的同時執行](../administration/scale-concurrent-execution-external-scripts.md)。
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>最佳化伺服器以執行指令碼

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的預設設定是為了最佳化伺服器的平衡，以處理資料庫引擎支援的各種服務，其中可能包含解壓縮、轉換和載入 (ETL) 程序、報告、稽核，以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的應用程式。 因此，在預設設定下，您可能會發現機器學習的資源有時會受到限制或遭遇瓶頸，尤其是需要大量記憶體的作業。

為確保機器學習優先處理且獲得適當的資源，建議您使用 SQL Server 資源管理員設定外部資源集區。 您也可能想要變更配置給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎的記憶體量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務下所執行的帳戶數目。

- 若要設定用來管理外部資源的資源集區，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更為資料庫保留的記憶體量，請參閱[伺服器記憶體設定選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 可以啟動的 R 帳戶數目，請參閱[在 SQL Server 機器學習服務中調整外部指令碼的同時執行](../administration/scale-concurrent-execution-external-scripts.md)。

如果您使用標準版且沒有「資源管理員」，則可以使用「動態管理檢視 (DMV)」與「擴充事件」，以及 Windows 事件監視，以協助管理伺服器資源。 如需詳細資訊，請參閱[監視及管理 R Services](../r/managing-and-monitoring-r-solutions.md) 和[監視及管理 Python Services](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-python-and-r-packages"></a>安裝額外的 Python 和 R 套件

您為 SQL Server 建立的 Python 和 R 解決方案可以呼叫基本函式、與 SQL Server 一起安裝的專屬套件中的函式，以及與 SQL Server 所安裝的開放原始碼 Python 和 R 版本相容的協力廠商套件。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您在電腦上有分開安裝的 Python 或 R，或者如果您將套件安裝到使用者程式庫，則無法從 T-SQL 使用這些套件。

若要安裝及管理其他套件，您可以將使用者群組設定為在每個資料庫層級上共用套件，或設定資料庫角色以讓使用者安裝自己的套件。 如需詳細資訊，請參閱[安裝 Python 套件](../package-management/install-additional-python-packages-on-sql-server.md)和[安裝新的 R 套件](../package-management/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。
