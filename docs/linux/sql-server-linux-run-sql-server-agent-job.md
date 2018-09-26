---
title: 建立並在 Linux 上的 SQL Server 執行作業 |Microsoft Docs
description: 本教學課程會示範如何在 Linux 上執行 SQL Server Agent 作業。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 6e91385974730facf657d28febe94c4320cf3799
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713260"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>建立和執行在 Linux 上的 SQL Server Agent 作業

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 作業用來定期執行您的 SQL Server 資料庫中的 相同的命令順序。 本教學課程提供如何在 Linux 上建立 SQL Server Agent 作業的範例使用 TRANSACT-SQL 和 SQL Server Management Studio (SSMS)。

> [!div class="checklist"]
> * 在 Linux 上安裝 SQL Server 代理程式
> * 建立新的作業來執行每日資料庫備份
> * 排程及執行工作
> * 在 SSMS （選擇性） 中執行相同的步驟

如需與 Linux 上的 SQL Server Agent 的已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>先決條件

若要完成本教學課程需要下列必要條件：

* Linux 機器會有下列先決條件：
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 的命令列工具。

下列必要條件為選擇性項目：

* 使用 SSMS 的 Windows 電腦：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)的 SSMS 的選擇性步驟。

## <a name="enable-sql-server-agent"></a>啟用 SQL Server Agent

若要在 Linux 上使用 SQL Server 代理程式，您必須先啟用 SQL Server 代理程式已安裝 SQL Server 的電腦上。

1. 若要啟用 SQL Server Agent，請遵循下列步驟。
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. 使用下列命令，重新啟動 SQL Server:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> 從 SQL Server 2017 CU4 開始，SQL Server Agent 是隨附**mssql server**封裝，並預設為停用。 代理程式設定之前 CU4 造訪[在 Linux 上安裝 SQL Server Agent](sql-server-linux-setup-sql-agent.md)。

## <a name="create-a-sample-database"></a>建立範例資料庫

使用下列步驟來建立名為的範例資料庫**SampleDB**。 每日備份作業會使用此資料庫。

1. 在您的 Linux 機器上開啟 bash 終端機工作階段。

1. 使用**sqlcmd**執行 Transact SQL **CREATE DATABASE**命令。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. 請確認所列出的資料庫伺服器上建立資料庫。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>使用 TRANSACT-SQL 建立工作

下列步驟會建立在 Linux 上的 SQL Server Agent 作業，使用 TRANSACT-SQL 命令。 在作業執行每日備份的範例資料庫**SampleDB**。

> [!TIP]
> 您可以使用 T-SQL 中的任何用戶端來執行下列命令。 例如，在 Linux 上您可以使用[sqlcmd](sql-server-linux-setup-tools.md)或是[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 從遠端 Windows 伺服器，您也可以在 SQL Server Management Studio (SSMS) 執行查詢，或使用 UI 介面進行工作管理下, 一節中所述。

1. 使用[sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)來建立名為作業`Daily SampleDB Backup`。

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. 呼叫[sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)若要建立一個作業步驟，建立一份`SampleDB`資料庫。

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. 然後建立工作的每日排程[sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)。

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. 將作業排程附加至作業[sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)。

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. 使用[sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)若要將作業指派至目標伺服器。 在此範例中，目標是在本機伺服器。

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. 啟動的工作[sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)。

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>使用 SSMS 建立作業

您也可以建立，並從遠端使用 Windows 中的 SQL Server Management Studio (SSMS) 來管理工作。

1. 在 Windows 上啟動 SSMS 並連線到您的 Linux SQL Server 執行個體。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上使用 SSMS 管理 SQL Server](sql-server-linux-manage-ssms.md)。

1. 請確認您已建立名為的範例資料庫**SampleDB**。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. 確認 SQL 代理程式已[安裝](sql-server-linux-setup-sql-agent.md)並正確設定。 在 [物件總管] 中的 SQL Server Agent 旁邊的加號的外觀。 如果未啟用 SQL Server Agent，請嘗試重新啟動**mssql server** Linux 上的服務。

   ![確認已安裝 SQL Server Agent](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 建立新的工作。

   ![建立新的工作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. 提供您的作業名稱，然後建立您的作業步驟。

   ![建立作業步驟](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 指定您想要使用哪一種子，以及應該執行的作業步驟。

   ![作業子系統](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![作業步驟的動作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 建立新的作業排程。

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. 啟動您的作業。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Linux 上安裝 SQL Server 代理程式
> * 使用 TRANSACT-SQL 和系統預存程序建立作業
> * 建立會執行每日資料庫備份作業
> * 使用 SSMS UI 來建立及管理作業

接下來，探索其他功能，來建立和管理工作：

> [!div class="nextstepaction"]
>[SQL Server 代理程式的文件](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
