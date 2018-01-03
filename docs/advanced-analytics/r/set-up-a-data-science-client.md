---
title: "設定用於 SQL Server 的資料科學用戶端 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 8f9156e11e906454e7cae00703d1ffd976424297
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="set-up-a-data-science-client-for-use-with-sql-server"></a>設定用於 SQL Server 的資料科學用戶端

您已設定的執行個體之後[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支援機器學習服務，您應該設定能夠連線到遠端執行和部署伺服器的開發環境。

本文說明某些一般用戶端案例，包括免費的 Visual Studio Community 版本 SQL Server 中執行 R 程式碼的組態。

## <a name="install-r-libraries-on-the-client"></a>在用戶端安裝 R 程式庫

用戶端環境必須包含 Microsoft R Open，以及支援在 SQL Server 上分散式執行 R 的其他 RevoScaleR 套件。 R 的標準分佈不需要支援遠端計算內容或平行執行 R 工作的封裝。

若要取得這些程式庫，請安裝下列其中一項：
  
+ [Microsoft R Client](http://aka.ms/rclient/download)

+ Microsoft R Server （適用於 SQL Server 2016)

    - 若要從 SQL Server 安裝程式安裝，請參閱[建立獨立 R 伺服器](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - 若要使用個別的 windows 安裝程式，請參閱[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ 機器學習伺服器 （適用於 SQL Server 2017)

    - 若要從 SQL Server 安裝程式安裝，請參閱[建立獨立 R 伺服器](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - 若要使用個別的 windows 安裝程式，請參閱[適用於 Windows 安裝 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="install-a-development-environment"></a>安裝開發環境

如果您還沒有慣用的 R 開發環境，我們建議下列其中一項：

+ 適用於 Visual Studio 的 R 工具

    適用於 Visual Studio 2015。

    安裝程式的資訊，請參閱[如何安裝 R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。
 
    若要設定 RTVS 以使用 Microsoft R 的用戶端程式庫，請參閱[有關 Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    即使免費的 Community Edition 包含資料科學工作負載，安裝適用於 R、 Python 和 F # 專案範本。

    下載 Visual Studio 從[此站台](https://www.visualstudio.com/vs/)。 

+ RStudio

    如果您偏好使用 RStudio，需要一些額外步驟才能使用 RevoScaleR 程式庫︰

    - 安裝 Microsoft R 用戶端，以取得需要的套件和程式庫。
    - 更新您的 R 路徑，以便使用 Microsoft R 執行階段。

    如需詳細資訊，請參閱[R 用戶端-設定您的 IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide)。

## <a name="configure-your-ide"></a>設定您的 IDE

+ 適用於 Visual Studio 的 R 工具

    請參閱[此站台](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)如需如何建置和偵錯 R 的一些範例專案中使用 R Tools for Visual Studio。 

+ Visual Studio 2017

    如果您安裝 Microsoft R 用戶端或 R 伺服器**之前**您安裝 Visual Studio、 「 R 伺服器程式庫會自動偵測與用於程式庫路徑。 如果您尚未安裝 RevoScaleR 程式庫中，從**R 工具**功能表上，選取**安裝 R 用戶端**。

## <a name="run-r-in-sql-server"></a>SQL Server 中執行 R

這個範例會使用 Visual Studio 2017 Community Edition 中，以安裝資料科學工作負載。

1. 從**檔案**功能表上，選取**新增**，然後選取 **專案**。

2. -手形窗格包含預先安裝的範本清單。 按一下**R**，然後選取**R 專案**。 在**名稱**方塊中，輸入`dbtest`按一下**確定**。

3. Visual Studio 會建立新的專案資料夾和預設指令碼檔案， `Script.R`。 

4. 型別`.libPaths()`指令碼的第一行上檔案，然後再按 CTRL + ENTER。

5. 目前的 R 程式庫路徑應該會顯示在**R 互動式**視窗。 

6. 按一下**R 工具**功能表，然後選取**Windows** ，查看您可以在您的工作區中顯示其他 R 特定視窗的清單。
 
    + 檢視目前的文件庫中的封裝上的 [說明]，按下 CTRL + 3。
    + 請參閱 R 變數中的**變數總管**，按下 CTRL + 8。

7. 建立 SQL Server 執行個體的連接字串和 RxInSqlServer 建構函式中使用的連接字串，若要建立 SQL Server 資料來源物件。 

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
    > 若要執行批次中，選取您想要執行，並按下 CTRL + ENTER。

8. 將計算內容到伺服器，然後再執行一些簡單的 R 程式碼的資料。

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    結果會傳回**R 互動式**視窗。
    
    如果您想要確保您自己的 SQL Server 執行個體上執行的程式碼，您可以使用程式碼剖析工具來建立追蹤。