---
title: 安裝 SQL Server 2017 機器學習服務 （資料庫） Windows 上 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 23fed22efe90a91905c4b36c967ad5fa72717b3f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585870"
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>安裝 SQL Server 2017 機器學習在 Windows 上的服務 （資料庫） 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 的機器學習服務元件將加入資料庫中的預測分析、 統計分析、 視覺化和機器學習演算法。 函式程式庫可提供在 R 和 Python，而且執行外部指令碼當做 database engine 執行個體上。 

這篇文章說明如何執行安裝的機器學習元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈和下列螢幕上的提示。

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

+ 如果您想要安裝 R、 Python 或兩者的語言支援機器學習服務需要 SQL Server 2017 安裝程式。 如果相反地，您會擁有 SQL Server 2016 安裝媒體，您可以安裝[SQL Server 2016 R 服務 （資料庫）](sql-r-services-windows-install.md)取得 R 語言支援。

+ 需要資料庫引擎執行個體。 您無法安裝只 R 或 Python 功能，雖然您可以將它們以累加方式加入現有的執行個體。

+ 請勿安裝容錯移轉叢集上的機器學習服務。 用來隔離 R 和 Python 程序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝機器學習服務。 安裝程式的機器學習服務部分將會失敗。

+ 請勿安裝**共用功能** > **機器學習伺服器 （獨立）** 同一部電腦上執行資料庫中執行個體。 在獨立伺服器將會競用相同的資源，破壞的兩個安裝效能。

+ 為支援與其他版本的 R，並將 Python 的並存安裝，但不是建議使用。 它支援，因為 SQL Server 執行個體使用的開放原始碼 R 和 Anaconda 發佈其本身複本。 但是，建議您不要因為執行 SQL Server 外部的 SQL Server 電腦使用 R，並將 Python 程式碼可能會導致各種問題：
    
  + 您使用不同的程式庫和其他可執行檔，並比您執行 SQL Server 中時，取得不同的結果。
  + 執行外部程式庫中的 R，並將 Python 指令碼不受 SQL Server，導致資源爭用的情況。
  
> [!IMPORTANT]
> 安裝程式完成之後，請務必完成後設定步驟本文中所述。 這些步驟包括啟用 SQL Server 以使用外部指令碼，並加入您的名義上執行 R，並將 Python 工作的 SQL Server 所需的帳戶。 組態變更通常需要重新啟動的執行個體或啟動控制板服務重新啟動。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2017 的安裝精靈。 您可以下載 
  
2. 在**安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入現有安裝**。

   ![安裝機器學習服務資料庫](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在 [特徵選取]  頁面上，選取下列選項：
  
    -   **Database Engine 服務**
  
         若要使用 SQL Server 中使用 R 和 Python，您必須安裝 database engine 執行的個體。 您可以使用預設或具名執行個體。
  
    -   **Machine Learning Services (資料庫內)**
  
         此選項會安裝支援 R 的資料庫服務和 Python 指令碼執行。

    -   **R**

        勾選此選項可新增 Microsoft R 封裝、 直譯器及開放原始碼。 

    -   **Python**

        核取此選項可新增 Microsoft Python 封裝，Python 3.5 可執行檔，選取媒體櫃 Anaconda 發佈。
        
        ![功能的 R，並將 Python 選項](media/2017setup-features-page-mls-rpy.png "設定 Python 的選項")

        > [!NOTE]
        > 
        > 未選取的選項**機器學習伺服器 （獨立）**。 若要安裝在機器學習伺服器選項**共用功能**為了在另一部電腦上使用。

4. 在**同意安裝 R**頁面上，選取**接受**。 此授權合約涵蓋 Microsoft R Open，其中包含開放原始碼 R 基底套件與工具，以及增強的 R 封裝和連線提供者來自 Microsoft 開發小組的散佈。

5. 在**同意安裝 Python**頁面上，選取**接受**。 Anaconda 和相關的工具，再加上 Microsoft 開發小組的一些新的 Python 程式庫，另外也涵蓋了 Python 開放原始碼授權合約。
     
     ![Python 授權的協議](media/2017setup-python-license.png "授權合約的 Python")
  
    > [!NOTE]
    >  如果您使用的電腦沒有網際網路存取，您可以暫停此時若要個別下載安裝程式的安裝程式。 如需詳細資訊，請參閱[安裝沒有網際網路存取的機器學習元件](../install/sql-ml-component-install-without-internet-access.md)。
  
     選取**接受**，等到**下一步**按鈕會變成作用中、，然後選取**下一步**。
  
6. 在**安裝準備就緒**頁面上，確認這些選取項目會包含在內，然後選取**安裝**。
  
    + Database Engine 服務
    + Machine Learning 服務 (資料庫內)
    + R、 Python 或兩者

    記下位置的路徑下的資料夾`..\Setup Bootstrap\Log`儲存組態檔。 安裝完成時，您可以檢閱摘要檔案中已安裝的元件。

## <a name="restart-the-service"></a>重新啟動服務

當安裝完成時，繼續下一步，啟用指令碼執行之前，先重新啟動資料庫引擎。

重新啟動服務時，也會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

您可以重新啟動服務，使用滑鼠右鍵**重新啟動**命令，在 SSMS 中，或使用的執行個體的**服務**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>啟用外部指令碼執行

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
    
3.  若要啟用外部指令碼處理功能，請執行下列陳述式：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果您已啟用的 R 語言功能，不會執行第二次重新設定 Python。 基礎的擴充性平台支援這兩種語言。

4. 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 SQL Server 服務。 也會自動重新啟動 SQL Server 服務重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

    您可以重新啟動服務，使用滑鼠右鍵**重新啟動**命令，在 SSMS 中，或使用的執行個體的**服務**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>確認安裝

使用下列步驟，確認所有元件，用來啟動外部指令碼正在都執行。

1. 在 SQL Server Management Studio，開啟新查詢視窗中，並執行下列命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。
    
2. 開啟**服務**面板或 SQL Server 組態管理員，並確認**SQL Server Launchpad 服務**正在執行。 您應該有一個適用於每個資料庫引擎執行個體具有 R 服務，或 Python 安裝。 如果未執行，請重新啟動服務。 如需詳細資訊，請參閱[元件來支援 Python 整合](../python/new-components-in-sql-server-to-support-python-integration.md)。 
   
3. 如果 [啟動列] 正在執行，您應該能夠執行簡單 R 和 Python 指令碼，確認外部指令碼的執行階段可以使用 SQL Server 進行通訊。

   開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行指令碼，如下所示：
    
    + R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

 **結果**

    若要執行，第一次載入外部指令碼執行階段時，可能有點需要指令碼。 結果應該類似這樣：

    | hello |
    |----|
    | @shouldalert|


> [!NOTE]
> Python 指令碼中使用的標題或資料行不會傳回，所設計。 若要加入您的輸出資料行名稱，您必須指定傳回的資料集的結構描述。 只要使用與結果參數的預存程序，命名資料行和指定的 SQL 資料類型。
> 
> 比方說，您可以將下列行加入產生任意資料行名稱： `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>其他組態

如果執行外部指令碼驗證步驟成功，您可以從 SQL Server Management Studio、 Visual Studio 程式碼或其他任何可以傳送至伺服器的 T-SQL 陳述式的用戶端執行 Python 指令。

如果您在執行命令時出現錯誤，請檢閱本節中的其他組態步驟。 您可能需要進行其他適當的組態服務或資料庫。

常見的案例，需要進行其他變更包括：

* [設定傳入連接的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [啟用額外的網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [啟用遠端連接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [擴充內建權限給遠端使用者](#bkmk_configureAccounts)
* [授與權限來執行外部指令碼](#permissions-external-script)
* [授與存取權的個別資料庫](#permissions-db)

> [!NOTE]
> 並非所有列出的變更是必要的並且不可能會需要。 需求取決於您的安全性結構描述，您安裝 SQL Server，然而您預期使用者連線到資料庫並執行外部指令碼的方式。 可以在這裡找到其他疑難排解提示：[升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> 啟用 [啟動列] 帳戶群組的隱含的驗證

在安裝期間建立了一些新的 Windows 使用者帳戶，以在 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務的安全性權杖下執行工作。 當使用者從外部用戶端傳送的 Python 或 R 指令碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動可用工作者帳戶。 然後將它對應至在呼叫的使用者的身分識別，並執行指令碼代表使用者。

這稱為*隱含的驗證*，而是 database engine 服務。 此服務會支援 SQL Server 2016 和 SQL Server 2017 中安全地執行外部指令碼。

您可以在 Windows 使用者群組 **SQLRUserGroup**中，檢視這些帳戶。 根據預設，會建立 20 個背景工作帳戶，這通常是超過不足以執行外部指令碼工作。

> [!IMPORTANT]
> 背景工作群組命名為**SQLRUserGroup**不論是否安裝 R 或 Python。 沒有單一的群組，每個執行個體。

如果您需要從遠端資料科學用戶端，執行指令碼，而且您使用 Windows 驗證，還有其他考量。 這些工作者帳戶必須獲得權限才能登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代替您執行個體。

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在 [物件總管] 中展開**安全性**。 以滑鼠右鍵按一下**登入**，然後選取**新登入**。
2. 在**登入-新增**對話方塊中，選取**搜尋**。
3. 選取**物件類型**，然後選取**群組**。 清除所有其他項目。
4. 在**輸入物件名稱來選取**，型別*SQLRUserGroup*，然後選取**檢查名稱**。
5. 與執行個體的 Launchpad 服務相關聯的本機群組名稱，應該解析為類似 *instancename\SQLRUserGroup*。 選取 [確定]。
6. 根據預設，群組指派給**公用**角色，而且具有連接到 database engine 的權限。
7. 選取 [確定]。

> [!NOTE]
> 如果您使用**SQL 登入**就 SQL Server 計算內容中執行指令碼，不需要這個額外步驟。

### <a name="permissions-external-script"></a> 提供使用者執行外部指令碼的權限

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自己，而且您在您自己的執行個體中執行 R 或 Python 指令碼，您通常會以系統管理員身分執行指令碼。 因此，您必須透過不同的作業和資料庫中的所有資料隱含的權限。

不過，大多數使用者而言不需要這類較高的權限。 例如，組織中，使用 SQL 登入通常存取資料庫的使用者沒有提高權限。 因此，每個使用者正在使用 R 或 Python，您必須授與使用者的機器學習服務會使用語言在每個資料庫中執行外部指令碼的權限。 方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 找不到支援的指令碼語言特有的權限。 換句話說，沒有與 Python 指令碼的 R 指令碼的不同權限層級。 如果您需要維護這些語言的個別權限，請個別執行個體上安裝 R，並將 Python。

### <a name="permissions-db"></a> 授與使用者讀取、 寫入或資料定義語言 (DDL) 資料庫的權限

當使用者執行指令碼時，使用者可能需要從其他資料庫讀取資料。 使用者可能也需要建立新的資料表來儲存結果，並將資料寫入資料表。

每個 Windows 使用者帳戶或 SQL 登入執行 R 或 Python 指令碼，請確定它在特定的資料庫上擁有適當的權限： `db_datareader`， `db_datawriter`，或`db_ddladmin`。

例如，下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式可讓 SQL 登入*MySQLLogin*執行 T-SQL 查詢的權限*ML_Samples*資料庫。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

如需包含每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源

您可以建立的機器學習資料科學用戶端電腦上的方案。 如果您需要使用 SQL Server 電腦當成計算內容中執行程式碼，您有兩個選項： 使用 SQL 登入存取的執行個體，或使用 Windows 帳戶。

+ SQL 登入： 請確定登入，讀取資料的資料庫上具有適當的權限。 您可以藉由新增*連接到*和*選取*權限，或加入登入`db_datareader`角色。 若要建立物件，指定`DDL_admin`權限。 如果您必須將資料儲存至資料表，加入`db_datawriter`角色。

+ Windows 驗證： 您可能需要在指定的執行個體名稱和其他連接資訊的資料科學用戶端上建立 ODBC 資料來源。 如需詳細資訊，請參閱[ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建議的最佳化

既然您已使用的所有項目，您也可以在最佳化伺服器以支援機器學習服務，或安裝預先定型的模型。

### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您預期許多使用者會同時執行的指令碼時，您可以增加背景工作帳戶指派給 Launchpad 服務數目。 如需詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server 機器學習服務](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="optimize-the-server-for-script-execution"></a>最佳化指令碼執行的伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式要取得最佳平衡伺服器的各種不同的服務所支援的資料庫引擎，其中可能包括擷取、 轉換及載入 (ETL) 處理序報告、 稽核和使用應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。 因此，在預設設定下，您可能會發現機器學習資源，有時限制或節流處理，特別是在需要大量記憶體的作業。

為了確保機器學習服務工作會設定優先權，並適當資源，我們建議您使用 SQL Server 資源管理員設定外部資源集區。 您也可以變更配置的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database engine、 或增加的帳戶下執行的數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

- 若要設定資源集區以便管理外部資源，請參閱[建立外部資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要變更保留給資料庫的記憶體數量，請參閱[伺服器記憶體組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要變更可以透過啟動的 R 帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，請參閱[修改使用者帳戶集區的機器學習](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用標準版，且沒有資源管理員，您可以使用動態管理檢視 (Dmv) 和擴充的事件，以及 Windows 事件監視，以協助管理伺服器資源。 如需詳細資訊，請參閱[監視及管理 R 服務](../r/managing-and-monitoring-r-solutions.md)和[監視及管理 Python 服務](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-r-packages"></a>安裝其他的 R 封裝

建立 SQL Server R 方案可以呼叫基本的 R 函數，從 SQL Server，而第三方開放原始碼 R SQL Server 安裝的版本相容的 R 封裝安裝 properietary packes 函式。

您想要從 SQL Server 使用的套件，必須安裝在執行個體所使用的預設程式庫中。 如果您已經在電腦上個別安裝的 R，或者封裝安裝到使用者程式庫，您將無法使用 T-SQL 從這些封裝。

安裝和管理的 R 封裝的程序是在 SQL Server 2016 和 SQL Server 2017 不同。 在 SQL Server 2016 中，資料庫管理員必須安裝 R 封裝，使用者需要。 在 SQL Server 2017，您可以設定使用者群組共用每個資料庫層級上的封裝，或設定資料庫角色，才能讓使用者安裝自己的封裝。 如需詳細資訊，請參閱[在 SQL Server 中安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)。


## <a name="get-help"></a>取得說明

需要協助以安裝或升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以瞭解如何使用 SQL Server 中的 Python，依照這些教學課程：

+ [教學課程： 在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [Python 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。
