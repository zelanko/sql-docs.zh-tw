
## <a name="add-a-database-to-the-availability-group"></a>將資料庫加入可用性群組

確定您要加入至可用性群組的資料庫處於完整復原模式，而且具有有效的記錄備份。 如果這是測試資料庫或建立新的資料庫，進行資料庫備份。 在主要 SQL 伺服器上，執行下列 TRANSACT-SQL 來建立和備份資料庫呼叫`db1`。

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

主要 SQL Server 在複本上，執行下列 TRANSACT-SQL 加入資料庫呼叫`db1`至可用性群組稱為`ag1`。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>確認已在次要伺服器上建立資料庫

每個次要 SQL Server 在複本上，執行下列查詢，以查看是否`db1`資料庫已建立，而且已同步處理。

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
