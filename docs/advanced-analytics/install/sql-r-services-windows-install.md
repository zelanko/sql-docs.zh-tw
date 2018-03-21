---
title: "安裝 SQL Server 2016 R Services （資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 SQL Server R 服務"
- "安裝 SQL Server 機器學習服務"
- "設定 R 服務"
- "安裝 SQL 機器學習服務"
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Active
ms.openlocfilehash: 0012b48101085b7ccb18695fbda1f25c10a6b90b
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2016-r-services-in-database"></a>安裝 SQL Server 2016 R 服務 (資料庫內) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何安裝及設定**SQL Server 2016 R 服務 （資料庫）**。 如果您有 SQL Server 2016 時，安裝此功能以啟用 SQL Server 中的 R 程式碼執行。

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

+ 需要 SQL Server 2016。 如果您有 SQL Server 2016，請安裝[SQL Server 2017 機器學習服務 （資料庫）](sql-machine-learning-services-windows-install.md)改為。

+ 需要資料庫引擎執行個體。 您無法安裝只 R，雖然您可以將它以累加方式加入現有的執行個體。

+ 請勿在容錯移轉叢集上安裝 R Services。 用來隔離 R 處理序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝 R Services。 安裝程式的 R 服務部分將會失敗。

+ 請勿安裝**共用功能** > **R 伺服器 （獨立）**同一部電腦上執行資料庫中執行個體。 

+ 與其他版本的 R，並將 Python 的並存安裝，可能會因為 SQL Server 執行個體使用的開放原始碼 R 和 Anaconda 發佈其本身複本。 不過，執行 SQL Server 外部的 SQL Server 電腦使用 R，並將 Python 程式碼可能會導致各種問題：
    
  + 您使用不同的程式庫和其他可執行檔，並比您執行 SQL Server 中時，取得不同的結果。
  + 執行外部程式庫中的 R，並將 Python 指令碼不受 SQL Server，導致資源爭用的情況。
  
如果您使用任何舊版的 Revolution Analytics 開發環境或 RevoScaleR 封裝，或是如果您已安裝 SQL Server 2016 的任何發行前版本，您就必須將它們解除安裝。 不支援執行舊版與新版的 RevoScaleR 與其他專屬的封裝版本。 正在移除舊版的說明，請參閱[升級及安裝常見問題集，SQL Server 機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安裝程式完成之後，請務必完成本文中所述的其他後置組態步驟。 這些步驟包括啟用 SQL Server 以使用外部指令碼，並加入您的名義上執行 R 工作的 SQL Server 所需的帳戶。 組態變更通常需要重新啟動的執行個體或啟動控制板服務重新啟動。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

## <a name="bkmk2016top"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2016 安裝程式精靈。

2. 在**安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入現有安裝**。
    
   ![安裝 R 服務 （資料庫）](media/2016-setup-installation-rsvcs.png "與 R Services 啟動 database engine 安裝")
   
3. 在**特徵選取**頁面上，選取下列選項：

   - 選取**Database Engine Services**。 需要資料庫引擎使用機器學習的每個執行個體。
   - 選取**R 服務 （資料庫）**。 安裝 r 的資料庫中使用的支援
    
     ![R 服務特徵選取](media/2016setup-rsvcs-features.png "選取這些功能的 R 服務資料庫")

    > [!IMPORTANT]
    > 請勿安裝 R Server 和 R 服務的方法，在相同的時間。 一般來說，您會安裝 R Server （獨立） 建立環境的資料科學家或開發人員用來連接到 SQL Server 和部署 R 解決方案。 因此，不需要在相同的電腦上同時安裝 R Server 和 R Services。

4.  在**同意安裝 Microsoft R Open**頁面上，按一下**接受**。
  
    此授權合約，才能下載 Microsoft R Open，其中包含開放原始碼 R 基底套件與工具，以及增強的 R 封裝和連線提供者，從 Microsoft R 開發小組的散佈。
  
5. 您接受授權合約之後，會短暫的暫停時，安裝程式已準備就緒。 按一下**下一步**當按鈕會變成可用。

6. 在**安裝準備就緒**頁面上，確認下列項目都包含在內，然後選取**安裝**。

   + Database Engine 服務
   + R Services (資料庫內)

    記下位置的路徑下的資料夾`..\Setup Bootstrap\Log`儲存組態檔。 安裝完成時，您可以檢閱摘要檔案中已安裝的元件。

7. 安裝完成時，重新啟動電腦。

##  <a name="bkmk_enableFeature"></a>啟用外部指令碼執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以下載並安裝適當版本，從這個頁面：[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 您也可以試用預覽版本的[SQL 作業 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)，可支援 SQL Server 查詢和管理工作。
  
2. 連接到機器學習服務安裝的執行個體，請按一下**新查詢**開啟查詢視窗中，並執行下列命令：

   ```SQL
   sp_configure
   ```
    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為預設關閉的功能。 您可以執行 R 或 Python 指令碼之前，此功能，必須明確啟用由系統管理員。
     
3. 若要啟用外部指令碼處理功能，請執行下列陳述式：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新啟動服務

當安裝完成時，繼續下一步，啟用指令碼執行之前，先重新啟動資料庫引擎。

重新啟動服務時，也會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

您可以重新啟動服務，使用滑鼠右鍵**重新啟動**命令，在 SSMS 中，或使用的執行個體的**服務**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>確認安裝

使用下列步驟，確認所有元件，用來啟動外部指令碼正在都執行。

1. 在 SQL Server Management Studio，開啟新查詢視窗中，並執行下列命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。

2. 開啟**服務**面板或 SQL Server 組態管理員，並確認**SQL Server Launchpad 服務**正在執行。 您應該有一個適用於每個資料庫引擎執行個體具有 R 服務，或 Python 安裝。 如果未執行，請重新啟動服務。 如需詳細資訊，請參閱[元件來支援 Python 整合](../python/new-components-in-sql-server-to-support-python-integration.md)。

7. 如果 [啟動列] 正在執行，您應該能夠執行簡單的 R 確認外部指令碼的執行階段可以使用 SQL Server 進行通訊。 

    開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行指令碼，如下所示：
    
    ```SQL
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

## <a name="bkmk_FollowUp"></a> 其他設定

如果執行外部指令碼驗證步驟成功，您可以從 SQL Server Management Studio、 Visual Studio 程式碼或其他任何可以傳送至伺服器的 T-SQL 陳述式的用戶端執行 Python 指令。

如果您在執行命令時出現錯誤，請檢閱本節中的其他組態步驟。 您可能需要進行其他適當的組態服務或資料庫。

常見的案例，需要進行其他變更包括：

* [設定傳入連接的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [啟用額外的網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [擴充內建權限給遠端使用者](#bkmk_configureAccounts)
* [授與權限來執行外部指令碼](#bkmk_AllowLogon)
* [授與存取權的個別資料庫](#permissions-db)

> [!NOTE]
> 並非所有列出的變更是必要的並且不可能會需要。 需求取決於您的安全性結構描述，您安裝 SQL Server，然而您預期使用者連線到資料庫並執行外部指令碼的方式。 可以在這裡找到其他疑難排解提示：[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>啟用 [啟動列] 帳戶群組的隱含的驗證

在安裝期間，某些新的 Windows 使用者帳戶建立執行工作的安全性 token 下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務。 當使用者從外部用戶端傳送的 R 指令碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動可用工作者帳戶、 將它對應至在呼叫的使用者的身分識別和執行 R 指令碼，以代表使用者。 Database engine 的這個新服務支援安全執行外部指令碼，呼叫*隱含的驗證*。

您可以檢視這些帳戶中的 Windows 使用者群組**SQLRUserGroup**。 根據預設，會建立 20 個背景工作帳戶，這通常是超過不足以執行 R 工作。

不過，如果您需要從遠端資料科學用戶端執行 R 指令碼，並使用 Windows 驗證，您必須授與這些背景工作帳戶登入的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代替您執行個體。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性] ，以滑鼠右鍵按一下 [登入] ，然後選取 [新增登入] 。
2. 在**登入-新增**對話方塊中，選取**搜尋**。
3. 選取**物件類型**和**群組**核取方塊，然後清除其他所有核取方塊。
4. 按一下**進階**，確認要搜尋的位置是目前的電腦，然後按一下**立即尋找**。
5. 捲動清單，直到您找到一開始在伺服器上的群組帳戶的`SQLRUserGroup`。
    
    + 群組為 Launchpad 服務相關聯的名稱_預設執行個體_只是一律**SQLRUserGroup**。 選取此帳戶僅針對預設執行個體。
    + 如果您使用_具名執行個體_，執行個體名稱會附加至的預設名稱， `SQLRUserGroup`。 因此，如果您的執行個體的名稱為"MLTEST"，這個執行個體的預設使用者群組名稱會是**SQLRUserGroupMLTest**。
5. 按一下**確定**以關閉 [進階的搜尋] 對話方塊中，並確認您已選取正確的帳戶，執行個體。 每個執行個體可以使用只有自己 Launchpad 服務並為該服務建立的群組。
6. 按一下**確定**以關閉 [**選取使用者或群組**] 對話方塊。
7. 在**登入-新增**對話方塊中，按一下 **確定**。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

### <a name="bkmk_AllowLogon"></a>提供使用者執行外部指令碼的權限

> [!NOTE]
> 如果您使用 SQL 登入 SQL Server 計算內容中執行 R 指令碼時，就不需要此步驟。

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在您自己的執行個體，通常執行指令碼身為管理員，或至少是資料庫擁有者，因此會有不同的作業、 在資料庫中，並且能夠安裝新的封裝中的所有資料的隱含權限視需要。

不過，在企業案例中，大部分的使用者，包括使用 SQL 登入、 存取資料庫的使用者沒有這類較高的權限。 因此，每個使用者執行 R 指令碼，您必須授與使用者權限來執行指令碼中每個資料庫將使用外部指令碼的位置。

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 需要安裝協助嗎？ 不確定是否執行了所有步驟嗎？ 使用這些自訂報表來檢查安裝狀態，並執行其他步驟。 
> 
> [監視使用自訂報表的機器學習服務](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

### <a name="permissions-db"></a> 提供您的使用者讀取、 寫入或 DDL 資料庫的權限

用來執行 R 的使用者帳戶可能需要從其他資料庫，讀取資料建立新的資料表來儲存結果，和寫入資料至資料表。 因此，每個使用者執行 R 指令碼，請確定使用者有適當的權限，在資料庫上： *db_datareader*， *db_datawriter*，或*db_ddladmin*.

例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 SQL 登入 *MySQLLogin* 在 *RSamples* 資料庫中執行 T-SQL 查詢的權限。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

如需包含每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源

如果您在資料科學用戶端電腦上建立 R 解決方案，而且需要使用 SQL Server 電腦當成計算內容中執行程式碼，您可以使用的 SQL 登入 」 或 「 整合式的 Windows 驗證。

* 針對 SQL 登入：確定此登入擁有您要讀取資料之資料庫的適當權限。 您可以藉由新增*連接到*和*選取*權限，或加入登入*db_datareader*角色。 針對要建立物件的登入、 新增*DDL_admin*權限。 登入，必須將資料儲存至資料表，請加入登入*db_datawriter*角色。

* Windows 驗證： 您可能需要在指定的執行個體名稱和其他連接資訊的資料科學用戶端上設定 ODBC 資料來源。 如需詳細資訊，請參閱[ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建議的最佳化

既然您已使用的所有項目，您也可以在最佳化伺服器以支援機器學習服務，或安裝預先定型的模型。

### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您認為您可能會有很大，使用 R，或者您預期許多使用者會同時為執行指令碼，您可以增加背景工作帳戶指派給 Launchpad 服務數目。 如需詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server 機器學習服務](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="bkmk_optimize"></a>最佳化執行外部指令碼伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式要取得最佳平衡伺服器的各種不同的服務所支援的資料庫引擎，其中可能包括擷取、 轉換及載入 (ETL) 處理序報告、 稽核和使用應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。 因此，在預設設定下，您可能會發現機器學習資源，有時限制或節流處理，特別是在需要大量記憶體的作業。

為了確保機器學習服務工作會設定優先權，並適當資源，我們建議您使用 SQL Server 資源管理員設定外部資源集區。 您也可以變更配置的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database engine、 或增加的帳戶下執行的數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

- 若要設定資源集區以便管理外部資源，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更保留給資料庫的記憶體數量，請參閱[伺服器記憶體組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以透過啟動的 R 帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，請參閱[修改使用者帳戶集區的機器學習](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用標準版，且沒有資源管理員，您可以使用動態管理檢視 (Dmv) 和擴充的事件，以及 Windows 事件監視，以協助管理伺服器資源所使用的。如需詳細資訊，請參閱[監視及管理 R 服務](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他的 R 封裝

建立 SQL Server R 方案可以呼叫基本的 R 函數，從 SQL Server，而第三方開放原始碼 R SQL Server 安裝的版本相容的 R 封裝安裝 properietary packes 函式。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您已經在電腦上個別安裝的 R，或者封裝安裝到使用者程式庫，您將無法使用 T-SQL 從這些封裝。

安裝和管理的 R 封裝的程序是在 SQL Server 2016 和 SQL Server 2017 不同。 在 SQL Server 2016 中，資料庫管理員必須安裝 R 封裝，使用者需要。 在 SQL Server 2017，您可以設定使用者群組共用每個資料庫層級上的封裝，或設定資料庫角色，才能讓使用者安裝自己的封裝。 如需詳細資訊，請參閱[封裝管理](../r/r-package-management-for-sql-server-r-services.md)。


## <a name="get-help"></a>取得說明

需要協助以安裝或升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。


