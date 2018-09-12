---
title: 安裝 SQL Server 2016 R Services （資料庫） |Microsoft Docs
description: 當您在 Windows 上安裝 SQL Server 2016 R Services 使用 SQL Server 中的 R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4df8391974214452c6b8b3226c3c9a845e4b556b
ms.sourcegitcommit: 8008ea52e25e65baae236631b48ddfc33014a5e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2018
ms.locfileid: "44311678"
---
# <a name="install-sql-server-2016-r-services"></a>安裝 SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何安裝和設定**SQL Server 2016 R Services**。 如果您有 SQL Server 2016 時，安裝此功能以啟用 SQL Server 中的 R 程式碼執行。

在 SQL Server 2017 中，提供 R 整合[Machine Learning 服務](../r/r-server-standalone.md)，反映的 Python。 如果您的 R 整合，並讓 SQL Server 2017 安裝媒體，請參閱[安裝 SQL Server 2017 Machine Learning 服務](sql-machine-learning-services-windows-install.md)新增功能。 

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

+ 需要資料庫引擎執行個體。 雖然您可以將它以累加方式加入現有的執行個體，您無法安裝只是 R。

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

 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

## <a name="bkmk2016top"></a>執行安裝程式

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


##  <a name="bkmk_enableFeature"></a>啟用指令碼執行

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以下載並安裝適當版本，從這個頁面：[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 您也可以試試預覽版[SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)，其支援的系統管理工作和 SQL Server 查詢。
  
2. 連接到您安裝 Machine Learning 服務的執行個體，請按一下**新的查詢**開啟查詢視窗中，並執行下列命令：

   ```SQL
   sp_configure
   ```
    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為預設關閉的功能。 您可以執行 R 或 Python 指令碼之前，此功能，必須明確啟用由系統管理員。
     
3. 若要啟用外部指令碼的功能，請執行下列陳述式：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新啟動服務

安裝完成後，重新啟動 database engine，再繼續下一步，啟用指令碼執行。

重新啟動服務時，也會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

您可以重新啟動服務，使用滑鼠右鍵**重新啟動**命令，在 SSMS 中，或使用之執行個體**Services**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>確認安裝

使用下列步驟，確認用來啟動外部指令碼的所有元件正在都執行。

1. 在 SQL Server Management Studio 中，開啟新的查詢視窗中，並執行下列命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。

2. 開啟**Services**面板或 SQL Server 組態管理員，並確認**SQL Server Launchpad 服務**正在執行。 您應該有一項服務，每個資料庫引擎執行個體具有 R 或 Python 安裝。 如需有關服務的詳細資訊，請參閱[Extensibility framework](../concepts/extensibility-framework.md)。

7. 如果 Launchpad 正在執行，您應該能夠執行簡單的 R，以確認外部指令碼的執行階段可與 SQL Server 通訊。 

    開啟新**查詢** 視窗中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行指令碼，如下所示：
    
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

如果外部指令碼驗證步驟成功，您可以從 SQL Server Management Studio、 Visual Studio Code 中或任何其他用戶端可以傳送至伺服器的 T-SQL 陳述式來執行 Python 命令。

如果執行命令時，您會收到錯誤，請檢閱本節中的其他設定步驟。 您可能需要對服務或資料庫中的其他適當的組態。

需要進行其他變更的常見案例包括：

* [設定傳入連接的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [啟用額外的網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [擴充內建的權限給遠端使用者](#bkmk_configureAccounts)
* [授與權限來執行外部指令碼](#bkmk_AllowLogon)
* [授與存取權，對個別的資料庫](#permissions-db)

> [!NOTE]
> 並非所有列出的變更是必要的而且沒有任何可能需要。 需求取決於您的安全性結構描述，您可在此安裝 SQL Server，和您預期使用者會連線到資料庫並執行外部指令碼的方式。 這裡可以找到其他疑難排解提示：[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>啟用為 Launchpad 帳戶群組的隱含的驗證

在安裝期間，建立一些新的 Windows 使用者帳戶來執行工作的安全性權杖下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務。 當使用者從外部用戶端傳送 R 指令碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動可用的工作者帳戶、 將它對應至呼叫的使用者的身分識別和執行 R 指令碼，以代表使用者。 這項新的資料庫引擎服務支援安全執行外部指令碼，稱之為*隱含的驗證*。

您可以檢視這些帳戶中的 Windows 使用者群組**SQLRUserGroup**。 根據預設，會建立 20 個背景工作帳戶，而這通常是足以適用於執行 R 作業。

不過，如果您需要從遠端資料科學用戶端執行 R 指令碼，並使用 Windows 驗證，您必須授與這些工作者帳戶來登入的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表您的執行個體。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性] ，以滑鼠右鍵按一下 [登入] ，然後選取 [新增登入] 。
2. 在 **登入-新增**對話方塊中，選取**搜尋**。
3. 選取 **物件的型別**並**群組**核取方塊，然後清除其他所有核取方塊。
4. 按一下 **進階**，確認要搜尋的位置是目前的電腦，然後按一下**立即尋找**。
5. 捲動清單，直到您找到一開始在伺服器上的群組帳戶的`SQLRUserGroup`。
    
    + Launchpad 服務相關聯的群組名稱_預設執行個體_只是一律**SQLRUserGroup**。 選取此帳戶僅針對預設執行個體。
    + 如果您使用_具名執行個體_，執行個體名稱會附加至預設名稱， `SQLRUserGroup`。 因此，如果您的執行個體名稱為"MLTEST 」，這個執行個體的預設使用者群組名稱會是**SQLRUserGroupMLTest**。
5. 按一下 **確定**以關閉 進階的搜尋 對話方塊中，並確認您已選取正確的帳戶，執行個體。 每個執行個體可以使用只有自己的 Launchpad 服務並為該服務建立的群組。
6. 按一下 [ **[確定]** 以關閉**選取使用者或群組**] 對話方塊。
7. 在 [**登入-新增**] 對話方塊中，按一下**確定**。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

### <a name="bkmk_AllowLogon"></a>給予使用者執行外部指令碼的權限

> [!NOTE]
> 如果您使用 SQL 登入的 SQL Server 計算內容中執行 R 指令碼，就不需要此步驟。

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中您自己的執行個體，您通常執行指令碼身為管理員，或至少是資料庫擁有者，因此會有不同的作業時，資料庫，它能夠在安裝新套件中的所有資料的隱含權限視需要。

不過，在企業案例中，大部分的使用者，包括使用 SQL 登入，來存取資料庫的使用者沒有這類更高的權限。 因此，每個使用者將執行 R 指令碼，您必須授與使用者權限，其中將使用外部指令碼中的每個資料庫執行指令碼。

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 需要安裝協助嗎？ 不確定是否執行了所有步驟嗎？ 若要檢查安裝狀態，並執行其他步驟中使用這些自訂報表。 
> 
> [監視使用的自訂報表的 Machine Learning 服務](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

### <a name="permissions-db"></a> 提供您的使用者讀取、 寫入或 DDL 」 權限的資料庫

用來執行 R 的使用者帳戶可能需要讀取資料與其他資料庫中，建立新的資料表來儲存結果，及將資料寫入至資料表。 因此，對於要執行 R 指令碼每個使用者，請確定使用者具有資料庫的適當的權限： *db_datareader*， *db_datawriter*，或*db_ddladmin*.

例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 SQL 登入 *MySQLLogin* 在 *RSamples* 資料庫中執行 T-SQL 查詢的權限。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

如需包含在每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源

如果您在資料科學用戶端電腦上建立 R 解決方案，並且需要使用 SQL Server 電腦當作計算內容中執行程式碼，您可以使用 SQL 登入或整合式的 Windows 驗證。

* 針對 SQL 登入：確定此登入擁有您要讀取資料之資料庫的適當權限。 則可以藉由新增*連接到*並*選取*權限，或藉由新增登入*db_datareader*角色。 針對要建立物件的登入、 新增*DDL_admin*權限。 登入，必須將資料儲存至資料表，新增的登入*db_datawriter*角色。

* Windows 驗證： 您可能需要指定執行個體名稱和其他連接資訊的資料科學用戶端上設定 ODBC 資料來源。 如需詳細資訊，請參閱 < [ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建議的最佳化

既然您已使用的所有項目，您也可以在最佳化的伺服器，以支援機器學習服務，或安裝預先定型的模型。

### <a name="add-more-worker-accounts"></a>新增更多的背景工作帳戶

如果您認為您可能會經常使用 R，或如果您預期有許多使用者同時執行指令碼，您可以增加指派給 Launchpad 服務的工作者帳戶數目。 如需詳細資訊，請參閱 <<c0> [ 修改 SQL Server Machine Learning 服務的使用者帳戶集區](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="bkmk_optimize"></a>最佳化執行外部指令碼伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式為了最佳化伺服器的平衡，針對各種服務所支援的資料庫引擎，其中可能包括擷取、 轉換和載入 (ETL) 程序、 報告、 稽核和使用應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。 因此，如果在預設設定下，您可能會發現適用於 machine learning 資源，有時限制或進行節流處理，尤其是需要大量記憶體的作業。

若要確保機器學習服務工作，優先處理且獲得適當的資源，我們建議您使用 SQL Server 資源管理員，來設定外部資源集區。 您也可以變更配置的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database engine、 或增加下執行的帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

- 若要設定資源集區來管理外部的資源，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更的資料庫保留的記憶體數量，請參閱[伺服器記憶體組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以啟動的 R 帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，請參閱 <<c2> [ 修改機器學習服務的使用者帳戶集區](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用 Standard Edition，而且沒有資源管理員，您可以使用動態管理檢視 (Dmv) 和擴充的事件，以及 Windows 事件監視，以協助您管理伺服器資源所使用的。如需詳細資訊，請參閱 <<c0> [ 監視和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他 R 套件

建立適用於 SQL Server 的 R 解決方案，可以呼叫基本 R 函式，函式與 SQL Server 一起安裝的專屬套件與第三方 R 套件開放原始碼 R 的 SQL Server 安裝的版本相容。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您有 R 的強大功能的個別安裝的電腦上，或如果您將套件安裝到使用者程式庫，您將無法使用 T-SQL 的那些套件。

安裝和管理 R 套件的程序是 SQL Server 2016 和 SQL Server 2017 中的不同。 在 SQL Server 2016 中，資料庫管理員必須安裝使用者所需的 R 套件。 在 SQL Server 2017 中，您可以設定使用者群組，共用每個資料庫層級上的封裝，或設定資料庫角色，以讓使用者安裝自己的封裝。 如需詳細資訊，請參閱 <<c0> [ 安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。


## <a name="get-help"></a>取得說明

需要安裝或升級的說明嗎？ 如需常見問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查的執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [適用於 R 開發人員教學課程： 在資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。


