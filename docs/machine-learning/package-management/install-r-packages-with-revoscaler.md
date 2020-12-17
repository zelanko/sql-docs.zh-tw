---
title: 使用 RevoScaleR 來安裝 R 套件
description: 了解如何使用 RevoScaleR 函式來搭配機器學習服務或 R 服務在 SQL Server 上安裝 R 套件。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017
ms.openlocfilehash: 28dbaf6f3496004ba90731d6bf5eaef693036e19
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471049"
---
# <a name="use-revoscaler-to-install-r-packages"></a>使用 RevoScaleR 來安裝 R 套件

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

此文章描述如何使用 [RevoScaleR](../r/ref-r-revoscaler.md) (9.0.1 版或更新版本) 函式來搭配機器學習服務或 R Services 在 SQL Server 上安裝 R 套件。 RevoScaleR 函式可以由遠端的非系統管理員用來在 SQL Server 上安裝套件，而不需要直接存取伺服器。

::: moniker range="=sql-server-2016"
> [!NOTE]
> SQL Server R Services 客戶必須進行[元件升級](../install/upgrade-r-and-python.md)以取得 RevoScaleR 套件管理函式。 如需如何擷取套件版本及內容的指示，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。
::: moniker-end

## <a name="revoscaler-functions-for-package-management"></a>適用於套件管理的 RevoScaleR 函式

下表描述用於 R 套件安裝及管理的函式。

| 函式 | 描述 |
|----------|-------------|
| [rxSqlLibPaths](/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) \(英文\) | 判斷遠端 SQL Server 上執行個體程式庫的路徑。 |
| [rxFindPackage (英文)](/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 取得遠端 SQL Server 上一或多個套件的路徑。 |
| [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) \(英文\) | 從遠端 R 用戶端呼叫此函式來從指定的存放庫，或是透過讀取本機儲存的壓縮套件，於 SQL Server 計算內容中安裝套件。 此函式會檢查相依性，並確保所有相關的套件都可以安裝至 SQL Server，就像本機計算內容中的 R 套件安裝一樣。 若要使用此選項，您必須在伺服器和資料庫上啟用套件管理。 用戶端和伺服器環境都必須具有相同版本的 RevoScaleR。 |
| [rxInstalledPackages (英文)](/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 取得在指定計算內容中所安裝之套件的清單。 |
| [rxSyncPackages](/machine-learning-server/r-reference/revoscaler/rxsyncpackages) \(英文\) | 針對指定的計算內容，複製檔案系統和資料庫之間的套件程式庫相關資訊。 |
| [rxRemovePackages](/machine-learning-server/r-reference/revoscaler/rxremovepackages) \(英文\) | 從指定的計算內容中移除套件。 其也會計算相依性，並確保會移除 SQL Server 上的其他套件不再使用的套件，以便釋出資源。 |

## <a name="prerequisites"></a>Prerequisites

+ 已在 SQL Server 上啟用遠端管理。 如需詳細資訊，請參閱[在 SQL Server 上啟用遠端 R 套件管理](r-package-how-to-enable-or-disable.md)。

+ 用戶端和伺服器環境上具有相同版本的 RevoScaleR。 如需詳細資訊，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。

+ 您具有連線至伺服器和資料庫，以及執行 R 命令權限。 您必須是資料庫角色的成員，其能允許您在指定的執行個體和資料庫上安裝套件。

  + 處於 **共用範圍** 中的套件，可以由屬於特定資料庫中 `rpkgs-shared` 角色的使用者安裝。 此角色中的所有使用者都可以將共用套件解除安裝。

  + 處於 **私人範圍** 中的套件，可以由屬於資料庫中 `rpkgs-private` 角色的任何使用者安裝。 不過，使用者只能查看並解除安裝自己的套件。

  + 資料庫擁有者可以使用共用或私人套件。

## <a name="client-connections"></a>用戶端連接

用戶端工作站可以是位於相同網路上的 [Microsoft R 用戶端](/machine-learning-server/r-client/install-on-windows) \(英文\) 或 [Microsoft Machine Learning Server](/machine-learning-server/install/machine-learning-server-windows-install) \(英文\) (資料科學家通常會使用免費的開發人員版本)。

從遠端 R 用戶端呼叫套件管理函式時，您必須先使用 [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) \(英文\) 函式建立計算內容物件。 之後，針對您使用的每個套件管理函式，請將計算內容以引數的形式傳遞。

使用者身分識別通常會在設定計算內容時指定。 如果您在建立計算內容時不指定使用者名稱和密碼，系統會使用執行 R 程式碼的使用者身分識別。

1. 從 R 命令列，定義針對執行個體和資料庫的連接字串。
2. 使用 [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) \(英文\) 建構函式來使用連接字串定義 SQL Server 計算內容。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 建立您想要安裝之套件的清單，然後將清單儲存在字串變數中。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 呼叫 [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) \(英文\) 並傳遞計算內容，以及包含套件名稱的字串變數。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果需要相依套件，系統也會加以安裝，前提是用戶端上有可用的網際網路連線。
    
    系統會使用進行連線之使用者的認證，在該使用者的預設範圍中安裝套件。

## <a name="call-package-management-functions-in-stored-procedures"></a>在預存程序中呼叫套件管理函式

您可以在 `sp_execute_external_script` 內執行套件管理函式。 當您這麼做時，系統會使用預存程序呼叫者的安全性內容來執行函式。

## <a name="examples"></a>範例

此節提供如何在連線至 SQL Server 執行個體或資料庫作為計算內容的情況下，從遠端用戶端使用這些函式的範例。

針對所有範例，您必須提供連接字串或是計算內容 (其需要連接字串)。 此範例提供針對 SQL Server 建立計算內容的其中一個方法：

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

取決於伺服器的所在位置，以及安全性模型，您可能需要在連接字串中提供網域和子網路規格，或是使用 SQL 登入。 例如：

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>在遠端 SQL Server 計算內容上取得套件路徑

此範例會取得計算內容 **上** RevoScaleR`sqlcc` 套件的路徑。

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**結果**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> 如果您已啟用查看 SQL 主控台輸出的選項，您可能會從 `print` 陳述式之前的函式取得狀態訊息。 在您完成程式碼測試之後，請在計算內容建構函式中將 `consoleOutput` 設定為 FALSE 以排除訊息。

### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會取得計算內容 **上** RevoScaleR **和** lattice`sqlcc` 套件的路徑。 若要取得多個套件的相關資訊，請傳遞包含套件名稱的字串向量。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>在遠端計算內容上取得套件版本

從 R 主控台執行此命令，來取得計算內容 *sqlServer* 上所安裝之套件的組建編號和版本號碼。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

此範例會將 **forecast** 套件及其相依性安裝到計算內容中。

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>從 SQL Server 移除封裝

此範例會將 **forecast** 套件及其相依性從計算內容中移除。

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>在資料庫和檔案系統之間同步套件

下列範例會檢查資料庫 **TestDB**，並判斷所有套件是否皆已安裝到檔案系統中。 如果遺失某些套件，系統會在檔案系統中加以安裝。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

套件同步會以每個資料庫及每個使用者為基礎運作。 如需詳細資訊，請參閱 [SQL Server 的 R 套件同步](package-install-uninstall-and-sync.md)。

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>使用預存程序來在 SQL Server 中列出套件

從 Management Studio 或其他支援 T-SQL 的工具執行此命令，以在預存程序中使用 `rxInstalledPackages` 來取得目前執行個體上的已安裝套件清單。

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths` 函式可以用來判斷 SQL Server 機器學習服務所使用的作用中程式庫。 此指令碼只能傳回目前伺服器的程式庫路徑。 

```sql
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```

## <a name="see-also"></a>另請參閱

+ [啟用遠端 R 封裝管理](r-package-how-to-enable-or-disable.md)
+ [同步 R 套件](package-install-uninstall-and-sync.md)
+ [使用 R 套件的祕訣](tips-for-using-r-packages.md)
+ [取得 R 套件資訊](../package-management/r-package-information.md)