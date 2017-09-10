---
title: "使用 TRANSACT-SQL (R SQL 快速入門) 中的 R 程式碼 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c023af0a3a9b9c53cb2b6adf7298c18657a60803
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>使用 TRANSACT-SQL (R SQL 快速入門) 中的 R 程式碼

本教學課程會逐步引導您完成從 T-SQL 預存程序呼叫 R 指令碼的基本機制。

**您將學習**

+ 如何在 T-SQL 函式中內嵌 R
+ 使用 R 和 SQL 資料類型和資料物件的一些秘訣
+ 如何建立簡單的模型，並將它儲存到 SQL Server
+ 如何建立預測和使用模型 R 繪圖

**預估的時間**

30 分鐘 (不包括設定)

## <a name="prerequisites"></a>必要條件

您必須具有存取 SQL server 執行個體已經安裝下列其中一種：

+ SQL Server 2017 機器學習服務，與安裝的 R 語言
+ SQL Server 2016 R Services

您的 SQL Server 執行個體可以是 Azure 虛擬機器或在內部部署。 只是知道，外部指令碼功能預設為停用，因此您可能需要執行一些額外的步驟，讓它運作。

若要執行 SQL 查詢，以包含 R 指令碼，您可以使用其他任何應用程式可以連接到資料庫並執行 T-SQL 程式碼。 SQL 專業人員可以使用 SQL Server Management Studio (SSMS) 或 Visual Studio。

此教學課程中，以顯示 執行 R SQL 伺服器內是多麼的輕鬆我們使用新**mssql 擴充 Visual Studio 程式碼**。 VS Code 是免費的開發環境可以在 Linux、 macOS、 或 Windows 上執行。 **Mssql*** 延伸模組是執行 Sql 查詢的輕量級擴充功能。 若要安裝它，請參閱這篇文章︰[使用適用於 Visual Studio Code 的 mssql 擴充功能 (英文)](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>連線到資料庫並執行 Hello World 測試指令碼

1. 在 Visual Studio Code 中，建立新的文字檔案並將它命名為 BasicRSQL.sql。
2. 開啟此檔案時，請按 CTRL+SHIFT+P (macOS 上為 COMMAND + P)，輸入 **sql** 以列出 SQL 命令，並選取 [連線]。 Visual Studio 程式碼會提示您建立要連接到特定的資料庫時使用的設定檔。 這是選擇性的但可讓您更輕鬆地切換資料庫和登入。
    + 選擇伺服器或已安裝 SQL Server 中的 R 執行個體。
    + 使用具有建立新資料庫權限的帳戶執行 SELECT 陳述式，並檢視資料表定義。
2. 如果連線成功，您應該能在狀態列中看到伺服器和資料庫名稱，以及您目前的認證。 如果連線失敗，請檢查電腦名稱和伺服器名稱是否正確。
3. 貼上此陳述式並加以執行。

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    在 Visual Studio Code 中，您可以將想要執行的程式碼醒目提示，並按下 CTRL+SHIFT+E。 如果這很難記住，您可以變更它！ 請參閱[自訂快速鍵繫結 (英文)](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。

    ![rsql basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**結果**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>疑難排解

+ 如果此查詢的任何錯誤，安裝可能不完整。 使用 SQL Server 安裝精靈新增該功能之後，您必須採取一些額外的步驟才能使用外部程式碼程式庫。  請參閱[設定 SQL Server R 服務](../r/set-up-sql-server-r-services-in-database.md)。

+ 請確定 Launchpad 服務正在執行。 根據您的環境，您可能需要啟用 R 背景工作帳戶以連線到 SQL Server、安裝額外的網路程式庫、啟用遠端程式碼執行，或在一切已設定完畢後重新啟動執行個體。 請參閱 [R 服務安裝和升級常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

+ 若要取得 Visual Studio Code，請參閱[下載並安裝 Visual Studio Code (英文)](https://code.visualstudio.com/Download)。

## <a name="next-lesson"></a>下一課

現在，您的執行個體已準備好使用 R，讓我們開始。

第 1 課：[處理輸入和輸出](rtsql-working-with-inputs-and-outputs.md)

第 2 課： [R 與 SQL 資料類型和資料物件](rtsql-r-and-sql-data-types-and-data-objects.md)

第 3 課：[使用 R 與 SQL Server 資料的函式](rtsql-using-r-functions-with-sql-server-data.md)

第 4 課：[建立預測模型](rtsql-create-a-predictive-model-r.md)

第 5 課：[預測和模型中的繪圖](rtsql-predict-and-plot-from-model.md)

