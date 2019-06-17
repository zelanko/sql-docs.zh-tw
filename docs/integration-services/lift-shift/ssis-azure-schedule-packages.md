---
title: 排程 Azure 中的 SSIS 套件 | Microsoft Docs
description: 提供可用於排程部署到 Azure SQL Database 之 SSIS 套件執行的方法概觀。
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: d879833ee055d857627890471a68cbbaf4263abb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012843"
---
# <a name="schedule-the-execution-of-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>排程部署於 Azure 中的 SQL Server Integration Services (SSIS) 套件執行

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



您可以選擇本文中所述的其中一個方法，來排程部署到 Azure SQL Database 伺服器上 SSISDB 目錄的 SSIS 套件執行。 您可以直接排程套件，或間接排程套件作為 Azure Data Factory 管線的一部分。 如需 Azure 上的 SSIS 概觀，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](ssis-azure-lift-shift-ssis-packages-overview.md)。

- 直接排程套件

  - [使用 SQL Server Management Studio (SSMS) 中的排程選項進行排程](#ssms)

  - [SQL Database 彈性作業](#elastic)

  - [SQL Server Agent](#agent)

- [間接排程套件作為 Azure Data Factory 管線的一部分](#activity)


## <a name="ssms"></a> 使用 SSMS 排程套件

在 SQL Server Management Studio (SSMS) 中，您可以在部署到 SSIS 目錄資料庫 (SSISDB) 的套件上按一下滑鼠右鍵，然後選取 [排程]  以開啟 [新增排程]  對話方塊。 如需詳細資訊，請參閱[在 Azure 中以 SSMS 排程 SSIS 套件](ssis-azure-schedule-packages-ssms.md)。

此功能需要 SQL Server Management Studio 17.7 版或更高版本。 若要取得最新版的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="elastic"></a> 使用 SQL Database 彈性作業排程套件

如需在 SQL Database 上彈性作業的詳細資訊，請參閱[管理相應放大的雲端資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>Prerequisites

您必須執行下列動作，才能使用彈性作業來排程 Azure SQL Database 伺服器的 SSISDB 目錄資料庫上所儲存的 SSIS 套件：

1.  安裝和設定彈性資料庫作業元件。 如需詳細資訊，請參閱[安裝彈性資料庫作業概觀](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)。

2. 建立作業可用來將命令傳送至 SSIS 目錄資料庫的資料庫範圍認證。 如需詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

### <a name="create-an-elastic-job"></a>建立彈性作業

使用與下列範例中所示指令碼類似的 Transact-SQL 指令碼，來建立作業：

```sql
-- Create Elastic Jobs target groupÂ 
EXECÂ jobs.sp_add_target_group 'TargetGroup'Â 

-- Add Elastic Jobs target group memberÂ 
EXECÂ jobs.sp_add_target_group_memberÂ @target_group_name='TargetGroup',Â 
    @target_type='SqlDatabase',Â @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB'Â 

-- Add a job to schedule SSIS package execution
EXECÂ jobs.sp_add_jobÂ @job_name='ExecutePackageJob',Â @description='Description',Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXECÂ jobs.sp_add_jobstepÂ @job_name='ExecutePackageJob',Â 
    @command=N'DECLAREÂ @exe_idÂ bigintÂ 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1,Â 
            @execution_id=@exe_idÂ OUTPUT       Â 
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0',Â 
    @credential_name='YourDBScopedCredentials',Â 
    @target_group_name='TargetGroup'Â 

-- Enable the job scheduleÂ 
EXECÂ jobs.sp_update_jobÂ @job_name='ExecutePackageJob',Â @enabled=1,Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60Â 
```

## <a name="agent"></a> 使用 SQL Server Agent 在內部部署排程套件

如需 SQL Server Agent 的詳細資訊，請參閱[套件的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。

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
        @location='',
        @provstr='',
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **設定連結的伺服器認證**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer',
        @useself = 'false',
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

2.  以滑鼠右鍵按一下 [SQL Server Agent]  節點，並選取 [新增]  ，然後選取 [作業]  開啟 [新增作業]  對話方塊。

3.  在 [新增作業]  對話方塊中，選取 [步驟]  頁面，然後選取 [新增]  開啟 [新增作業步驟]  對話方塊。

4.  在 [新增作業步驟]  對話方塊中，選取 `SSISDB` 作為 [資料庫]  。

5.  在 [命令]  欄位中，輸入與下列範例中所示指令碼類似的 Transact-SQL 指令碼：

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_valueÂ int,Â @exe_idÂ bigintÂ 

    EXEC @return_valueÂ =Â [YourLinkedServer].[SSISDB].[catalog].[create_execution]Â 
        @folder_name=N'folderName',Â @project_name=N'projectName',Â 
        @package_name=N'packageName',Â @use32bitruntime=0,Â @runincluster=1,Â @useanyworker=1,
        @execution_id=@exe_idÂ OUTPUTÂ 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution]Â @execution_id=@exe_id
    ```

6.  完成設定和排程作業。

## <a name="activity"></a> 排程套件作為 Azure Data Factory 管線的一部分

您可以使用觸發程序來執行將執行 SSIS 套件的 Azure Data Factory 管線，藉以間接排程套件。

若要排程 Data Factory 管線，請使用下列其中一個觸發程序：

- [排程觸發程序](https://docs.microsoft.com/azure/data-factory/how-to-create-schedule-trigger)

- [輪轉視窗觸發程序](https://docs.microsoft.com/azure/data-factory/how-to-create-tumbling-window-trigger)

- [事件架構觸發程序](https://docs.microsoft.com/azure/data-factory/how-to-create-event-trigger)

若要執行 SSIS 套件作為 Data Factory 管線的一部分，請使用下列其中一個活動：

- [執行 SSIS 套件活動](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)。

- [預存程序活動](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)。

## <a name="next-steps"></a>後續步驟

檢閱執行部署到 Azure 之 SSIS 套件的選項。 如需詳細資訊，請參閱[在 Azure 中執行 SSIS 套件](ssis-azure-run-packages.md)。
