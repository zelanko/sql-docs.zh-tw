---
title: "SQL Server 的 R 封裝管理 |Microsoft 文件"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 封裝管理

本主題描述可用來管理 SQL Server 執行個體執行的 R 封裝的封裝管理功能。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="package-management-using-t-sql"></a>使用 T-SQL 的封裝管理

您可以繼續的電腦上，系統管理員身分安裝 R 封裝，如果您沒有這些權限，而且如果您是唯一的人使用機器學習工作的伺服器。

不過，如果您要與他人共用封裝，或有多人需要在伺服器上執行機器學習工作，它會更有效率，設定套件共用程式庫。 SQL Server 支援透過資料庫角色。

資料庫管理員負責設定角色，以及新增使用者至角色。 透過角色，資料庫管理員可以控制已加入或移除 SQL Server 環境中，R 封裝的權限的人員，以及可以稽核套件安裝。

### <a name="database-roles-for-package-management"></a>用於封裝管理的資料庫角色

下列新的資料庫角色支援安全的安裝 R 封裝管理中與 SQL Server:

- `rpkgs-users`： 可讓使用者使用所安裝的成員的任何共用的封裝`rpkgs-shared`角色。

- `rpkgs-private`： 提供的相同權限與共用封裝的存取權`rpkgs-users`角色。 此角色成員也可以安裝、移除和使用具有私用範圍的封裝。

-  `rpkgs-shared`： 提供相同的權限`rpkgs-private`角色。 屬於此角色成員的使用者也可以安裝或移除共用封裝。

- `db_owner`： 具有相同的權限`rpkgs-shared`角色。 也可以授與使用者安裝或移除共用和私用封裝的權限。

### <a name="creating-an-external-package-library-using-t-sql"></a>建立使用 T-SQL 的外部封裝程式庫

此外，SQL Server 2017 支援 T-SQL 陳述式**建立外部程式庫**、 支援的資料庫管理員外部的程式庫的管理。 目前您可以使用此陳述式來建立 Windows 架構的程式庫 r 額外支援已規劃未來 Python 封裝和其他平台，例如 Linux 上執行寫入的封裝。

如需詳細資訊，請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="package-management-using-r"></a>使用 R 封裝管理

**RevoScaleR**封裝現在包含函式來支援更容易安裝及管理的 R 封裝。 這些新的函式，資料庫角色的封裝管理與結合可支援這些案例：

- 資料科學家可以安裝 SQL Server 上所需的 R 封裝，而不需要 SQL Server 電腦的系統管理權限。
- 針對每個資料庫上會安裝封裝和封裝當移動資料庫時，隨著一起移動。
- 它很容易與其他人共用封裝。 如果您設定本機封裝儲存機制時，每個資料科學家可以使用儲存機制安裝套件，他或她自己的資料庫。
- 資料庫管理員不需要了解如何執行 R 命令，並不需要追蹤複雜封裝的相依性。
- DBA 可以使用熟悉的資料庫角色，來控制允許哪些 SQL Server 的使用者安裝、 解除安裝，或使用封裝。

### <a name="r-package-management-functions"></a>R 封裝管理功能

RevoScaleR，提供下列封裝管理功能的安裝與移除指定的計算內容中的封裝：

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages)： 尋找指定的計算內容中安裝套件的相關資訊。

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages)： 安裝封裝到計算內容中，從指定的儲存機制，或藉由讀取本機儲存壓縮封裝。

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages)： 移除計算內容從安裝套件。

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage)： 取得指定的計算內容中的一個或多個封裝的路徑。

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)： 在指定的計算內容中複製封裝程式庫檔案系統與資料庫之間。

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths)： 在 SQL Server 內執行時取得封裝程式庫的樹狀目錄的搜尋路徑。

根據預設，在 SQL Server 2017 也包含這些封裝。 您可以將封裝加入 SQL Server 2016 的執行個體，如果您執行個體升級到最少使用 Microsoft R 9.0.1。 如需詳細資訊，請參閱[使用 SqlBindR.exe 升級 R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

如需這些函數的資訊，請參閱 RevoScaleR 函式參考頁面: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>封裝管理的運作方式

如果您具有安裝封裝的權限，您可以從 R 程式碼執行其中一個封裝管理函數，並指定要加入或移除封裝的計算內容。 計算內容可以是您的本機電腦，或 SQL Server 執行個體上的資料庫。 如果在 SQL Server 上執行安裝封裝的呼叫，您的認證會決定是否可以在伺服器上完成作業。 封裝安裝函數會檢查相依性，並確保所有相關的封裝都會安裝至 SQL Server，就像是本機計算內容中的 R 封裝安裝一樣。 解除安裝封裝的函數也會計算相依性，並確保移除 SQL Server 上的其他封裝不再使用的封裝，以便釋出資源。

每個資料科學家可以安裝不會顯示給其他人的私人封裝建立 R 封裝的私用沙箱。 因為封裝可以限定在資料庫和每一位使用者每個資料庫中取得隔離的套件沙箱，所以您更輕鬆地安裝不同版本的相同的 R 封裝。

如果您將工作資料庫移轉至新的伺服器時，您可以使用封裝的同步處理函式來讀取您的封裝清單，並將其安裝在新的伺服器上的資料庫。

> [!NOTE]
> 
> 開始使用 Microsoft R Server 9.0.1 提供封裝管理的 R 函數。 如果您在 RevoScaleR 中找不到函式，您可能需要升級至最新版本。

### <a name="bkmk_scope"></a>封裝範圍的角色

新的封裝管理函數提供兩種範圍，可在 SQL Server 的特定資料庫上安裝和使用封裝：

- **共用範圍**

  *共用範圍*表示具有共用的範圍角色的權限之使用者 (`rpkgs-shared`) 可以安裝和解除安裝指定的資料庫中的封裝。 安裝在共用範圍中的封裝可供 SQL Server 資料庫的其他使用者使用，但前提是這些使用者可以使用已安裝的 R 封裝。

- **私用範圍**

  *私用範圍*表示使用者已經提供成員資格的私用範圍的角色 (`rpkgs-private`) 可以安裝或解除封裝安裝到每個使用者定義的私用程式庫位置。 因此，安裝在私用範圍中的任何封裝只能供安裝的使用者使用。 換句話說，SQL Server 上的使用者無法使用其他使用者所安裝的私用封裝。

您可以結合這些「共用」  和「私用」  範圍模型，開發可在 SQL Server 上部署和管理封裝的自訂安全系統。

例如，藉由使用共用範圍，可授與資料科學家群組的負責人或管理員安裝封裝的權限，這些封裝接著可供相同 SQL Server 執行個體中的所有其他使用者或資料科學家使用。

另一種情況可能需要提高使用者之間的隔離，或使用不同版本的封裝。 在此情況下，負責只安裝和使用所需封裝的資料科學家，可透過私用範圍來取得個別權限。 由於這些封裝是針對每位使用者所安裝，因此某位使用者所安裝的封裝不會影響使用相同 SQL Server 資料庫之其他使用者的工作。

### <a name="synchronizing-r-package-libraries"></a>同步處理的 R 封裝程式庫

CTP 2.0 版本的 SQL Server 2017 （和 Microsoft R Server 2017 年 4 月發行） 包含新的 R 函數，如*同步處理封裝*。

封裝的同步處理表示 database engine 會追蹤由特定擁有者和群組，並視需要將這些封裝寫入數個檔案系統的封裝。 在這些情況下，您可以使用封裝的同步處理：

+ 您想要 SQL Server 執行個體之間移動的 R 封裝
+ 您需要重新安裝套件的特定使用者或群組之後還原資料庫

如需詳細資訊，請參閱[rxSyncPackages](../r/package-install-uninstall-and-sync.md)。

## <a name="examples"></a>範例

這些範例示範基本的使用方式，封裝管理功能。 若要執行這些命令需要您有執行個體上執行 R 命令的權限。

+ 從終端機遠端 R 執行時，您會建立計算內容物件，指定 SQL Server 執行個體，然後再執行此函式，做為引數傳遞的計算內容。

+ 若要從預存程序中執行封裝管理功能，您必須將它們包裝在呼叫`sp_execute_external_script`。

### <a name="package-scoping"></a>封裝範圍

這個範例會檢查執行個體已安裝的封裝`myServer`，在資料庫中`TestDB`。 封裝管理範圍的特定資料庫和使用者。 如果使用者未指定，則會假設執行計算內容，請呼叫的使用者。 如需詳細資訊，請參閱[封裝角色的領域設定](#bkmk_scope)。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>取得遠端的 SQL Server 計算內容上的封裝位置

此範例會取得計算內容 **sqlServer** 上的 *RevoScaleR*封裝路徑。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會取得計算內容 **sqlServer** 上的 **RevoScaleR** 和 *lattice*封裝路徑。 若要取得多個封裝的相關資訊，請傳遞字串向量，其中包含封裝名稱。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

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

### <a name="get-package-versions-on-a-remote-compute-context"></a>取得遠端計算內容上的封裝版本

執行此命令從 R 主控台上計算內容中，安裝的封裝中取得的組建編號和版本號碼*sqlServer*。

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

此範例會將 **ggplot2** 封裝及其相依性安裝到計算內容 *sqlServer*中。

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

### <a name="package-synchronization"></a>封裝的同步處理

下列範例會同步處理管理資料庫中的封裝清單之檔案系統中已安裝的套件。 如果遺漏了某些封裝，它們會安裝在檔案系統。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>後續的步驟

[如何啟用或停用的 R 封裝管理](../r/r-package-how-to-enable-or-disable.md)

