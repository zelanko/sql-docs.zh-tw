---
title: 在 Windows 上安裝 SQL Server Machine Learning 服務 (資料庫內)
description: SQL Server 或 Python 中的 R, 適用于 Windows 上 SQL Server Machine Learning 服務的 SQL Server 安裝步驟。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fba13ea5d6d91ab83cb2560727ed75c79bc4c48b
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531050"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>在 Windows 上安裝 SQL Server Machine Learning 服務

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式, 並遵循螢幕上的提示來安裝機器學習服務元件。

## <a name="bkmk_prereqs"></a>預先安裝檢查清單

+ 如果您想要安裝具有 R 或 Python 語言支援的 Machine Learning 服務, 則需要 SQL Server 2017 (或更新版本) 安裝程式。 如果您改為 SQL Server 2016 安裝媒體, 您可以安裝[SQL Server R Services (資料庫內)](sql-r-services-windows-install.md)來取得 R 語言支援。

+ 需要資料庫引擎實例。 您不能只安裝 R 或 Python 功能, 雖然您可以將它們累加新增至現有的實例。

+ 針對商務持續性, Machine Learning 服務支援[Always On 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。 您必須在每個節點上安裝 Machine Learning 服務, 以及設定套件。

+ SQL Server 2017 中的容錯移轉叢集上*不支援*安裝 Machine Learning 服務。 不過, SQL Server 2019*支援*。 
 
+ 請勿在網域控制站上安裝 Machine Learning 服務。 安裝程式的 Machine Learning 服務部分將會失敗。

+ 請勿在執行同資料庫實例的同一部電腦上安裝**共用功能** >  **Machine Learning Server (獨立式)** 。 獨立伺服器會競爭相同的資源, 破壞這兩個安裝的效能。

+ 支援與其他 R 和 Python 版本並存安裝, 但不建議這麼做。 這是受支援的原因, 因為 SQL Server 實例會使用自己的開放原始碼 R 和 Anaconda 發行版本複本。 但不建議您這樣做, 因為在 SQL Server 外的 SQL Server 電腦上執行使用 R 和 Python 的程式碼可能會導致各種問題:
    
  + 您可以使用不同的程式庫和不同的可執行檔, 並取得不同的結果, 而不是在 SQL Server 中執行。
  + 在外部程式庫中執行的 R 和 Python 腳本無法由 SQL Server 管理, 因而導致資源競爭。
  
> [!IMPORTANT]
> 安裝完成之後, 請務必完成本文中所述的後續設定步驟。 這些步驟包括讓 SQL Server 使用外部腳本, 以及新增 SQL Server 執行 R 和 Python 作業所需的帳戶。 設定變更通常需要重新開機實例, 或重新開機啟動列服務。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2017 的安裝程式。 
  
2. 在 [**安裝**] 索引標籤上, 選取 [**新增 SQL Server 獨立安裝或將功能加入至現有安裝**]。

   ![新的 SQL Server 獨立安裝](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在 [特徵選取] 頁面上，選取下列選項：
  
    -   **Database Engine 服務**
  
         若要搭配 SQL Server 使用 R 和 Python, 您必須安裝 database engine 的實例。 您可以使用預設或已命名的實例。
  
    -   **Machine Learning Services (資料庫內)**
  
         此選項會安裝支援 R 和 Python 腳本執行的資料庫服務。

    -   **R**

        核取此選項可新增 Microsoft R 封裝、解譯器和開放原始碼 R。 

    -   **Python**

        核取此選項可新增 Microsoft Python 套件、Python 3.5 可執行檔, 以及從 Anaconda 發佈選取程式庫。
        
        ![R 和 Python 的功能選項](media/2017setup-features-page-mls-rpy.png "Python 的安裝選項")

        > [!NOTE]
        > 
        > 請勿選取 [ **Machine Learning Server (獨立式)** ] 選項。 在 [**共用功能**] 下安裝 Machine Learning Server 的選項, 是要在另一部電腦上使用。

4. 在 [**同意安裝 R** ] 頁面上, 選取 [**接受**]。 本授權合約涵蓋 Microsoft R Open, 其中包含開放原始碼 R 基底套件和工具的散發, 以及來自 Microsoft 開發小組的增強型 R 套件和連線提供者。

5. 在 [**同意安裝 Python** ] 頁面上, 選取 [**接受**]。 Python 開放原始碼授權合約也涵蓋 Anaconda 和相關工具, 以及 Microsoft 開發小組的一些新 Python 程式庫。
     
     ![Python 授權的合約](media/2017setup-python-license.png "Python 的授權合約")
  
    > [!NOTE]
    >  如果您使用的電腦沒有網際網路存取權, 您可以在此時暫停安裝程式, 以分別下載安裝程式。 如需詳細資訊, 請參閱[安裝沒有網際網路存取的機器學習服務元件](../install/sql-ml-component-install-without-internet-access.md)。
  
     選取 [**接受**], 等到 [**下一步]** 按鈕變成作用中狀態, 然後選取 **[下一步]** 。
  
6. 在 [**準備安裝**] 頁面上, 確認包含這些選項, 然後選取 [**安裝**]。
  
    + Database Engine 服務
    + Machine Learning 服務 (資料庫內)
    + R 或 Python, 或兩者

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

## <a name="enable-script-execution"></a>啟用腳本執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以從這個頁面下載並安裝適當的版本:[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > 您也可以使用[Azure Data Studio](../../azure-data-studio/what-is.md), 以支援 SQL Server 的系統管理工作和查詢。
  
2. 連接到您安裝 Machine Learning Services 的實例, 按一下 [追加**查詢**] 以開啟查詢視窗, 然後執行下列命令:

    ```sql
    sp_configure
    ```

    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為功能預設是關閉的。 系統管理員必須明確地啟用此功能, 才能執行 R 或 Python 腳本。
    
3.  若要啟用外部腳本功能, 請執行下列語句:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果您已啟用 R 語言的功能, 請不要再次執行 Python 的重新設定。 基礎擴充性平臺支援這兩種語言。

## <a name="restart-the-service"></a>重新啟動服務

當安裝完成時, 請重新開機資料庫引擎, 然後繼續進行下一步, 啟用腳本執行。

重新開機服務也會自動重新開機[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]相關的服務。

您可以使用 SSMS 中實例的右鍵 [**重新開機**] 命令, 或使用 [控制台] 中的 [**服務**] 面板, 或使用 [ [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)] 來重新開機服務。

## <a name="verify-installation"></a>確認安裝

在 [[自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)] 或 [安裝記錄檔] 中檢查實例的安裝狀態。

請使用下列步驟來確認用來啟動外部腳本的所有元件都在執行中。

1. 在 SQL Server Management Studio 中, 開啟新的查詢視窗, 然後執行下列命令:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。
    
2. 開啟 [**服務**] 面板或 SQL Server 組態管理員, 並確認**SQL Server Launchpad 服務**正在執行。 針對每個已安裝 R 或 Python 的資料庫引擎實例, 您應該會有一個服務。 如需服務的詳細資訊, 請參閱擴充性[架構](../concepts/extensibility-framework.md)。 
   
3. 如果啟動控制板正在執行, 您應該能夠執行簡單的 R 和 Python 腳本, 以確認外部腳本執行時間可以與 SQL Server 通訊。

   在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]開啟新的**查詢**視窗, 然後執行如下所示的腳本:
    
    + 適用于 R
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + 適用于 Python
    
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

    當第一次載入外部腳本執行時間時, 腳本可能需要一些時間才能執行。 結果應該如下所示:

    | hello |
    |----|
    | 1|

> [!NOTE]
> 根據設計, 不會傳回 Python 腳本中使用的資料行或標題。 若要為您的輸出新增資料行名稱, 您必須指定傳回資料集的架構。 若要這麼做, 請使用預存程式的 WITH RESULTS 參數、命名資料行, 並指定 SQL 資料類型。
> 
> 例如, 您可以加入下面這一行來產生任意的資料行名稱:`WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累計更新套用至資料庫引擎和機器學習服務元件。

在連線到網際網路的裝置上, 累積更新通常會透過 Windows Update 套用, 但您也可以使用下列步驟來進行受控制的更新。 當您套用資料庫引擎的更新時, 安裝程式會針對您安裝在相同實例上的任何 R 或 Python 功能提取累計更新。 

在中斷連線的伺服器上, 需要額外的步驟。 如需詳細資訊, 請參閱[在沒有網際網路存取的電腦上安裝 > 套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 從已安裝的基準實例開始:SQL Server 2017 初始版本

2. 移至累計更新清單:[SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 選取最新的累計更新。 可執行檔會自動下載並解壓縮。

4. 執行安裝程式。 接受授權條款, 然後在 [特徵選取] 頁面上, 檢查已套用累積更新的功能。 您應該會看到針對目前實例安裝的每項功能, 包括機器學習功能。 安裝程式會下載更新所有功能所需的封包檔。

  ![已安裝功能的摘要](media/cumulative-update-feature-selection.png)

5. 繼續執行嚮導, 並接受 R 和 Python 散發套件的授權條款。 

## <a name="additional-configuration"></a>其他組態

如果外部腳本驗證步驟成功, 您可以從 SQL Server Management Studio、Visual Studio Code 或任何其他可將 T-sql 語句傳送至伺服器的用戶端執行 R 或 Python 命令。

如果您在執行命令時遇到錯誤, 請參閱本節中的其他設定步驟。 您可能需要對服務或資料庫進行其他適當的設定。

在實例層級, 其他設定可能包括:

* [SQL Server Machine Learning 服務的防火牆設定](../../advanced-analytics/security/firewall-configuration.md)
* [啟用其他網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連線](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [建立 SQLRUserGroup 的登入](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [管理磁片配額](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas), 以避免外部腳本執行耗盡磁碟空間的工作

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
在 Windows 上的 SQL Server 2019 中, 隔離機制已經變更。 這會影響**SQLRUserGroup**、防火牆規則、檔案許可權, 以及隱含的驗證。 如需詳細資訊, 請參閱[Machine Learning 服務的隔離變更](sql-server-machine-learning-services-2019.md)。
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

在資料庫上, 您可能需要下列設定更新:

* [授與使用者 SQL Server Machine Learning 服務的許可權](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> 是否需要額外的設定, 取決於您的安全性架構、您安裝 SQL Server, 以及您希望使用者如何連接到資料庫並執行外部腳本。

## <a name="suggested-optimizations"></a>建議的優化

現在您已有所有工作, 您可能也會想要優化伺服器以支援機器學習服務, 或安裝預先定型模型。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您預期有許多使用者同時執行腳本, 您可以增加指派給啟動列服務的背景工作帳戶數目。 如需詳細資訊, 請參閱[修改 SQL Server Machine Learning 服務的使用者帳戶集](../administration/modify-user-account-pool.md)區。
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>優化伺服器以執行腳本

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式的預設設定是針對資料庫引擎支援的各種服務優化伺服器的平衡, 其中可能包括解壓縮、轉換和載入 (ETL) 程式、報告、審核, 以及使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料的應用程式。 因此, 在預設設定下, 您可能會發現機器學習服務的資源有時候會受到限制或節流, 特別是在需要大量記憶體的作業中。

若要確保機器學習作業的優先順序和適當地設定資源, 建議您使用 SQL Server Resource Governor 來設定外部資源集區。 您也可能想要變更配置給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎的記憶體數量, 或增加[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]在服務下執行的帳戶數目。

- 若要設定用來管理外部資源的資源集區, 請參閱[建立外部資源集](../../t-sql/statements/create-external-resource-pool-transact-sql.md)區。
  
- 若要變更為資料庫保留的記憶體數量, 請參閱[伺服器記憶體設定選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以啟動[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]的 R 帳戶數目, 請參閱[修改機器學習服務的使用者帳戶集](../administration/modify-user-account-pool.md)區。

如果您使用的是 Standard Edition, 而且沒有 Resource Governor, 您可以使用動態管理檢視 (Dmv) 和擴充事件, 以及 Windows 事件監視來協助管理伺服器資源。 如需詳細資訊, 請參閱[監視和管理 R 服務](../r/managing-and-monitoring-r-solutions.md)和[監視和管理 Python 服務](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他 R 套件

您為 SQL Server 建立的 R 解決方案可以呼叫基本的 R 函式、與 SQL Server 一起安裝之專屬套件的函式, 以及與 SQL Server 所安裝的開放原始碼 R 版本相容的協力廠商 R 套件。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您在電腦上個別安裝 R, 或如果您已將套件安裝至使用者程式庫, 則無法從 T-sql 使用這些套件。

若要安裝和管理 R 封裝, 您可以將使用者群組設定為在每個資料庫層級上共用封裝, 或設定資料庫角色以讓使用者安裝自己的封裝。 如需詳細資訊, 請參閱[在 SQL Server 中安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。
