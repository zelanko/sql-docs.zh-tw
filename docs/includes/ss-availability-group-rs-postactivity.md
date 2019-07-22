---
ms.openlocfilehash: bf755ccfe5a1a6816129173dcb6ad5050ea5e114
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213310"
---

## <a name="add-a-database-to-the-availability-group"></a>將資料庫新增至可用性群組

確定您要新增至可用性群組的資料庫處於完整復原模式，而且具有有效的記錄備份。 如果資料庫是測試資料庫或新建立的資料庫，請進行資料庫備份。 若要建立和備份稱為 `db1` 的資料庫，請在主要 SQL Server 執行個體上執行下列 Transact-SQL 指令碼：

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\db1.bak';
```

若要將稱為 `db1` 的資料庫新增至稱為 `ag1` 的可用性群組，請在 SQL Server 主要複本上執行下列 Transact-SQL 指令碼：

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>確認已在次要伺服器上建立資料庫

若要查看 `db1` 資料庫是否已建立且已同步處理，請在每個 SQL Server 次要複本上執行下列查詢：

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
