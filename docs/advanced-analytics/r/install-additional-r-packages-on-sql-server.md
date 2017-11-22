---
title: "SQL Server 上安裝其他的 R 封裝 |Microsoft 文件"
ms.date: 11/15/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8c8e95bf2f0715684bb656d2b2de4dd94aea14f8
ms.sourcegitcommit: 06bb91d138a4d6395c7603a2d8f99c69a20642d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2017
---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server 上安裝其他的 R 封裝

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。

> [!IMPORTANT]
> 加入新封裝的程序需視您正在執行，SQL Server 和工具版本而有所不同。 

**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="overview-of-package-installation-process"></a>封裝的安裝程序概觀

1.  判斷是否有任何封裝的 Windows 版本：[取得正確的封裝版本和格式](#packageVersion)

2.  如果伺服器沒有網際網路存取，下載二進位檔案事先：[下載 zip 檔案](#bkmk_zipPreparation)

    請務必檢查封裝的相依性，並取得任何可能需要在安裝期間的相關的封裝。 若要準備封裝及其相依性的集合，我們建議[miniCRAN 封裝](#bkmk_packageDependencies)。

    如果您下載或安裝時發生錯誤，請嘗試不同的鏡像網站。

3.  安裝封裝的方式取決於是否伺服器具有網際網路存取權，您的 SQL Server 版本上。 建議的程序如下所示：

    **封裝安裝 SQL Server 2016**
    
    1. 資料科學家提供了適用於專案或小組所需的封裝。 使用[miniCRAN](create-a-local-package-repository-using-minicran.md)準備封裝及其相依性的集合。

    2. 資料庫管理員會將封裝安裝至執行個體文件庫使用的 R 工具。

    **SQL Server 2017 的封裝安裝**

    1. 資料庫管理員可讓封裝執行個體上的管理，並將使用者加入新的封裝管理角色。

    2. 資料科學家提供了適用於專案或小組所需的封裝。 使用[miniCRAN](create-a-local-package-repository-using-minicran.md)準備封裝及其相依性的集合。

    3. 封裝上傳至 SQL Server 執行個體，使用建立外部程式庫陳述式。
    
    4. 任何具有適當的權限的使用者加入封裝的執行個體之後，才能安裝封裝，R 指令碼執行，藉由呼叫 R 程式碼，從資料庫`sp_execute_external_script`。
    
    5. 具有適當的權限的使用者也可以安裝或從遠端 R 用戶端，使用新的 RevoScaleR 函數封裝管理尋找封裝。

## <a name="install-new-packages"></a>安裝新的封裝

本節提供金鑰封裝安裝案例的詳細程序。 選擇最佳的方法，取決於：

- 您使用 SQL Server 的版本

- 無論您是唯一的擁有者的執行個體，或嘗試管理多人使用資料庫角色的封裝。

- 是否安裝封裝時或多個封裝相依性

**使用 SQL Server 封裝管理**

如果您的執行個體支援封裝管理功能，您可以使用 T-SQL 或傳統的 R 工具。

-  SQL server 存取封裝管理與以角色為基礎的封裝上傳的 R 封裝會啟用。 使用者再安裝使用 T-SQL 的套件。

    [使用建立外部程式庫安裝封裝](#bkmk_sqlInstall)

- 使用遠端的 R 用戶端將新的封裝加入至伺服器。 需要 SQL Server 2017。 封裝管理必須已啟用伺服器上。 

    [使用 R 來啟用封裝管理時，在伺服器上安裝封裝](#bkmk_rAddPackage)

- 建立外部程式庫，其中包含多個封裝及其相依性以及用於準備封裝程式庫。

    [安裝多個封裝從 miniCRAN 儲存機制](#bkmk_minicran)

**使用傳統的 R 工具**

如果您使用舊版的 SQL Server R 服務，遵循這些指示使用傳統的 R 工具安裝封裝。 （選擇性） 使用 miniCRAN 準備安裝之封裝的集合。

-  將 R 封裝安裝到預設執行個體程式庫使用的 R 工具。 需要系統管理權限。

    [安裝使用的 R 工具的執行個體文件庫中的封裝](#bkmk_rInstall)

- 建立的封裝，以支援多個封裝及其相依性的簡易安裝共用的集合。

    [建立使用 miniCRAN 封裝儲存機制](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>使用 SQL Server 工具安裝封裝

1. 請確定執行個體已啟用 SQL Server 2017 中的外部程式庫管理功能。

    [如何啟用或停用封裝管理](r-package-how-to-enable-or-disable.md)

2. 連接到伺服器使用已安裝新的封裝，使用其中一個支援的資料庫角色，本主題中所述的權限的帳戶： [for SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)

3.  將 zip 的檔案包含您想要安裝至伺服器電腦上的資料夾，例如的 R 封裝複製您**使用者**或**文件**資料夾。 從網路磁碟機或用戶端電腦上的資料夾，您無法加入封裝。 如果您已建立的封裝儲存機制使用 miniCRAN，封裝儲存機制的整個複製到伺服器上任何本機資料夾： 也就是不在網路磁碟機上。

    如果您沒有存取任何伺服器上的資料夾，您可以傳遞的套件內容以二進位格式。 請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)的範例。

4.  從資料庫，您要使用的封裝，執行[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式。

    此範例中，我們假設您的帳戶具有權限，將新的封裝上傳至伺服器，並安裝他們**共用**資料庫中的範圍。

    下列陳述式加入的發行版本[zoo](https://cran.r-project.org/web/packages/zoo/index.html)封裝到目前資料庫內容中，從本機檔案共用。

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    如果您使用資料庫的擁有者 （dbo 角色的成員） 的帳戶連線，封裝可在**共用**範圍： 也就是身為成員的任何使用者所安裝的`rpkgs-users`角色。

    如果您上傳封裝使用的帳戶，只可以存取**私人**範圍，可以只由您安裝此套件。

4.  若要將封裝安裝到執行個體所使用的預設 R 程式庫，執行 R`library()`內預存程序 sp_execute_external_script 命令。

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    如果成功的話，**訊息**視窗應該報告一則訊息，例如 「 已成功解壓縮封裝 'zoo' 和 MD5 總和檢查 」。 如果已安裝必要的套件，安裝程序然後附加並載入所需的套件。

    > [!NOTE]
    > 如果找不到必要的套件，會傳回錯誤: 「 沒有呼叫封裝\<required_package\>"。 
    > 
    > 若要避免發生錯誤，我們建議您事先，檢查封裝的相依性，或使用 miniCRAN 收集所有必要的封裝中的單一 zip 檔案，再執行`CREATE EXTERNAL LIBRARY`。

### <a name="bkmk_rAddPackage"></a>使用 R 來啟用封裝管理時，在伺服器上安裝封裝

如果您已啟用的執行個體上的封裝管理，您可以從遠端 R 用戶端，封裝管理使用 RevoScaleR 函數來安裝新的 R 封裝。

1. 開始之前，請確定符合這些條件：

    + 使用最新版的 Microsoft R 用戶端，以包含 RevoScale 的更新。
    + 封裝管理的執行個體和資料庫已啟用。
    + 您有下列其中一個資料庫管理角色的權限。

2. 列出您想要將字串變數中所安裝的封裝。

    ```R
    packageList <- c("e1071")

3. Define a connection string to the instance and database where package management is enabled, and use the connection string to create a SQL Server compute context.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. 呼叫`rxInstallPackages`和傳遞計算內容以及其中包含封裝名稱的字串變數。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果需要相依套件，也會下載它們。
    
    在此範例中，因為未指定封裝擁有者和範圍，使用進行連接，使用者的認證來安裝此套件，並使用的預設範圍為該使用者會安裝封裝。

### <a name="bkmk_rInstall"></a>安裝使用的 R 工具的執行個體文件庫中的封裝

若要在 SQL Server 2016 和 SQL Server 2017 上安裝新的封裝，您可以使用 R 工具。 不過，您必須是系統管理員，才能執行這項操作。

1.  如果伺服器沒有網際網路存取，下載事先的套件。

    我們建議您將封裝儲存機制使用準備離線封裝的集合。 如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

2.  瀏覽至伺服器上安裝的執行個體的 R 程式庫的資料夾。

    > [!IMPORTANT] 
    > 請務必要與目前的執行個體相關聯的預設文件庫安裝封裝。 永遠不會安裝到使用者目錄的封裝。 如需如何找出預設程式庫的指示，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。

    您用來執行封裝的每個執行個體，請安裝獨立封裝的副本。 封裝無法執行個體之間共用。

4.  以系統管理員身分開啟 R 命令提示字元。

    例如，如果您使用 Windows 命令提示字元，瀏覽至 RTerm.Exe 或 RGui.exe 檔案所在的目錄中。 

    **預設執行個體**

    SQL Server 2017:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **具名執行個體**

    SQL Server 2017:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  執行 R 指令`install.packages`安裝套件。

    語法取決於是否取得封裝從網際網路或本機 zip 檔案。 

    **使用網際網路連線安裝套件**

    例如，下列陳述式會安裝熱門 e1071 封裝。 雙引號不一定需要封裝名稱。

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    當系統要求您的鏡像網站，選取對您位置而言方便的任何網站。

    如果目標封裝相依於其他封裝，R 安裝程式會自動下載相依性，並讓您將進行安裝。

    **沒有網際網路存取手動或的電腦上安裝套件**

    如果您想要安裝的套件具有相依項目，請事先取得所需的套件，然後將它們新增到含有其他套件壓縮檔的資料夾。 請參閱[安裝秘訣](#bkmk_tips)準備封裝的說明 > 一節。

    在 R 命令提示字元中輸入下列命令，指定要安裝的封裝名稱與路徑︰

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會從其本機的 zip 檔案，假設您的複本儲存在目錄中擷取單一的 R 封裝`C:\Temp\Downloaded packages`，並將封裝 （及其相依性） 安裝到本機電腦上的 R 程式庫。

### <a name="bkmk_minicran"></a>安裝多個封裝從 miniCRAN 儲存機制

從 miniCRAN 儲存機制安裝套件的整體程序是類似的單一 zip 檔案從安裝套件。 不過，而不是上傳 zip 格式在個別的封裝，miniCRAN 儲存機制包含目標套件，以及任何相關的必要的封裝。

1.  準備 miniCRAN 儲存機制，然後將 zip 壓縮的檔案複製到伺服器上的本機資料夾。

2.  如果您使用 T-SQL，系統管理員可以執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上傳到資料庫的 zip 壓縮的封裝集合。

    例如，下列陳述式參考 miniCRAN 儲存機制包含 randomForest 封裝及其相依性。

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. 若要與 SQL Server 安裝使用的套件，請執行下列命令做為預存程序中的 R 程式碼的一部分。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    如果成功的話，**訊息**視窗應該報告訊息，例如 「 封裝已成功解壓縮 ' randomForest' 和 MD5 總和檢查 」 和 「 已完成串連執行 」。

## <a name="package-installation-tips"></a>封裝安裝秘訣

本節提供各種的秘訣和 SQL Server 上的 R 封裝安裝相關的範例程式碼。 

###  <a name="packageVersion"></a>取得正確的封裝版本和格式

有多個來源可取得 R 封裝，中其最廣為人知的是 CRAN 和 Bioconductor。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出許多這些資源。 許多封裝會發佈到 GitHub，您可以在這裡取得原始程式碼。 不過，您可能會提供已由公司中的某人所開發的 R 封裝。

不論來源為何，您必須確定您想要安裝的封裝具有二進位格式，以便在 Windows 平台。 否則下載的封裝無法執行 SQL Server 環境中。

在下載之前，您也應該檢查封裝是否與執行 SQL Server 中的 R 版本相容。

### <a name="bkmk_zipPreparation"></a>下載為 zip 檔案的套件

安裝在沒有網際網路存取的伺服器上，下載離線安裝的 zip 檔案格式的封裝副本。 無法將封裝解壓縮。

例如，下列程序描述現在以取得正確的版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存位置，而按一下**儲存**。

此程序會建立套件的本機複本。 然後，您可以安裝套件，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

Zip 檔案格式，以及如何建立 R 封裝的內容的相關詳細資訊，我們建議您可以從 R 專案網站的 PDF 格式下載本教學課程：[建立 R 封裝](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。

### <a name="bkmk_packageDependencies"></a>取得封裝的相依性

R 封裝經常會相依於其他的多個封裝，其中有些可能無法使用執行個體所使用的預設 R 程式庫中。 或者，有時封裝需要相依的套件已經安裝不同版本。

如果您需要安裝多個封裝，或想要確保您的組織中每個人都取得正確的封裝類型和版本，我們建議您建立可在多個使用者或電腦之間共用的本機儲存機制使用 miniCRAN 套件。 如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="permissions"></a>Permissions

如果您是經驗豐富的 R 使用者，您可能會是習慣於從命令列不具特殊權限，或不需事先下載安裝封裝。 不過，大部分的伺服器沒有網際網路連線。 此外，存取檔案共用或儲存體限制。

本節描述安裝在 SQL Server 2016 和 SQl Server 2017 封裝所需的權限的不同層級。 可以完成安裝使用的 R 工具或 SQL Server，但程序和權限稍有不同。

-   SQL Server 2016

    在此版本中，只有在電腦上的系統管理員可以安裝封裝到需要的位置。 您使用標準的 R 工具來安裝封裝，但是您必須以系統管理員身分執行，並使用執行個體相關聯的 R 工具。

-   SQL Server 2017

    此版本中提供新的功能，可讓資料庫管理員委派給使用者的套件安裝。 DBA 必須啟用每個執行個體為基礎的封裝管理功能。 啟用此功能之後，DBA 可以使用資料庫角色來授與個別使用者的能力來安裝封裝，如有需要或共用上的每個資料庫為基礎的封裝。

    如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)。


> [!IMPORTANT]
> 
> 有經驗的 R 使用者通常都會安裝在使用者程式庫中的封裝，接著在指定的檔案路徑的 R 解決方案中，參考該資料夾中的封裝。 不過，在 SQL Server 不支援這種做法。 如需詳細資訊和因應措施，請參閱[如何在使用者程式庫中使用封裝](packages-installed-in-user-libraries.md)。

### <a name="comparing-package-management-methods"></a>比較封裝管理方法

本章節會比較套件安裝方法可用，並列出一些其他考量和秘訣可協助您決定適當的封裝管理與安裝策略。

#### <a name="using-sql-server-package-management-features"></a>使用 SQL Server 封裝管理功能

如果您啟用封裝管理，您會安裝特定資料庫的封裝。 如果您要使用的封裝中的所有資料庫啟用 R 指令碼的位置，您必須將其安裝到每個資料庫。

不過，因為 SQL Server 管理有關哪些使用者有權使用的封裝的資訊，所以您更輕鬆地將複製的使用者與資料庫之間的套件相關資訊。 所以也可以輕鬆地重新建立一組工作的封裝的使用者或多個使用者資料庫，還原時，或執行個體之間移動時。

在 SQL Server 2017 使用 T-SQL 和封裝管理功能是慣用的方法，只要有多個資料庫使用者安裝或執行的 R 封裝。

這項功能是可用的 SQL Server 2017 開頭。

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>若要安裝 SQL Server 執行個體的封裝中使用的 R 工具

如果您使用這個方法，為執行個體安裝的套件中有任何資料庫。 不過，封裝會安裝直接到檔案系統，因為它們必須管理 SQL Server 外部。 無法備份或還原封裝。 此外，資料庫管理員必須了解如何使用 R 工具。

如果您是唯一的擁有者的資料庫，不過，此解決方案是最簡單的其中一個。

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>管理多個封裝和多個相同的封裝版本

如果您要執行離線安裝的 R 封裝，請設定本機儲存機制使用[miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/)可讓您共用封裝及組織所管理的版本可供使用。

#### <a name="establish-a-single-mirror-site-as-standard"></a>建立單一鏡像站台的標準

如果不想每次加入新封裝都要選取鏡像網站，您可以將 R 開發環境設定成一律使用相同的儲存機制。 若要這樣做，請編輯全域 R 設定檔**。Rprofile**，並加入下列一行：

`options(repos=structure(c(CRAN="<mirror site URL>")))`

目前的 CRAN 鏡像會列在[此站台](https://cran.r-project.org/mirrors.html)。

如需喜好設定和 R 執行階段啟動時載入其他檔案的詳細資訊，請從 R 主控台執行此命令：`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>知道您要用於安裝的程式庫

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，暫停時間，並確保 R 環境變數`.libPath`會使用單一路徑。

這個路徑應該指向 R_SERVICES 資料夾執行個體。 如需詳細資訊，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。

#### <a name="side-by-side-installation-with-r-server"></a>使用 R Server-並存安裝

如果您已安裝 Microsoft 機器學習伺服器 （獨立） 以及 SQL Server 機器學習服務，您的電腦應該有個別安裝的 R 每兩個，所有的 R 工具和程式庫的重複項目。

> [!IMPORTANT]
> 
> 僅供 Microsoft R Server R_SERVER 程式庫安裝套件，並無法透過 SQL Server 存取。
> 
> 務必使用`R_SERVICES`安裝您想要使用 SQL Server 中的封裝時，程式庫。
