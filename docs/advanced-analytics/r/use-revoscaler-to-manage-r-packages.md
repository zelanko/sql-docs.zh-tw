---
title: 如何使用 RevoScaleR 函數來尋找或安裝 R 套件
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: dafbe12c6304866dc36dde6fffec44da441e582f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344829"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函數在 SQL Server 上尋找或安裝 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 和更新版本包含 R 套件管理 SQL Server 計算內容的函式。 遠端、非系統管理員可以使用這些函式在 SQL Server 上安裝封裝, 而不需要直接存取伺服器。

SQL Server 2017 Machine Learning 服務已包含較新版本的 RevoScaleR。 SQL Server 2016 R 服務客戶必須執行[元件升級](../install/upgrade-r-and-python.md), 才能取得 RevoScaleR 套件管理功能。 如需有關如何取得封裝版本和內容的指示, 請參閱[取得封裝資訊](../package-management/installed-package-information.md)。

## <a name="revoscaler-functions-for-package-management"></a>適用于封裝管理的 RevoScaleR 函式

下表描述用於 R 封裝安裝和管理的功能。

| 功能 | 描述 |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | 判斷遠端 SQL Server 上實例程式庫的路徑。 |
| [rxFindPackage (英文)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 取得遠端 SQL Server 上一或多個封裝的路徑。 |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | 從遠端 R 用戶端呼叫此函式, 從指定的存放庫或藉由讀取本機儲存的壓縮封裝, 在 SQL Server 計算內容中安裝套件。 此函式會檢查相依性, 並確保可以將任何相關的套件安裝至 SQL Server, 就像在本機計算內容中安裝 R 套件一樣。 若要使用此選項, 您必須已在伺服器和資料庫上啟用封裝管理。 用戶端和伺服器環境都必須有相同版本的 RevoScaleR。 |
| [rxInstalledPackages (英文)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 取得在指定的計算內容中安裝的封裝清單。 |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 在檔案系統與資料庫之間, 針對指定的計算內容複寫有關封裝程式庫的資訊。 |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 從指定的計算內容中移除封裝。 它也會計算相依性, 並確保移除 SQL Server 上其他封裝不再使用的封裝, 以釋放資源。 |

## <a name="prerequisites"></a>先決條件

+ [在 SQL Server 上啟用遠端 R 套件管理](r-package-how-to-enable-or-disable.md)

+ 用戶端和伺服器環境上的 RevoScaleR 版本必須相同。 如需詳細資訊, 請參閱[取得封裝資訊](../package-management/installed-package-information.md)。

+ 連接到伺服器和資料庫, 以及執行 R 命令的許可權。 您必須是資料庫角色的成員, 讓您能夠在指定的實例和資料庫上安裝封裝。

+ 屬於指定資料庫中角色的使用者, 可以安裝**共用領域**中的`rpkgs-shared`封裝。 此角色中的所有使用者都可以卸載共用的封裝。

+ 私用**範圍**中的封裝可以由任何屬於資料庫中角色`rpkgs-private`的使用者來安裝。 不過, 使用者只能看到並卸載自己的套件。

+ 資料庫擁有者可以使用共用或私用封裝。

## <a name="client-connections"></a>用戶端連接

用戶端工作站可以[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (資料科學家通常會在相同的網路上使用免費的開發人員版本)。

從遠端 R 用戶端呼叫封裝管理函式時, 您必須先使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函數來建立計算內容物件。 之後, 針對您所使用的每個套件管理函式, 傳遞計算內容做為引數。

設定計算內容時, 通常會指定使用者識別。 如果您在建立計算內容時未指定使用者名稱和密碼, 則會使用執行 R 程式碼之使用者的身分識別。

1. 從 R 命令列中, 定義實例和資料庫的連接字串。
2. 使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)的函式, 以使用連接字串來定義 SQL Server 計算內容。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 建立您想要安裝的套件清單, 並將清單儲存在字串變數中。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 呼叫[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)並傳遞計算內容和包含封裝名稱的字串變數。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果需要相依套件, 則也會安裝它們, 假設用戶端上有網際網路連線。
    
    封裝會使用建立連線之使用者的認證, 在該使用者的預設範圍中安裝。

## <a name="call-package-management-functions-in-stored-procedures"></a>呼叫預存程式中的封裝管理函數

您已在內`sp_execute_external_script`執行套件管理功能。 當您這麼做時, 會使用預存程式呼叫者的安全性內容來執行函數。

## <a name="examples"></a>範例

本節提供的範例說明如何在連接到 SQL Server 實例或資料庫作為計算內容時, 從遠端用戶端使用這些函數。

針對所有範例, 您必須提供連接字串或需要連接字串的計算內容。 這個範例提供一種方法來建立 SQL Server 的計算內容:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

根據伺服器所在的位置和安全性模型, 您可能需要在連接字串中提供網域和子網規格, 或使用 SQL 登入。 例如:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>取得遠端 SQL Server 計算內容的封裝路徑

這個範例會取得計算內容`sqlcc`上的**RevoScaleR**封裝路徑。

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**結果**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> 如果您已啟用選項來查看 SQL 主控台輸出, 您可能會從`print`語句前面的函式取得狀態訊息。 在您完成程式碼測試之後, 請`consoleOutput`在計算內容的函式中將設定為 FALSE, 以排除訊息。

### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會在`sqlcc`計算內容上取得**RevoScaleR**和**lattice**封裝的路徑。 若要取得多個封裝的相關資訊, 請傳遞包含封裝名稱的字串向量。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>取得遠端計算內容上的套件版本

從 R 主控台執行此命令, 以取得計算內容*sqlServer*上所安裝之封裝的組建編號和版本號碼。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**結果**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

這個範例會將**預測**封裝及其相依性安裝到計算內容中。

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>從 SQL Server 移除封裝

此範例會從計算內容中移除**預測**封裝及其相依性。

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>同步處理資料庫與檔案系統之間的封裝

下列範例會檢查資料庫**TestDB**, 並判斷所有封裝是否安裝在檔案系統中。 如果部分封裝遺失, 則會安裝在檔案系統中。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

封裝同步處理適用于每個資料庫和每個使用者。 如需詳細資訊, 請參閱[SQL Server 的 R 封裝同步](../r/package-install-uninstall-and-sync.md)處理。

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>使用預存程式來列出中的封裝 SQL Server

從 Management Studio 或另一個支援 t-sql 的工具執行此命令, 以使用`rxInstalledPackages`預存程式中的, 取得目前實例上已安裝的封裝清單。

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

函式可以用來判斷 SQL Server Machine Learning 服務所使用的作用中程式庫。`rxSqlLibPaths` 此腳本只會傳回目前伺服器的程式庫路徑。 

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
+ [安裝 R 套件的秘訣](packages-installed-in-user-libraries.md)
+ [預設封裝](../package-management/default-packages.md)