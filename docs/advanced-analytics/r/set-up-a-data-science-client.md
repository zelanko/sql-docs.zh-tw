---
title: 設定適用于 R 開發的資料科學用戶端
description: 在開發工作站上安裝本機 R 程式庫和工具, 以 SQL Server 的遠端連線。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e87770447c371f46ad384daffa3c7bc40b836904
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715598"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>在 SQL Server 上設定適用于 R 開發的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

當您在[SQL Server 2016 R services](../install/sql-r-services-windows-install.md)或[SQL Server Machine Learning Services (資料庫內)](../install/sql-machine-learning-services-windows-install.md)安裝中包含 r 語言選項時, 會在 SQL Server 2016 或更新版本中提供 r 整合。 

若要開發及部署適用于 SQL Server 的 R 解決方案, 請在您的開發工作站上安裝[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) , 以取得[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)和其他 R 程式庫。 RevoScaleR 程式庫 (在遠端 SQL Server 實例上也需要) 會協調兩個系統之間的計算要求。 

在本文中, 您將瞭解如何設定 R 用戶端開發工作站, 讓您可以與啟用機器學習和 R 整合的遠端 SQL Server 進行互動。 完成本文中的步驟之後, 您將會擁有與 SQL Server 上相同的 R 程式庫。 您也將瞭解如何將計算從本機 R 會話推送至 SQL Server 上的遠端 R 會話。

![用戶端-伺服器元件](media/sqlmls-r-client-revo.png "本機和遠端 R 會話和程式庫")

若要驗證安裝, 您可以使用本文中所述的內建**rgui.exe**工具, 或將[程式庫連結](#install-ide)至 RStudio 或您通常使用的其他任何 IDE。

> [!Note]
> 用戶端程式庫安裝的另一個替代方案是使用[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)做為豐富型用戶端, 而某些客戶會偏好更深入的案例工作。 獨立伺服器與 SQL Server 完全分離, 但因為它具有相同的 R 程式庫, 所以您可以使用它做為 SQL Server 資料庫內分析的用戶端。 您也可以將它用於與非 SQL 相關的工作, 包括能夠從其他資料平臺匯入和模型資料。 如果您安裝獨立伺服器, 您可以在此位置找到 R 可執行檔: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`。 若要驗證您的安裝, 請[開啟 r 主控台應用程式](#R-tools), 以使用該位置上的 .exe 執行命令。

## <a name="commonly-used-tools"></a>常用的工具

無論您是 SQL 的 R 開發人員新手, 或是 R 的 SQL 開發人員新手和資料庫內分析, 您都需要 R 開發工具和 T-SQL 查詢編輯器 (例如[SQL Server Management Studio (SSMS))](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)來執行資料庫內的所有功能分析.

針對簡單的 R 開發案例, 您可以使用 RGUI.EXE 可執行檔 (隨附于 MRO 和 SQL Server 中的基底 R 散發)。 本文說明如何針對本機和遠端 R 會話使用 RGUI.EXE。 為了提升生產力, 您應該使用完整功能的 IDE, 例如[RStudio 或 Visual Studio](#install-ide)。

SSMS 是個別的下載, 適用于在 SQL Server 上建立和執行預存程式, 包括包含 R 程式碼的程式。 您在開發環境中撰寫的任何 R 程式碼, 幾乎都可以內嵌在預存程式中。 您可以逐步執行其他教學課程, 以瞭解[SSMS 和 Embedded R](../tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="1---install-r-packages"></a>1-安裝 R 套件

Microsoft 的 R 套件適用于多項產品和服務。 在本機工作站上, 建議您安裝 Microsoft R Client。 R 用戶端提供[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)、 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)、 [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)和其他 r 套件。

1. [下載 Microsoft R Client](https://aka.ms/rclient/download)。

2. 在安裝精靈中, 接受或變更預設安裝路徑、接受或變更元件清單, 並接受 Microsoft R Client 授權條款。

  當安裝完成時, [歡迎使用] 畫面會向您介紹產品和檔。

3. 建立 MKL_CBWR 系統內容變數, 以確保在 Intel 數學核心程式庫 (MKL) 計算上有一致的輸出。

  + 在 [控制台] 中, 按一下 [**系統及安全性** > **系統** > ] [系統**設定** > ] [**環境變數**]。
  + 建立名為**MKL_CBWR**的新系統變數, 並將其值設定為**AUTO**。

## <a name="2---locate-executables"></a>2-尋找可執行檔

找出並列出安裝資料夾的內容, 以確認已安裝 R .exe、RGUI.EXE 和其他套件。 

1. 在 [檔案管理器] 中, 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\bin 資料夾以確認 R .exe 的位置。

2. 開啟 x64 子資料夾以確認**rgui.exe**。 您將在下一個步驟中使用此工具。

3. 開啟 C:\Program Files\Microsoft\R Client\R_SERVER\library, 以查看與 R 用戶端一起安裝的套件清單, 包括 RevoScaleR、MicrosoftML 和其他。


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-開始 RGUI.EXE

當您使用 SQL Server 安裝 R 時, 會取得 R 的任何基底安裝標準的相同 R 工具, 例如 Rgui.exe、Rterm 等等。 這些工具很輕量, 適用于檢查套件和程式庫資訊、執行臨機操作命令或腳本, 或逐步解說教學課程。 您可以使用這些工具來取得 R 版本資訊, 並確認連線能力。

1. 開啟 [C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64], 然後按兩下 [ **rgui.exe** ], 使用 r 命令提示字元啟動 r 會話。

  當您從 Microsoft 程式資料夾啟動 R 會話時, 會自動載入數個套件 (包括 RevoScaleR)。 

2. 在`print(Revo.version)`命令提示字元中輸入, 以傳回 RevoScaleR 套件版本資訊。 您的 RevoScaleR 版本應為9.2.1 或9.3.0。

3. 在 R 提示字元中輸入**search ()** , 以取得已安裝套件的清單。

   ![載入 R 時的版本資訊](../install/media/rclient-rgui-r-prompt.png "開啟 R 提示")字元


## <a name="4---get-sql-permissions"></a>4-取得 SQL 許可權

在 R 用戶端中, R 處理的限制為兩個執行緒和記憶體中的資料。 若要使用多個核心和大型資料集進行可調整的處理, 您可以將執行 (稱為*計算內容*) 轉移至遠端 SQL Server 實例的資料集和計算能力。 這是用戶端與生產 SQL Server 實例整合的建議方法, 而且您將需要許可權和連線資訊, 才能讓它運作。

若要連接到 SQL Server 的實例, 以執行腳本並上傳資料, 您必須在資料庫伺服器上有有效的登入。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常會建議您使用 Windows 整合式驗證, 但在某些情況下, 使用 SQL 登入比較簡單, 特別是當您的腳本包含外部資料的連接字串時。

用來執行程式碼的帳戶至少必須具有讀取您所使用之資料庫的許可權, 以及執行任何外部腳本的特殊許可權。 大部分的開發人員也需要許可權來建立預存程式, 以及將資料寫入包含定型資料或計分資料的資料表。 

要求資料庫管理員在您使用 R 的資料庫中, 為[您的帳戶設定下列許可權](../security/user-permission.md):

+ **執行任何外部腳本**, 以在伺服器上執行 R 腳本。
+ **db_datareader**許可權, 以執行用來定型模型的查詢。
+ **db_datawriter**以寫入定型資料或評分資料。
+ **db_owner**以建立預存程式、資料表、函數等物件。 
  您也需要**db_owner**來建立範例和測試資料庫。 

如果您的程式碼需要 SQL Server 預設不會安裝的封裝, 請向資料庫管理員安排, 讓封裝與實例一起安裝。 SQL Server 是安全的環境, 而且可能會限制安裝套件的位置。 如需詳細資訊, 請參閱[在 SQL Server 上安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。

## <a name="5---test-connections"></a>5-測試連接

 在驗證步驟中, 請使用**rgui.exe**和 RevoScaleR 來確認與遠端伺服器的連接。 您必須針對[遠端連線](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)啟用 SQL Server, 而且您必須具有許可權, 包括使用者登入和要連接的資料庫。 

下列步驟假設示範資料庫、 [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)和 Windows 驗證。

1. 在用戶端工作站上開啟**rgui.exe** 。 例如, 移至`~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` , 然後按兩下**rgui.exe**來啟動它。

2. RevoScaleR 會自動載入。 執行下列命令來確認 RevoScaleR 可運作:`print(Revo.version)`

3. 輸入在遠端伺服器上執行的示範腳本。 您必須修改下列範例腳本, 使其包含遠端 SQL Server 實例的有效名稱。 這個會話會以本機會話開始, 但是**rxSummary**函數會在遠端 SQL Server 實例上執行。

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

  此腳本會連接到遠端伺服器上的資料庫、提供查詢、建立遠端程式碼執行`cc`的計算內容指示, 然後提供 RevoScaleR 函數**rxSummary**來傳回查詢的統計摘要。更.

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

4. 取得並設定計算內容。 一旦您設定了計算內容, 它在會話的持續時間內仍會生效。 如果您不確定是在本機或遠端計算, 請執行下列命令來找出。指定連接字串的結果會指出遠端計算內容。

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

5. 傳回資料來源中變數的相關資訊, 包括名稱和類型。

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  結果包括23個變數。


6. 產生散佈圖, 以探索兩個變數之間是否有相依性。 

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

  下列螢幕擷取畫面顯示輸入和散佈圖輸出。

   ![Rgui.exe 中的散佈]圖(media/rclient-setup-scatterplot.png "NYC 計程車示範資料的散佈圖")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-R .exe 的連結工具

針對持續性和嚴重的開發專案, 您應該安裝整合式開發環境 (IDE)。 SQL Server 工具和內建的 R 工具都不適用於繁重的 R 開發。 一旦有了工作程式碼, 您就可以將它部署為預存程式, 以便在 SQL Server 上執行。

將您的 IDE 指向本機 R 程式庫: 基本 R、RevoScaleR 等等。 在腳本執行期間, 當您的腳本在 SQL Server 上叫用遠端計算內容, 並存取該伺服器上的資料和作業時, 就會在遠端 SQL Server 發生工作負載。

### <a name="rstudio"></a>RStudio

使用[RStudio](https://www.rstudio.com/)時, 您可以將環境設定為使用對應至遠端 SQL Server 上的 R 程式庫和可執行檔。

1. 檢查 SQL Server 上安裝的 R 套件版本。 如需詳細資訊, 請參閱[取得 R 封裝資訊](../package-management/installed-package-information.md)。

1. 安裝 Microsoft R Client 或其中一個獨立伺服器選項, 以新增 RevoScaleR 和其他 R 套件, 包括 SQL Server 實例所使用的基底 R 散發。 選擇相同層級或更低的版本 (套件回溯相容), 其提供的封裝版本與伺服器上的相同。 如需版本資訊, 請參閱本文中的版本對應:[升級 R 和 Python 元件](../install/upgrade-r-and-python.md)。

1. 在 RStudio 中,[更新您的 r 路徑](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R), 以指向提供 RevoScaleR、Microsoft R Open 和其他 Microsoft 套件的 r 環境。 

  + 針對 R 用戶端安裝, 尋找 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + 針對獨立伺服器, 尋找 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 或 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. 關閉, 然後開啟 RStudio。

當您重新開啟 RStudio 時, r 用戶端 (或獨立伺服器) 的 R 可執行檔是預設的 R 引擎。


### <a name="r-tools-for-visual-studio-rtvs"></a>Visual Studio R 工具 (RTVS)

如果您還沒有適用于 R 的慣用 IDE, 建議**Visual Studio R 工具**。

+ [下載 Visual Studio R 工具 (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [安裝指示](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio)-RTVS 在數個 Visual Studio 版本中都有提供。
+ [開始使用 Visual Studio R 工具](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>從 RTVS 連接到 SQL Server

這個範例會使用已安裝資料科學工作負載的 Visual Studio 2017 社區版。

1. 從 [檔案] 功能表中, 選取 [**新增**], 然後選取 [**專案**]。

2. 左窗格包含預先安裝的範本清單。 按一下 [ **r**], 然後選取 [ **r 專案**]。 在 [**名稱**] 方塊中`dbtest` , 輸入, 然後按一下 **[確定]** 。 

  Visual Studio 會建立新的專案資料夾和預設的腳本`Script.R`檔案。 

3. 輸入`.libPaths()`腳本檔案的第一行, 然後按 CTRL + ENTER。

  目前的 R 程式庫路徑應該會顯示在 [ **R 互動**] 視窗中。 

4. 按一下 [ **R 工具**] 功能表, 然後選取 [ **Windows** ], 以查看您可以在工作區中顯示的其他 R 特定視窗清單。
 
  + 按 CTRL + 3, 以在目前文件庫中查看封裝的說明。
  + 按 CTRL + 8 來查看**變數總管**中的 R 變數。

## <a name="next-steps"></a>後續步驟

兩個不同的教學課程包含練習, 讓您可以練習將計算內容從本機切換至遠端 SQL Server 實例。

+ [教學課程：搭配 SQL Server 資料使用 RevoScaleR R 函數](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)