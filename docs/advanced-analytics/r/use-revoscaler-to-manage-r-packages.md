---
title: "如何使用 RevoScaleR 函數來尋找或安裝 R 封裝的 SQL Server 上 |Microsoft 文件"
ms.custom: 
ms.date: 01/08/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: e10435c2a0cdc5ed181aeab9bdd0bbfefa9a7f25
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>如何使用 RevoScaleR 函數來尋找或 SQL Server 上的安裝 R 封裝

Microsoft R Server 版本 9.0.1 導入了新的 RevoScaleR 函數支援使用已安裝封裝，SQL Server 計算內容中。 這些新功能，方便在 SQL Server 中執行 R 程式碼無法直接存取伺服器的資料科學家。

每個資料科學家可以安裝不讓其他人看見的私人封裝。 因為封裝可以限定在資料庫和每一位使用者每個資料庫中取得隔離的套件沙箱，所以您更輕鬆地安裝不同版本的相同的 R 封裝。

如果您將工作資料庫移轉至新的伺服器時，您也可以使用封裝的同步處理函式來讀取您的封裝清單，並將其安裝在新的伺服器上的資料庫。

本文將描述這些函式，並提供函式的使用方式的範例。

## <a name="requirements"></a>需求

+ 若要執行這些函式，您必須執行個體上執行 R 命令的權限。

+ 如果您未指定使用者名稱和密碼建立計算內容時，會使用執行 R 程式碼之使用者的身分識別。

+ 使用這些函數，從遠端 R 用戶端時，您必須建立計算內容物件首先，使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式。 之後，您使用的每個封裝管理功能，通過計算內容做為引數。

+ 可執行的封裝管理功能使用`sp_execute_external_script`。 當您這樣做時，請使用預存程序的呼叫端的安全性內容執行函式。

## <a name="list-of-package-management-functions"></a>封裝管理功能的清單

RevoScaleR，提供下列封裝管理功能的安裝與移除指定的計算內容中的封裝：

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)： 尋找指定的計算內容中安裝套件的相關資訊。

+ [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)： 安裝封裝到計算內容中，從指定的儲存機制，或藉由讀取本機儲存壓縮封裝。

+ [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages)： 移除計算內容從安裝套件。

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)： 取得指定的計算內容中的一個或多個封裝的路徑。

+ [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)： 在指定的計算內容中複製封裝程式庫檔案系統與資料庫之間。

+ [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)： 在 SQL Server 內執行時取得封裝程式庫的樹狀目錄的搜尋路徑。

根據預設，在 SQL Server 2017 包含這些封裝。 如需這些函數的資訊，請參閱 RevoScaleR 函式參考頁面: (https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> 封裝管理的 R 函數會從 Microsoft R Server 9.0.1。 如果您在 RevoScaleR 中找不到函式，您可能需要升級至最新版本。 

## <a name="examples"></a>範例

本章節包含如何使用 SQL Server 執行個體或資料庫中的封裝管理功能的範例。 

+ 封裝安裝函數會檢查相依性，並確保所有相關的封裝都會安裝至 SQL Server，就像是本機計算內容中的 R 封裝安裝一樣。

+ 此函式，_解除安裝_封裝也會計算相依性，並可確保，移除不再由 SQL Server 上的其他封裝的封裝，以便釋出資源。

+ 找不到封裝，或將封裝新增至特定資料庫，您可以使用使用者和領域的組合：

    + 封裝中**共用範圍**屬於的使用者可以安裝`rpkgs-shared`中指定的資料庫角色。 此角色中的所有使用者，可以解除都安裝共用的封裝。
    + 封裝中**私用範圍**可以屬於任何使用者安裝`rpkgs-private`資料庫中的角色。 不過，使用者可以看到，並解除安裝它們自己的封裝。
    + 資料庫擁有者可以使用共用或私用的封裝。

**從 R 程式碼**

如果您有安裝封裝的權限，執行封裝的其中一個管理功能從您的 R 用戶端，並指定要加入或移除封裝的位置計算內容。  計算內容可以是您的本機電腦，或 SQL Server 執行個體上的資料庫。 您的認證會決定是否可以在伺服器上完成作業。

**From Transact-SQL**

若要從預存程序中執行封裝管理功能，將它們包裝在呼叫`sp_execute_external_script`。

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>取得 SQL Server 計算內容中的封裝清單

這個範例會檢查執行個體已安裝的封裝`myServer`，在資料庫中`TestDB`。 封裝管理範圍的特定資料庫和使用者。 如果使用者未指定，則會假設執行計算內容，請呼叫的使用者。 如需詳細資訊，請參閱[封裝角色的領域設定](#bkmk_scope)。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>取得封裝路徑上的遠端 SQL Server 計算內容

此範例會取得計算內容 **sqlServer** 上的 *RevoScaleR*封裝路徑。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會取得計算內容 **sqlServer** 上的 **RevoScaleR** 和 *lattice*封裝路徑。 若要取得多個封裝的相關資訊，請傳遞字串向量，其中包含封裝名稱。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>取得遠端計算內容上的封裝版本

執行此命令從 R 主控台上計算內容中，安裝的封裝中取得的組建編號和版本號碼*sqlServer*。

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

此範例會安裝**預測**封裝和其相依性到計算內容中， *sqlServer*。

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>從 SQL Server 移除封裝

此範例會從計算內容 **sqlServer** 移除 *ggplot2*封裝及其相依性。

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
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
