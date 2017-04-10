---
title: "SQL Server R 服務的 R 封裝管理 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server R 服務的 R 封裝管理
為了能夠更輕鬆地管理 SQL Server 執行個體上所執行的 R 封裝，**RevoScaleR** 封裝現在包含可支援 R 封裝安裝和管理的函數。 

這項新功能支援下列幾種情況：

- 資料科學家可以在 SQL Server 上安裝所需的 R 封裝，而不需要具有 SQL Server 電腦的系統管理存取權。 這些封裝會安裝到每個資料庫上。
- 您可以輕鬆與其他人共用封裝。 只要建立本機封裝存放庫，並讓每位資料科學家將封裝安裝到個別資料庫即可。
- 資料庫管理員不需要了解如何執行 R 命令，也不需要了解封裝相依性。 DBA 使用資料庫角色，來控制哪些 SQL Server 使用者可以安裝、解除安裝或使用封裝。
 
**運作方式**

* 資料庫管理員負責設定角色及將使用者加入角色，以控制哪些人員有權限在 SQL Server 環境中加入或移除 R 封裝。
* 如果您具有安裝封裝的權限，您可以從 R 程式碼執行其中一個封裝管理函數，並指定要加入或移除封裝的計算內容。 計算內容可以是您的本機電腦，或 SQL Server 執行個體上的資料庫。 
* 如果在 SQL Server 上執行安裝封裝的呼叫，您的認證會決定是否可以在伺服器上完成作業。 
- 封裝安裝函數會檢查相依性，並確保所有相關的封裝都會安裝至 SQL Server，就像是本機計算內容中的 R 封裝安裝一樣。
- 解除安裝封裝的函數也會計算相依性，並確保移除 SQL Server 上的其他封裝不再使用的封裝，以便釋出資源。
- 每個資料科學家可以安裝其他人看不到的私用封裝，這會提供他們一個隔離的沙箱來處理自己的 R 封裝。
-  因為封裝可以限定為一個資料庫，而且每位使用者會在每個資料庫中取得一個隔離的封裝沙箱，所以可以更容易使用相同 R 封裝的不同版本進行安裝。 

> [!NOTE]
> 這項功能目前僅針對搭配使用 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 發行。 

## <a name="database-roles-and-database-scoping"></a>資料庫角色和資料庫範圍

新的封裝管理函數提供兩種範圍，可在 SQL Server 的特定資料庫上安裝和使用封裝：

- **共用範圍**

  「共用範圍」表示具有共用範圍角色 (**rpkgs-shared**) 權限的使用者可以在指定的資料庫上安裝和解除安裝封裝。 安裝在共用範圍中的封裝可供 SQL Server 資料庫的其他使用者使用，但前提是這些使用者可以使用已安裝的 R 封裝。 

- **私用範圍** 

  「私用範圍」表示具有私用範圍角色 (**rpkgs-private**) 成員資格的使用者，可以在每位使用者定義的私用程式庫位置安裝或解除安裝封裝。 因此，安裝在私用範圍中的任何封裝只能供安裝的使用者使用。 換句話說，SQL Server 上的使用者無法使用其他使用者所安裝的私用封裝。 

您可以結合這些「共用」和「私用」範圍模型，開發可在 SQL Server 上部署和管理封裝的自訂安全系統。 

例如，藉由使用共用範圍，可授與資料科學家群組的負責人或管理員安裝封裝的權限，這些封裝接著可供相同 SQL Server 執行個體中的所有其他使用者或資料科學家使用。 

另一種情況可能需要提高使用者之間的隔離，或使用不同版本的封裝。 在此情況下，負責只安裝和使用所需封裝的資料科學家，可透過私用範圍來取得個別權限。 由於這些封裝是針對每位使用者所安裝，因此某位使用者所安裝的封裝不會影響使用相同 SQL Server 資料庫之其他使用者的工作。 

### <a name="database-roles-for-package-management"></a>用於封裝管理的資料庫角色

下列新的資料庫角色支援 SQL R 服務的安全安裝和封裝管理： 

- **rpkgs-users**：可讓使用者使用 **rpkgs-shared** 角色成員所安裝的任何共用封裝。

- **rpkgs-private**：提供與 **rpkgs-users** 角色相同的權限來存取共用封裝。 此角色成員也可以安裝、移除和使用具有私用範圍的封裝。

-  **rpkgs-shared**：提供與 **rpkgs-private** 角色相同的權限。 屬於此角色成員的使用者也可以安裝或移除共用封裝。 
 
- **db_owner**：具有與 **rpkgs-shared** 角色相同的權限。 也可以授與使用者安裝或移除共用和私用封裝的權限。



## <a name="new-package-management-functions"></a>新的封裝管理函數


+ `rxInstalledPackages`︰尋找指定計算內容中所安裝之封裝的相關資訊。

+ `rxInstallPackages`︰從指定的儲存機制，或透過讀取本機儲存的壓縮封裝，將封裝安裝到計算內容中。

+ `rxRemovePackages`︰從計算內容中移除已安裝的封裝。

+ `rxFindPackage`︰取得指定計算內容中一或多個封裝的路徑。

+ `rxSqlLibPaths`︰取得在 SQL Server 內執行之封裝的程式庫樹狀結構路徑。

## <a name="examples"></a>範例

### <a name="get-package-location-on-sql-server-compute-context"></a>取得 SQL Server 計算內容上的封裝位置

此範例會取得計算內容 *sqlServer* 上的 **RevoScaleR** 封裝路徑。

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>取得多個封裝的位置

下列範例會取得計算內容 *sqlServer* 上的 **RevoScaleR** 和 **lattice** 封裝路徑。 當找到多個封裝的相關資訊後，會傳遞包含封裝名稱的字串向量。

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>列出指定計算內容中的封裝

此範例會列出計算內容 *sqlServer* 中安裝的所有封裝，然後顯示在主控台中。

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>取得封裝版本

此範例會取得計算內容 *sqlServer* 上所安裝之封裝的組建編號和版本號碼。

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer) 
```

### <a name="install-a-package-on-sql-server"></a>在 SQL Server 上安裝封裝

此範例會將 **ggplot2** 封裝及其相依性安裝到計算內容 *sqlServer* 中。

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>從 SQL Server 移除封裝

此範例會從計算內容 *sqlServer* 移除 **ggplot2** 封裝及其相依性。

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

## <a name="see-also"></a>另請參閱

[如何啟用或停用 R 封裝管理](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)