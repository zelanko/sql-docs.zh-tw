---
title: 建立使用 miniCRAN-SQL Server Machine Learning 服務的本機 R 套件存放庫
description: 使用 miniCran 來偵測、 組合，並將 R 封裝相依性安裝到單一的彙總套件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7dc2e286e6eb80fe1eef3e8b86ed1002a6344cfb
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431751"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>建立使用 miniCRAN 本機 R 套件儲存機制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)所建立的封裝[Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)、 識別，以及下載套件和相依性到單一資料夾中，您可以複製到離線的 R 套件安裝的其他電腦。

做為輸入，請指定一個或多個封裝。 **miniCRAN**以遞迴方式讀取這些套件的相依性樹狀結構，並從 CRAN 或類似的存放庫下載只有列出的封裝和其相依性。

做為輸出中， **miniCRAN**會建立內部一致性的存放庫，其中包含所選的封裝和所有必要的相依性。 您可以將此本機儲存機制移到伺服器，並繼續安裝沒有網際網路連線的封裝。

> [!NOTE]
> 有經驗的 R 使用者通常會查看已下載的封裝 DESCRIPTION 檔案中的相依套件的清單。 不過，套件會列入**匯入**可能會有第二個層級相依性。 基於這個理由，我們建議您**miniCRAN**組合所需的套件的完整集合。

## <a name="why-create-a-local-repository"></a>為什麼建立本機存放庫

建立本機套件存放庫的目標是提供 伺服器管理員或組織中的其他使用者可用來安裝新的 R 套件在伺服器上，尤其是一個沒有網際網路存取的單一位置。 建立存放庫之後, 您可以藉由新增新的封裝或升級現有封裝的版本中修改它。

套件存放庫是在這些情況下很有用：

- **安全性**:許多 R 使用者已經習慣下載並安裝新的 R 套件位置，從 CRAN 或其中一個鏡像站台。 不過，基於安全性理由，執行的實際執行伺服器[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通常不需要網際網路連線。

- **更輕鬆地離線安裝**:若要封裝安裝到離線的伺服器需要，您也可以下載所有的套件相依性，使用 miniCRAN 可讓您更輕鬆地取得正確格式的所有相依性。

    使用 miniCRAN，您可以避免套件相依性錯誤準備要使用安裝套件時才[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式。

- **改進的版本管理**:在多使用者環境中，有很好的理由，若要避免不受限制的安裝在伺服器上的多個封裝版本。 使用本機儲存機制來提供一組一致的套件以供您的分析師。 

> [!TIP]
> 您也可以使用 miniCRAN 來準備使用 Azure Machine Learning 中的封裝。 如需詳細資訊，請參閱這篇部落格：[使用 miniCRAN 在 Azure ML 中，由 Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>安裝 miniCRAN

**MiniCRAN**套件本身就是相依於其他 18 CRAN 套件，即之間**RCurl**套件，它具有系統相依性上**curl devel**封裝。 同樣地，封裝**XML**具有相依性**libxml2 devel**。 若要解決相依性，我們建議您建立本機存放庫一開始有完整的網際網路存取的電腦上。 

基底 R 的電腦上執行下列命令 R 工具，以及網際網路連線。 這假設*不*您 SQL Server 的電腦。 下列命令會安裝**miniCRAN**套件和所需**igraph**封裝。 這個範例會檢查是否已安裝封裝，但您可以略過 if 陳述式並直接安裝套件。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>設定的 CRAN 鏡像和 MRAN 快照集

指定要用於取得封裝的鏡像網站。 例如，您可以使用 MRAN 網站或任何其他站台，在您的區域，其中包含所需的套件。 如果下載失敗，請嘗試另一個鏡像站台。

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>建立本機資料夾

建立本機資料夾，例如`C:\mylocalrepo`用來儲存所收集的封裝。 如果您重複此步驟通常，您應該使用更具描述性的名稱，例如"miniCRANZooPackages 」 或 「 miniCRANMyRPackagev2"。

本機儲存機制中指定的資料夾。 R 的語法會使用正斜線的路徑名稱，也就是相反 Windows 慣例。

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>將套件新增至本機存放庫

在後**miniCRAN**已安裝並載入，建立清單，可指定您想要下載的其他套件。

請勿**不**將相依性新增到這個初始的清單。 **Igraph**所使用的封裝**miniCRAN**會為您產生相依性的清單。 如需如何使用產生的相依性圖形的詳細資訊，請參閱[使用 miniCRAN 來識別封裝相依性](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

1. 新增目標套件，"zoo"和"forecast"的變數。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. （選擇性） 繪製相依性圖形中，但是很有幫助。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 建立本機存放庫。 請務必變更 R 版本，視您的 SQL Server 執行個體上安裝的版本。 SQL Server 2016 上是版本 3.2.2、 3.3 版位於 SQL Server 2017。 如果您執行元件升級時，您的版本可能是較新。 如需詳細資訊，請參閱 <<c0> [ 取得 R 和 Python 封裝資訊](determine-which-packages-are-installed-on-sql-server.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   這項資訊，miniCRAN 套件會建立您要將套件複製到資料夾結構[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]更新版本。

此時，您應該有包含您所需，封裝的資料夾和任何其他套件，且需要。 路徑應該類似此範例：C:\mylocalrepo\bin\windows\contrib\3.3 和它應該包含壓縮封裝的集合。 請勿將套件解壓縮或重新命名任何檔案。

（選擇性） 執行下列程式碼，列出本機 miniCRAN 儲存機制中包含的封裝。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>將封裝新增至執行個體文件庫

具有所需的套件的本機存放庫之後，請將封裝儲存機制移至 SQL Server 電腦。 下列程序描述如何使用 R 工具安裝封裝。

1. 複製包含 miniCRAN 儲存機制，以您要安裝套件的伺服器，將整個資料夾。 資料夾通常會有此結構： miniCRAN 根 > bin > windows > contrib > 版本 > 的所有套件。 在下列範例中，我們假設根磁碟機的資料夾： 

2. 開啟執行個體相關聯的 R 工具 （例如，您可以使用 Rgui.exe）。 以滑鼠右鍵按一下**系統管理員身分執行**以允許此工具可讓您的系統更新。

    - SQL Server 2017，RGUI 的檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。

    - SQL Server 2016 中，他 RGUI 的檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 取得執行個體文件庫的路徑，並將它新增至程式庫路徑的清單。 在 SQL Server 2017 中，路徑是類似下列的範例。

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 在您複製的伺服器上指定的新位置**miniCRAN**存放庫中，為`server_repo`。

    在此範例中，我們假設您在伺服器上的暫存資料夾，複製儲存機制。

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 因為您正在伺服器上新的 R 工作區中，您也必須提供要安裝套件的清單。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安裝套件，提供 miniCRAN 儲存機制的本機複本的路徑。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 從執行個體文件庫中，您可以檢視已安裝的套件使用的命令，如下所示：

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另請參閱

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [使用說明指南](sql-server-machine-learning-tasks.md)


