---
title: "安裝和設定 Python 機器學習服務 |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e3142bcf06fa2ed88ead730d0cc127cf41cfde56
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="set-up-python-machine-learning-services-in-database"></a>設定 Python 機器學習服務 （資料庫）

  安裝 Python 藉由執行所需的元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈，並遵循本主題中所述的互動式提示。

## <a name="machine-learning-options-in-sql-server-setup"></a>機器學習中 SQL Server 安裝程式選項

選擇**機器學習服務**功能，並選取**Python**做為語言。

**共用功能**區段包含個別的安裝選項時，**機器學習伺服器 （獨立）**。 這個選項的伺服器上沒有 SQL Server，或不需要使用 SQL Server 計算內容支援實施 Python 程式碼。 因此，我們建議您*不*安裝這項 SQL Server 執行個體的同一部電腦上。 相反地，安裝在另一部電腦上的機器學習伺服器 （獨立）。

已完成安裝之後，重新設定為允許使用外部可執行檔的指令碼執行的執行個體。 您可能需要進行其他變更到伺服器，以支援機器學習工作負載。 組態變更通常需要重新啟動的執行個體或啟動控制板服務重新啟動。

### <a name="prerequisites"></a>必要條件

+ 需要 SQL Server 2017。 舊版的 SQL Server 上不支援 Python 整合。
+ 請務必安裝 database engine。 SQL Server 執行個體，才能執行 Python 指令碼中的資料庫。
+ Python 元件安裝程式的一部分安裝必要元件。
+ 您無法安裝 machine learning Python 上的服務容錯移轉叢集。 用來隔離 Python 處理程序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。
   
  因應措施，您可以使用複寫，將必要資料表複製到使用 Python 服務的獨立 SQL Server 執行個體。 或者，您可以安裝機器學習服務與 Python 的服務使用的 AlwaysOn 設定，而且可用性群組的一部分的獨立電腦上。

+ SQL Server 執行個體使用 Anaconda 發佈其本身複本，則可能與其他的 Python 版本的並存安裝。 不過，執行 SQL Server 外部的 SQL Server 電腦使用 Python 程式碼可能會導致各種問題：
    + 您使用不同的程式庫和其他可執行檔，並比您執行 SQL Server 中時，取得不同的結果。
    + 在 外部程式庫中執行 Python 指令碼無法受 SQL Server，導致資源爭用的情況。
  
> [!IMPORTANT]
> 安裝程式完成後，請務必在完成本主題中所述的其他後置組態步驟。 其中包括啟用 SQL Server 以使用外部指令碼，以及新增 SQL Server 來代表您執行 Python 作業所需的帳戶。

### <a name="unattended-installation"></a>自動安裝

若要執行自動的安裝，使用 SQL Server 安裝程式和 Python 的特定引數的命令列選項。 如需詳細資訊，請參閱[Python 機器學習服務與 SQL server 安裝的自動安裝](unattended-installs-of-sql-server-python-services.md)。

##  <a name="bkmk_installPythonInDatabase"></a>步驟 1： 安裝的機器學習 SQL Server 上的服務 （資料庫）

1. 執行 SQL Server 2017 的安裝精靈。
  
2. 在**安裝**索引標籤上，選取**新的 SQL Server 獨立安裝或將功能加入現有安裝**。

    ![安裝 Python 資料庫](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在 [特徵選取]  頁面上，選取下列選項：
  
    -   **Database Engine 服務**
  
         若要使用 SQL Server 中使用 Python，您必須安裝 database engine 執行的個體。 您可以使用預設或具名執行個體。
  
    -   **機器學習服務 （資料庫）**
  
         此選項會安裝支援 Python 指令碼執行的資料庫服務。

    -   **Python**勾選此選項可取得之 Python 3.5 可執行檔，然後選取從 Anaconda 發佈的文件庫。 安裝每個執行個體只能有一個語言。
        
        ![功能的 Python 選項](media/ml-svcs-features-python-highlight.png "設定 Python 的選項")

        > [!NOTE]
        > 
        > 未選取的選項**機器學習伺服器 （獨立）**。 若要安裝在機器學習伺服器選項**共用功能**為了在另一部電腦上使用。 例如，您可以安裝相同版本的機器學習用於專案的開發，例如資料科學家的膝上型電腦的其他電腦上的元件。

4. 在**同意安裝 Python**頁面上，選取**接受**。
  
     此授權合約，才能下載可執行檔，Python Anaconda Python 封裝。
     
     ![Python 授權的協議](media/ml-svcs-license-python.png "授權合約的 Python")
  
    > [!NOTE]
    >  如果您使用的電腦沒有網際網路存取，您可以暫停此時若要個別下載安裝程式的安裝程式。 如需詳細資訊，請參閱[安裝沒有網際網路存取元件](../r/installing-ml-components-without-internet-access.md)。
  
     選取**接受**，等到**下一步**按鈕會變成作用中、，然後選取**下一步**。
  
5. 在**安裝準備就緒**頁面上，確認這些選取項目會包含在內，然後選取**安裝**。
  
     + Database Engine 服務
     + Machine Learning 服務 (資料庫內)
     + Python
  
    這些選取項目代表使用 Python 與所需的最低設定[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。
    
    ![準備好安裝 Python](media/ready-to-install-python.png "Python 安裝所需的元件")

    （選擇性） 請記下的路徑下的資料夾位置`..\Setup Bootstrap\Log`儲存組態檔。 安裝完成時，您可以檢閱摘要檔案中已安裝的元件。

6. 安裝完成時，重新啟動電腦。

##  <a name="bkmk_enableFeature"></a>步驟 2： 啟用執行 Python 指令碼

1. 開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果未安裝，您可以執行一次，若要開啟下載連結，並將它安裝 SQL Server 安裝精靈。
  
2. 連接到機器學習服務，安裝的執行個體，並執行下列命令：

   ```SQL
   sp_configure
   ```

    屬性 `external scripts enabled` 的值目前應該為 **0**。 這是因為預設關閉的功能。 您可以執行 R 或 Python 指令碼之前，此功能，必須明確啟用由系統管理員。
    
3.  若要啟用外部指令碼的功能支援 Python，執行下列陳述式：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果您已啟用的 R 語言功能，您不需要執行第二次重新設定 Python。 基礎的擴充性平台支援這兩種語言。

4. 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 SQL Server 服務。 也會自動重新啟動 SQL Server 服務重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。

    您可以藉由重新啟動服務**服務**面板在控制台中，或使用[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。

## <a name="step-3-verify-that-the-external-script-execution-feature-is-running"></a>步驟 3： 確認正在執行的外部指令碼執行功能

請花一點時間來確認用來啟動 Python 指令碼的所有元件正在都執行。

1. 在 SQL Server Management Studio，開啟新查詢視窗中，並執行下列命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 現在應該設定為 1。
    
2. 開啟**服務**面板或 SQL Server 組態管理員，並確認您的執行個體的啟動控制板服務正在執行。 如果未執行 [啟動列]，重新啟動服務。
  
    如果您已安裝多個 SQL Server 執行個體，R 或 Python 啟用任何執行個體都擁有自己 Launchpad 服務。

    如果您在單一執行個體上安裝 R 和 Python，只能有一個 [啟動列] 會安裝。 獨立的語言特有啟動器 DLL 會加入每一種語言。 如需詳細資訊，請參閱[元件來支援 Python 整合](new-components-in-sql-server-to-support-python-integration.md)。 
   
3. 如果 [啟動列] 正在執行，您應該能夠執行簡單的 Python 指令碼，如下所示，在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'OutputDataSet = InputDataSet',
    @input_data_1 = N'SELECT 1 AS col'
    ```
    
    **結果**
    
    *<code>&nbsp;&nbsp;</code>* *1*

> [!NOTE]
> Python 指令碼中使用的標題或資料行不會傳回，所設計。 若要加入您的輸出資料行名稱，您必須指定傳回的資料集的結構描述。 只要使用與結果參數的預存程序，命名資料行和指定的 SQL 資料類型。
> 
> 比方說，您可以將下列行加入產生任意資料行名稱：`WITH RESULT SETS ((Col1 AS int))`

## <a name="step-4-additional-configuration"></a>步驟 4： 其他組態

如果前一個命令執行成功，您可以從 SQL Server Management Studio、 Visual Studio 程式碼或其他任何可以傳送至伺服器的 T-SQL 陳述式的用戶端執行 Python 指令。

如果您在執行命令時出現錯誤，請檢閱下列清單。 您可能需要進行其他適當的組態服務或資料庫。

> [!NOTE]
> 
> 並非所有列出的變更是必要的並且不可能會需要。 需求取決於您的安全性結構描述，您安裝 SQL Server，然而您預期使用者連線到資料庫並執行外部指令碼的方式。

###  <a name="bkmk_configureAccounts"></a>啟用 [啟動列] 帳戶群組的隱含的驗證

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

### <a name="give-users-permission-to-run-external-scripts"></a>提供使用者執行外部指令碼的權限

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自己，而且您在您自己的執行個體中執行 Python 指令碼，您通常會以系統管理員身分執行指令碼。 因此，您必須透過不同的作業和資料庫中的所有資料隱含的權限。

不過，大多數使用者而言不需要這類較高的權限。 例如，組織中，使用 SQL 登入通常存取資料庫的使用者沒有提高權限。 因此，每個使用者正在使用 Python，您必須授與使用者的機器學習服務正 Python 每個資料庫中執行外部指令碼的權限。 方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 找不到支援的指令碼語言特有的權限。 換句話說，沒有與 Python 指令碼的 R 指令碼的不同權限層級。 如果您需要維護這些語言的個別權限，請個別執行個體上安裝 R，並將 Python。

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>授與使用者讀取、 寫入或資料定義語言 (DDL) 資料庫的權限

當使用者執行指令碼時，使用者可能需要從其他資料庫讀取資料。 使用者可能也需要建立新的資料表來儲存結果，並將資料寫入資料表。

每個 Windows 使用者帳戶或 SQL 登入執行 R 或 Python 指令碼，請確定它在特定的資料庫上擁有適當的權限： `db_datareader`， `db_datawriter`，或`db_ddladmin`。

例如，下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式可讓 SQL 登入*MySQLLogin*執行 T-SQL 查詢的權限*ML_Samples*資料庫。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

如需包含每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。

### <a name="ensure-that-the-sql-server-installation-supports-remote-connections"></a>請確認 SQL Server 安裝支援的遠端連線

如果您無法從遠端電腦連接，請檢查防火牆是否允許 SQL Server 存取權。 在預設安裝中，可能會停用遠端連線，或使用 SQL Server 的特定通訊埠可能遭到防火牆封鎖。 如需詳細資訊，請參閱[設定用於 database engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>為您的資料科學用戶端執行個體建立 ODBC 資料來源

您可以建立的機器學習資料科學用戶端電腦上的方案。 如果您需要使用 SQL Server 電腦當成計算內容中執行程式碼，您有兩個選項： 使用 SQL 登入存取的執行個體，或使用 Windows 帳戶。

+ SQL 登入： 請確定登入，讀取資料的資料庫上具有適當的權限。 您可以藉由新增*連接到*和*選取*權限，或加入登入`db_datareader`角色。 若要建立物件，指定`DDL_admin`權限。 如果您必須將資料儲存至資料表，加入`db_datawriter`角色。

+ Windows 驗證： 您可能需要在指定的執行個體名稱和其他連接資訊的資料科學用戶端上建立 ODBC 資料來源。 如需詳細資訊，請參閱[ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="additional-optimizations"></a>額外的最佳化

既然您已使用的所有項目，您也可以在最佳化伺服器以支援機器學習服務，或安裝預先定型的模型。

### <a name="add-more-worker-accounts"></a>新增更多背景工作帳戶

如果您預期許多使用者會同時執行的指令碼時，您可以增加背景工作帳戶指派給 Launchpad 服務數目。 如需詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server 機器學習服務](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="optimize-the-server-for-script-execution"></a>最佳化指令碼執行的伺服器

預設設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式取得最佳平衡伺服器的各種不同的服務。 這些服務包括 ETL 程序、 報告、 稽核和使用的應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料。

如果您使用預設設定，您可能會發現適用於執行外部指令碼資源會限制或節流處理，特別是在需要大量記憶體的作業。 如果機器學習的優先順序，請變更預設資料庫設定，以確保外部指令碼工作可以設定優先權，並適當地資源。 這些變更包括：

+ 減少配置給記憶體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎。
+ 數目增加帳戶下執行[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服務。 這不會增加資源的數目，但是會增加可同時執行的指令碼的數目。

如果您有 SQL Server Enterprise Edition 時，使用資源管理員來設定外部資源集區的 Python。 如需詳細資訊，請參閱下列文件：

-   設定資源集區以便管理外部資源
  
     [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
  
-   變更保留給資料庫引擎的記憶體數量
  
     [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
  
-   變更可以透過啟動的背景工作帳戶數目[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
     [修改 SQL Server R services 的使用者帳戶集區](../r/modify-the-user-account-pool-for-sql-server-r-services.md)

如果您使用 SQL Server Standard Edition，且沒有資源管理員，您可以使用動態管理檢視和擴充的事件，可協助您管理伺服器資源。 您也可以使用 Windows 事件監視針對此目的。 如需詳細資訊，請參閱[監視及管理 R 服務](../r/managing-and-monitoring-r-solutions.md)。

### <a name="upgrade-the-machine-learning-components"></a>升級的機器學習服務元件

當您使用 SQL Server 2017 安裝機器學習服務時，您會取得元件的版本在發行版本時的時間。 每次您更新或升級 SQL Server 執行個體的機器學習元件也會升級。

您可以升級的機器學習服務元件快排程超過支援的 SQL Server 版本中，藉由安裝 Microsoft 機器學習的伺服器。 當您這樣做時，您也可以取得支援最新版的機器學習伺服器，任何新功能：

+ Python 封裝更新[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。
+ [預先定型模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)影像分類和文字分析。

如需如何升級執行個體資訊，請參閱[升級 R 元件，透過繫結](..\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="tutorials"></a>教學課程

請參閱下列教學課程，如需如何使用 Python 與 SQL Server 建置和部署的機器學習解決方案的一些範例：

[在 T-SQL 中使用 Python](../tutorials/run-python-using-t-sql.md)

[建立使用 revoscalepy Python 模型](../tutorials/use-python-revoscalepy-to-create-model.md)
