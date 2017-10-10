---
title: "排程在 Azure 上的 SSIS 封裝執行 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: a3ecfce9a6adac332b72033955ba51271ed8197b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>排程的 SSIS 封裝在 Azure 上執行
您可以排定執行的封裝儲存在 Azure SQL Database 伺服器上的 SSISDB 目錄資料庫中，選擇其中一個排程的下列選項：
-   [SQL Server Agent](#agent)
-   [SQL Database 彈性的工作](#elastic)
-   [Azure 資料 Factory SQL Server 預存程序活動](#sproc)

## <a name="agent"></a>排程 SQL Server Agent 的封裝

### <a name="prerequisite"></a>必要條件

您可以在內部部署使用 SQL Server Agent 來排程儲存在 Azure SQL Database 伺服器上的封裝執行之前，您必須將 SQL Database 伺服器新增為連結的伺服器。 如需詳細資訊，請參閱[建立連結的伺服器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[連結的伺服器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>建立 SQL Server Agent 作業

若要排程在內部部署 SQL Server Agent 的封裝，請使用作業步驟呼叫 SSIS 目錄的建立作業預存程序`[catalog].[create_execution]`然後`[catalog].[start_execution]`。 如需詳細資訊，請參閱[封裝的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio 中，連接到您要建立作業在內部部署 SQL Server 資料庫。

2.  以滑鼠右鍵按一下**SQL Server Agent**節點中，選取**新增**，，然後選取 [**作業**開啟**新工作**] 對話方塊。

3.  在**新工作**對話方塊中，選取**步驟**頁面，然後再選取**新增**開啟**新增作業步驟** 對話方塊。

4.  在**新增作業步驟**對話方塊中，選取`SSISDB`為**資料庫。**

5.  在 [命令] 欄位中，輸入類似下列範例所示的指令碼的 TRANSACT-SQL 指令碼：

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runincluster=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  完成設定和排程工作。

## <a name="elastic"></a>排程 SQL Database 彈性工作的封裝

如需在 SQL Database 彈性作業的詳細資訊，請參閱[管理向外延展雲端資料庫](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>必要條件

您可以使用彈性的作業來排程儲存在 Azure SQL Database 伺服器上的 SSISDB 目錄資料庫的 SSIS 封裝之前，您必須執行下列動作：

1.  安裝和設定的彈性資料庫工作元件。 如需詳細資訊，請參閱[安裝彈性資料庫工作概觀](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation)。

2. 建立工作可用來將命令傳送至 SSIS 目錄資料庫的資料庫範圍認證。 如需詳細資訊，請參閱[CREATE DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

### <a name="create-an-elastic-job"></a>建立彈性的工作

使用類似下列範例所示的指令碼的 TRANSACT-SQL 指令碼，以建立作業：

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 
? 
-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 
? 
-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runincluster=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a>排程封裝，以與 Azure 資料 Factory SQL Server 預存程序活動

若要排程封裝，以與 Azure 資料 Factory SQL Server 預存程序活動，執行下列動作：
1.  建立 Data Factory。
2.  建立連結的服務，SQL database 主控 SSISDB。
3.  建立輸出資料集的磁碟機的排程。
4.  建立 Data Factory 管線用來執行 SSIS 封裝的 SQL Server 預存程序活動。

本節提供這些步驟的概觀。 完整的 Data Factory 教學課程已超出本文的範圍。 如需詳細資訊，請參閱[SQL Server 預存程序活動](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity)。

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>建立連結的服務，SQL database 主控 SSISDB
連結的服務可讓連接到 SSISDB 的 Data Factory。

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30 "
        }
    }
}
```

### <a name="create-an-output-dataset"></a>建立輸出資料集
輸出資料集包含排程的資訊。

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>建立 Data Factory 管線
管線會使用 SQL Server 預存程序活動執行 SSIS 封裝。

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

您不必建立新的預存程序，將封裝以建立並啟動 SSIS 封裝執行所需的 Transact SQL 命令。 您可以提供指令碼的值為`stmt`上述的 JSON 範例中的參數。 以下是範例指令碼：

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runincluster=1,@useanyworker=1, @execution_id=@exe_id OUTPUT
                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
-- To synchronize SSIS package execution, poll package execution status
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
                                          
WHILE(SELECT [status]
      FROM [SSISDB].[catalog].[executions]
      WHERE execution_id=@exe_id) NOT IN(3,4,6,7,9)
BEGIN
    WAITFOR DELAY '00:00:01';
END

-- Raise an error for unsuccessful package execution
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: '+CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

如需此指令碼中的程式碼的詳細資訊，請參閱[部署及執行 SSIS 封裝使用預存程序](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)。

## <a name="next-steps"></a>後續的步驟
如需 SQL Server Agent 的詳細資訊，請參閱[封裝的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

如需在 SQL Database 彈性作業的詳細資訊，請參閱[管理向外延展雲端資料庫](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。
