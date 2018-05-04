---
title: 排程 Azure 上的 SSIS 套件執行 | Microsoft Docs
ms.date: 04/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c946055e7579478d65de31f737b1c265b2a38eba
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>排程 Azure 上的 SSIS 套件執行
您可以選擇下列其中一個排程選項，來排程執行 Azure SQL Database 伺服器的 SSISDB 目錄資料庫上所儲存的套件：
-   [SQL Server Agent](#agent)
-   [SQL Database 彈性作業](#elastic)
-   [Azure Data Factory 執行 SSIS 套件活動](#activities)
-   [Azure Data Factory SQL Server 預存程序活動](#activities)

## <a name="agent"></a> 使用 SQL Server Agent 排程套件

### <a name="prerequisite---create-a-linked-server"></a>必要條件 - 建立連結的伺服器

您必須先將 SQL Database 伺服器新增至內部部署 SQL Server 作為連結的伺服器，才能在內部部署環境中使用 SQL Server Agent 來排程執行 Azure SQL Database 伺服器上所儲存的套件。

1.  **設定連結的伺服器**

    ```sql
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',     
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location=‘’,
        @provstr=‘’,
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **設定連結的伺服器認證**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer’,
        @useself = 'false’,
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **設定連結的伺服器選項**

    ```sql
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

如需詳細資訊，請參閱[建立連結的伺服器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[連結的伺服器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>建立 SQL Server Agent 作業

若要使用 SQL Server Agent 來排程內部部署環境中的套件，請使用可依序呼叫 SSIS 目錄預存程序 `[catalog].[create_execution]` 和 `[catalog].[start_execution]` 的作業步驟來建立作業。 如需詳細資訊，請參閱[套件的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio 中，連線至您要在其上建立作業的內部部署 SQL Server 資料庫。

2.  以滑鼠右鍵按一下 [SQL Server Agent] 節點，並選取 [新增]，然後選取 [作業] 開啟 [新增作業] 對話方塊。

3.  在 [新增作業] 對話方塊中，選取 [步驟] 頁面，然後選取 [新增] 開啟 [新增作業步驟] 對話方塊。

4.  在 [新增作業步驟] 對話方塊中，選取 `SSISDB` 作為 [資料庫]。

5.  在 [命令] 欄位中，輸入與下列範例中所示指令碼類似的 Transact-SQL 指令碼：

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
        @folder_name=N'folderName', @project_name=N'projectName', 
        @package_name=N'packageName', @use32bitruntime=0, @runincluster=1, @useanyworker=1,
        @execution_id=@exe_id OUTPUT 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id
    ```

6.  完成設定和排程作業。

## <a name="elastic"></a> 使用 SQL Database 彈性作業排程套件

如需在 SQL Database 上彈性作業的詳細資訊，請參閱[管理相應放大的雲端資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>Prerequisites

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

## <a name="activities"></a> 使用 Azure Data Factory 排定套件

如需如何使用 Azure Data Factory 活動排定 SSIS 套件的資訊，請參閱下列文章：

-   針對 Data Factory 第 2 版：[在 Azure Data Factory 中使用 SSIS 活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)

-   針對 Data Factory 第 2 版：[在 Azure Data Factory 中使用預存程序活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)

-   針對 Data Factory 第 1 版：[在 Azure Data Factory 中使用預存程序活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/v1/how-to-invoke-ssis-package-stored-procedure-activity)

## <a name="next-steps"></a>後續步驟
如需 SQL Server Agent 的詳細資訊，請參閱[套件的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

如需在 SQL Database 上彈性作業的詳細資訊，請參閱[管理相應放大的雲端資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。
