---
title: 建立本機 R 封裝儲存機制使用 miniCRAN （SQL Server 機器學習） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1f7ba3b4acde90d9e416eb092ac80cb0dfcbba8a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585640"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>建立使用 miniCRAN 本機 R 封裝儲存機制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)所建立的封裝[Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)、 識別和下載套件和相依性至單一資料夾中，您可以複製到其他電腦離線的 R 封裝安裝。

做為輸入，指定一個或多個封裝。 **miniCRAN**遞迴讀取這些封裝的相依性樹狀結構，而且會從 CRAN 或類似的儲存機制下載列出的封裝和其相依性。

做為輸出， **miniCRAN**會建立內部一致的儲存機制，所選的套件和所有必要的相依性所組成。 您可以將這個本機儲存機制移至伺服器，並繼續安裝沒有網際網路連線的封裝。

> [!NOTE]
> 有經驗的 R 使用者通常會查看針對下載的封裝 DESCRIPTION 檔案中的相依封裝的清單。 不過，封裝會列入**匯入**可能有第二個層級相依性。 基於這個理由，我們建議**miniCRAN**的組合所需的封裝的完整集合。

## <a name="why-create-a-local-repository"></a>建立本機儲存機制的原因

建立本機封裝儲存機制的目標是提供伺服器管理員或組織中的其他使用者可以使用新的 R 封裝安裝在伺服器上，尤其是一個沒有網際網路存取的單一位置。 建立儲存機制之後, 您可以藉由新增新的封裝，或升級現有的封裝的版本修改它。

封裝儲存機制是在這些情況下很有用：

- **安全性**： 許多 R 使用者習慣於下載和安裝新的 R 封裝，在從 CRAN 或其中一個鏡像站台。 不過，基於安全性理由，實際執行伺服器執行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常不需要網際網路連線。

- **更容易離線安裝**： 若要封裝安裝到離線的伺服器需要，您也可以下載所有套件相依性，使用 miniCRAN 可讓您更輕鬆地取得正確格式的所有相依性。

    藉由使用 miniCRAN，您可以避免封裝相依性錯誤準備要使用安裝套件時[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式。

- **版本管理改善**： 在多使用者環境中，有合理的原因，若要避免不受限制的伺服器上的多個封裝版本的安裝。 使用本機儲存機制以提供一致的封裝集以供分析師。 

> [!TIP]
> 您也可以使用 miniCRAN 準備封裝以便在 Azure Machine Learning 中使用。 如需詳細資訊，請參閱這篇部落格： [miniCRAN 使用在 Azure ML，由 Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>安裝 miniCRAN

**MiniCRAN**封裝本身會相依於其他 18 CRAN 封裝，也就是之間**RCurl**封裝，有系統相依性上**curl 對內**封裝。 同樣地，封裝**XML**具有相依性**libxml2 對內**。 若要解析的相依性，我們建議您建立本機儲存機制一開始包含完整的網際網路存取的電腦上。 

使用基底 R 中，在電腦上執行下列命令 R 工具和網際網路連線。 這假設*不*SQL Server 電腦。 下列命令會安裝**miniCRAN**封裝和所需**igraph**封裝。 這個範例會檢查是否已安裝封裝，但您可以略過 if 陳述式並直接安裝封裝。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>設定的 CRAN 鏡像和 MRAN 快照集

指定要用於取得封裝的鏡像網站。 例如，您可以使用 MRAN 站台或任何其他站台在您的地區，其中包含您需要的套件。 如果下載失敗，請嘗試另一個鏡像網站。

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>建立本機資料夾

建立本機資料夾，例如`C:\mylocalrepo`用來儲存收集的封裝。 如果您重複此步驟通常，您應該使用更具描述性的名稱，例如"miniCRANZooPackages"或"miniCRANMyRPackagev2"。

指定的資料夾做為本機儲存機制。 R 語法會使用正斜線的路徑名稱，也就是相反從 Windows 慣例。

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>將封裝新增至本機儲存機制

之後**miniCRAN**已安裝並載入，建立指定您想要下載的其他封裝的清單。

請勿**不**加入這個初始清單中的相依性。 **Igraph**所使用的封裝**miniCRAN**為您產生相依性的清單。 如需如何使用產生的相依性圖形的詳細資訊，請參閱[來識別封裝的相依性使用 miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

1. 新增目標套件，"zoo"和 「 預測 」 變數。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. （選擇性） 繪製的相依性圖形，但很有幫助。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 建立本機儲存機制。 請務必變更 R 版本，視您的 SQL Server 執行個體上安裝的版本。 3.2.2 版本是 SQL Server 2016 上，SQL Server 2017 上是版本 3.3。 如果您沒有元件升級，您的版本可能是較新。 如需詳細資訊，請參閱[取得 R，並將 Python 封裝資訊](determine-which-packages-are-installed-on-sql-server.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   這項資訊，從 miniCRAN 封裝會建立您要複製之封裝的資料夾結構[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]更新版本。

此時您應該有包含在需要時，封裝的資料夾和任何其他封裝的所需。 路徑應該類似這個範例： C:\mylocalrepo\bin\windows\contrib\3.3 和它應該包含壓縮封裝的集合。 請勿將封裝解壓縮或重新命名任何檔案。

（選擇性） 執行下列程式碼，列出本機 miniCRAN 儲存機制中所包含的封裝。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>將封裝新增至執行個體文件庫

需要封裝的本機儲存機制之後，請將封裝儲存機制移至 SQL Server 電腦。 下列程序描述如何安裝封裝使用的 R 工具。

1. 複製包含 miniCRAN 儲存機制，以您要安裝封裝的伺服器，將整個資料夾。 資料夾通常具有此結構： miniCRAN 根目錄 > bin > windows > contrib > 版本 > 所有封裝。 在下列範例中，我們假設關閉根磁碟機的資料夾： 

2. 開啟執行個體相關聯的 R 工具 （例如，您可以使用 Rgui.exe）。 以滑鼠右鍵按一下**系統管理員身分執行**允許此工具可讓您的系統更新。

    - SQL Server 2017，RGUI 的檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。

    - SQL Server 2016，RGUI 他檔案位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 取得執行個體文件庫的路徑，並將它加入至程式庫路徑的清單。 SQL Server 2017，路徑是類似下列的範例。

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 指定新的位置複製其中的伺服器上**miniCRAN**儲存機制，做為`server_repo`。

    在此範例中，我們假設您在伺服器上的暫存資料夾複製儲存機制。

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 因為您正在伺服器上新的 R 工作區中，您也必須提供要安裝套件的清單。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安裝封裝，並提供本機複本 miniCRAN 儲存機制的路徑。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 從執行個體文件庫中，您可以檢視已安裝的封裝，使用類似下列的命令：

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另請參閱

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [使用說明指南](sql-server-machine-learning-tasks.md)


