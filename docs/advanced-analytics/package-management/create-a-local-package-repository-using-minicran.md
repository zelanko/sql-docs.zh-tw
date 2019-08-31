---
title: 使用 miniCRAN 建立本機 R 封裝存放庫
description: 瞭解如何使用 miniCRAN 套件離線安裝 R 套件, 以建立套件和相依性的本機存放庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68f86d673b944a029c7bd0f74c9594692bd579f4
ms.sourcegitcommit: 00350f6ffb73c2c0d99beeded61c5b9baa63d171
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2019
ms.locfileid: "70196331"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>使用 miniCRAN 建立本機 R 封裝存放庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何使用[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)建立套件和相依性的本機存放庫, 以離線方式安裝 R 套件。 **miniCRAN**會識別套件和相依性, 並將其下載到您複製到其他電腦以進行離線 R 封裝安裝的單一資料夾中。

您可以指定一或多個封裝, **miniCRAN**會以遞迴方式讀取這些封裝的相依性樹狀結構。 然後, 它只會從 CRAN 或類似的存放庫下載列出的套件及其相依性。

完成後, **miniCRAN**會建立內部一致的存放庫, 其中包含選取的封裝和所有必要的相依性。 您可以將此本機存放庫移至伺服器, 並在沒有網際網路連線的情況下繼續安裝套件。

有經驗的 R 使用者通常會在所下載封裝的描述檔案中尋找相依套件的清單。 不過, 匯**入**中列出的套件可能會有第二層相依性。 基於這個理由, 我們建議**miniCRAN**組合必要套件的完整集合。

## <a name="why-create-a-local-repository"></a>為何要建立本機存放庫

建立本機封裝存放庫的目標, 是要提供伺服器系統管理員或組織中其他使用者可用來在伺服器上安裝新 R 套件的單一位置, 特別是無法存取網際網路的帳戶。 建立存放庫之後, 您可以藉由新增封裝或升級現有套件的版本來加以修改。

套件存放庫在下列案例中很有用:

- **安全性**:許多 R 使用者都習慣下載和安裝新的 R 套件, 從 CRAN 或其鏡像網站之一開始。 不過, 基於安全性理由, 執行的生產[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]伺服器通常沒有網際網路連線能力。

- **更容易離線安裝**:若要將封裝安裝到離線服務器, 您必須同時下載所有套件相依性。 使用 miniCRAN 可讓您更輕鬆地以正確的格式取得所有相依性。 藉由使用 miniCRAN, 您可以在準備封裝以[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)語句時, 避免封裝相依性錯誤。

- **改良的版本管理**:在多使用者環境中, 有個很好的理由可以避免在伺服器上安裝多個套件版本的不受限制。 使用本機存放庫, 為您的使用者提供一組一致的套件。

## <a name="install-minicran"></a>安裝 miniCRAN

**MiniCRAN**套件本身相依于18個其他 CRAN 套件, 其中是**RCurl**套件, 其具有**捲曲對內**套件的系統相依性。 同樣地, package **XML**相依于**libxml2-對內**。 若要解決相依性, 我們建議您一開始在具有完整網際網路存取權的電腦上建立本機存放庫。

在具有基底 R、R 工具和網際網路連線的電腦上執行下列命令。 假設這不是您 SQL Server 的電腦。 下列命令會安裝**miniCRAN**封裝和**igraph**套件。 這個範例會檢查是否已安裝封裝, 但是您可以略過`if`語句並直接安裝套件。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>設定 CRAN 鏡像和 MRAN 快照集

指定要用於取得封裝的鏡像網站。 例如, 您可以使用 MRAN 網站, 或您所在區域中包含所需套件的任何其他網站。 如果下載失敗, 請嘗試另一個鏡像網站。

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>建立本機資料夾

建立本機資料夾, 以在其中儲存收集的封裝。 如果您經常重複此動作, 您可能會想要使用描述性名稱, 例如 "miniCRANZooPackages" 或 "miniCRANMyRPackageV2"。

將資料夾指定為本機存放庫。 R 語法會針對路徑名稱使用正斜線, 這與 Windows 慣例相反。

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>將套件新增至本機存放庫

安裝並載入**miniCRAN**之後, 請建立清單來指定您想要下載的其他套件。

請勿將相依性加入此初始清單。 **MiniCRAN**使用的**igraph**套件會自動產生相依性的清單。 如需如何使用產生的相依性圖形的詳細資訊, 請參閱[使用 miniCRAN 來識別封裝](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)相依性。

1. 將目標封裝「zoo」和「預測」新增至變數。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. (選擇性) 繪製相依性圖形。 這不是必要的, 但它可以有資訊。

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 建立本機存放庫。 如有必要, 請務必將 R 版本變更為安裝在 SQL Server 實例上的版本。 如果您已執行元件升級, 您的版本可能會比原始版本還新。 如需詳細資訊, 請參閱[取得 R 封裝資訊](../package-management/r-package-information.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   在此資訊中, miniCRAN 封裝會建立您[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]稍後將封裝複製到其中的資料夾結構。

此時, 您應該會有一個資料夾, 其中包含您所需的套件, 以及所需的任何其他套件。 此資料夾應包含 zip 壓縮封裝的集合。 請勿解壓縮封裝或重新命名任何檔案。

(選擇性) 執行下列程式碼, 以列出包含在本機 miniCRAN 存放庫中的封裝。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>將封裝新增至實例程式庫

在您擁有具有所需套件的本機存放庫之後, 請將封裝存放庫移至 SQL Server 電腦。 下列程式描述如何使用 R 工具安裝套件。

1. 將包含 miniCRAN 存放庫的資料夾完整複製到您打算安裝封裝的伺服器。 資料夾通常具有此結構: 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   在此程式中, 我們會假設根磁片磁碟機上有一個資料夾。

2. 開啟與實例相關聯的 R 工具 (例如, 您可以使用 Rgui.exe)。 以滑鼠右鍵按一下並選取 [以**系統管理員身分執行**], 讓工具能夠對您的系統進行更新。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - 例如, RGUI.EXE 的預設檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   - 例如, RGUI.EXE 的檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - 例如, RGUI.EXE 的檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64`。
   ::: moniker-end

3. 取得實例程式庫的路徑, 並將它新增至程式庫路徑清單。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   例如，套用至物件的

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   例如，套用至物件的

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   例如，套用至物件的

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL15.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

4. 在您將**miniCRAN**存放庫`server_repo`複製到其中的伺服器上指定新的位置。

    在此範例中, 我們假設您已將存放庫複製到伺服器上的暫存資料夾。

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. 由於您是在伺服器上的新 R 工作區中工作, 因此您也必須提供要安裝的套件清單。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安裝套件, 並提供 miniCRAN 存放庫本機複本的路徑。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 從實例程式庫, 您可以使用類似下列的命令來查看已安裝的套件:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另請參閱

+ [取得 R 封裝資訊](../package-management/r-package-information.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
