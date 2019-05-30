---
title: 使用 Visual Studio Code 的 mssql 擴充功能適用於 SQL Server
titleSuffix: SQL Server
description: 編輯和執行適用於 SQL Server 的 TRANSACT-SQL 指令碼，在 Linux 上使用 Visual Studio Code 的 mssql 擴充功能。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: 3643e66e190ec1b45961f36af471498a56924cb0
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265381"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>使用 Visual Studio Code 來建立和執行 TRANSACT-SQL 指令碼

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章示範如何使用**mssql**開發 SQL Server 資料庫的 Visual Studio Code 的延伸模組。 由於 Visual Studio Code 跨平台，您可以使用**mssql** Linux、 macOS 和 Windows 上的擴充功能。

## <a name="install-and-start-visual-studio-code"></a>安裝並啟動 Visual Studio Code

Visual Studio Code 是跨平台、 圖形化程式碼編輯器支援擴充功能。

1. [下載並安裝 Visual Studio Code](https://code.visualstudio.com/)您的電腦上。

1. 啟動 Visual Studio Code。

   >[!NOTE]
   >如果當您連接到 xrdp 遠端桌面工作階段，不會啟動 Visual Studio Code，請參閱[無法運作時使用 XRDP 連線在 Ubuntu 上的 VS Code](https://github.com/Microsoft/vscode/issues/3451)。

## <a name="install-the-mssql-extension"></a>安裝 mssql 擴充功能

[適用於 Visual Studio Code 的 mssql 擴充功能](https://aka.ms/mssql-marketplace)可讓您連接到 SQL Server 中，使用 TRANSACT-SQL (T-SQL)，查詢和檢視結果。

1. 在 Visual Studio Code 中，選取**檢視** > **命令選擇區**，或按**Ctrl**+**Shift** +**P**，或按**F1**以開啟**命令選擇區**。

1. 在 **命令調色盤**，選取**延伸模組：安裝擴充功能**從下拉式清單。 

1. 在 **延伸模組**窗格中，輸入*mssql*。

1. 選取  **SQL Server (mssql)** 延伸模組，然後選取**安裝**。

   ![安裝 mssql 擴充功能](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)

1. 安裝完成之後，請選取**重新載入**啟用該擴充功能。

## <a name="create-or-open-a-sql-file"></a>建立或開啟 SQL 檔案

Mssql 擴充功能可讓 mssql 命令和 T-SQL IntelliSense 程式碼編輯器中將語言模式設定為當**SQL**。

1. 選取 **檔案** > **新檔案**或按**Ctrl**+**N**。 Visual Studio 程式碼預設會開啟新的純文字檔案。 

1. 選取**純文字**下方的 [狀態] 列，或按下**Ctrl**+**K** > **M**，然後選取**SQL**從語言下拉式清單。 

   ![SQL 語言模式](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > 如果這是您已使用延伸模組的第一次，安裝支援的 SQL Server 工具擴充功能。

如果您開啟現有的檔案具有 *.sql*檔案延伸模組，將語言模式會自動設為 SQL。  

## <a name="connect-to-sql-server"></a>連接至 SQL Server

請遵循下列步驟來建立連線設定檔，並連接到 SQL Server。

1. 按下**Ctrl**+**Shift**+**P**或**F1**以開啟**命令選擇區**. 

1. 型別*sql*顯示 mssql 命令或型別*sqlcon*，然後選取  **MS SQL:連接**從下拉式清單。

   ![mssql 命令](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >SQL 檔案，例如空白的 SQL 檔案建立時，必須具有焦點在程式碼編輯器才能執行 mssql 命令。

1. 選取**MS SQL:管理連線設定檔**命令。

1. 然後選取**建立**為您的 SQL Server 中建立新的連線設定檔。

1. 遵循提示來指定新的連線設定檔的屬性。 指定每個值之後, 按下**Enter**以繼續。

   | 連線屬性 | 描述 |
   |---|---|
   | **伺服器名稱或 ADO 連接字串** | 指定 SQL Server 執行個體名稱。 使用*localhost*連接到本機電腦上的 SQL Server 執行個體。 若要連接到遠端的 SQL Server，請輸入目標 SQL Server 的名稱或 IP 位址。 若要連接到 SQL Server 容器，指定容器的主機電腦的 IP 位址。 如果您需要指定連接埠，請使用逗號來分隔的名稱。 例如，在連接埠 1401年上接聽的伺服器，請輸入`<servername or IP>,1401`。<br/><br/>或者，您可以輸入 ADO 連接字串，為您的資料庫。 |
   | **資料庫名稱**（選擇性） | 您想要使用的資料庫。 若要連接的預設資料庫，請勿指定資料庫名稱。 |
   | **驗證類型** | 選擇 **整合式**或是**SQL 登入**。 |
   | **使用者名稱** | 如果您選取**SQL 登入**，輸入資料庫伺服器上具有存取權的使用者名稱。 |
   | **密碼** | 請輸入指定之使用者的密碼。 |
   | **儲存密碼** | 按下**Enter**來選取**是**並儲存密碼。 選取  **No**每次連線設定檔時，密碼的提示時。 |
   | **設定檔名稱**（選擇性） | 輸入連線設定檔的名稱，例如*本機主機設定檔*。 |

   您輸入所有值，並選取之後**都 Enter**，Visual Studio Code 建立連線設定檔，並連接到 SQL Server。

   > [!TIP]
   > 如果連線失敗，請試著診斷問題中的錯誤訊息從**輸出**Visual Studio Code 中的面板。 若要開啟 **輸出**面板中，選取**檢視** > **輸出**。 也檢閱[連線疑難排解建議](./sql-server-linux-troubleshooting-guide.md#connection)。

1. 請確認您在下方的 [狀態] 列中的連線。

   ![連線狀態](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)

替代方案的上一個步驟中，您也可以建立及編輯使用者設定檔中的連線設定檔 (*settings.json*)。 若要開啟 設定檔，請選取**檔案** > **喜好設定** > **設定**。 如需詳細資訊，請參閱 [管理連線設定檔](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles)。

## <a name="create-a-sql-database"></a>建立 SQL database

1. 在 新的 SQL 檔案您稍早開始，鍵入*sql*顯示可編輯的程式碼片段的清單。 

   ![SQL 程式碼片段](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)

1. 選取  **sqlCreateDatabase**。

1. 在片段中，輸入`TutorialDB`取代 'DatabaseName':

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

1. 按下**Ctrl**+**Shift**+**E**執行 TRANSACT-SQL 命令。 在查詢視窗中檢視結果。

   ![建立資料庫訊息](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)

   > [!TIP]
   > 您可以自訂用於 mssql 命令的快速鍵。 請參閱[自訂快速鍵](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。

## <a name="create-a-table"></a>建立資料表

1. 刪除程式碼編輯器視窗的內容。

1. 按下**Ctrl**+**Shift**+**P**或**F1**以開啟**命令選擇區**. 

1. 型別*sql*顯示 mssql 命令或型別*sqluse*，然後選取  **MS SQL:使用資料庫**命令。

1. 選取新**TutorialDB**資料庫。 

   ![使用資料庫](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)

1. 在程式碼編輯器中，輸入*sql*若要顯示的程式碼片段，請選取**sqlCreateTable**，然後按**Enter**。

1. 在片段中，輸入`Employees`資料表名稱。

1. 按下 **索引標籤**若要取得下一個欄位，然後輸入`dbo`結構描述名稱。

1. 取代下列資料行的資料行定義：

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

1. 按下**Ctrl**+**Shift**+**E**來建立資料表。

## <a name="insert-and-query"></a>插入和查詢

1. 加入下列陳述式以新增四個資料列至 **Employees** 資料表。

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```

   雖然您輸入時，T-SQL IntelliSense 可協助您完成陳述式：

   ![T-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > Mssql 擴充功能也會有幫助您建立 INSERT 和 SELECT 陳述式的命令。 這些不是在上述範例中使用。

1. 按下**Ctrl**+**Shift**+**E**以執行命令。 這兩個結果集顯示在**結果**視窗。 

   ![結果](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>檢視及儲存結果

1. 選取 **檢視** > **編輯器配置** > **翻轉配置**切換至垂直或水平分割配置。

1. 選取 **結果**並**訊息**面板摺疊和展開面板的標頭。

   ![切換標頭](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > 您可以自訂 mssql 擴充功能的預設行為。 請參閱[自訂延伸模組選項](https://github.com/Microsoft/vscode-mssql/wiki/customize-options)。

1. 選取 [最大化格線] 圖示，在第二個結果方格來縮放這些結果。

   ![最大化方格](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > 您的 T-SQL 指令碼會產生兩個或多個結果方格時，會顯示 [最大化] 圖示。

1. 以滑鼠右鍵按一下方格中開啟方格內容功能表。 

   ![操作功能表](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)

1. 選取 **選取所有**。

1. 再次開啟格線操作功能表，然後選取**將儲存為 JSON**儲存至結果 *.json*檔案。

1. 指定 JSON 檔案的檔案名稱。 

1. 請確認儲存 JSON 檔案，並會在 Visual Studio Code 中開啟。

   ![將儲存為 JSON](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)

如果您需要儲存及更新版本中，系統管理或較大的開發專案中，執行 SQL 指令碼儲存與指令碼 *.sql*延伸模組。

## <a name="next-steps"></a>後續步驟

如果您還不熟悉 T-SQL，請參閱[教學課程：撰寫 TRANSACT-SQL 陳述式](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)而[TRANSACT-SQL 參考 (Database Engine)](https://docs.microsoft.com/sql/t-sql/language-reference)。

如需有關使用或促成 mssql 擴充功能的詳細資訊，請參閱 < [mssql 擴充功能專案 wiki](https://github.com/Microsoft/vscode-mssql/wiki)。

如需有關如何使用 Visual Studio Code 的詳細資訊，請參閱 < [Visual Studio Code 文件](https://code.visualstudio.com/docs)。