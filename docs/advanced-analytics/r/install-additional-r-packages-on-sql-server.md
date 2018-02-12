---
title: "SQL Server 上安裝其他的 R 封裝 |Microsoft 文件"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 530745918dfd4808694b401be55e40bac00f3cce
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server 上安裝其他的 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。

**適用於：** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>필수 구성 요소

+ 判斷是否有任何封裝的 Windows 版本：[取得正確的封裝版本和格式](#packageVersion)

+ 如果伺服器沒有網際網路存取，您必須事先下載 Windows 二進位檔案：[下載 zip 檔案](#bkmk_zipPreparation)

+ 識別封裝的相依性。 

    - 如果伺服器具有網際網路存取，您不需要擔心相依性;可以自動安裝所有必要的套件。

    - 如果伺服器執行**不**能存取網際網路，您必須識別所有相依性，並且在 zip 格式事先下載必要的封裝。 若要這樣做的簡單方法是使用[miniCRAN](create-a-local-package-repository-using-minicran.md)準備的所有相依性的封裝集合。 這個儲存機制可以再複製到伺服器電腦。

+ 檢查封裝的相容性。 封裝應該在執行 SQL Server 中的 R 版本相容。

    另請檢查封裝 （或任何它所需要的套件） 包含 SQL Server 或原則會遭到封鎖的功能。 例如，特定套件是強行寫入的 SQL Server 環境的不佳的符合。 這類封裝可能包括存取網路，使用 Java 或不常使用的 SQL Server 環境或需要提高權限的檔案系統存取封裝中的其他架構的套件。

+ Permissions

    需要系統管理權限執行 SQL Server 的電腦。

    此外，若要執行 SQL Server 中，封裝必須安裝在與目前的執行個體相關聯的預設文件庫。 如需如何找出預設程式庫的指示，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。
    
    如果您是經驗豐富的 R 使用者，您可能會是習慣於從命令列不具特殊權限，或不需事先下載安裝封裝。 不過，這個方法不適用於 SQL Server。 在許多情況下，SQL Server 的電腦沒有網際網路連線。 此外，存取伺服器的檔案或外部儲存體限制。 無法存取 SQL Server 中的 R 工作 runnign 封裝安裝到使用者程式庫。 

    如果您沒有 SQL Server 電腦的系統管理權限，尋找 封裝安裝協助資料庫管理員。

+ 每個執行個體是在您要使用的封裝，請分別執行安裝。

     封裝無法執行個體之間共用。 您可以使用相同的壓縮的檔的來源安裝套件，個別執行個體，但個別封裝的副本會加入至每個執行個體文件庫。

## <a name="install-packages"></a>安裝封裝

此章節提供封裝的安裝步驟在下列狀況：

+ [具有網際網路存取的伺服器上安裝新的封裝](#bkmk_rInstall)
+ [使用的伺服器上執行離線安裝套件的**沒有**網際網路存取](#bkmk_offlineInstall)
+ [將封裝安裝到使用 RevoScaleR 的 SQL Server 計算內容](#bkmk_rAddPackage)
+ [使用建立外部程式庫陳述式安裝封裝](#bkmk_createlibrary)（SQL Server 2017 只; 套用其他限制）

### <a name="bkmk_rInstall"></a>線上安裝使用的 R 工具

您可以使用標準的 R 工具來安裝新的封裝上的 SQL Server 2016 或 SQL Server 2017 執行個體。 不過，您必須是系統管理員，才能執行這項操作。

1.  瀏覽至伺服器上安裝的執行個體的 R 程式庫的資料夾。

    > [!IMPORTANT] 
    > 請務必要與目前的執行個體相關聯的預設文件庫安裝封裝。 永遠不會安裝到使用者目錄的封裝。

    如果您沒有必要的權限，請連絡資料庫管理員，並提供您需要的套件清單。

2.  以系統管理員身分開啟 R 命令提示字元。

    例如，如果您使用 Windows 命令提示字元，瀏覽至 RTerm.Exe 或 RGui.exe 的所在位置的目錄中。 

    **預設執行個體**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **具名執行個體**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    如果您已使用繫結，若要升級的機器學習服務元件，可能已變更路徑。 安裝新的封裝之前，務必檢查執行個體路徑。 

3.  執行 R 指令`install.packages`安裝套件。 例如，下列陳述式會安裝熱門 e1071 封裝。 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    雙引號所需的封裝名稱。

4. 當系統要求您的鏡像網站，選取對您位置而言方便的任何網站。

5. 如果目標封裝相依於其他封裝，R 安裝程式會自動下載相依性，並讓您將進行安裝。

> [!IMPORTANT]
> 每個執行個體是在您要使用的封裝，請分別執行安裝。 封裝無法執行個體之間共用。

### <a name = "bkmk_offlineInstall"></a>使用的 R 工具的離線安裝 

如果您想要安裝的封裝有相依性，準備**所有**需要事先的封裝。  請參閱[安裝秘訣](#bkmk_tips)準備封裝的說明 > 一節。

> [!IMPORTANT]
>  每當您在沒有網際網路存取的伺服器上安裝封裝，很重要，您事先在分析完成的相依性，並確定您已下載所有必要的封裝**之前**開始安裝。 我們建議[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此處理程序。 此 R 封裝會採用您想要安裝、 分析相依性，以及讓您取得所有 zip 的檔案的封裝清單。 miniCRAN 接著會建立單一的存放庫，您可以複製到伺服器電腦。
> 
> 如需詳細資訊，請參閱[建立使用 miniCRAN 本機封裝儲存機制](create-a-local-package-repository-using-minicran.md)

1. 將封裝或儲存機制以壓縮格式複製到本機共用或其他伺服器可以存取的位置。

2.  尋找在伺服器上安裝的執行個體的 R 程式庫的資料夾。

    例如，如果您使用 Windows 命令提示字元，瀏覽至 RTerm.Exe 或 RGui.exe 的所在位置的目錄中。

    **預設執行個體**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **具名執行個體**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. 以系統管理員身分開啟 R 命令提示字元。

4.  執行 R 指令`install.packages`並指定封裝或儲存機制名稱和壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會擷取 R 封裝`mynewpackage`從其本機的 zip 檔案，假設您的複本儲存在目錄中`C:\Temp\Downloaded packages`，並在本機電腦上安裝封裝。 如果封裝有任何相依性，安裝程式會檢查文件庫中現有的封裝。 如果您已經建立包含相依性的儲存機制，安裝程式會安裝的 requireed 封裝。

    如果任何必要的封裝不會出現在執行個體文件庫，zip 檔案中找不到目標套件的安裝將會失敗。

### <a name="bkmk_rAddPackage"></a>從遠端 R 用戶端在伺服器上安裝 R 封裝

最新版的[R 伺服器或機器學習伺服器](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)，RevoScaleR 包含支援新的 R 封裝安裝到 SQL Server 計算內容的函式。 

1. 開始之前，請確定符合這些條件：

    + 您的用戶端具有 RevoScale 9.0.1 或更新版本。
    + RevoScaleR 的對等版本已安裝 SQL Server 執行個體。
    + [封裝管理功能](..\r\r-package-how-to-enable-or-disable.md)執行個體上已啟用。
    + 您是可讓您在指定的執行個體及 ddatabase 安裝共用中的封裝或 prvate 內容中，資料庫角色的成員。

2. 從 R 命令列定義的連接字串的執行個體和資料庫，並使用的連接字串[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)建構函式來建立 SQL Server 計算內容。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 建立您想要安裝，並將該清單儲存在字串變數中的封裝清單。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 呼叫[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)和傳遞計算內容以及其中包含封裝名稱的字串變數。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果相依套件是必要的它們會一併安裝，假設提供網際網路連線。
    
    在此範例中，因為未指定的擁有者和範圍，封裝會安裝使用進行連接，該使用者的預設範圍中之使用者的認證。

### <a name="bkmk_createlibrary"></a>用來安裝封裝 miniCRAN 儲存機制，建立外部程式庫 

SQL Server 2017 提供安裝和管理使用 T-SQL 的 R 封裝的新功能。 不過，此程序需要為本機壓縮檔案，而非從網際網路下載的封裝，可供使用。 如果所有的封裝未事先準備陳述式執行失敗。

在這些情況下支援建立外部程式庫：

+ 您要安裝在單一封裝不含相依性
+ 您要安裝多個封裝或封裝的相依性，並已經事先備妥所有封裝。 

**步驟**

1.  準備 zip 壓縮的格式的封裝，或建立 miniCRAN 儲存機制，其中包含封裝和其相依性。  

2. 將儲存機制的 zip 的檔案複製到伺服器上的本機資料夾中。

     > [!IMPORTANT]
     > 您指定的目標套件，以及任何相關的必要的封裝，必須包含來源檔案。

3. 身為管理員，執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上傳到資料庫的 zip 壓縮的封裝集合。

    例如，下列陳述式參考 miniCRAN 儲存機制包含 randomForest 封裝及其相依性。 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    您無法使用 CREATE 陳述式; 中的任意名稱外部程式庫名稱都必須具有您預期時載入，或呼叫封裝所使用的相同名稱。

4. 執行預存程序內的程式碼與 SQL Server 安裝使用的封裝。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    如果成功的話，**訊息**視窗應該報告訊息，例如 「 封裝已成功解壓縮 ' randomForest' 和 MD5 總和檢查 」 和 「 已完成串連執行 」。

    如果安裝失敗，所有的封裝無法安裝，以及後續嘗試安裝套件的安裝可能也會失敗，與此訊息： 

    「 錯誤 rxSqlPkgInstallPackages 中...無法安裝封裝-請檢查記錄檔以取得詳細資料 」

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>封裝安裝秘訣和常見問題 (集 FAQ)

本節提供各種的秘訣和 SQL Server 上的 R 封裝安裝相關的常見問題。

###  <a name="packageVersion"></a>取得正確的封裝版本和格式

有多個來源可取得 R 封裝，中其最廣為人知的是 CRAN 和 Bioconductor。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出許多這些資源。 許多封裝會發佈到 GitHub，您可以在這裡取得原始程式碼。 不過，您可能會提供已由公司中的某人所開發的 R 封裝。

不論來源為何，您必須確定您想要安裝的封裝具有二進位格式，以便在 Windows 平台。 否則下載的封裝無法執行 SQL Server 環境中。

### <a name="bkmk_zipPreparation"></a>下載為 zip 檔案的套件

在沒有網際網路存取的伺服器上安裝，您必須下載離線安裝的 zip 檔案格式的封裝副本。 無法將封裝解壓縮。

例如，下列程序描述現在以取得正確的版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] \(封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存位置，而按一下**儲存**。

    此程序會建立套件的本機複本。 如果您收到的下載錯誤，請嘗試不同的鏡像網站。

4. 已下載封裝封存之後，您可以安裝封裝，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

> [!TIP]
> 如果不小心安裝而不是下載二進位檔案的套件，下載 zip 檔案的副本也會儲存到您的電腦。 查看已安裝此套件，來判斷檔案位置的狀態訊息。 您可以將該 zip 的檔案複製到沒有網際網路存取的伺服器。
> 如果您下載套件使用此方法，並不包括封裝相依性。 

Zip 檔案格式，以及如何建立 R 封裝的內容的相關詳細資訊，我們建議您可以從 R 專案網站的 PDF 格式下載本教學課程：[建立 R 封裝](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。

### <a name="bkmk_packageDependencies"></a>取得封裝的相依性

R 封裝經常會相依於其他的多個封裝，其中有些可能無法使用執行個體所使用的預設 R 程式庫中。 有時封裝需要相依的套件已經安裝不同版本。

如果您需要安裝多個封裝，或想要確保您的組織中每個人都取得正確的封裝類型和版本，我們建議您使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)封裝以建立可共用的本機儲存機制在多個使用者或電腦。 如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="permissions"></a>Permissions

本節描述安裝在 SQL Server 2016 和 SQL Server 2017 封裝所需的權限的不同層級。 可以完成安裝使用的 R 工具或 SQL Server，但程序和權限稍有不同。

-   SQL Server 2016

    在此版本中，只有在電腦上的系統管理員可以安裝封裝到需要的位置。 您使用標準的 R 工具來安裝封裝，但是您必須以系統管理員身分執行，並使用執行個體相關聯的 R 工具。

-   SQL Server 2017

    如果您有系統管理存取權，您可以安裝執行個體層級為基礎的封裝所使用的 R 工具。

    如果您是資料庫擁有者，您可以安裝 R 封裝，從遠端用戶端中，如果您定義的連接，並連接到使用 RxInSqlServer 的執行個體即可。
    
    本版包含新功能，可在即將發行版本中支援的 R 或 Python 封裝，資料庫管理員進行管理。 若要使用這項功能時，DBA 必須先啟用每個執行個體為基礎的封裝管理功能。 啟用此功能之後，個別使用者可以安裝封裝，特定資料庫，根據其資料庫角色。 如需詳細資訊，請參閱[啟用或停用 SQL Server 的 R 封裝管理](../r/r-package-how-to-enable-or-disable.md)。

> [!IMPORTANT]
> 
> 有經驗的 R 使用者通常都會安裝在使用者程式庫中的封裝，接著在指定的檔案路徑的 R 解決方案中，參考該資料夾中的封裝。 不過，在 SQL Server 不支援這種做法。 如需詳細資訊和因應措施，請參閱[如何在使用者程式庫中使用封裝](packages-installed-in-user-libraries.md)。

### <a name="establish-a-single-mirror-site-as-standard"></a>建立單一鏡像站台的標準

如果不想每次加入新封裝都要選取鏡像網站，您可以將 R 開發環境設定成一律使用相同的儲存機制。 若要這樣做，請編輯全域 R 設定檔**。Rprofile**，並加入下列一行：

`options(repos=structure(c(CRAN="<mirror site URL>")))`

目前的 CRAN 鏡像會列在[此站台](https://cran.r-project.org/mirrors.html)。

如需喜好設定和 R 執行階段啟動時載入其他檔案的詳細資訊，請從 R 主控台執行此命令：`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>知道您要用於安裝的程式庫

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，暫停時間，並確保 R 環境變數`.libPath`會使用單一路徑。

這個路徑應該指向 R_SERVICES 資料夾執行個體。 如需詳細資訊，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-r-server"></a>使用 R Server-並存安裝

如果您已安裝 Microsoft 機器學習伺服器 （獨立） 以及 SQL Server 機器學習服務，您的電腦應該有重複項目，所有的 R 工具和程式庫的每個個別安裝的 R。

> [!IMPORTANT]
> 
> 僅供 Microsoft R Server R_SERVER 程式庫安裝套件，並無法透過 SQL Server 存取。
> 
> 務必使用`R_SERVICES`安裝您想要使用 SQL Server 中的封裝時，程式庫。

### <a name="how-to-determine-which-packages-are-already-installed"></a>如何判斷已安裝哪個封裝？

 請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)