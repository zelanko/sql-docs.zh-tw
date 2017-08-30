
## <a name="add-a-database-to-the-availability-group"></a>將資料庫新增至可用性群組

確定您要新增至可用性群組的資料庫處於完整復原模式，而且具有有效的記錄備份。 如果這是測試資料庫或建立的新資料庫，請進行資料庫備份。 在主要 SQL Server 上，執行下列 Transact-SQL 來建立和備份名為 `db1` 的資料庫。

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

在主要 SQL Server 複本上，執行下列 Transact-SQL 將名為 `db1` 的資料庫新增 `ag1` 可用性群組。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>確認已在次要伺服器上建立資料庫

在每個次要 SQL Server 複本上，執行下列查詢來查看 `db1` 資料庫是否已建立且已同步處理。

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
