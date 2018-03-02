---
title: "SQL Server 上安裝其他的 R 封裝 |Microsoft 文件"
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: a328b07027f61f50df7e3ca2b6ac12b92508688b
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server 上安裝其他的 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。

有多種方法，如安裝新的 R 封裝，根據您擁有 SQL server 版本，以及伺服器是否有網際網路存取。

+ [安裝新的封裝，使用具有網際網路存取權的 R 工具](#bkmk_rInstall)

    若要從網際網路安裝封裝中使用傳統的 R 命令。 這是最簡單的方法，但是需要系統管理權限。

    **適用於：**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]。     也所需的執行個體[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]封裝管理透過 Ddl 其中尚未啟用。

+ [伺服器上安裝新的 R 封裝**沒有**網際網路存取](#bkmk_offlineInstall)

    如果伺服器沒有網際網路存取，一些額外的步驟準備所需的封裝。 本章節描述如何準備安裝封裝及其相依性所需的檔案。

+ [使用建立外部程式庫陳述式安裝封裝](#bkmk_createlibrary) 

    SQL Server 2017，才能讓 DBA 不直接執行 R 或 Python 程式碼中建立套件庫中，會提供建立外部程式庫陳述式。 不過，此方法需要事先準備所有必要的封裝。  

    **適用於：** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; 其他限制也適用  

## <a name="bkmk_rInstall"></a> 安裝新的 R 封裝，使用網際網路

您可以使用標準的 R 工具來安裝新的封裝上的 SQL Server 2016 或 SQL Server 2017 執行個體。 此程序，您都必須在電腦上的系統管理員。

> [!IMPORTANT] 
> 請務必要與目前的執行個體相關聯的預設文件庫安裝封裝。 永遠不會安裝到使用者目錄的封裝。

此程序描述如何安裝封裝使用 RGui;不過，您可以使用 RTerm 或任何其他 R 命令列工具，可支援高的存取權限。

### <a name="install-a-package-using-rgui-or-rterm"></a>使用 RGui 或 RTerm 安裝封裝

1. 瀏覽至伺服器上安裝的執行個體的 R 程式庫的資料夾。

  **預設執行個體**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **具名執行個體**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  如果您已使用繫結，若要升級的機器學習服務元件，可能已變更路徑。 安裝新的封裝之前，務必檢查執行個體路徑。 

2. 以滑鼠右鍵按一下 RGui.exe，然後選取**系統管理員身分執行**。

    如果您沒有必要的權限，請連絡資料庫管理員，並提供您需要的套件清單。

3. 從命令列中，如果您知道封裝名稱，您可以輸入：`install.packages("the_package-name")`雙引號所需的封裝名稱。

4. 當系統要求您的鏡像網站，選取對您位置而言方便的任何網站。

5. 如果目標封裝相依於其他封裝，R 安裝程式會自動下載相依性，並讓您將進行安裝。

6. 每個執行個體是在您要使用的封裝，請分別執行安裝。 封裝無法執行個體之間共用。

## <a name = "bkmk_offlineInstall"></a> 使用的 R 工具的離線安裝

若要在沒有網際網路存取的伺服器上安裝 R 封裝，您必須：

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

2. 開啟伺服器上安裝的執行個體的 R 程式庫的資料夾。 例如，如果您使用 Windows 命令提示字元，瀏覽至 RTerm.Exe 或 RGui.exe 的所在位置的目錄中。

  **預設執行個體**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **具名執行個體**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. RGui 或命令提示字元上按一下滑鼠右鍵，然後選取**系統管理員身分執行**。

4. 執行 R 指令`install.packages`並指定封裝或儲存機制名稱和壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會擷取 R 封裝`mynewpackage`從其本機的 zip 檔案，假設您的複本儲存在目錄中`C:\Temp\Downloaded packages`，並在本機電腦上安裝封裝。 如果封裝有任何相依性，安裝程式會檢查文件庫中現有的封裝。 如果您已經建立包含相依性的儲存機制，安裝程式會安裝必要的封裝。

    如果任何必要的封裝不會出現在執行個體文件庫，zip 檔案中找不到目標套件的安裝將會失敗。

## <a name="bkmk_createlibrary"></a> 若要安裝封裝中使用 DDL 陳述式 

在 SQL Server 2017，您可以使用[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式來加入執行個體或特定資料庫的封裝的集合。 此 DDL 陳述式和支援的資料庫角色被專為了安裝和管理封裝的 BA 而不需要使用 R 或 Python 工具。

此程序需要一些準備工作，相較於安裝封裝使用傳統的 R 或 Python 方法。

+ 必須是所有的封裝，可做為壓縮檔案，在本機，而不是從網際網路下載。

    如果您在伺服器上沒有存取檔案系統，您也可以傳遞完整的封裝為變數，使用一種二進位格式。 如需詳細資訊，請參閱[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)。

+ 如果沒有套件所需，陳述式將會失敗。 您必須分析您想要安裝並確定封裝會上載到伺服器和資料庫的封裝的相依性。 我們建議您使用**miniCRAN**或**igraph**分析封裝相依性。

### <a name="prepare-the-packages-in-archive-format"></a>準備封裝封存格式

1. 如果您要安裝在單一封裝，請下載 zip 格式的封裝。 

2. 如果封裝需要任何其他封裝，您必須驗證所需的封裝是否可用。 您可以使用 miniCRAN 來分析目標的封裝，並識別所有相依性。 

3. 複製壓縮的檔案或 miniCRAN 儲存機制包含所有的封裝，以在伺服器上的本機資料夾。

4. 開啟**查詢**視窗中，使用具有系統管理權限的帳戶。

5. 執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上傳到資料庫的 zip 壓縮的封裝集合。

    例如，下列陳述式做為封裝來源 miniCRAN 儲存機制含有名稱**randomForest**封裝，以及其相依性。 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    您無法使用任意名稱。外部程式庫名稱都必須具有您預期時載入，或呼叫封裝所使用的相同名稱。

6. 如果已成功建立文件庫，您可以在 SQL Server 中，執行封裝，藉由呼叫預存程序。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>建立外部程式庫的已知的問題

在這些情況下支援建立外部程式庫：

+ 您正在安裝單一封裝不含相依性。
+ 您要安裝封裝的相依性，並已經事先備妥所有封裝。 

如果遺漏任何封裝相依性，就會失敗的 DDL 陳述式。 例如，已知安裝程序無法在這些情況下：

+ 安裝第二個層級相依性的封裝，您的分析未延伸到第二個層級的封裝。 例如，您要安裝**gglot2**，和識別資訊清單中列出的所有封裝; 不過，這些封裝未安裝其他相依性。
+ 您已安裝一組需要不同版本的支援封裝的封裝，而且您的伺服器有錯誤的版本。

## <a name="package-installation-tips"></a>封裝安裝秘訣

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


### <a name="know-which-library-you-are-using-for-installation"></a>知道您要用於安裝的程式庫

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，暫停時間，並確保 R 環境變數`.libPath`會使用單一路徑。

這個路徑應該指向 R_SERVICES 資料夾執行個體。 如需詳細資訊，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-r-server"></a>使用 R Server-並存安裝

如果您已安裝 Microsoft 機器學習伺服器 （獨立） 以及 SQL Server 機器學習服務，您的電腦應該有重複項目，所有的 R 工具和程式庫的每個個別安裝的 R。

僅供 Microsoft R Server R_SERVER 程式庫安裝套件，並無法透過 SQL Server 存取。 務必使用`R_SERVICES`安裝您想要使用 SQL Server 中的封裝時，程式庫。

### <a name="how-to-determine-which-packages-are-already-installed"></a>如何判斷已安裝哪個封裝？

 請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)