---
title: 使用 sqlmlutils 安裝新的 R 套件
description: 瞭解如何使用 sqlmlutils 將新的 R 封裝安裝至 SQL Server Machine Learning 服務或 SQL Server R Services 的實例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 579f4c4e236fcc9ee22067522c47a8286b869d51
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000781"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>使用 sqlmlutils 安裝新的 R 套件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何使用[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils)封裝中的函數, 將新的 R 封裝安裝至 SQL Server Machine Learning 服務或 SQL Server R Services 的實例。 您安裝的套件可用於在資料庫中執行的 R 腳本, 其方式是使用 T-sql [sp-](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) ------------i-T--------sql

> [!NOTE]
> 不建議將`install.packages`標準 r 命令新增至 SQL Server 上的 r 套件。 相反地, 請使用**sqlmlutils** , 如本文中所述。

## <a name="prerequisites"></a>必要條件

- 在您用來連接到 SQL Server 的用戶端電腦上安裝[R](https://www.r-project.org)和[RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) 。 您可以使用任何 R IDE 來執行腳本, 但本文假設 RStudio。

- 在您用來連線到 SQL Server 的用戶端電腦上安裝[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is)或[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)。 您可以使用其他資料庫管理或查詢工具, 但本文假設 Azure Data Studio 或 SSMS。

### <a name="other-considerations"></a>其他考慮

- 在 SQL Server 中執行的 R 腳本只能使用安裝在預設實例程式庫中的套件。 SQL Server 無法從外部程式庫載入封裝, 即使該程式庫位於相同的電腦上也一樣。 這包括與其他 Microsoft 產品一起安裝的 R 程式庫。

- 在強化的 SQL Server 環境中, 您可能會想要避免下列情況:
  - 需要網路存取的套件
  - 需要提升檔案系統存取權的封裝
  - 在 SQL Server 內執行時, 用於 網頁程式開發或其他工作的套件不會有任何好處

## <a name="install-sqlmlutils-on-the-client-computer"></a>在用戶端電腦上安裝 sqlmlutils

若要使用**sqlmlutils**, 您必須先將它安裝在用來連接到 SQL Server 的用戶端電腦上。

**Sqlmlutils**套件相依于**RODBCext**套件, 而**RODBCext**則相依于其他數個封裝。 下列程式會以正確的順序安裝所有這些套件。

### <a name="install-sqlmlutils-online"></a>線上安裝 sqlmlutils

如果用戶端電腦可存取網際網路, 您可以在線上下載並安裝**sqlmlutils**及其相依的套件。

1. 從 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 將最新的**sqlmlutils** zip 檔案下載到用戶端電腦。 不要解壓縮檔案。

1. 開啟**命令提示**字元並執行下列命令, 以安裝**sqlmlutils**和**RODBCext**套件。 以您下載的**sqlmlutils** zip 檔案的完整路徑取代 (此範例假設檔案位於您的 [檔] 資料夾中)。 **RODBCext**套件可在線上找到並安裝。

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>離線安裝 sqlmlutils

如果用戶端電腦沒有網際網路連線, 您必須使用可存取網際網路的電腦, 預先下載套件**sqlmlutils**和**RODBCext** 。 接著, 您可以將檔案複製到用戶端電腦上的資料夾, 並離線安裝套件。

**RODBCext**套件有數個相依封裝, 識別套件的所有相依性會變得複雜。 建議您使用[**miniCRAN**](https://andrie.github.io/miniCRAN/)來建立包含所有相依封裝之封裝的本機存放庫資料夾。
如需詳細資訊, 請參閱[使用 MiniCRAN 建立本機 R 封裝存放庫](../r/create-a-local-package-repository-using-minicran.md)。

**Sqlmlutils**套件是由單一 zip 檔案所組成, 您可以將它複製到用戶端電腦並安裝。

在具有網際網路存取的電腦上:

1. 安裝**miniCRAN**。 如需詳細資訊, 請參閱[安裝 miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) 。

1. 在 RStudio 中, 執行下列 R 腳本以建立封裝**RODBCext**的本機存放庫。 這個範例會在資料夾`c:\downloads\rodbcext`中建立存放庫。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   `Rversion`針對值, 使用 SQL Server 上所安裝的 R 版本。 若要確認已安裝的版本, 請使用下列 T-sql 命令。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 從 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 下載最新的**sqlmlutils** zip 檔案 (不要解壓縮檔案)。 例如, 將檔下載至`c:\downloads\sqlmlutils_0.7.1.zip`。

1. 將整個**RODBCext**存放庫資料夾 (`c:\downloads\rodbcext`) 和**sqlmlutils** zip 檔案 (`c:\downloads\sqlmlutils_0.7.1.zip`) 複製到用戶端電腦。 例如, 將它們複製到用戶端`c:\temp\packages`電腦上的資料夾。

在您用來連線到 SQL Server 的用戶端電腦上, 開啟命令提示字元, 然後執行下列命令來安裝**RODBCext** , 然後**sqlmlutils**。

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>在 SQL Server 上新增 R 封裝

在下列範例中, 您會將[**膠水**](https://cran.r-project.org/web/packages/glue/)封裝加入 SQL Server。

### <a name="add-the-package-online"></a>線上新增封裝

如果您用來連線到 SQL Server 的用戶端電腦可以存取網際網路, 您可以使用**sqlmlutils**來尋找透過網際網路的**粘連**套件和任何相依性, 然後從遠端將封裝安裝至 SQL Server 實例。

1. 在用戶端電腦上, 開啟 RStudio, 並建立新的**R 腳本**檔案。

1. 使用下列 R 腳本, 使用**sqlmlutils**安裝**粘連**套件。 以您自己的 SQL Server 資料庫連接資訊取代。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > **範圍**可以是「**公用**」或「**私**用」。 公用範圍適用于資料庫管理員安裝所有使用者都可以使用的封裝。 私用範圍可讓套件僅供安裝的使用者使用。 如果您未指定範圍, 預設範圍為 [**私**用]。

### <a name="add-the-package-offline"></a>離線新增封裝

如果用戶端電腦沒有網際網路連線, 您可以使用**miniCRAN** , 以使用可存取網際網路的電腦來下載**粘連**套件。 然後將套件複製到用戶端電腦, 您可以在其中離線安裝套件。
如需安裝**miniCRAN**的相關資訊, 請參閱[安裝 miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) 。

在具有網際網路存取的電腦上:

1. 執行下列 R 腳本, 以建立**粘附**的本機儲存機制。 這個範例會在中`c:\downloads\glue`建立存放庫資料夾。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   `Rversion`針對值, 使用 SQL Server 上所安裝的 R 版本。 若要確認已安裝的版本, 請使用下列 T-sql 命令。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 將整個 [**粘連**存放庫]`c:\downloads\glue`資料夾 () 複製到用戶端電腦。 例如, 將它複製到資料夾`c:\temp\packages\glue`。

在用戶端電腦上:

1. 開啟 RStudio, 並建立新的**R 腳本**檔案。

1. 使用下列 R 腳本, 使用**sqlmlutils**安裝**粘連**套件。 以您自己的 SQL Server 資料庫連接資訊取代。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > **範圍**可以是「**公用**」或「**私**用」。 公用範圍適用于資料庫管理員安裝所有使用者都可以使用的封裝。 私用範圍可讓套件僅供安裝的使用者使用。 如果您未指定範圍, 預設範圍為 [**私**用]。

## <a name="use-the-package"></a>使用封裝

一旦安裝了**粘附**套件, 您就可以在 SQL Server 中的 R 腳本中使用 t-sql **sp_execute_external_script**命令。

1. 開啟 Azure Data Studio 或 SSMS, 並連接到您的 SQL Server 資料庫。

1. 執行下列命令：

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **結果**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>移除封裝

如果您想要移除**粘附**套件, 請執行下列 R 腳本。 使用您稍早定義的相同**連接**變數。

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>後續步驟

- 如需已安裝 R 套件的詳細資訊, 請參閱[取得 r 封裝資訊](r-package-information.md)
- 如需使用 R 封裝的說明, 請參閱[使用 r 套件的秘訣](../r/packages-installed-in-user-libraries.md)
- 如需安裝 Python 套件的詳細資訊, 請參閱[使用 Pip 安裝 python 套件](install-additional-python-packages-on-sql-server.md)
- 如需 SQL Server Machine Learning 服務的詳細資訊, 請參閱[什麼是 SQL Server Machine Learning 服務 (Python 和 R)？](../what-is-sql-server-machine-learning.md)
