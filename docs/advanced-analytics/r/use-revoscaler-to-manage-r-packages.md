---
title: 如何使用 RevoScaleR 函數來尋找或安裝 R 封裝的 SQL Server 上 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5e2fd6276e3429b7a59dc0729ce8901a984ec694
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函數來尋找或 SQL Server 上的安裝 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft R Server 版本 9.0.1 導入了新的 RevoScaleR 函數支援使用已安裝封裝，SQL Server 計算內容中。 這些新功能，方便執行 R 程式碼，並在 SQL Server 上安裝封裝，無法直接存取伺服器的資料科學家。

## <a name="how-does-it-work"></a>它如何運作

如果您有 R Server 9.0.1 或更新版本中，您可以使用[rxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages)函式，從遠端 R 用戶端安裝套件中的 SQL Server 計算內容。 若要使用此選項，您必須已啟用伺服器和資料庫上的封裝管理。 這項功能也需要對等版本的 R 服務或機器學習服務會安裝在伺服器上。

RevoScaleR 的新版本也包含這些函式： 

+ [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)函式中指定的計算內容取得一個或多個封裝的路徑。

    找不到封裝，或將封裝新增至特定資料庫，您可以使用使用者和領域的組合：

+ [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)函式會取得指定的計算內容中安裝的封裝清單。

+ [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)函式會將封裝安裝到計算內容中，從指定的儲存機制，或藉由讀取本機儲存壓縮封裝。

    此函式會檢查有相依性，並確保任何相關的封裝可以安裝到 SQL Server，就像在本機計算內容中的 R 封裝安裝。

+ [RxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages)函式會移除指定的計算內容中的封裝。

    它也會計算相依性，並可確保，移除不再由 SQL Server 上的其他封裝的封裝，以便釋出資源。

+ 使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函式來複製之間的檔案系統和資料庫中，為指定的計算內容套件程式庫的相關資訊。

+ 使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函式來判斷路徑的執行個體上的程式庫的 SQL Server 計算內容。

**適用於：** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]。 此外也提供支援[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]進行升級時為 R Server 9.0 或更新版本。 其他限制也適用。

## <a name="requirements"></a>需求

+ 若要執行這些函式，您必須連接到伺服器和資料庫，以及執行 R 命令的權限。

+ 使用這些函數，從遠端 R 用戶端時，您必須建立計算內容物件首先，使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式。 之後，您使用的每個封裝管理功能，通過計算內容做為引數。

+ 如果您未指定使用者名稱和密碼建立計算內容時，會使用執行 R 程式碼之使用者的身分識別。

+ 它也可執行的封裝管理功能內`sp_execute_external_script`。 當您這樣做時，請使用預存程序的呼叫端的安全性內容執行函式。

+ 封裝中**共用範圍**屬於的使用者可以安裝`rpkgs-shared`中指定的資料庫角色。 此角色中的所有使用者，可以解除都安裝共用的封裝。

+ 封裝中**私用範圍**可以屬於任何使用者安裝`rpkgs-private`資料庫中的角色。 不過，使用者可以看到，並解除安裝它們自己的封裝。

+ 資料庫擁有者可以使用共用或私用的封裝。

## <a name="package-installation-from-machine-learning-server-or-remote-r-client"></a>從機器學習伺服器或遠端 R 用戶端封裝安裝

開始之前，請確定符合這些條件：

+ 您的用戶端具有 RevoScale 9.0.1 或更新版本。
+ RevoScaleR 的對等版本已安裝 SQL Server 執行個體。
+ [封裝管理功能](..\r\r-package-how-to-enable-or-disable.md)執行個體上已啟用。
+ 您是可讓您指定的執行個體和資料庫上安裝封裝的資料庫角色的成員。 在未來，角色會共用或私用位置支援設為 安裝套件。 現在，您可以安裝封裝，如果您是資料庫擁有者。

1. 從 R 命令列定義的執行個體和資料庫的連接字串。
2. 使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)建構函式來定義 SQL Server 計算內容，使用連接字串。

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

    如果相依套件是必要的它們會一併安裝，假設在用戶端提供網際網路連線。
    
    封裝會安裝使用進行連接，該使用者的預設範圍中之使用者的認證。

## <a name="examples"></a>範例

本節提供如何連接到 SQL Server 執行個體或資料庫做為計算內容時使用這些函式，從遠端用戶端的範例。

所有範例中，您必須都提供連接字串或為運算環境，需要連接字串。 此範例提供一種方式建立 SQL Server 計算內容：

```R
instance_name <- "Machine name/Instance name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

根據伺服器所在和安全性模型，您可能需要提供連接字串中的網域和子網路規格，或使用 SQL 登入。 例如：

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"


### Get package path on a remote SQL Server compute context

This example gets the path for the **RevoScaleR** package on the compute context, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**結果**

"C: / Program 檔案/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/程式庫/RevoScaleR"

> [!TIP]
> 如果您已啟用，請參閱 SQL 主控台輸出的選項，您可能會收到狀態訊息之前的函式從`print`陳述式。 當您完成測試您的程式碼之後，設定`consoleOutput`為 FALSE 的計算內容建構函式消除訊息中。

### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會取得的路徑**RevoScaleR**和**斜格紋**計算內容上的封裝， `sqlcc`。 若要取得多個封裝的相關資訊，請傳遞字串向量，其中包含封裝名稱。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>取得遠端計算內容上的封裝版本

執行此命令從 R 主控台上計算內容中，安裝的封裝中取得的組建編號和版本號碼*sqlServer*。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**結果**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

此範例會安裝**預測**封裝和其相依性到計算內容。

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>從 SQL Server 移除封裝

這個範例會移除**預測**封裝和其相依性從計算內容。

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>同步處理資料庫和檔案系統之間的封裝

下列範例會檢查資料庫**TestDB**，並決定是否在檔案系統中安裝所有封裝。 如果遺漏了某些封裝，它們會安裝在檔案系統。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

適用於封裝的同步處理每個資料庫和每個使用者為基礎。 如需詳細資訊，請參閱[R 封裝的同步處理 SQL server](../r/package-install-uninstall-and-sync.md)。

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>使用 SQL Server 中的列出封裝的預存程序

從 Management Studio 或其他工具，可支援 T-SQL，以取得已安裝的封裝清單，在目前的執行個體，執行此命令使用`rxInstalledPackages`預存程序。

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths`函式可用來判斷 SQL Server 機器學習服務使用作用中的程式庫。 此指令碼可能會傳回只針對目前的伺服器程式庫路徑。 

```SQL
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
