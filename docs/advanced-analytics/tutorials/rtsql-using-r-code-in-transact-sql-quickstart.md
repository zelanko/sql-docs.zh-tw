---
title: "\"Hello World\"基本 R 程式碼執行 T-SQL (SQL Server Machine Learning) 中的快速入門 |Microsoft Docs"
description: SQL Server 中的 R 指令碼的快速入門。 了解呼叫 R 指令碼在 hello world 練習使用 sp_execute_external_script 的系統預存程序的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/08/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1a51fcb9e67bef48346ff74ebfb1e911a6ee3365
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878081"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入門： 在 SQL Server 中的"Hello world"的 R 指令碼 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包含內建的 SQL Server 資料的資料科學分析的 R 語言支援。 您的 R 指令碼可以包含開放原始碼 R 函數，第三方的 R 程式庫或內建的 Microsoft R 程式庫這類[RevoScaleR](../r/revoscaler-overview.md)進行大規模的預測性分析。 

執行指令碼是透過預存程序，使用下列其中一個方法：

+ 內建[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)預存程序，將 R 指令碼中的傳遞做為輸入參數。
+ 換行中的 R 指令碼[之自訂預存程序](sqldev-in-database-r-for-sql-developers.md)您所建立。

在本快速入門中，您將了解重要的概念，透過執行"Hello World"R 指令碼 inT SQL，簡介**sp_execute_external_script**系統預存程序。 

## <a name="prerequisites"></a>先決條件

這個練習需要存取 SQL server 執行個體與其中一個已安裝下列項目：

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，與安裝的 R 語言
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

  您的 SQL Server 執行個體可位於 Azure 虛擬機器或內部部署。 要小心，外部指令碼功能預設為停用，因此您可能需要[啟用外部指令碼](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並確認**SQL Server Launchpad 服務**開始之前執行。

+ 執行 SQL 查詢工具。 您可以使用任何應用程式可以連接到 SQL Server 資料庫並執行 T-SQL 程式碼。 SQL 專業人員可以使用 SQL Server Management Studio (SSMS) 或 Visual Studio。

本快速入門中，以顯示 執行 R 在 SQL Server 內是多麼我們使用新**適用於 Visual Studio Code 的 mssql 擴充功能**。 VS Code 是免費的開發環境可在 Linux、 macOS 或 Windows 上執行。 **Mssql**延伸模組是執行 T-SQL 查詢的輕量級擴充功能。 若要取得 Visual Studio Code，請參閱[下載並安裝 Visual Studio Code (英文)](https://code.visualstudio.com/Download)。 若要新增**mssql**延伸模組，請參閱這篇文章：[使用 Visual Studio Code 的 mssql 擴充功能](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>連線到資料庫並執行 Hello World 測試指令碼

1. 在 Visual Studio Code 中，建立新的文字檔案並將它命名為 BasicRSQL.sql。

2. 開啟此檔案時，請按 CTRL+SHIFT+P (macOS 上為 COMMAND + P)，輸入 **sql** 以列出 SQL 命令，並選取 [連線]。 Visual Studio Code 會提示您建立設定檔，連接到特定的資料庫時使用。 這是選擇性的但可讓您更輕鬆地切換資料庫和登入。
    + 選擇伺服器或已安裝 SQL Server 中的 R 的執行個體。
    + 使用具有建立新資料庫權限的帳戶執行 SELECT 陳述式，並檢視資料表定義。

2. 如果連線成功，您應該能在狀態列中看到伺服器和資料庫名稱，以及您目前的認證。 如果連線失敗，請檢查電腦名稱和伺服器名稱是否正確。

3. 貼上此陳述式並加以執行。

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([Hello World] int));
    GO
    ```

這個預存程序的輸入包括：

+ *@language* 參數會定義要呼叫，在此情況下，r 語言擴充功能
+ *@script* 參數會定義傳遞至 R 執行階段的命令。 您的整個 R 指令碼必須以 Unicode 文字的格式包含在此引數中。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ *@input_data_1* 會傳回查詢所傳遞至 R 執行階段，將資料傳回給 SQL Server 做為資料框架的資料。
+ 結果集子句會定義傳回的資料表的結構描述 SQL Server，將"Hello World"新增為資料行名稱，如**int**資料類型。

**結果**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

如果您收到任何錯誤，此查詢，排除任何安裝問題。 若要啟用外部程式碼程式庫需要後續安裝設定。 請參閱[安裝 SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)或是[安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。同樣地，請確定 Launchpad 服務正在執行。 

根據您的環境，您可能需要啟用 R 背景工作帳戶以連線到 SQL Server、安裝額外的網路程式庫、啟用遠端程式碼執行，或在一切已設定完畢後重新啟動執行個體。 如需詳細資訊，請參閱[R Services 安裝和升級常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!TIP]
> 在 Visual Studio Code 中，您可以將想要執行的程式碼醒目提示，並按下 CTRL+SHIFT+E。 如果這很難記住，您可以變更它！ 請參閱[自訂快速鍵繫結 (英文)](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。
> 
> ![rsql basictut_hello1code](media/rsql-basictut-hello1code.PNG)
> 

## <a name="next-steps"></a>後續步驟

現在您確認您的執行個體已準備好使用 R 時，看看建構輸入和輸出。

> [!div class="nextstepaction"]
> [快速入門： 處理輸入和輸出](rtsql-working-with-inputs-and-outputs.md)
