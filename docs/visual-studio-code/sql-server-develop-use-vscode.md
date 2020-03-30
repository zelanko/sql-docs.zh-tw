---
title: 使用 Visual Studio Code MSSQL 延伸模組
description: 使用適用於 Visual Studio Code 的 mssql 延伸模組，在 Linux 上編輯和執行適用於 SQL Server 的 Transact-SQL 指令碼。
ms.topic: conceptual
ms.prod: sql
ms.technology: tools-other
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
author: markingmyname
ms.author: maghan
ms.date: 10/28/2019
ms.openlocfilehash: 615e205566ced2c1d0a66ab69b3e9eb80c7f82f3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75558453"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>使用 Visual Studio Code 建立和執行 Transact-SQL 指令碼

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章說明如何使用適用於 Visual Studio Code 的 **mssql** 延伸模組來開發 SQL Server 資料庫。 由於 Visual Studio Code 是跨平台的，因此，您可以在 Linux、macOS 和 Windows 上使用 **mssql** 延伸模組。

## <a name="install-and-start-visual-studio-code"></a>安裝並啟動 Visual Studio Code

Visual Studio Code 是跨平台的圖形化程式碼編輯器，可支援延伸模組。

1. 在您的電腦上[下載並安裝 Visual Studio Code](https://code.visualstudio.com/) \(英文\)。

2. 啟動 Visual Studio Code。

    >[!NOTE]
    >如果您在透過 xrdp 遠端桌面工作階段連線時並未啟動 Visual Studio Code，請參閱[使用 XRDP 連線時，VS Code 未在 Ubuntu 上運作](https://github.com/Microsoft/vscode/issues/3451) \(英文\)。

## <a name="install-the-mssql-extension"></a>安裝 mssql 延伸模組

[適用於 Visual Studio Code 的 mssql 延伸模組](https://aka.ms/mssql-marketplace) \(英文\) 可讓您連線到 SQL Server、使用 Transact-SQL (T-SQL) 查詢並檢視結果。

1. 在 Visual Studio Code 中，選取 [檢視]   > [命令選擇區]  ，或按 **Ctrl**+**Shift**+**P** 鍵，或按 **F1** 鍵以開啟 [命令選擇區]  。

2. 在 [命令選擇區]  中，從下拉式清單中選取 [延伸模組:  安裝延伸模組]。

3. 在 [延伸模組]  窗格中，輸入 *mssql*。

4. 選取 [SQL Server (mssql)]  延伸模組，然後選取 [安裝]  。

   ![安裝 mssql 延伸模組](./media/sql-server-develop-use-vscode/vscode-extension.png)

5. 安裝完成之後，選取 [重新載入]  以啟用延伸模組。

## <a name="create-or-open-a-sql-file"></a>建立或開啟 SQL 檔案

將語言模式設定為 [SQL]  時，mssql 延伸模組會在程式碼編輯器中啟用 mssql 命令和 T-SQL IntelliSense。

1. 選取 [檔案]   > [新增檔案]  ，或按 **Ctrl**+**N** 鍵。 Visual Studio Code 預設會開啟新的純文字檔。 

2. 在下方狀態列上選取 [純文字]  ，或按 **Ctrl**+**K** > **M** 鍵，然後從語言下拉式清單中選取 [SQL]  。 

   ![SQL 語言模式](./media/sql-server-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > 如果這是您第一次使用此延伸模組，此延伸模組就會安裝支援 SQL Server 工具。

如果您開啟副檔名為 *.sql* 的現有檔案，語言模式會自動設定為 SQL。  

## <a name="connect-to-sql-server"></a>連接至 SQL Server

遵循下列步驟來建立連線設定檔，並連線到 SQL Server。

1. 按 **Ctrl**+**Shift**+**P** 或 **F1** 鍵以開啟 [命令選擇區]  。 

2. 輸入 *sql* 以顯示 mssql 命令，或輸入 *sqlcon*，然後從下拉式清單中選取 [MS SQL:  連線]。

   ![mssql 命令](./media/sql-server-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >SQL 檔案 (例如，您所建立的空 SQL 檔案) 在程式碼編輯器中必須有焦點，才能執行 mssql 命令。

3. 選取 [MS SQL:  管理連線設定檔] 命令。

4. 接著，選取 [建立]  ，為您的 SQL Server 建立新的連線設定檔。

5. 遵循提示來指定新連線設定檔的屬性。 指定每個值之後，按 **Enter** 鍵繼續。

   | 連線屬性 | 描述 |
   |---|---|
   | **伺服器名稱或 ADO 連接字串** | 指定 SQL Server 執行個體名稱。 使用 *localhost* 連線到本機電腦上的 SQL Server 執行個體。 若要連線到遠端 SQL Server，請輸入目標 SQL Server 的名稱或其 IP 位址。 若要連線到 SQL Server 容器，則指定容器主機電腦的 IP 位址。 如果您需要指定連接埠，可使用逗號來將它與名稱隔開。 例如，針對接聽連接埠 1401 的伺服器，輸入 `<servername or IP>,1401`。<br/><br/>或者，您也可以在這裡輸入資料庫的 ADO 連接字串。 |
   | **資料庫名稱** (選擇性) | 您要使用的資料庫。 若要連線到預設資料庫，請不要在這裡指定資料庫名稱。 |
   | **驗證類型** | 選擇 [整合式]  或 [SQL 登入]  。 |
   | **使用者名稱** | 如果您選取 [SQL 登入]  ，請輸入有權存取伺服器上之資料庫的使用者名稱。 |
   | **密碼** | 請輸入指定之使用者的密碼。 |
   | **儲存密碼** | 按 **Enter** 鍵以選取 [是]  並儲存密碼。 每次使用連線設定檔時，當系統提示您輸入密碼時選取 [否]  。 |
   | **設定檔名稱** (選擇性) | 輸入連線設定檔的名稱，例如 *localhost profile*。 |

   輸入所有值並選取 **Enter** 鍵之後，Visual Studio Code 會建立連線設定檔並連線到 SQL Server。

   > [!TIP]
   > 如果連線失敗，則嘗試在 Visual Studio Code 的 [輸出]  面板中，從錯誤訊息中診斷問題。 若要開啟 [輸出]  面板，請選取 [檢視]   > [輸出]  。 另請檢閱[連線疑難排解建議](../linux/sql-server-linux-troubleshooting-guide.md)。

6. 在下方狀態列中確認您的連線。

   ![連線狀態](./media/sql-server-develop-use-vscode/vscode-connection-status.png)

作為先前步驟的替代項，您也可以在「使用者設定」檔案 (*settings.json*) 中建立和編輯連線設定檔。 若要開啟設定檔案，請選取 [檔案]   > [喜好設定]   > [設定]  。 如需詳細資訊，請參閱[管理連線設定檔](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles) \(英文\)。

## <a name="create-a-sql-database"></a>建立 SQL 資料庫

1. 在您稍早開啟的新 SQL 檔案中，輸入 *sql* 以顯示可編輯的程式碼片段清單。

   ![SQL 程式碼片段](./media/sql-server-develop-use-vscode/vscode-sql-snippets.png)

2. 選取 [sqlCreateDatabase]  。

3. 在程式碼片段中，輸入 `TutorialDB` 來取代 'DatabaseName'：

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

4. 按 **Ctrl**+**Shift**+**E** 鍵來執行 Transact-SQL 命令。 在查詢視窗中檢視結果。

    ![建立資料庫訊息](./media/sql-server-develop-use-vscode/vscode-create-database-messages.png)

    > [!TIP]
    > 您可以自訂 mssql 命令的快速鍵。 請參閱[自訂快速鍵](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts) \(英文\)。

## <a name="create-a-table"></a>建立資料表

1. 刪除 [程式碼編輯器] 視窗的內容。

2. 按 **Ctrl**+**Shift**+**P** 或 **F1** 鍵以開啟 [命令選擇區]  。

3. 輸入 *sql* 以顯示 mssql 命令，或者輸入 *sqluse*，然後選取 [MS SQL:  使用資料庫] 命令。

4. 選取新的 **TutorialDB** 資料庫。

   ![使用資料庫](./media/sql-server-develop-use-vscode/vscode-use-database.png)

5. 在程式碼編輯器中，輸入 *sql* 以顯示程式碼片段、選取 [sqlCreateTable]  ，然後按 **Enter** 鍵。

6. 在程式碼片段中，針對資料表名稱輸入 `Employees`。

7. 按 **Tab** 鍵移至下一個欄位，接著輸入 `dbo` 作為架構名稱。

8. 使用下列資料行來取代資料行定義：

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

9. 按 **Ctrl**+**Shift**+**E** 鍵來建立資料表。

## <a name="insert-and-query"></a>插入和查詢

1. 新增下列陳述式，將四個資料列插入至 **Employees** 資料表。

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

   當您輸入時，T-SQL IntelliSense 可協助您完成陳述式：

   ![T-SQL IntelliSense](./media/sql-server-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > Mssql 延伸模組也有可協助建立 INSERT 和 SELECT 陳述式的命令。 上述範例中並未用到這些命令。

2. 按 **Ctrl**+**Shift**+**E** 鍵來執行命令。 這兩個結果集會顯示於 [結果]  視窗中。

   ![結果](./media/sql-server-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>檢視並儲存結果

1. 選取 [檢視]   > [編輯器配置]   > [翻轉配置]  ，以切換為垂直或水平分割配置。

2. 選取 [結果]  和 [訊息]  面板標題，以摺疊和展開面板。

   ![切換標題](./media/sql-server-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > 您可以自訂 mssql 延伸模組的預設行為。 請參閱[自訂延伸模組選項](https://github.com/Microsoft/vscode-mssql/wiki/customize-options) \(英文\)。

3. 選取第二個結果方格上的 [將方格最大化] 圖示，以放大這些結果。

   ![將方格最大化](./media/sql-server-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > 當您的 T-SQL 指令碼產生兩個或多個結果方格時，即會顯示最大化圖示。

4. 在方格上按一下滑鼠右鍵，以開啟方格捷徑功能表。

   ![捷徑功能表](./media/sql-server-develop-use-vscode/vscode-grid-context-menu.png)

5. 選取 [全選]  。

6. 再次開啟 [方格] 捷徑功能表，然後選取 [另存為 JSON]  ，以將結果儲存為 *.json* 檔案。

7. 指定 JSON 檔案的檔案名稱。

8. 確認 JSON 檔案會在 Visual Studio Code 中儲存並開啟。

   ![另存為 JSON](./media/sql-server-develop-use-vscode/vscode-save-as-json.png)

如果您稍後需要儲存並執行 SQL 指令碼以用於管理或較大的開發專案，請使用 *.sql* 副檔名來儲存指令碼。

## <a name="next-steps"></a>後續步驟

如果您不熟悉 T-SQL，請參閱[教學課程：撰寫 Transact-SQL 陳述式](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)和 [Transact-SQL 參考 (資料庫引擎)](https://docs.microsoft.com/sql/t-sql/language-reference)。

如需使用或參與 mssql 延伸模組的詳細資訊，請參閱 [mssql 延伸模組專案 wiki](https://github.com/Microsoft/vscode-mssql/wiki) \(英文\)。

如需使用 Visual Studio Code 的詳細資訊，請參閱 [Visual Studio Code 文件](https://code.visualstudio.com/docs) \(英文\)。