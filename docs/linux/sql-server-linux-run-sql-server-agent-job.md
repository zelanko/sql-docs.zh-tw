---
title: 建立及執行適用於 Linux 上的 SQL Server 的作業
description: 本教學課程會示範如何在 Linux 上執行 SQL Server Agent 作業。
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 5abd2db590a89350f45497d7f94b81940a0ec5bc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68065147"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>在 Linux 上建立及執行 SQL Server Agent 作業

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 作業被用來在 SQL Server 資料庫中定期執行相同的命令序列。 本教學課程會提供如何使用 Transact-SQL 和 SQL Server Management Studio (SSMS) 在 Linux 上建立 SQL Server Agent 作業的範例。

> [!div class="checklist"]
> * 在 Linux 上安裝 SQL Server Agent
> * 建立新作業以執行每日資料庫備份
> * 對作業進行排程並執行該作業
> * 在 SSMS 中執行相同的步驟 (選擇性)

如需 Linux 上 SQL Server Agent 的已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>Prerequisites

必須擁有下列先決條件，才能完成本教學課程：

* 具有下列先決條件的 Linux 電腦：
  * 具有命令列工具的 SQL Server ([RHEL](quickstart-install-connect-red-hat.md)、[SLES](quickstart-install-connect-suse.md) 或 [Ubuntu](quickstart-install-connect-ubuntu.md))。

下列先決條件為選擇性：

* 具有 SSMS 的 Windows 電腦：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 以進行選擇性的 SSMS 步驟。

## <a name="enable-sql-server-agent"></a>啟用 SQL Server Agent

若要在 Linux 上使用 SQL Server Agent，您必須先在已安裝 SQL Server 的電腦上啟用 SQL Server Agent。

1. 若要啟用 SQL Server Agent，請遵循下列步驟。
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. 使用下列命令來重新啟動 SQL Server：
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> 從 SQL Server 2017 CU4 開始，SQL Server Agent 已隨附於 **mssql-server** 套件，而且預設為停用。 如需使用 CU4 之前的版本來設定 Agent 的相關資訊，請參閱[在 Linux 上安裝 SQL Server Agent](sql-server-linux-setup-sql-agent.md)。

## <a name="create-a-sample-database"></a>建立範例資料庫

使用下列步驟來建立名為 **SampleDB** 的範例資料庫。 此資料庫是用來進行每日備份作業。

1. 在您的 Linux 電腦上，開啟 bash 終端機工作階段。

1. 使用 **sqlcmd** 來執行 Transact-SQL **CREATE DATABASE** 命令。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. 透過列出您伺服器上的所有資料庫來確認資料庫是否已建立。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>搭配 Transact-SQL 建立作業

下列步驟會使用 Transact-SQL 命令在 Linux 上建立 SQL Server Agent 作業。 該作業會針對範例資料庫 **SampleDB** 執行每日備份。

> [!TIP]
> 您可以使用任何 T-SQL 用戶端來執行這些命令。 例如，在 Linux 上您可以使用 [sqlcmd](sql-server-linux-setup-tools.md) 或 [Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 從遠端 Windows Server，您也可以在 SQL Server Management Studio 中執行查詢，或是使用 UI 介面來進行作業管理，其將於下一節中描述。

1. 使用 [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) 以建立名為 `Daily SampleDB Backup` 的作業。

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. 呼叫 [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) 來建立能建立 `SampleDB` 資料庫備份的作業步驟。

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

1. 然後使用 [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) 來針對您的作業建立每日排程。

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

1. 使用 [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md) 來將作業排程附加至作業。

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. 使用 [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) 來將作業指派至目標伺服器。 在此範例中，目標是本機伺服器。

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. 使用 [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) 來啟動作業。

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>搭配 SSMS 建立作業

您也可以在 Windows 上使用 SQL Server Management Studio (SSMS) 來從遠端建立及管理作業。

1. 在 Windows 上啟動 SSMS，然後連線至您的 Linux SQL Server 執行個體。 如需詳細資訊，請參閱[使用 SSMS 管理 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md)。

1. 確認您已建立名為 **SampleDB** 的範例資料庫。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. 確認 SQL Agent [已經安裝](sql-server-linux-setup-sql-agent.md)且設定正確。 在 [物件總管] 中尋找位於 SQL Server Agent 旁邊的加號。 如果 SQL Server Agent 尚未啟用，請在 Linux 上嘗試重新啟動 **mssql-server** 服務。

   ![確認已安裝 SQL Server Agent](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 建立新作業。

   ![建立新作業](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. 為作業取名，並建立您的作業步驟。

   ![建立作業步驟](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 指定您想要使用的子系統，以及作業步驟應該執行的動作。

   ![作業子系統](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![作業步驟動作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 建立新的作業排程。

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. 啟動作業。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Linux 上安裝 SQL Server Agent
> * 使用 Transact-SQL 和系統預存程序來建立作業
> * 建立能執行每日資料庫備份的作業
> * 使用 SSMS UI 來建立及管理作業

接下來，請探索建立及管理作業的其他功能：

> [!div class="nextstepaction"]
>[SQL Server Agent 文件](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
