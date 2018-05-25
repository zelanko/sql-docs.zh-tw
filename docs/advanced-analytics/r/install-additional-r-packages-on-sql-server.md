---
title: SQL Server 機器學習服務上安裝新的 R 封裝 |Microsoft 文件
description: 將新的 R 封裝加入至 SQL Server 2016 R Services 或 SQL Server 2017 機器學習服務 （資料庫）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 20ef7181c5ab8c0494f73b205dddcdf1ac0a620e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server 上安裝新的 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。 有多種方法，如安裝新的 R 封裝，根據您擁有 SQL server 版本，以及伺服器是否有網際網路連線。 適用於新的封裝安裝下列方法也有可能的。

| 方法                           | Permissions  | 遠端/本機 |
|------------------------------------|---------------------------|-------|
| [使用傳統的 R 封裝管理員](#bkmk_rInstall)  | 管理 | 本機 |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) | 管理 | 本機 |
| [使用 T-SQL （建立外部程式庫）](install-r-packages-tsql.md) | 安裝程式，資料庫角色之後的系統管理員 | both 
| [若要建立本機儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md) | 安裝程式，資料庫角色之後的系統管理員 | both |

## <a name="bkmk_rInstall"></a> 安裝 R 封裝，透過網際網路連接

您可以使用標準的 R 工具來安裝新的封裝上的 SQL Server 2016 執行個體或 SQL Server 2017，提供在電腦已開啟的連接埠 80，並可讓系統管理員權限。

> [!IMPORTANT] 
> 請務必要與目前的執行個體相關聯的預設文件庫安裝封裝。 永遠不會安裝到使用者目錄的封裝。

此程序使用 RGui，但您可以使用 RTerm 或任何其他 R 命令列工具，可支援高的存取權限。

### <a name="install-a-package-using-rgui"></a>使用 RGui 安裝封裝

1. [判斷執行個體文件庫的位置](installing-and-managing-r-packages.md)。 瀏覽至安裝 R 工具的資料夾。 例如，SQL Server 2017 預設執行個體的預設路徑如下所示： `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 以滑鼠右鍵按一下 RGui.exe，然後選取**系統管理員身分執行**。 如果您沒有必要的權限，請連絡資料庫管理員，並提供您需要的套件清單。

1. 從命令列中，如果您知道封裝名稱，您可以輸入：`install.packages("the_package-name")`雙引號所需的封裝名稱。

1. 當系統要求您的鏡像網站，選取對您位置而言方便的任何網站。

如果目標封裝相依於其他封裝，R 安裝程式會自動下載相依性，並讓您將進行安裝。

如果您有多個執行個體的 SQL Server，並存的執行個體的 SQL Server 2016 R 服務和 SQL Server 2017 機器學習服務，例如執行分別為每個執行個體的安裝，如果您想要使用這兩種內容中的封裝。 封裝無法執行個體之間共用。

## <a name = "bkmk_offlineInstall"></a> 使用的 R 工具的離線安裝

如果伺服器沒有網際網路存取，不需要其他步驟以準備封裝。 若要在沒有網際網路存取的伺服器上安裝 R 封裝，您必須：

+ 事先分析相依性。
+ 目標套件下載至具有網際網路存取的電腦。
+ 相同的電腦下載任何所需的封裝，並將所有封裝都放在單一封裝的保存。
+ 如果它尚未以壓縮格式，zip 封存。
+ 將套件保存複製到伺服器上的位置。
+ 安裝目標封裝封存檔案指定為來源。

> [!IMPORTANT] 
> > 確定您分析所有相依性，並下載**所有**所需封裝**之前**開始安裝。 我們建議[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此處理程序。 此 R 封裝會採用您想要安裝、 分析相依性，以及讓您取得所有 zip 的檔案的封裝清單。 miniCRAN 接著會建立單一的存放庫，您可以複製到伺服器電腦。
> 
> 如需詳細資訊，請參閱[建立使用 miniCRAN 本機封裝儲存機制](create-a-local-package-repository-using-minicran.md)

此程序假設您已經備妥您需要以壓縮格式，並準備好將它們複製到伺服器的所有封裝。

1. 複製封裝壓縮檔案，或多個封裝，完整的儲存機制包含中的所有封裝壓縮格式，伺服器可以存取的位置。

2. 開啟伺服器上安裝 R 工具的執行個體所在的資料夾。 例如，如果您使用 SQL Server 2016 R Services 的系統上的 Windows 命令提示字元，切換至`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 以滑鼠右鍵按一下 RGui 或 RTerm，然後選取**系統管理員身分執行**。

4. 執行 R 指令`install.packages`並指定封裝或儲存機制名稱和壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會擷取 R 封裝`mynewpackage`從其本機的 zip 檔案，假設您的複本儲存在目錄中`C:\Temp\Downloaded packages`，並在本機電腦上安裝封裝。 如果封裝有任何相依性，安裝程式會檢查文件庫中現有的封裝。 如果您已經建立包含相依性的儲存機制，安裝程式會安裝必要的封裝。

    如果任何必要的封裝不會出現在執行個體文件庫，zip 檔案中找不到目標套件的安裝將會失敗。

## <a name="tips-for-package-installation"></a>封裝安裝的秘訣

本節提供各種的秘訣和 SQL Server 上的 R 封裝安裝相關的常見問題。

###  <a name="packageVersion"></a> 取得正確的封裝版本和格式

有多個來源的 R 封裝，像是 CRAN 和 Bioconductor。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出許多資源。 許多封裝會發佈到 GitHub，您可以在這裡取得原始程式碼。 最後，可能會提供您已由貴公司的某人所開發的 R 封裝，或是您沒有在您撰寫的自訂封裝。

不論來源為何之前嘗試安裝封裝，請確定您已取得 Windows 平台的二進位格式。 

### <a name="bkmk_zipPreparation"></a> 下載為 zip 檔案的套件

在沒有網際網路存取的伺服器上安裝，您必須下載離線安裝的 zip 檔案格式的封裝副本。 **無法將封裝解壓縮。**

例如，下列程序描述現在以取得正確的版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] \(封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存位置，而按一下**儲存**。

    此程序會建立套件的本機複本。 

4. 如果您收到的下載錯誤，請嘗試不同的鏡像網站。

5. 已下載封裝封存之後，您可以安裝封裝，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

> [!TIP]
> 如果不小心安裝而不是下載二進位檔案的套件，下載 zip 檔案的副本也會儲存到您的電腦。 查看已安裝此套件，來判斷檔案位置的狀態訊息。 您可以將該 zip 的檔案複製到沒有網際網路存取的伺服器。
> 
> 不過，當您取得使用此方法的封裝時，相依性不包含。 

### <a name="bkmk_packageDependencies"></a> 取得所需的封裝

R 封裝經常會相依於其他的多個封裝，其中有些可能無法使用執行個體所使用的預設 R 程式庫中。 有時封裝需要相依的套件已經安裝不同版本。

如果您需要安裝多個封裝，或想要確保您的組織中每個人都取得正確的封裝類型和版本，我們建議您使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)封裝来分析的完整相依性鏈結。 minicRAN 建立可以在多個使用者或電腦間共用的本機儲存機制。 如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。


### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道您要安裝哪一個程式庫，以及已安裝的封裝。

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，暫停時間，並確保 R 環境變數`.libPath`會使用單一路徑。

這個路徑應該指向 R_SERVICES 資料夾執行個體。 如需詳細資訊，包括如何判斷已安裝的封裝，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>與獨立 R 或 Python 伺服器-並存安裝

如果您已安裝 SQL Server 2017 Microsoft Machine Learning 伺服器 （獨立） 或 SQL Server 2016 R 伺服器 （獨立），除了資料庫中的分析 （SQL Server 2017 機器學習服務和 SQL Server 2016 R Services），您的電腦具有分隔重複項目，所有的 R 工具和程式庫的每個安裝的 R。

封裝安裝至 R_SERVER 文件庫只由獨立伺服器，並無法存取 SQL Server （資料庫） 執行個體。 一律使用`R_SERVICES`安裝您想要使用 SQL Server 上的資料庫中的封裝時，程式庫。
