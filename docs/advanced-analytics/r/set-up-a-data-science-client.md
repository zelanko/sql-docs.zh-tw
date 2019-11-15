---
title: 設定 R 資料科學用戶端
description: 在開發工作站上安裝本機 R 程式庫和工具，以便與 SQL Server 進行遠端連線。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 643de4d56692687b7c88b88c712fb1cc478eb0a1
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727375"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>在 SQL Server 上設定用於 R 開發的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

當您在 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 或 [SQL Server 機器學習服務 (資料庫內)](../install/sql-machine-learning-services-windows-install.md) 安裝中納入 R 語言選項時，SQL Server 2016 或更新版本中便會提供 R 整合。 

若要開發和部署適用於 SQL Server 的 R 解決方案，請在開發工作站上安裝 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)，以取得 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 和其他 R 程式庫。 遠端 SQL Server 執行個體上也需要的 RevoScaleR 程式庫會協調兩個系統之間的計算要求。 

請在本文中了解如何設定 R 用戶端開發工作站，以便與已啟用機器學習和 R 整合的遠端 SQL Server 互動。 在完成本文中的步驟之後，您將會獲得與 SQL Server 上相同的 R 程式庫。 您也會知道如何將本機 R 工作階段的計算推送到 SQL Server 上的遠端 R 工作階段。

![用戶端伺服器元件](media/sqlmls-r-client-revo.png "本機和遠端 R 工作階段和程式庫")

若要驗證安裝，您可以使用本文所述的內建 **RGUI** 工具，或是[將程式庫連結](#install-ide)到 RStudio 或您平常使用的任何其他 IDE。

> [!Note]
> 除了用戶端程式庫安裝之外，還有另一種方式是使用[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)作為豐富型用戶端；針對更深入的案例工作，某些客戶會偏好使用此選項。 獨立伺服器會與 SQL Server 完全分離，但由於它具有相同的 R 程式庫，因此您可以使用它作為 SQL Server 資料庫內分析的用戶端。 您也可以將它用於非 SQL 相關的工作，包括從其他資料平台匯入及模型化資料的能力。 如果您安裝獨立伺服器，您可以在此位置找到 R 可執行檔：`C:\Program Files\Microsoft SQL Server\140\R_SERVER`。 若要驗證您的安裝，請[開啟 R 主控台應用程式](#R-tools)，在該位置使用 R.exe 來執行命令。

## <a name="commonly-used-tools"></a>常用工具

無論您是不熟悉 SQL 的 R 開發人員，還是不熟悉 R 及資料庫內分析的 SQL 開發人員，您都會需要 R 開發工具和 T-SQL 查詢編輯器 (例如 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)) 來執行資料庫內分析的所有功能。

針對簡單的 R 開發案例，您可以使用 RGUI 可執行檔 (隨附於 MRO 和 SQL Server 中的基底 R 散發套件)。 本文會說明如何針對本機和遠端的 R 工作階段使用 RGUI。 為了提高生產力，您應該使用功能完整的 IDE，例如 [RStudio 或 Visual Studio](#install-ide)。

SSMS 是個別的下載，很適合用來建立及執行 SQL Server 上的預存程序，包括那些包含 R 程式碼的預存程序。 您在開發環境中撰寫的 R 程式碼，幾乎都可以內嵌在預存程序中。 您可以逐步執行其他教學課程以了解 [SSMS 和內嵌的 R](../tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="1---install-r-packages"></a>1 - 安裝 R 套件

多項產品和服務皆有提供 Microsoft 的 R 套件。 在本機工作站上，建議您安裝 Microsoft R Client。 R Client 會提供 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)、[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)、[SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) 和其他 R 套件。

1. [下載 Microsoft R Client](https://aka.ms/rclient/download)。

2. 在安裝精靈中，接受或變更預設安裝路徑、接受或變更元件清單，並接受 Microsoft R Client 授權條款。

  安裝完成時會有歡迎使用畫面向您介紹產品和文件。

3. 建立 MKL_CBWR 系統環境變數，以確保 Intel Math Kernel Library (MKL) 計算會有一致的輸出。

  + 在 [控制台] 中，按一下 [系統及安全性]   > [系統]   > [進階系統設定]   > [環境變數]  。
  + 建立名為 **MKL_CBWR** 的新系統變數，並將值設定為 [自動]  。

## <a name="2---locate-executables"></a>2 - 尋找可執行檔

找到並列出安裝資料夾的內容，以確認 R.exe、RGUI 和其他套件均已安裝好。 

1. 在檔案總管中，開啟 C:\Program Files\Microsoft\R Client\R_SERVER\bin 資料夾，以確認 R.exe 的位置。

2. 開啟 x64 子資料夾以確認 **RGUI**。 您會在下一個步驟中用到此工具。

3. 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\library，以檢閱與 R Client 一起安裝的套件清單，包括 RevoScaleR、MicrosoftML 和其他套件。


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - 啟動 RGUI

當您使用 SQL Server 來安裝 R 時，將會取得與 R 的任何基底安裝標準相同的 R 工具，例如 RGUI、RTerm 等等。 這些工具很小，適合用來檢查套件和程式庫資訊、執行特定命令或指令碼，或逐步進行教學課程。 您可以使用這些工具來取得 R 的版本資訊，並確認連線能力。

1. 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64，然後按兩下 **RGUI** 以使用 R 命令提示字元啟動 R 工作階段。

  當您從 Microsoft 程式資料夾啟動 R 工作階段時，系統會自動載入數個套件 (包括 RevoScaleR)。 

2. 在命令提示字元中輸入 `print(Revo.version)`，以傳回 RevoScaleR 套件的版本資訊。 您的 RevoScaleR 版本應為 9.2.1 或 9.3.0。

3. 在 R 提示字元中輸入 **search()** ，以取得已安裝套件的清單。

   ![載入 R 時的版本資訊](../install/media/rclient-rgui-r-prompt.png "開啟 R 提示字元")


## <a name="4---get-sql-permissions"></a>4 - 取得 SQL 權限

在 R Client 中，R 處理會受限於兩個執行緒和記憶體內部資料。 若要使用多個核心和大型資料集來進行可調整規模的處理，您可以將執行 (稱為「計算內容」  ) 轉移至遠端 SQL Server 執行個體的資料集和計算能力。 這是建議用來整合用戶端與生產環境 SQL Server 執行個體的方法，而且您需要權限和連線資訊才能讓此方法運作。

若要連線至 SQL Server 執行個體以執行指令碼及上傳資料，您必須擁有資料庫伺服器的有效登入。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常會建議您使用 Windows 整合式驗證，但針對某些案例使用 SQL 登入會比較簡單，特別是當您的指令碼包含外部資料的連接字串時。

至少，用來執行程式碼的帳戶必須擁有從您所使用的資料庫讀取的權限，以及 EXECUTE ANY EXTERNAL SCRIPT 特殊權限。 大部分的開發人員也會需要權限以建立預存程序，以及將資料寫入包含定型資料或評分資料的資料表中。 

詢問資料庫管理員以在您使用 R 的資料庫中[針對您的帳戶設定下列權限](../security/user-permission.md)：

+ **EXECUTE ANY EXTERNAL SCRIPT** 以在伺服器上執行 R 指令碼。
+ **db_datareader** 權限以執行用來將模型定型的查詢。
+ **db_datawriter** 以寫入定型資料或評分資料。
+ **db_owner** 以建立如預存程序、資料表、函式等的物件。 
  您也需要 **db_owner** 以建立範例和測試資料庫。 

如果您的程式碼需要 SQL Server 預設不會安裝的套件，請向資料庫管理員安排以搭配執行個體安裝那些套件。 SQL Server 是安全的環境，因此會限制可以安裝套件的位置。 如需詳細資訊，請參閱[在 SQL Server 上安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。

## <a name="5---test-connections"></a>5 - 測試連線

 在驗證步驟中，請使用 **RGUI** 和 RevoScaleR 來確認是否能與遠端伺服器連線。 SQL Server 必須啟用[遠端連線](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)功能，而且您必須具有權限，包括使用者登入資訊和所要連線的目標資料庫。 

下列步驟採用示範資料庫 ([NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)) 和 Windows 驗證。

1. 在用戶端工作站上開啟 **RGUI**。 例如，移至 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`，然後按兩下 **RGui.exe** 來加以啟動。

2. RevoScaleR 會自動載入。 執行下列命令來確認 RevoScaleR 是否正常運作：`print(Revo.version)`

3. 輸入會在遠端伺服器上執行的示範指令碼。 您必須修改下列範例指令碼，使其包含遠端 SQL Server 執行個體的有效名稱。 這個工作階段會以本機工作階段的形式來啟動，但是 **rxSummary** 函式會在遠端 SQL Server 執行個體上執行。

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

  此指令碼會連線至遠端伺服器上的資料庫、提供查詢、建立適用於遠端程式碼執行的計算內容 `cc` 指示，然後提供 RevoScaleR 函式 **rxSummary**，以傳回查詢結果的統計摘要。

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

4. 取得並設定計算內容。 設定了計算內容後，其便會在工作階段的持續時間內保持有效。 如果您不確定所進行的是本機還是遠端計算，請執行下列命令來加以了解。指定連接字串的結果代表是遠端計算內容。

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

5. 傳回關於資料來源變數的資訊，包括名稱和類型。

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  結果包括 23 個變數。


6. 產生散佈圖，以探索兩個變數之間是否有相依性。 

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

  下列螢幕擷取畫面會顯示輸入和散佈圖輸出。

   ![RGUI 中的散佈圖](media/rclient-setup-scatterplot.png "紐約市計程車示範資料的散佈圖")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - R.exe 的連結工具

針對持續且重大的開發專案，請安裝整合式開發環境 (IDE)。 SQL Server 工具和內建的 R 工具都不適用於繁重的 R 開發工作。 獲得可運作的程式碼後，便可將其部署為預存程序，以便在 SQL Server 上執行。

將 IDE 指向本機 R 程式庫：基底 R、RevoScaleR 等等。 在指令碼執行期間，當您的指令碼在 SQL Server 上叫用遠端計算內容，並存取該伺服器上的資料和作業時，系統就會在遠端 SQL Server 上執行工作負載。

### <a name="rstudio"></a>RStudio

使用 [RStudio](https://www.rstudio.com/) 時，您可以將環境設定為使用與遠端 SQL Server 上的項目對應的 R 程式庫和可執行檔。

1. 檢查 SQL Server 上安裝的 R 套件版本。 如需詳細資訊，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。

1. 安裝 Microsoft R Client 或其中一個獨立伺服器選項，以新增 RevoScaleR 和其他 R 套件，包括 SQL Server 執行個體所使用的基底 R 散發套件。 選擇相同層級以下的版本 (套件具有回溯相容性)，其所提供的套件版本會與伺服器上的版本相同。 如需版本資訊，請參閱本文中的版本對應：[升級 R 與 Python 元件](../install/upgrade-r-and-python.md)。

1. 在 RStudio 中，[更新 R 路徑](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)以指向提供 RevoScaleR、Microsoft R Open 和其他 Microsoft 套件的 R 環境。 

  + 針對 R Client 安裝，請尋找 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + 針對獨立伺服器，請尋找 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 或 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. 先關閉再開啟 RStudio。

當您重新開啟 RStudio 時，R Client (或獨立伺服器) 中的 R 可執行檔會是預設的 R 引擎。


### <a name="r-tools-for-visual-studio-rtvs"></a>Visual Studio R 工具 (RTVS)

如果您還沒有用來處理 R 的慣用 IDE，建議您使用 **Visual Studio R 工具**。

+ [下載 Visual Studio R 工具 (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [安裝指示](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) - Visual Studio 的數個版本中都有提供 RTVS。
+ [開始使用 Visual Studio R 工具](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>從 RTVS 連線至 SQL Server

此範例會使用已安裝了資料科學工作負載的 Visual Studio 2017 Community Edition。

1. 從 [檔案]  功能表選取 [新增]  ，再選取 [專案]  。

2. 左窗格包含預先安裝的範本清單。 按一下 [R]  ，然後選取 [R 專案]  。 在 [名稱]  方塊中輸入 `dbtest`，然後按一下 [確定]  。 

  Visual Studio 會建立新的專案資料夾和預設的指令檔 `Script.R`。 

3. 在指令檔的第一行輸入 `.libPaths()`，然後按 CTRL + ENTER。

  目前的 R 程式庫路徑應該會顯示在 [R 互動]  視窗中。 

4. 按一下 [R 工具]  功能表，然後選取 [Windows]  ，以查看您可以在工作區中顯示的其他 R 專屬視窗清單。
 
  + 按 CTRL + 3，可在目前的程式庫中查看套件的說明。
  + 按 CTRL + 8，則可在**變數總管**中查看 R 變數。

## <a name="next-steps"></a>後續步驟

兩個不同的教學課程都包含練習，以便讓您練習如何將計算內容從本機切換至遠端 SQL Server 執行個體。

+ [教學課程：搭配 SQL Server 資料使用 RevoScaleR R 函式](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)