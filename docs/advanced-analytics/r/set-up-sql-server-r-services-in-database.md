---
title: "設定 SQL Server 機器學習服務 （資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 SQL Server R 服務"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 9b3449e8c1f19ee69b36107f3530eac80fae0227
ms.contentlocale: zh-tw
ms.lasthandoff: 09/29/2017

---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>設定 SQL Server 機器學習服務 （資料庫）

本主題描述如何使用 SQL Server 中的機器學習服務設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈。

**適用於：** SQL Server 2016 R 服務 （唯讀），SQL Server 2017 機器學習服務 （R 和 Python）

## <a name="machine-learning-options-in-sql-server-setup"></a>機器學習中 SQL Server 安裝程式選項

SQL Server 安裝程式會提供安裝機器學習的下列選項：

* 安裝機器學習服務與 SQL Server 資料庫

  此選項可讓您可以使用預存程序中執行 R 或 Python 指令碼。 您也可以使用遠端計算內容的 SQL Server 電腦的外部連線從執行的 R 或 Python 指令碼。

  若要安裝此選項：
  
  * 在 SQL Server 2016 中，選取**R 服務 （資料庫）**。
  * 在 SQL Server 2017，選取**機器學習服務 （資料庫）**。


* 安裝獨立的機器學習伺服器

  此選項會建立用於機器學習解決方案，不需要或使用 SQL Server 的開發環境。 因此，我們通常建議您安裝一個主控的 SQL Server 不同的電腦上的這個選項。 如需有關這個選項的詳細資訊，請參閱[建立獨立 R 伺服器](../r/create-a-standalone-r-server.md)。

安裝程序需要多個步驟，其中有些是選擇性。 選擇性的方面取決於兩者計劃如何使用機器學習和安全性環境的狀態。 

## <a name="bkmk_prereqs"></a>必要條件

*  請避免同時安裝 R Server 和 R 服務。 一般來說，您會安裝 R Server （獨立） 建立環境的資料科學家或開發人員用來連接到 SQL Server 和部署 R 解決方案。 因此，不需要在相同的電腦上同時安裝 R Server 和 R Services。

* 如果您使用任何舊版的 Revolution Analytics 開發環境或 RevoScaleR 封裝，或是如果您已安裝 SQL Server 2016 的任何發行前版本，您就必須將它們解除安裝。 不支援的並存安裝。 正在移除舊版的說明，請參閱[升級及安裝常見問題集，SQL Server R services](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

* 您無法在容錯移轉叢集上安裝機器學習服務。 原因是，用於隔離外部指令碼處理序的安全性機制不相容於 Windows Server 容錯移轉叢集環境。 因應措施，您可以執行下列其中一項：
    * 您可以使用複寫，將必要資料表複製到與 R Services 的獨立 SQL Server 執行個體。
    * 安裝[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，使用 AlwaysOn 可用性群組的一部分，而且在獨立電腦上。

> [!IMPORTANT]
> 安裝程式完成之後，一些額外的步驟啟用所需機器學習功能。 您可能也需要特定的資料庫使用者權限授與變更或設定帳戶，或設定的遠端資料科學用戶端。

##  <a name="bkmk_installExt"></a>步驟 1： 安裝的擴充性功能，然後選擇的機器學習語言

若要使用機器學習服務，您必須安裝 SQL Server 2016 或更新版本。 若要使用[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，無須資料庫引擎的至少一個執行個體。 您可以使用預設或具名執行個體。

1. 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。
  
    如需如何執行自動的安裝資訊，請參閱[自動安裝的 SQL Server R Services](../r/unattended-installs-of-sql-server-r-services.md)。
  
2. 在**安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入現有安裝**。
   
3. 在**特徵選取**頁面上，若要安裝 R 所使用的資料庫服務作業，並且安裝的擴充功能支援外部指令碼和處理序中，選取下列選項：
   
   **SQL Server 2016**
   - 選取**Database Engine Services**。
   - 選取**R 服務 （資料庫）**。

   **SQL Server 2017**
   - 選取**Database Engine Services**。
   - 選取**機器學習服務 （資料庫）**。
   - 選取至少一部機器學習若要啟用的語言。 您可以選取只 R，或者您可以加入 R 和 Python。
   
   > [!NOTE]
   > 如果您未選取 [R] 或 [Python 語言選項，安裝精靈正在安裝只能擴充性架構，其中包括 SQL Server 受信任的啟動列]，但不會安裝任何語言特有的元件。 這個選項適用於繫結 SQL Server 執行個體 R 或 Python Microsoft 現代生命週期原則的一部分。 如需詳細資訊，請參閱[升級 R Services 的執行個體使用 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

4.  在**同意安裝 Microsoft R Open**頁面上，選取**接受**。
  
     此授權合約，才能下載 Microsoft R Open，其中包含開放原始碼 R 基底套件與工具，以及增強的 R 封裝和連線提供者，從 Microsoft R 開發小組的散佈。
  
    > [!NOTE]
    >  如果您使用的電腦沒有網際網路存取，您可以暫停安裝程式此時下載安裝程式分別中所述[安裝 R 元件沒有網際網路存取](installing-ml-components-without-internet-access.md)。
  
5. 選取 **[下一步]**。

6. 在**安裝準備就緒**頁面上，確認下列項目都包含在內，然後選取**安裝**。

   **SQL Server 2017**
   - Database Engine 服務
   - Machine Learning 服務 (資料庫內)
   - R、 Python 或兩者

   **SQL Server 2016**
   - Database Engine 服務
   - R 服務 (資料庫內)

7. 安裝完成時，重新啟動電腦。

##  <a name="bkmk_enableFeature"></a>步驟 2： 啟用外部指令碼服務

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果未安裝，您可以重新執行 SQL Server 安裝精靈以開啟下載連結並安裝它。
  
2. 連線到機器學習，而安裝的執行個體，並執行下列命令：

   ```SQL
   sp_configure
   ```

    值**啟用外部指令碼**屬性現在應該**0**。 這是因為若要減少介面區，預設關閉的功能，而且必須由系統管理員明確地啟用。
     
3. 若要啟用外部指令碼處理功能，請執行下列陳述式：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 SQL Server 服務。 也會自動重新啟動 SQL Server 服務重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

    您可以藉由重新啟動服務**服務**面板控制台 中，或使用 SQL Server 組態管理員。

## <a name="bkmk_TestScript"></a>步驟 3： 確認指令碼執行本機運作

確認已啟用外部指令碼執行服務。

1. 在 SQL Server Management Studio，開啟 新**查詢**視窗，然後執行下列命令：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    **run_value** 現在應該設定為 1。
    
2. 開啟**服務**面板，並確認您的執行個體的啟動控制板服務正在執行。 如果您安裝多個執行個體，每個執行個體都有它自己的 Launchpad 服務。
   
3. 開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行簡單的 R 指令碼，如下所示：
  
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
  
    **結果**
  
    *hello* *1*
  
   如果命令執行時沒有發生錯誤，請移至下一個步驟。 如果您收到錯誤，取得一份一些常見的問題，請參閱[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

## <a name="bkmk_FollowUp"></a>步驟 4： 其他組態

根據 R 或 Python 您使用案例，您可能需要進行其他變更伺服器、 防火牆、 服務或資料庫權限所用的帳戶。 您必須進行的變更會因大小寫。

常見的案例，需要進行其他變更包括：

* 變更防火牆規則以允許 SQL Server 的傳入的連接。
* 啟用額外的網路通訊協定。
* 確定伺服器支援遠端連線。
* 啟用*隱含的驗證*，如果使用者從遠端的 R 開發終端機的 SQL Server 資料存取和使用 RODBC 封裝或其他 Microsoft 開放式資料庫連接 (ODBC) 提供者執行 R 程式碼。
* 賦予使用者有權執行 R 指令碼或使用資料庫。
* 修正導致無法與 Launchpad 服務通訊的安全性問題。
* 確保使用者可以執行 R 程式碼，或安裝封裝的權限。

> [!NOTE]
> 並非所有列出的變更可能需要。 不過，我們建議您先檢閱以查看它們是否適合您案例的所有項目。

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

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和您自己的執行個體中執行 R 指令碼，您通常會執行指令碼，身為管理員，或至少是資料庫擁有者，因此會有不同的作業、 資料庫和功能中的所有資料的隱含權限若要安裝新的 R 封裝做為所需。

不過，在企業案例中，大部分的使用者，包括使用 SQL 登入、 存取資料庫的使用者沒有這類較高的權限。 因此，每個使用者執行 R 或 Python 指令碼，您必須授與使用者權限來執行指令碼中每個資料庫將使用外部指令碼的位置。

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 需要安裝協助嗎？ 不確定是否執行了所有步驟嗎？ 請使用這些自訂報表檢查 R Services 的安裝狀態。 如需詳細資訊，請參閱 [使用自訂報表監視 R Services](monitor-r-services-using-custom-reports-in-management-studio.md)。

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>請確認 SQL Server 電腦支援遠端連線

如果您無法從遠端電腦連線，請檢查伺服器是否允許遠端連接。 預設有時會停用遠端連線。

也請確認防火牆是否允許 SQL Server 存取權。 根據預設，SQL Server 所使用的通訊埠通常會被防火牆封鎖。 如果您使用 Windows 防火牆，請參閱[設定用於 database engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>提供您的使用者讀取、 寫入或 DDL 資料庫的權限

執行 R 指令碼，使用者帳戶或 SQL 登入可能需要從其他資料庫，讀取資料建立新的資料表來儲存結果，和寫入資料到資料表。

每個使用者帳戶或執行 R 指令碼的 SQL 登入，請務必確認帳戶或登入具有適當的權限在資料庫上： *db_datareader*， *db_datawriter*，或*db_ddladmin*。

例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 SQL 登入 *MySQLLogin* 在 *RSamples* 資料庫中執行 T-SQL 查詢的權限。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

如需包含每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。

### <a name="use-machine-learning-in-an-azure-vm"></a>使用 Azure VM 中的機器學習服務

如果您在 Azure 虛擬機器上安裝機器學習服務 （或 R Services），您可能需要變更一些額外的預設值。 如需詳細資訊，請參閱[Azure 的虛擬機器上安裝 SQL Server 機器學習](installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源

如果您在資料科學用戶端電腦上建立 R 解決方案，而且需要使用 SQL Server 電腦當成計算內容中執行程式碼，您可以使用的 SQL 登入 」 或 「 整合式的 Windows 驗證。

* 針對 SQL 登入：確定此登入擁有您要讀取資料之資料庫的適當權限。 您可以藉由新增*連接到*和*選取*權限，或加入登入*db_datareader*角色。 針對要建立物件的登入、 新增*DDL_admin*權限。 登入，必須將資料儲存至資料表，請加入登入*db_datawriter*角色。

* Windows 驗證： 您可能需要在指定的執行個體名稱和其他連接資訊的資料科學用戶端上設定 ODBC 資料來源。 如需詳細資訊，請參閱[ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="next-steps"></a>後續的步驟

SQL Server 中的指令碼執行功能，適用於在您確認之後，您可以執行 R 和 Python 命令從 SQL Server Management Studio、 Visual Studio 程式碼或任何其他用戶端，可以將 T-SQL 陳述式傳送到伺服器。

不過，您可能想要進行一些變更系統設定中，以支援大量使用機器學習服務，或將新的 R 封裝。

本節列出一些常見的修改，您可以對支援機器學習。

### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您認為您可能會有很大，使用 R，或者您預期許多使用者會同時為執行指令碼，您可以增加背景工作帳戶指派給 Launchpad 服務數目。 如需詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server R Services](modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="bkmk_optimize"></a>最佳化執行外部指令碼伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式要取得最佳平衡伺服器的各種不同的服務所支援的資料庫引擎，其中可能包括擷取、 轉換及載入 (ETL) 處理序報告、 稽核和使用應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。 因此，在預設設定下，您可能會發現機器學習資源，有時限制或節流處理，特別是在需要大量記憶體的作業。

為了確保機器學習服務工作會設定優先權，並適當資源，我們建議您使用 SQL Server 資源管理員設定外部資源集區。 您也可以變更配置的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database engine、 或增加的帳戶下執行的數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

- 若要設定資源集區以便管理外部資源，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更保留給資料庫的記憶體數量，請參閱[伺服器記憶體組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以透過啟動的 R 帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，請參閱[修改使用者帳戶集區的機器學習](modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用標準版，且沒有資源管理員，您可以使用動態管理檢視 (Dmv) 和擴充的事件，以及 Windows 事件監視，以協助管理伺服器資源所使用的。如需詳細資訊，請參閱[監視及管理 R 服務](managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他的 R 封裝

花點時間安裝任何其他的 R 封裝，您將會使用。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您已經在電腦上個別安裝的 R，或者封裝安裝到使用者程式庫，您將無法使用 T-SQL 從這些封裝。 如需詳細資訊，請參閱[SQL Server 上安裝其他的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。

您也可以設定使用者群組共用每個資料庫層級上的封裝，或設定資料庫角色，才能讓使用者安裝自己的封裝。 如需詳細資訊，請參閱[封裝管理](r-package-management-for-sql-server-r-services.md)。

### <a name="upgrade-the-machine-learning-components"></a>升級的機器學習服務元件

當您安裝使用 SQL Server 2016 的 R 服務時，您會取得的 R 元件版本時已發行版本或 service pack 的最新狀態。 每次您更新或升級伺服器、 機器學習元件也會升級。

不過，您可以升級的機器學習服務元件快排程超過支援的 SQL Server 版本中，安裝 Microsoft R Server，並繫結執行個體。 當您升級時，您也可以取得下列的新功能，支援的 Microsoft R Server 的最新版本中：

* 新的 R 封裝，包括[sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)， [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)，和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。
* [預先定型模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)影像分類和文字分析。

如需如何升級的 SQL Server 2016 執行個體資訊，請參閱[升級 R 元件，透過繫結](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

如果您不確定的 R 版本是執行個體相關聯，您可以執行下列命令：

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'
myvar <- version$version.string
OutputDataSet <- as.data.frame(myvar);'
```

> [!NOTE]
> 會針對 SQL Server 2017 也支援透過繫結程序的升級。 不過，目前升級僅支援 SQL Server 2016 執行個體。

### <a name="tutorials"></a>教學課程

若要開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念，請參閱[TRANSACT-SQL 中的使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。

### <a name="troubleshooting"></a>疑難排解

遇到問題嗎？ 嘗試升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](monitor-r-services-using-custom-reports-in-management-studio.md)

