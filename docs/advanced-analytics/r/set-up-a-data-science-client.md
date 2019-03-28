---
title: 設定適用於 R 開發-SQL Server Machine Learning 服務的資料科學用戶端
description: 在 遠端連線到 SQL Server 的開發工作站上安裝本機的 R 程式庫和工具。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 12fefddcc01caeb9705c823a4e7283169dda1cc3
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510435"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>設定 SQL Server 上的 R 開發工具的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

可在 SQL Server 2016 或更新版本，包括中的 R 語言選項時，是 R 整合[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或是[SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)安裝。 

若要開發並部署 R 解決方案，適用於 SQL Server，安裝[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)以取得開發工作站上[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)和其他的 R 程式庫。 RevoScaleR 程式庫，也需要在遠端 SQL Server 執行個體，可協調計算這兩個系統之間的要求。 

在這篇文章，了解如何設定 R 用戶端的開發工作站，以便您可以與遠端的 SQL Server machine learning 及 R 整合啟用互動。 完成這篇文章中的步驟之後，您必須使用相同的 SQL Server 上的 R 程式庫。 您也會知道如何在 SQL Server 上推入本機的 R 工作階段的遠端 R 工作階段的計算。

![用戶端-伺服器元件](media/sqlmls-r-client-revo.png "本機和遠端 R 工作階段和程式庫")

若要驗證安裝，您可以使用內建**RGUI**工具在本文中所述或是[連結程式庫](#install-ide)RStudio 或您通常會使用任何其他 IDE。

> [!Tip]
> 如需這些練習的影片示範，請參閱 <<c0> [ 執行的 R 和 Python，在從 Jupyter Notebook 的 SQL Server 中遠端](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)。

> [!Note]
> 用戶端程式庫安裝的替代方案使用[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)做為豐富的用戶端，有些客戶偏好的更深入的案例中工作。 在獨立伺服器完全分開的 SQL Server，但因為它有相同的 R 程式庫，您可以使用它做為用戶端的 SQL Server 資料庫內分析。 您也可以使用它針對非 SQL 相關的工作，包括匯入，並從其他資料平台的資料模型的能力。 如果您安裝獨立伺服器，您可以找到此位置的 R 可執行檔： `C:\Program Files\Microsoft SQL Server\140\R_SERVER`。 若要驗證您的安裝，[開啟 R 主控台應用程式](#R-tools)使用 R.exe 該位置來執行命令。

## <a name="commonly-used-tools"></a>常用的工具

不論您是剛接觸 SQL，R 開發人員或 SQL 開發人員熟悉 R 和資料庫內分析，您需要的 R 開發工具和 T-SQL 查詢編輯器這類[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)執行所有的資料庫內分析功能。

簡單的 R 開發案例中，您可以使用可執行檔，RGUI 一起包含在基底 R 散發 MRO 和 SQL Server 中。 這篇文章說明如何使用本機和遠端 R 工作階段的 RGUI。 改善產能，您應該使用完整的 IDE 這類[RStudio 或 Visual Studio](#install-ide)。

SSMS 屬於不同下載，用於建立和執行預存程序，在 SQL Server，包括所包含的 R 程式碼。 您在開發環境中撰寫任何 R 程式碼可以內嵌在預存程序中。 您可以逐步執行其他教學課程來了解[SSMS 和內嵌的 R](../tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="1---install-r-packages"></a>1-安裝 R 套件

Microsoft 的 R 封裝有多個產品和服務。 在本機工作站上，我們建議您安裝 Microsoft R Client。 R 用戶端會提供[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)， [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)， [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)，和其他 R 套件。

1. [下載 Microsoft R Client](https://aka.ms/rclient/download)。

2. 在安裝精靈中，接受或變更預設安裝路徑，接受或變更 [元件] 清單中，並接受 Microsoft R Client 授權條款。

  安裝完成時，歡迎使用畫面向您介紹的產品和文件。

3. 建立以確保一致的輸出，在 Intel 數學核心程式庫 (MKL) 計算 MKL_CBWR 系統環境變數。

  + 在控制台中，按一下**系統及安全性** > **System** > **進階系統設定** >  **環境變數**。
  + 建立新的系統變數，名為**MKL_CBWR**，值設為**自動**。

## <a name="2---locate-executables"></a>2-找出可執行檔

找出並列出要確認已安裝 R.exe、 RGUI 和其他套件的安裝資料夾的內容。 

1. 在 [檔案總管] 中，開啟 C:\Program Files\Microsoft\R Client\R_SERVER\bin 資料夾以確認 R.exe 的位置。

2. 開啟 x64 子資料夾，以確認**RGUI**。 下一個步驟中，您將使用此工具。

3. 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\library 以檢閱使用 R 用戶端，包括 RevoScaleR、 MicrosoftML 及其他安裝的套件清單。


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-啟動 RGUI

當您安裝 R 與 SQL Server 時，您會取得相同的 R 工具，是個 R 版本，例如 RGui 或 Rterm，等等任何基底安裝的標準。 這些工具是輕量、 適用於檢查封裝和程式庫的資訊、 執行臨機操作的命令或指令碼，或逐步教學課程。 您可以使用這些工具，以取得 R 版本資訊，並確認連線能力。

1. 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64，然後按兩下**RGui**啟動 R 工作階段使用 R 命令提示字元。

  當您從 Microsoft 程式資料夾啟動 R 工作階段時，數個封裝，包括 RevoScaleR，就會自動載入。 

2. 輸入`print(Revo.version)`在命令提示字元中，返回 RevoScaleR 封裝的版本資訊。 您應該 RevoScaleR 9.2.1 或 9.3.0 版本。

3. 請輸入**search**在 R 提示字元中，取得一份已安裝的套件。

   ![載入 R 時的版本資訊](../install/media/rclient-rgui-r-prompt.png "開啟 R 提示字元")


## <a name="4---get-sql-permissions"></a>4-取得 SQL 權限

在 R 用戶端中，R 處理僅限使用兩個執行緒和記憶體中的資料。 使用多個核心和大型資料集的可調整處理，您可以使用 shift 同時執行 (稱為*計算內容*) 的資料集和遠端的 SQL Server 執行個體的運算能力。 這是建議的實際執行 SQL Server 執行個體中，與用戶端整合，您需要的權限和連接資訊，讓它運作。

若要連接到執行指令碼，並上傳資料的 SQL Server 的執行個體，您必須具有有效的登入資料庫伺服器上。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是某些情況下，更容易，尤其是您的指令碼包含到外部資料的連接字串。

最小值，用來執行程式碼的帳戶必須具有您正在使用，再加上特殊權限執行的任何外部指令碼，從資料庫讀取的權限。 大部分的開發人員也需要若要建立預存程序，並將資料寫入資料表，其中包含定型資料的權限，或評分的資料。 

請詢問資料庫管理員，以便[設定您的帳戶的下列權限](../security/user-permission.md)，在資料庫中，您可以使用:

+ **EXECUTE ANY EXTERNAL SCRIPT**伺服器上執行 R 指令碼。
+ **db_datareader**權限才能執行用來定型模型的查詢。
+ **db_datawriter**撰寫定型資料或評分的資料。
+ **db_owner**為了建立物件，例如預存程序，資料表，函式。 
  您也需要**db_owner**建立範例和測試資料庫。 

如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列資料庫系統管理員，以具有安裝與執行個體的套件。 SQL Server 是安全的環境，並限制可安裝套件的位置。 如需詳細資訊，請參閱 < [SQL Server 上安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。

## <a name="5---test-connections"></a>5-測試連接

 驗證步驟中，使用**RGUI**和 RevoScaleR 確認連線到遠端伺服器。 SQL Server 必須能夠進行[的遠端連線](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)而且您必須具備權限，包括使用者登入並連接到資料庫。 

下列步驟假設示範資料庫[NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)，和 Windows 驗證。

1. 開啟**RGUI**用戶端工作站上。 例如，請移至`~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`，然後按兩下**RGui.exe**啟動它。

2. RevoScaleR 會自動載入。 確認 RevoScaleR 可以執行此命令運作： `print(Revo.version)`

3. 輸入遠端伺服器執行的示範指令碼。 您必須修改下列的範例指令碼，以包含遠端的 SQL Server 執行個體的有效名稱。 此工作階段開始的本機工作階段，但**rxSummary**函式會執行遠端 SQL Server 執行個體上。

  ```R
  # Define a connection. Replace server with a valid server name.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
  # Specify the input data in a SQL query.
  sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
  # Define a remote compute context based on the remote server.
  cc <-RxInSqlServer(connectionString=connStr)

  # Execute the function using the remote compute context.
  rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
  ```

  **結果：**

  此指令碼會連線到遠端伺服器上的資料庫，可提供查詢、 建立計算內容`cc`指示遠端執行程式碼，然後提供的 RevoScaleR 函式**rxSummary**傳回統計查詢結果的摘要。

  ```R
    Call:
  rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
      connectionString = connStr), computeContext = cc)

  Summary Statistics Results for: ~.
  Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
  Number of valid observations: 100 
  
  Name       Mean   StdDev   Min Max ValidObs MissingObs
  tip_amount 63.245 31.61087 36  180 100      0     
  ```

4. 取得及設定計算內容。 一旦您設定計算內容時，就會生效的工作階段的持續時間。 如果您不確定計算是本機或遠端，請執行下列命令，以了解。指定連接字串的結果會指出遠端計算內容。

  ```R
  # Return the current compute context.
  rxGetComputeContext()

  # Revert to a local compute context.
  rxSetComputeContext("local")
  rxGetComputeContext()

  # Switch back to remote.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  cc <-RxInSqlServer(connectionString=connStr)
  rxSetComputeContext(cc)
  rxGetComputeContext()
  ```  

5. 傳回資料來源，包括名稱和型別中的變數的詳細資訊。

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  結果包含 23 的變數。


6. 產生散佈圖來探索是否有兩個變數之間的相依性。 

  ```R
  # Set the connection string. Substitute a valid server name for the placeholder.
  connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

  # Specify a query on the nyctaxi_sample table.
  # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
  sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
  cc <-RxInSqlServer(connectionString=connStr)

  # Generate a scatter plot.
  rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
  ```

  下列螢幕擷取畫面顯示輸入和散佈圖的輸出。

   ![散佈圖中 RGUI](media/rclient-setup-scatterplot.png "NYC 計程車示範資料的散佈圖")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-連結 R.exe 工具

對於持續性和嚴重的開發專案，您應該安裝整合式的開發環境 (IDE)。 SQL Server 工具和內建的 R 工具沒法沈重的 R 開發工具的。 運作的程式碼之後，您可以將它部署為 SQL Server 上執行的預存程序。

您的 IDE 指向本機的 R 程式庫： 基底 R、 RevoScaleR，等等。 遠端 SQL Server 上執行工作負載發生指令碼執行期間，您的指令碼叫用上存取資料和作業在該伺服器上的 SQL 伺服器的遠端計算內容時。

### <a name="rstudio"></a>RStudio

使用時[RStudio](https://www.rstudio.com/)，您可以設定要使用的 R 程式庫和對應於遠端的 SQL Server 上的可執行檔的環境。

1. 請檢查 SQL Server 上安裝的 R 套件版本。 如需詳細資訊，請參閱 <<c0> [ 取得 R 封裝資訊](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。

1. 安裝 Microsoft R Client，或其中一個獨立伺服器選項，以新增 RevoScaleR 和其他 R 套件，包括您的 SQL Server 執行個體所使用的基底 R 散發。 選擇在相同的版本層級或更低 （套件都是具有回溯相容性），在伺服器上提供相同的套件版本。 版本資訊，請參閱這篇文章中對應的版本：[升級 R 和 Python 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

1. 在 RStudio 中，[更新您的 R 路徑](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)指向提供 RevoScaleR、 Microsoft R Open，以及其他 Microsoft 套件的 R 環境。 

  + 針對 R 用戶端安裝中，尋找 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + 適用於獨立伺服器，尋找 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 或 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. 關閉然後再開啟 RStudio。

當您重新開啟 RStudio 時，R 可執行檔從 R 用戶端 （或獨立伺服器） 會是預設 R 引擎。


### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools for Visual Studio (RTVS)

如果您還沒有慣用的 IDE for R，我們建議您**R Tools for Visual Studio**。

+ [下載 R Tools for Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [安裝指示](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio)-RTVS 位於數個版本的 Visual Studio。
+ [開始使用 R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>從 RTVS 連線到 SQL Server

此範例會使用 Visual Studio 2017 Community Edition，已安裝資料科學工作負載。

1. 從**檔案**功能表上，選取**新增**，然後選取**專案**。

2. 在左窗格包含一份預先安裝的範本。 按一下  **R**，然後選取**R 專案**。 在 **名稱**方塊中，輸入`dbtest`然後按一下**確定**。 

  Visual Studio 會建立新的專案資料夾和預設指令碼檔案， `Script.R`。 

3. 型別`.libPaths()`在第一行的指令碼檔案，然後再按 CTRL + ENTER。

  目前的 R 程式庫路徑應該會顯示在**R 互動式**視窗。 

4. 按一下  **R 工具**功能表，然後選取**Windows**以查看您可以在您的工作區中顯示其他 R 特定視窗的清單。
 
  + 檢視目前的文件庫中的封裝上的 [說明]，按下 CTRL + 3。
  + 請參閱中的 R 變數**變數總管**，按下 CTRL + 8。

## <a name="next-steps"></a>後續步驟

兩個不同的教學課程包含練習，讓您將能練習切換計算內容從本機到遠端的 SQL Server 執行個體。

+ [教學課程：使用 RevoScaleR R 函式與 SQL Server 資料](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)