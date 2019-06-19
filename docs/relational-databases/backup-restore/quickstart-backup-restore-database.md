---
title: 快速入門：備份與還原內部部署的 SQL Server 資料庫
titleSuffix: SQL Server
description: 本快速入門示範如何在您選擇的雲端中的 Linux 上執行 SQL Server。
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.date: 05/25/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: backup-restore
ms.prod_service: backup-restore
ms.assetid: ''
ms.openlocfilehash: 8453d74227e1007a42adfbd8ac1f91bf1a6d86da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499667"
---
# <a name="quickstart-backup-and-restore-a-sql-server-database-on-premises"></a>快速入門：備份與還原內部部署的 SQL Server 資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中，您將建立新的資料庫、進行簡單備份，然後將它還原。 

如需更詳細的操作說明，請參閱[建立完整資料庫備份](create-a-full-database-backup-sql-server.md)和[使用 SSMS 還原備份](restore-a-database-backup-using-ssms.md)。

## <a name="prerequisites"></a>Prerequisites
若要完成本快速入門，您需要下列項目： 

- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)

## <a name="create-a-test-database"></a>建立測試資料庫 

1. 啟動 [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) 並連線至 SQL Server 執行個體。
1. 開啟 [新增查詢]  視窗。 
1. 執行下列 Transact-SQL (T-SQL) 程式碼以建立測試資料庫。 重新整理 [物件總管]  中的 [資料庫]  節點以查看新的資料庫。 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
 
## <a name="take-a-backup"></a>進行備份
若要備份資料庫，請執行下列作業： 

1. 啟動 [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) 並連線至 SQL Server 執行個體。
1. 在 [物件總管]  中，展開 [資料庫]  節點。  
1. 以滑鼠右鍵按一下資料庫、將滑鼠游標暫留在[工作]  上，然後選取 [備份]  。 
1. 在 [目的地]  下方，確認您的備份路徑正確。 如果您需要變更此路徑，請選取 [移除]  以移除現有路徑，然後選取 [新增]  以輸入新的路徑。 您可以使用省略符號來瀏覽至特定檔案。 
1. 選取 [確定]  ，即會備份您的資料庫。 

![進行 SQL 備份](media/quickstart-backup-restore-database/backup-db-ssms.png)

或者，您可以執行下列 Transact-SQL 命令來備份資料庫： 

```sql
BACKUP DATABASE [SQLTestDB] 
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' 
WITH NOFORMAT, NOINIT,  
NAME = N'SQLTestDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO
```


## <a name="restore-a-backup"></a>還原備份
若要還原資料庫，請執行下列作業： 

1. 啟動 [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) 並連線至 SQL Server 執行個體。
1. 以滑鼠右鍵按一下 [物件總管]  中的 [資料庫]  節點，然後選取 [還原資料庫]  。

    ![還原資料庫](media/quickstart-backup-restore-database/restore-db-ssms1.png)

1. 選取 [裝置:]  ，然後選取省略符號 (...) 以找出您的備份檔案。 
1. 選取 [新增]  ，然後瀏覽至您的 `.bak` 檔案所在位置。 選取 `.bak` 檔案，然後選取 [確定]  。 
1. 選取 [確定]  以關閉 [選取備份裝置]  對話方塊。 
1. 選取 [確定]  ，即會還原您的資料庫備份。 

    ![還原資料庫](media/quickstart-backup-restore-database/restore-db-ssms2.png)

或者，您可以執行下列 Transact-SQL 命令來還原資料庫：

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] 
FROM DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO
```

### <a name="clean-up-resources"></a>清除資源
執行下列 Transact-SQL 命令來移除您建立的資料庫，以及其在 MSDB 資料庫中的備份記錄：

```sql
EXEC msdb.dbo.sp_delete_database_backuphistory @database_name = N'SQLTestDB'
GO

USE [master]
DROP DATABASE [SQLTestDB]
GO
```

## <a name="see-more"></a>查看更多
[備份與還原概觀](back-up-and-restore-of-sql-server-databases.md)
[備份至 URL](sql-server-backup-to-url.md)
[建立完整備份](create-a-full-database-backup-sql-server.md)
[還原資料庫備份](restore-a-database-backup-using-ssms.md)
