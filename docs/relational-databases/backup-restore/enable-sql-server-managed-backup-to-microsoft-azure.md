---
title: "啟用 SQL Server Managed Backup to Microsoft Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de5d4d788520c9fd8addc98c19be11cf2361456d
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>啟用 SQL Server Managed Backup to Microsoft Azure
  本主題說明如何使用資料庫和執行個體層級的預設設定來啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 它也會說明啟用電子郵件通知以及監視備份活動的方式。  
  
 本教學課程使用 Azure PowerShell。 開始本教學課程之前，請 [下載並安裝 Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)。  
  
> [!IMPORTANT]  
>  如果您也想要啟用進階選項或使用自訂排程，則在啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前，需先進行這些設定。 如需詳細資訊，請參閱 [Configure Advanced Options for SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)。  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 並使用預設值進行設定  
  
#### <a name="create-the-azure-blob-container"></a>建立 Azure Blob 容器  
  
1.  **註冊 Azure：** 如果您已經有 Azure 訂用帳戶，請移至下一個步驟。 否則，您可以開始使用 [免費試用版](http://azure.microsoft.com/pricing/free-trial/) 或瀏覽 [購買選項](http://azure.microsoft.com/pricing/purchase-options/)。  
  
2.  **建立 Azure 儲存體帳戶︰** 如果您已經有儲存體帳戶，請移至下一個步驟。 否則，您可以使用 [Azure 管理入口網站](https://manage.windowsazure.com/) 或 Azure PowerShell 來建立儲存體帳戶。 下列 `New-AzureStorageAccount` 命令會在美東地區建立名為 `managedbackupstorage` 的儲存體帳戶。  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     如需儲存體帳戶的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](http://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account/)。  
  
3.  **建立適用於備份檔案的 Blob 容器︰** 您可以在 Azure 管理入口網站或 Azure PowerShell 中建立 Blob 容器。 下列 `New-AzureStorageContainer` 命令會在 `backupcontainer` 儲存體帳戶中建立名為 `managedbackupstorage` 的 Blob 容器。  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **產生共用存取簽章 (SAS)：** 若要存取此容器，您必須建立 SAS。 您可以在某些工具、程式碼和 Azure PowerShell 中完成此動作。 下列 `New-AzureStorageContainerSASToken` 命令可為一年內過期的 `backupcontainer` Blob 容器建立 SAS 權杖。  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
    New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
    ```  
  
     此命令的輸出將包含容器和 SAS 權杖的 URL。 以下是一個範例：  
  
    ```  
    https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl  
    ```  
  
     在上述範例中，使用問號來分隔容器 URL 和 SAS 權杖 (不包含問號)。 例如，上述輸出會產生下列這兩個值。  
  
    |||  
    |-|-|  
    |**容器 URL：**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
    |**SAS 權杖︰**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
  
     記下容器 URL 和 SAS，以便在建立 SQL 認證時使用。 如需 SAS 的詳細資訊，請參閱 [共用存取簽章，第 1 部分：了解 SAS 模型](http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **建立適用於 SAS URL 的 SQL 認證︰** 使用 SAS 權杖來建立適用於 Blob 容器 URL 的 SQL 認證。 在 SQL Server Management Studio 中，使用下列 TRANSACT-SQL 查詢，根據下列範例來建立適用於 Blob 容器 URL 的認證：  
  
    ```tsql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Server Agent 設定為自動執行，以確保備份作業定期執行。  
  
3.  **指定保留週期：** 指定備份檔案的保留週期。 保留週期的指定單位為天，範圍從 1 到 30。  
  
4.  **Enable and configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ：** 啟動 SQL Server Management Studio 並連接到目標 SQL Server 執行個體。 在您根據每個需求修改資料庫名稱、容器 URL及保留週期的值之後，從查詢視窗中執行下列陳述式：  
  
    > [!IMPORTANT]  
    >  若要在執行個體層級啟用受管理的備份，請針對 `NULL` 參數指定 `database_name` 。  
  
    ```tsql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 已在您指定的資料庫上啟用。 資料庫上的備份作業可能需要 15 分鐘才會開始執行。  
  
5.  **檢閱擴充事件預設組態：** 執行下列 Transact-SQL 陳述式，以檢閱擴充事件設定。  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     預設會顯示已經啟用 Admin、Operational 和 Analytical 通道事件，且無法予以停用。 這應該足以監視需要手動介入的事件。  您可以啟用偵錯事件，不過偵錯通道包含 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 用來偵測及解決問題的資訊和偵錯事件。  
  
6.  **啟用及設定健全狀態通知：**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知，以接收備份錯誤及警告：** 在查詢視窗中，執行下列 Transact-SQL 陳述式：  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **檢視 Microsoft Azure 儲存體帳戶中的備份檔案：** 從 SQL Server Management Studio 或 Azure 管理入口網站連接至儲存體帳戶。 您將會看到指定容器中的所有備份檔案。 請注意，您可能會在針對資料庫啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的 5 分鐘內，看到資料庫和記錄備份。  
  
8.  **監視健全狀態：**  您可以透過先前設定的電子郵件通知進行監視，或主動監視記錄的事件。 以下是用於檢視事件的一些 Transact-SQL 陳述式範例：  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 本節所描述的步驟是針對第一次在資料庫上設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 您可以使用相同的系統預存程序來修改現有的組態並提供新值。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  

