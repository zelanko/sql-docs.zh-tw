---
title: 使用 miniCRAN 建立存放庫
description: 了解如何使用 miniCRAN 套件離線安裝 R 套件，以建立套件和相依性的本機存放庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c8ddfcf997cd4cc62f1c65efd7ecfc4cf3aff730
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118151"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>使用 miniCRAN 建立本機 R 套件存放庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文描述如何使用 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) \(英文\) 離線安裝 R 套件，以建立套件和相依性的本機存放庫。 **miniCRAN** 會識別套件和相依性並下載至單一資料夾，讓您可複製到其他電腦以進行離線 R 套件安裝。

您可以指定一或多個套件，而 **miniCRAN** 會以遞迴方式讀取這些套件的相依性樹狀結構。 然後，它只會從 CRAN 或類似的存放庫下載列出的套件及其相依性。

完成後，**miniCRAN** 會建立內部一致的存放庫，其中包含選取的套件及所有必要的相依性。 您可以將此本機存放庫移至伺服器，並且在沒有網際網路連線的情況下繼續安裝套件。

有經驗的 R 使用者通常會在已下載套件的描述檔案中尋找相依套件清單。 不過，**匯入**中列出的套件可能具有第二層相依性。 基於這個理由，建議使用 **miniCRAN** 來組合必要套件的完整集合。

## <a name="why-create-a-local-repository"></a>為何要建立本機存放庫

建立本機套件存放庫的目標是，提供伺服器系統管理員或組織中其他使用者可用來在伺服器上安裝新 R 套件的單一位置，特別是無法存取網際網路的使用者。 建立存放庫之後，您可以藉由新增套件或升級現有套件版本進行修改。

套件存放庫適用於下列案例：

- **安全性**：許多 R 使用者都習慣從 CRAN 或其鏡像網站之一隨意下載並安裝新的 R 套件。 不過，基於安全性理由，執行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的實際執行伺服器通常不具網際網路連線能力。

- **更輕鬆進行離線安裝**：若要將套件安裝到離線服務器，您也必須下載所有套件相依性。 使用 miniCRAN 可讓您更輕鬆地以正確的格式取得所有相依性，並避免相依性錯誤。

- **已改良版本管理**：在多使用者環境中，有充分的理由來避免在伺服器上無限制地安裝多個套件版本。 使用本機存放庫，為使用者提供一組一致性套件。

## <a name="install-minicran"></a>安裝 miniCRAN

**miniCRAN** 套件本身相依於 18 個其他 CRAN 套件，其中 **RCurl** 套件具有 **curl-devel** 套件的系統相依性。 同樣地，套件 **XML** 具有 **libxml2-devel** 的相依性。 若要解決相依性，建議您一開始就在具有完整網際網路存取權的電腦上建置本機存放庫。

在具有基底 R、R 工具及網際網路連線的電腦上執行下列命令。 假設這不是您的 SQL Server 電腦。 下列命令會安裝 **miniCRAN** 套件和 **igraph** 套件。 此範例會檢查是否已經安裝套件，但您可以略過 `if` 陳述式，直接安裝套件。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>設定 CRAN 鏡像和 MRAN 快照集

指定要用來取得套件的鏡像網站。 例如，您可以使用 MRAN 網站，或您所在區域中包含所需套件的任何其他網站。 如果下載失敗，請嘗試另一個鏡像網站。

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>建立本機資料夾

建立本機資料夾，以將所收集的套件儲存於其中。 如果您經常重複此動作，可能就會想要使用描述性名稱，例如 "miniCRANZooPackages" 或 "miniCRANMyRPackageV2"。

將資料夾指定為本機存放庫。 R 語法會針對路徑名稱使用斜線，這與 Windows 慣例相反。

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>將套件新增至本機存放庫

安裝並載入 **miniCRAN** 之後，建立清單來指定您想要下載的其他套件。

**請勿**將相依性新增至此初始清單。 **miniCRAN** 所使用的 **igraph** 套件會自動產生相依性清單。 如需如何使用所產生之相依性關係圖的詳細資訊，請參閱[使用 miniCRAN 來識別套件相依性](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html) \(英文\)。

1. 將目標套件 "zoo" 和 "forecast" 新增至變數。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 選擇性地繪製相依性關係圖。 這並非必要，但它可提供很多資訊。

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 建立本機存放庫。 如有必要，務必將 R 版本變更為安裝在您 SQL Server 執行個體上的版本。 如果您已進行元件升級，則您的版本可能比原始版本還新。 如需詳細資訊，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   在此資訊中，miniCRAN 套件會建立您稍後將套件複製到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 所需的資料夾結構。

此時，您應該會有一個資料夾，其中包含您所需的套件及所需的任何其他套件。 此資料夾應該包含 ZIP 壓縮套件的集合。 請勿將套件解壓縮或將任何檔案重新命名。

選擇性地執行下列程式碼，以列出本機 miniCRAN 存放庫中內含的套件。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>將套件新增至執行個體程式庫

當您擁有具備所需套件的本機存放庫之後，將該套件存放庫移至 SQL Server 電腦。 下列程序描述如何使用 R 工具安裝套件。

::: moniker range=">sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 安裝套件的建議方法是使用 **sqlmlutils**。 請參閱[使用 sqlmlutils 安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。
::: moniker-end

1. 將包含 miniCRAN 存放庫的資料夾完整複製到您打算安裝套件的伺服器。 該資料夾通常具有下列結構： 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   在此程序中，我們假設根磁碟機上有一個資料夾。

2. 開啟與執行個體相關聯的 R 工具 (例如，您可以使用 Rgui.exe)。 以滑鼠右鍵按一下並選取 [以系統管理員身分執行]  ，讓該工具能夠對您的系統進行更新。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - 例如，RGUI 的預設檔案位置是 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

   ::: moniker range"=sql-server-2017||=sqlallproducts-allversions"
   - 例如，RGUI 的檔案位置是 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - 例如，RGUI 的檔案位置是 `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

3. 取得執行個體程式庫的路徑，並將它新增至程式庫路徑清單。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   例如，

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   例如，

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   例如，

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL15.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

4. 在伺服器上，指定您將 **miniCRAN** 存放庫複製為 `server_repo` 的新位置。

    在此範例中，我們假設您已將存放庫複製到伺服器上的暫存資料夾。

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. 由於您是在伺服器上新的 R 工作區中工作，因此，也必須提供要安裝的套件清單。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安裝套件，並提供 miniCRAN 存放庫本機複本的路徑。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 在執行個體程式庫中，您可以使用類似下列的命令來檢視安裝的套件：

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另請參閱

+ [取得 R 套件資訊](../package-management/r-package-information.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
