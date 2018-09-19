---
title: 設定 SQL Server 上的 R 開發工具的資料科學用戶端 |Microsoft Docs
description: 在 遠端連線到 SQL Server 的開發工作站上安裝本機的 R 程式庫和工具。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 309a78a2195f55a3ec39604b0c2bd385bb06a271
ms.sourcegitcommit: 9d0ff4f3e40db48fc01788684d34719065d159b6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/12/2018
ms.locfileid: "44724312"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>設定 SQL Server 上的 R 開發工具的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您已設定的執行個體之後[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支援機器學習服務，您應該設定能夠連線到遠端執行和部署伺服器的 R 開發環境。

### <a name="evaluation-and-independent-development"></a>評估和獨立的開發
 
如果您有 developer 版和計劃要在本機處理 R 指令碼想要移至 SQL Server，您可以跳到[安裝 IDE](#install-ide)指向本機 SQL Server 所使用的 R 程式庫中的工具。

> [!Tip]
> 如需示範和影片逐步解說，請參閱[執行的 R 和遠端 SQL Server 從 Jupyter Notebook 或任何 IDE 中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)或這[YouTube 影片](https://youtu.be/D5erljpJDjE)。

## <a name="1---install-r-packages"></a>1-安裝 R 套件

Microsoft 產品中的 R 功能是多層式。 開始使用 Microsoft 的開放原始碼基底 R 散發，但然後與特定產品套件，例如延伸[RevoScaleR](revoscaler-overview.md)，可讓遠端計算內容和 R 工作的平行執行。

用戶端與遠端伺服器之間的協調的作業都需要這兩個具有相同的封裝的系統。 若要取得完整的程式庫的用戶端工作站上，安裝下表中其中一個軟體套件。 

| 程式庫提供者 | 使用方式  |
|------------------|--------------------------------|
| [Microsoft R Client](http://aka.ms/rclient/download) |  這個免費的下載提供 RevoScaleR、 MicrosoftML，以及其他 R 套件，但上限為兩個執行緒和記憶體中的資料。 不過，還是建立在本機啟動的 R 解決方案，轉移執行 (稱為*計算內容*) 存取資料與遠端的 SQL Server 執行個體的運算能力。 這是建議的方法與實際執行 SQL Server 執行個體的用戶端整合。 如需有關這項工具的詳細資訊，請參閱 <<c0> [ 什麼是 Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)。|
| 獨立伺服器 | 底下**共用功能**，SQL Server 安裝程式包含適用於 SQL Server 2016 R Services 和 SQL Server 2017 machine learning 的獨立伺服器安裝選項。 這些是功能完整的伺服器，從 SQL Server 中完全分離，連接到並取用來自多種資料平台資料的能力。 但是，您可能無法使用用戶端的功能軟體，來存取 SQL Server database engine 執行個體執行的 R 和 Python 的工作。 [SQL Server 2017 Machine Learning 伺服器 （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)具有相同的程式庫，為 SQL Server 2017 machine learning 執行個體。 [SQL Server 2016 R Server （獨立式）](../install/sql-r-standalone-windows-install.md)具有相同的程式庫與 SQL Server 2016 R Services。 |


<a name="r-tool"></a>
 
## <a name="2---open-an-r-prompt"></a>2-開啟 R 提示字元

當您安裝 R 與 SQL Server 時，您會取得相同的 R 工具，是個 R 版本，例如 RGui 或 Rterm，等等任何基底安裝的標準。 這些工具是輕量、 適用於檢查封裝和程式庫的資訊、 執行臨機操作的命令或指令碼，或逐步教學課程。 您可以使用這些工具，以取得 R 版本資訊，並確認連線能力。

若要使用 R 與 SQL Server 或 R 用戶端一起安裝的版本，請從 SQL Server 或 R 用戶端的程式資料夾中開啟 R 提示字元。 下列步驟適用於 R 用戶端和 RGui.exe。

1. R Client，請移至`~\Program Files\Microsoft\R Client\R_SERVER\bin\x64`。
2. 按兩下**RGui.exe**啟動 R 工作階段使用 R 命令提示字元。

當您從 Microsoft 程式資料夾啟動 R 工作階段時，數個封裝，包括 RevoScaleR，就會自動載入。 請輸入**search**在 R 提示字元中，確認。

   ![載入 R 時的版本資訊](../install/media/rclient-rgui-r-prompt.png "開啟 R 提示字元")

### <a name="tool-list-and-location"></a>工具清單和位置

| 工具 | 描述 | 
|------|-------------|
| **RTerm**: | 命令列終端機中執行 R 指令碼 | 
| **RGui.exe** | 簡單的互動式編輯器，如。命令列引數都 RGui.exe 和 RTerm 相同。 |
| **RScript** | 在 批次模式中執行 R 指令碼的命令列工具。 |

俬柈糔槲**bin**與已安裝的 SQL Server 的基底 R 或 R 用戶端資料夾。 下列的路徑是有效的工具，在您安裝取決於哪一個產品版本和功能的位置：

| Microsoft 產品 | R 工具的位置 |
|-------------------|-----------------|
| Microsoft R Client | `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64` |
| Microsoft Machine Learning (R) 伺服器 | `~\Program Files\Microsoft\R_SERVER\bin\x64`
| SQL Server 2016 R Services | `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2016 R 獨立伺服器 | `~\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64` 
| SQL Server 2017 Machine Learning 服務 (R) | `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2017 Machine Learning (R) 獨立伺服器 | `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` |

## <a name="3---permissions"></a>3-權限

若要連接到執行指令碼，並上傳資料的 SQL Server 的執行個體，您必須具有有效的登入資料庫伺服器上。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是在某些情況下更簡單。

最小值，用來執行程式碼的帳戶必須具有您正在使用，再加上特殊權限執行的任何外部指令碼，從資料庫讀取的權限。 大部分的開發人員也需要在包含您的指令碼的預存程序的形式中建立新物件的權限和資料寫入其中包含定型資料的資料表或評分的資料。 

詢問資料庫管理員來設定，您可以使用： 資料庫中的下列權限的帳戶

+ **EXECUTE ANY EXTERNAL SCRIPT**伺服器上執行 R。
+ **db_datareader**權限才能執行用來定型模型的查詢。
+ **db_datawriter**撰寫定型資料或評分的資料。
+ **db_owner**為了建立物件，例如預存程序，資料表，函式。 
  您也需要**db_owner**建立範例和測試資料庫。 

如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列資料庫系統管理員，以具有安裝與執行個體的套件。 SQL Server 是安全的環境，並限制可安裝套件的位置。 不建議為您的程式碼的一部分臨機操作安裝封裝，即使您有權限。 此外，請務必仔細考慮安全性隱含意義 server 文件庫中安裝新套件之前。

> [!Tip]
> 如果您熟悉 SQL Server 和在本機開發環境中的工作，您可以逐步執行本教學課程來了解登入和設定權限：[深入探討 RevoScaleR](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

## <a name="4---test-connections"></a>4-測試連接

SQL Server 必須能夠進行[的遠端連線](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)而且您必須具備權限，包括使用者登入並連接到資料庫。 下列步驟假設示範資料庫[NYCTaxi_Sample](../tutorials/sqldev-download-the-sample-data.md) 」 和 「 Windows 驗證。

 驗證步驟中，使用內建的工具和 RevoScaleR 來確認連線到遠端伺服器。

1. 著手[開啟 R 工具](#r-tool)用戶端工作站上。 RevoScaleR 會自動載入。 例如，請移至`~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`，然後按兩下**RGui.exe**啟動它。

2. 確認 RevoScaleR 可以執行此命令會傳回統計摘要，在示範資料集上運作。 請確定您提供有效的伺服器名稱的 SQL Server 資料庫引擎執行個體。

```r
connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
testQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
cc <-RxInSqlServer(connectionString=connStr)
rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=testQuery, connectionString=connStr), computeContext=cc)
```
此指令碼會連線到遠端伺服器上的資料庫，可提供查詢、 建立計算內容`cc`指示遠端執行程式碼，然後提供的 RevoScaleR 函式**rxSummary**傳回統計查詢結果的摘要。

<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-安裝 IDE

對於持續性和嚴重的開發專案，您應該安裝整合式的開發環境 (IDE)。 SQL Server 工具和內建的 R 工具沒法沈重的 R 開發工具的。 運作的程式碼之後，您可以將它部署為 SQL Server 上執行的預存程序。

您應該將您的 IDE 指向本機的 R 程式庫： 基底 R、 RevoScaleR，等等。 遠端 SQL Server 上執行工作負載發生指令碼執行期間，您的指令碼叫用上存取資料和作業在該伺服器上的 SQL 伺服器的遠端計算內容時。

### <a name="rstudio"></a>RStudio

使用時[RStudio](https://www.rstudio.com/)，您可以設定要使用的 R 程式庫和對應於遠端的 SQL Server 上的可執行檔的環境。

1. 請檢查 SQL Server 上安裝的 R 套件版本。 如需詳細資訊，請參閱 <<c0> [ 取得 R 封裝資訊](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。

1. 安裝 Microsoft R Client，或其中一個獨立伺服器選項，以新增 RevoScaleR 和其他 R 套件，包括您的 SQL Server 執行個體所使用的基底 R 散發。 選擇在相同的版本層級或更低 （套件都是具有回溯相容性），提供相同的套件版本，在伺服器上的一樣。 版本資訊，請參閱這篇文章中對應的版本：[升級 R 和 Python 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

1. 在 RStudio 中，[更新您的 R 路徑](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)指向提供 RevoScaleR、 Microsoft R Open，以及其他 Microsoft 套件的 R 環境。 根據您如何取得 RevoScaleR 和其他程式庫，它是最可能的下列路徑：

  + C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library
  + C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library
  + C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64

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

5. 建立 SQL Server 執行個體的連接字串和 RxInSqlServer 建構函式中使用的連接字串，來建立 SQL Server 資料來源物件。 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```
    > [!TIP]
    > 若要執行批次，選取您想要執行並按下 CTRL + ENTER。

6. 到伺服器，設定計算內容，然後對資料執行一些簡單的 R 程式碼。

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    結果會傳回**R 互動式**視窗。
    
    如果您想要確保您自己的程式碼正在執行的 SQL Server 執行個體上，您可以使用 Profiler 建立追蹤。

## <a name="next-steps"></a>後續步驟

兩個不同的教學課程包含練習，讓您將能練習切換計算內容從本機到遠端的 SQL Server 執行個體。

+ [SQL Server 資料的教學課程： 使用 RevoScaleR R 函式](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)