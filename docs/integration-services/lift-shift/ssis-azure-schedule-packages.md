---
title: "排程 Azure 上的 SSIS 套件執行 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b8dbc635523b33a480ad887b73d9f395d71c8d
ms.sourcegitcommit: ffa4ce9bd71ecf363604966c20cbd2710d029831
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>排程 Azure 上的 SSIS 套件執行
您可以選擇下列其中一個排程選項，來排程執行 Azure SQL Database 伺服器的 SSISDB 目錄資料庫上所儲存的套件：
-   [SQL Server Agent](#agent)
-   [SQL Database 彈性作業](#elastic)
-   [Azure Data Factory SQL Server 預存程序活動](#sproc)

## <a name="agent"></a> 使用 SQL Server Agent 排程套件

### <a name="prerequisite"></a>必要條件

您必須先將 SQL Database 伺服器新增為連結的伺服器，才能在內部部署環境中使用 SQL Server Agent 來排程執行 Azure SQL Database 伺服器上所儲存的套件。 如需詳細資訊，請參閱[建立連結的伺服器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[連結的伺服器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>建立 SQL Server Agent 作業

若要使用 SQL Server Agent 來排程內部部署環境中的套件，請使用可依序呼叫 SSIS 目錄預存程序 `[catalog].[create_execution]` 和 `[catalog].[start_execution]` 的作業步驟來建立作業。 如需詳細資訊，請參閱[套件的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio 中，連線至您要在其上建立作業的內部部署 SQL Server 資料庫。

2.  以滑鼠右鍵按一下 [SQL Server Agent] 節點，並選取 [新增]，然後選取 [作業] 開啟 [新增作業] 對話方塊。

3.  在 [新增作業] 對話方塊中，選取 [步驟] 頁面，然後選取 [新增] 開啟 [新增作業步驟] 對話方塊。

4.  在 [新增作業步驟] 對話方塊中，選取 `SSISDB` 作為 [資料庫]。

5.  在命令欄位中，輸入與下列範例中所示指令碼類似的 Transact-SQL 指令碼：

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  完成設定和排程作業。

## <a name="elastic"></a> 使用 SQL Database 彈性作業排程套件

如需在 SQL Database 上彈性作業的詳細資訊，請參閱[管理相應放大的雲端資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>必要條件

您必須執行下列動作，才能使用彈性作業來排程 Azure SQL Database 伺服器的 SSISDB 目錄資料庫上所儲存的 SSIS 套件：

1.  安裝和設定彈性資料庫作業元件。 如需詳細資訊，請參閱[安裝彈性資料庫作業概觀](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)。

2. 建立作業可用來將命令傳送至 SSIS 目錄資料庫的資料庫範圍認證。 如需詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

### <a name="create-an-elastic-job"></a>建立彈性作業

使用與下列範例中所示指令碼類似的 Transact-SQL 指令碼，來建立作業：

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a> 使用 Azure Data Factory SQL Server 預存程序活動來排程套件

> [!IMPORTANT]
> 搭配使用下列範例中的 JSON 指令碼與 Azure Data Factory 第 1 版預存程序活動。

若要使用 Azure Data Factory SQL Server 預存程序活動來排程套件，請執行下列動作：

1.  建立 Data Factory。

2.  針對裝載 SSISDB 的 SQL Database 建立連結的服務。

3.  建立進行排程的輸出資料集。

4.  建立 Data Factory 管線，以使用 SQL Server 預存程序活動來執行 SSIS 套件。

本節提供這些步驟的概觀。 完整 Data Factory 教學課程超出本文範圍。 如需詳細資訊，請參閱 [SQL Server 預存程序活動](https://docs.microsoft.com/azure/data-factory/data-factory-stored-proc-activity)。

如果排定的執行失敗，且 ADF 預存程序活動提供了執行失敗的執行識別碼，請在 SSIS 目錄中查看 SSMS 中該識別碼的執行報告。

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>針對裝載 SSISDB 的 SQL Database 建立連結的服務
連結的服務可讓 Data Factory 連線至 SSISDB。

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>建立輸出資料集
輸出資料集包含排程資訊。

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
此管線使用 SQL Server 預存程序活動來執行 SSIS 套件。

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

您不需要建立新的預存程序，即可封裝建立和啟動 SSIS 套件執行所需的 Transact-SQL 命令。 您可以將整個指令碼提供為先前 JSON 範例中的 `stmt` 參數值。 範例指令碼如下：

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

若要提供如上所示的 SQL 指令碼作為 `stmt` 參數的值，您通常必須如下列範例所示，在單一行上包含完整的指令碼。 ([JSON 標準](https://json.org/)不支援控制字元，包含其他語言中用來在多行字串中分隔行的 `\n` 換行控制字元)。

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'test', @project_name=N'TestProject', @package_name=N'STestPackage.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Minute",
                    "interval": 15
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2017-12-06T12:00:00Z",
        "end": "2017-12-06T12:30:00Z",
        "isPaused": false,
        "hubName": "test_hub",
        "pipelineMode": "Scheduled"
    }
}
```

如需此指令碼中程式碼的詳細資訊，請參閱[使用預存程序部署和執行 SSIS 套件](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)。

## <a name="next-steps"></a>後續的步驟
如需 SQL Server Agent 的詳細資訊，請參閱[套件的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

如需在 SQL Database 上彈性作業的詳細資訊，請參閱[管理相應放大的雲端資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。
