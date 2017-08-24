---
title: "建立和執行 SQL Server on Linux 作業 |Microsoft 文件"
description: "本教學課程會示範如何在 Linux 上執行 SQL Server Agent 作業。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3ffb76838940f42d7a696e1c17f227517d89012d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>建立和執行在 Linux 上的 SQL Server Agent 作業

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

SQL Server 工作可用來定期執行的命令相同的順序，SQL Server 資料庫中。 本主題提供有關如何在 Linux 上建立 SQL Server Agent 作業的範例使用 TRANSACT-SQL 和 SQL Server Management Studio (SSMS)。

在此版本 SQL Server 代理程式的已知問題，請參閱[Release Notes](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>필수 구성 요소 
若要建立並執行工作，您必須先安裝 SQL Server Agent 服務。 如需安裝指示，請參閱[SQL Server 代理程式安裝主題](sql-server-linux-setup-sql-agent.md)。

## <a name="create-a-job-with-transact-sql"></a>使用 TRANSACT-SQL 建立工作

下列步驟提供如何使用 TRANSACT-SQL 命令，在 Linux 上建立 SQL Server Agent 作業的範例。 在此範例中的這些工作的範例資料庫上執行每日備份`SampleDB`。 


> [!TIP]
> 您可以使用任何 T-SQL 的用戶端來執行下列命令。 例如，在 Linux 上您可以使用[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 從遠端 Windows 伺服器，您也可以在 SQL Server Management Studio (SSMS) 執行查詢或使用 UI 介面進行作業管理下, 一節中所述。

1. **建立作業**。 下列範例會使用[sp_add_job](https://msdn.microsoft.com/library/ms182079.aspx)來建立名為作業`Daily AdventureWorks Backup`。

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **加入一或多個作業步驟**。 下列的 TRANSACT-SQL 指令碼會使用[sp_add_jobstep](https://msdn.microsoft.com/library/ms187358.aspx)建立作業步驟所建立的備份`AdventureWlorks2014`資料庫。

    ```tsql
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

3. **建立作業排程**。 這個範例會使用[sp_add_schedule](https://msdn.microsoft.com/library/ms366342.aspx)建立作業每日排程。

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **將作業排程附加至作業**。 使用[sp_attach_schedule](https://msdn.microsoft.com/library/ms186766.aspx)附加至作業的 作業排程。

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **將工作指派給目標伺服器**。 將工作指派給目標伺服器與[sp_add_jobserver](https://msdn.microsoft.com/library/ms178625.aspx)。 在此範例中，本機伺服器為目標。

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **啟動工作**。 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>使用 SSMS 建立作業

您也可以建立及管理在 Windows 上使用遠端 SQL Server Management Studio (SSMS) 的工作。

1. **在 Windows 上啟動 SSMS 並連接至您的 Linux SQL Server 執行個體。** 如需詳細資訊，請參閱[管理 SQL Server on Linux 使用 SSMS](sql-server-linux-develop-use-ssms.md)。

1. **建立新的資料庫名為 SampleDB**。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **請確認 SQL 代理程式已安裝且設定正確。** 尋找在 [物件總管] 中的 SQL Server Agent 旁邊的加號。 如果未安裝 SQL Server 代理程式，請參閱[Linux 上安裝 SQL Server Agent](sql-server-linux-setup-sql-agent.md)。

    ![確認已安裝 SQL Server 代理程式](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **建立新的工作。**

    ![建立新的工作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **提供您的工作名稱，然後建立作業步驟。**

    ![建立作業步驟](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **指定您想要使用何種子系統，應該執行的作業步驟。**

    ![作業子系統](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![作業步驟的動作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **建立新的作業排程。**

    ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![作業排程](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **啟動您的工作。**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>後續步驟

如需有關建立及管理 SQL Server Agent 作業的詳細資訊，請參閱[SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)。

