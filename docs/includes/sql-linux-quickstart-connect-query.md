## <a name="connect-locally"></a>在本機連線

下列步驟使用 **sqlcmd**，在本機連線到您的新 SQL Server 執行個體。

1. 執行 **sqlcmd**，並提供您的 SQL Server 名稱 (-S)、使用者名稱 (-U) 和密碼 (-P) 的參數。 在本教學課程中，您將在本機連線，因此伺服器名稱是 `localhost`。 使用者名稱是 `SA`，而密碼則是您在安裝期間為 SA 帳戶所提供的密碼。

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > 您可以在命令列中省略密碼，不要在提示時輸入密碼。

   > [!TIP]
   > 如果您稍後決定從遠端連線，請針對 **-S** 參數指定電腦名稱或 IP 位址，並確定已開啟您防火牆上的連接埠 1433。

1. 如果成功，您應該會收到 **sqlcmd** 命令提示字元：`1>`。

1. 如果您收到連線失敗，請先嘗試從錯誤訊息診斷問題。 然後檢閱[連線疑難排解建議](../linux/sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="create-and-query-data"></a>建立及查詢資料
下列各節將逐步引導您使用 **sqlcmd** 和 Transact-SQL，來建立新的資料庫、新增資料及執行簡單的查詢。

### <a name="create-a-new-database"></a>建立新的資料庫

下列步驟會建立名為 `TestDB` 的新資料庫。

1. 從 **sqlcmd** 命令提示字元，貼上下列 Transact-SQL 命令以建立測試資料庫：

   ```sql
   CREATE DATABASE TestDB
   ```

1. 在下一行，撰寫查詢以傳回您伺服器上所有資料庫的名稱：

   ```sql
   SELECT Name from sys.Databases
   ```

1. 上述兩個命令不會立即執行。 您必須在新的一行鍵入 `GO`，以執行上述命令：

   ```sql
   GO
   ```

### <a name="insert-data"></a>插入資料

接下來，建立新的資料表 `Inventory`，然後插入兩個新的資料列。

1. 從 **sqlcmd** 命令提示字元，將內容切換至 `TestDB` 資料庫：

   ```sql
   USE TestDB
   ```

1. 建立名為 `Inventory` 的新資料表：

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 將資料插入新的資料表：

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. 鍵入 `GO` 以執行上述命令：

   ```sql
   GO
   ```

### <a name="select-data"></a>選取資料

現在，執行查詢以從 `Inventory` 資料表傳回資料。

1. 從 **sqlcmd** 命令提示字元，輸入查詢以從數量大於 152 的 `Inventory` 資料表傳回資料列：

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 執行命令：

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>結束 sqlcmd 命令提示字元

若要結束您的 **sqlcmd** 工作階段，請鍵入 `QUIT`：

```sql
QUIT
```

## <a name="connect-from-windows"></a>從 Windows 連線

請務必注意，Windows 上的 SQL Server 工具連線到 Linux 上的 SQL Server 執行個體的方式，與連線到任何遠端 SQL Server 執行個體的方式相同。

如果您有可連線到 Linux 電腦的 Windows 電腦，請嘗試本主題中的相同步驟，從 Windows 命令提示字元執行 **sqlcmd**。 請確認您使用目標 Linux 電腦名稱或 IP 位址，而不是 localhost，並確定已開啟 TCP 連接埠 1433。 如果從 Windows 連線有任何問題，請參閱[連線疑難排解建議](../linux/sql-server-linux-troubleshooting-guide.md#connection)。

如需在 Windows 上執行但連線到 Linux 上 SQL Server 的其他工具，請參閱：

- [SQL Server Management Studio (SSMS)](../linux/sql-server-linux-develop-use-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SQL Server Data Tools (SSDT)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="next-steps"></a>後續步驟

如果您不熟悉 T-SQL，請參閱[教學課程：撰寫 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)和 [Transact-SQL 參考 (Database Engine)](../t-sql/language-reference.md)。

若要探索連線及管理 SQL Server 的其他方式，請參閱 [Visusal Studio Code](../linux/sql-server-linux-develop-use-vscode.md) 和 [SQL Server Management Studio](../linux/sql-server-linux-develop-use-ssms.md)。