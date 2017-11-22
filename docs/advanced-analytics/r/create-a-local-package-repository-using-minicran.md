---
title: "建立本機封裝儲存機制使用 miniCRAN |Microsoft 文件"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7cc7c216cb95d10c4158a3ac0998d458cec3d7b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-local-package-repository-using-minicran"></a>建立使用 miniCRAN 本機封裝儲存機制

有兩種方式，您可以準備沒有網際網路存取的伺服器上安裝 R 封裝。

-   [若要建立單一的本機儲存機制使用 miniCRAN 封裝](#bkmk_miniCRAN)

    [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)會建立內部一致的儲存機制，類似的 CRAN 儲存機制中選取的封裝所組成。 使用者指定一組所需的封裝，並 miniCRAN 以遞迴方式讀取這些封裝的相依性樹狀結構，並會下載列出的封裝和其相依性。

    您可以將這個本機儲存機制移至伺服器，並繼續進行而不使用網際網路安裝封裝。

-   [手動下載並複製封裝一個](#bkmk_manual)

本文章說明如何建立使用這兩種方法中，R 封裝儲存機制，並建議使用的**miniCRAN**封裝。

## <a name="prepare-packages-using-minicran"></a>準備使用 miniCRAN 封裝

建立本機封裝儲存機制的目標是提供伺服器管理員或組織中的其他使用者可用來在沒有網際網路存取的伺服器上安裝新的 R 封裝的單一位置。

[MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)封裝的寫入為 R [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)可更輕鬆地建立一致，受管理的組 R 封裝的組織。 

有許多使用 miniCRAN 建立儲存機制的優點：

-   **安全性**： 許多 R 使用者習慣於下載和安裝新的 R 封裝，在從 CRAN 或其中一個鏡像站台。 不過，基於安全性理由，實際執行伺服器執行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常不需要網際網路連線。

-   **更容易離線安裝**： 若要封裝安裝到離線的伺服器需要，您也可以下載所有套件相依性，使用 miniCRAN 可讓您更輕鬆地取得正確格式的所有相依性。

-   **版本管理改善**： 在多使用者環境中，有合理的原因，若要避免不受限制的伺服器上的多個封裝版本的安裝。

建立儲存機制之後, 您可以藉由新增新的封裝，或升級現有的封裝的版本修改它。

### <a name="step-1-install-the-minicran-package"></a>步驟 1： 安裝 miniCRAN 套件

您開始建立要當做來源使用的 miniCRAN 儲存機制。 您應該可以存取網際網路的電腦上建立這個儲存機制。

1.  安裝 miniCRAN 封裝和所需**igraph**封裝。

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>步驟 2： 定義封裝來源： CRAN 鏡像或 MRAN 快照集

1. 指定要用於取得封裝的鏡像網站。

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  表示用來儲存收集的封裝的本機資料夾。 您不需要命名資料夾 miniCRAN;可能是更具描述性的名稱，例如"GeneticsPackages"或"ClientRPackages1.0.2"。

    只是確定預先建立的資料夾。 如果會引發錯誤`local_repo`資料夾不存在，當您稍後執行的 R 程式碼。

    ```R
    local_repo <- "~/miniCRAN"
    ```

    波狀符號展開運算子所傳回的結果相當於的環境變數， `Sys.getenv("R_USER")`。

### <a name="step-3-add-packages-to-the-repository"></a>步驟 3： 將封裝新增至儲存機制

1.  MiniCRAN 安裝之後，建立指定您想要下載的其他封裝的清單。

    無法將相依性加入至這個初始的清單。**igraph** miniCRAN 所使用的封裝會為您產生相依性的清單。 如需如何使用此圖表的詳細資訊，請參閱[來識別封裝的相依性使用 miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

    下列的 R 指令碼會示範如何取得目標的封裝、"zoo"和"預測 」。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. （選擇性） 繪製相依性圖形，很有幫助，並且看起來很酷。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 建立本機儲存機制。 請務必視需要變更的 R 版本

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    這項資訊，從 miniCRAN 封裝會建立您要複製之封裝的資料夾結構[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]更新版本。

4. 此時您應該有包含在需要時，封裝的資料夾和任何其他封裝的所需。

    您可以執行下列程式碼列出 miniCRAN 儲存機制中所包含的封裝。

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>步驟 4： 若要將 R 封裝新增至執行個體文件庫中使用的儲存機制

您已建立儲存機制，並加入您需要的套件之後，您必須將封裝儲存機制移至伺服器電腦，並確保 R 封裝會安裝在正確的程式庫，以用於 SQL Server。

根據 SQL Server 版本，有兩個選項，將 SQL Server 執行個體相關聯的 R 程式庫中加入新的封裝：

-   安裝至執行個體文件庫使用 miniCRAN 儲存機制和 R 工具。

-   將封裝上傳至 SQL 資料庫並在每個資料庫為基礎，使用建立外部程式庫陳述式上安裝封裝。 請參閱[SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)。

下列程序描述如何安裝封裝使用的 R 工具。

1.  複製包含 miniCRAN 儲存機制，其完整，您將在其中安裝封裝的伺服器中的資料夾。

2.  開啟 R 命令提示字元使用執行個體相關聯的 R 工具。

    - 預設資料夾是針對 SQL Server 2017， `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`。

    - 就 SQL Server 2016 而言，預設資料夾是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`。

    - 具名的執行個體，預設路徑看起來應該像： `<instance_path>.RTEST/R_SERVICES/library`。

    -  如果您已將 SQL Server 安裝到不同的磁碟機，或在安裝路徑中進行了任何其他變更，並務必一併進行這些變更。

3.  取得路徑的執行個體中的程式庫 （情況下您的使用者目錄中），並將它加入至程式庫路徑的清單。

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    這應該會傳回執行個體路徑，"c: / Program 檔案/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/媒體櫃 」

2.  指定您用來複製 mininCRAN 儲存機制中的伺服器上的位置`server_repo`。

    在此範例中，我們假設您複製到您在伺服器上的使用者資料夾的儲存機制。

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  因為您正在伺服器上新的 R 工作區中，您也必須提供要安裝套件的清單。

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  安裝封裝，使用本機複本 miniCRAN 儲存機制的路徑。

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  現在，檢視已安裝的封裝。

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> 在 SQL Server 2017，其他資料庫角色和 T-SQL 陳述式提供可協助伺服器系統管理員透過封裝管理權限。 資料庫管理員可以擁有使用 R 或 T-SQL，如果您想要安裝的套件的工作。 不過，DBA 也可以使用角色，讓使用者能夠安裝其自己的封裝。 如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)。
> 
> 在 SQL Server 2016 中，伺服器管理員必須從安裝套件 miniCRAN 儲存機制至執行個體所使用的預設程式庫。 若要這樣做，請使用中所述的 R 工具[前面一節](#bkmk_Rtools)。

## <a name="manually-download-single-packages"></a>手動下載單一封裝

如果您不想要使用 miniCRAN，也可以手動下載您需要封裝和其相依性。 若要這樣做，您都必須是系統管理員或伺服器的唯一擁有者。

下載封裝之後, 您可以安裝的 R 封裝從 zip 的檔案的位置。

1.  下載封裝 zip 檔案，並將它們儲存在本機資料夾

2.  複製到該資料夾[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]電腦。

3.  將封裝安裝到 SQL Server 執行個體文件庫。

> [!NOTE]
> 當您使用 R 工具來安裝封裝時，它們會安裝執行個體的整體。 
> 
> 如果您想要將封裝安裝到資料庫，而且使用資料庫角色的使用者與共用封裝，您必須上傳使用建立外部程式庫陳述式的程式庫。 請參閱[安裝 SQL Server 中的其他 R 封裝](install-additional-r-packages-on-sql-server.md)
