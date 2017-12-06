---
title: "建立和執行 SQL Server on Linux 作業 |Microsoft 文件"
description: "本教學課程會示範如何在 Linux 上執行 SQL Server Agent 作業。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.workload: Inactive
ms.openlocfilehash: fe2705d9d1bfefd9953ff03da123621dd4ef95f3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>建立和執行在 Linux 上的 SQL Server Agent 作業

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server 工作可用來定期執行的命令相同的順序，SQL Server 資料庫中。 本教學課程提供如何在 Linux 上建立 SQL Server Agent 作業的範例使用 TRANSACT-SQL 和 SQL Server Management Studio (SSMS)。

> [!div class="checklist"]
> * Linux 上安裝 SQL Server 代理程式
> * 建立新的作業來執行每日資料庫備份
> * 排程及執行工作
> * （選擇性） SSMS 中執行相同的步驟

如需與 SQL Server Agent，在 Linux 上的已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>必要條件

若要完成本教學課程中，需要下列必要條件：

* Linux 機器會有下列先決條件：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 與命令列工具。

下列必要條件為選擇性：

* 使用 SSMS 的 Windows 電腦：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)選擇性 SSMS 步驟。

## <a name="install-sql-server-agent"></a>安裝 SQL Server 代理程式

若要在 Linux 上使用 SQL Server 代理程式，您必須先安裝**mssql server agent**已安裝的 SQL Server 2017 機器上的封裝。

1. 安裝**mssql server agent**與 Linux 作業系統的適當命令。

   | 平台 | 安裝命令 |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. 使用下列命令，重新啟動 SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="create-a-sample-database"></a>建立範例資料庫

使用下列步驟來建立範例資料庫名為**SampleDB**。 此資料庫用於每日備份工作。

1. 在您的 Linux 電腦上開啟 bash 終端機工作階段。

1. 使用**sqlcmd**執行 Transact SQL **CREATE DATABASE**命令。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. 請確認所列出的資料庫伺服器上建立資料庫。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>使用 TRANSACT-SQL 建立工作

下列步驟會建立 TRANSACT-SQL 命令與 Linux 上的 SQL Server Agent 作業。 在作業執行的範例資料庫中，每日備份**SampleDB**。

> [!TIP]
> 您可以使用任何 T-SQL 的用戶端來執行下列命令。 例如，在 Linux 上您可以使用[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 從遠端 Windows 伺服器，您也可以在 SQL Server Management Studio (SSMS) 執行查詢或使用 UI 介面進行作業管理下, 一節中所述。

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

1. 呼叫[sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)建立作業步驟所建立的備份`SampleDB`資料庫。

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

1. 然後建立與您工作的每日排程[sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)。

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

1. 將作業排程附加至作業的[sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)。

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. 使用[sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)將作業指派至目標伺服器。 在此範例中，目標是本機伺服器。

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. 開始使用工作[sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)。

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>使用 SSMS 建立作業

您也可以建立及管理在 Windows 上使用遠端 SQL Server Management Studio (SSMS) 的工作。

1. 在 Windows 上啟動 SSMS 並連接至您的 Linux SQL Server 執行個體。 如需詳細資訊，請參閱[管理 SQL Server on Linux 使用 SSMS](sql-server-linux-develop-use-ssms.md)。

1. 請確認您已建立名為的範例資料庫**SampleDB**。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. 確認 SQL 代理程式已[安裝](sql-server-linux-setup-sql-agent.md)且已正確設定。 尋找在 [物件總管] 中的 SQL Server Agent 旁邊的加號。 如果未啟用 SQL Server 代理程式，請嘗試重新啟動**mssql 伺服器**Linux 上的服務。

   ![確認已安裝 SQL Server 代理程式](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 建立新的工作。

   ![建立新的工作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. 提供您的工作名稱，然後建立作業步驟。

   ![建立作業步驟](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 指定您想要使用何種子系統，應該執行的作業步驟。

   ![作業子系統](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![作業步驟的動作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 建立新的作業排程。

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. 啟動您的工作。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>後續步驟

在此教學課程中，您學會如何：

> [!div class="checklist"]
> * Linux 上安裝 SQL Server 代理程式
> * 使用 TRANSACT-SQL 及系統預存程序來建立作業
> * 建立工作執行每日資料庫備份
> * 使用 SSMS UI 來建立和管理工作

接下來，瀏覽其他功能來建立和管理工作：

> [!div class="nextstepaction"]
>[SQL Server 代理程式的文件](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
