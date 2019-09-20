---
title: 啟用 SQL Server 到 Azure 的受控備份 | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0b778c458852adc2c26d62eb9d7ef8066b9fbb89
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238739"
---
# <a name="enable-sql-server-managed-backup-to-azure"></a>啟用 SQL Server 到 Azure 的受控備份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題說明如何使用資料庫和執行個體層級的預設設定來啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 它也會說明啟用電子郵件通知以及監視備份活動的方式。  
  
 本教學課程使用 Azure PowerShell。 開始本教學課程之前，請 [下載並安裝 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
> [!IMPORTANT]  
>  如果您也想要啟用進階選項或使用自訂排程，則在啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前，需先進行這些設定。 如需詳細資訊，請參閱[設定 SQL Server 到 Azure 的受控備份進階選項](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)。  
  
## <a name="create-the-azure-blob-container"></a>建立 Azure Blob 容器

此程序需要 Azure 帳戶。 如果您已經有帳戶，請移至下一個步驟。 否則，您可以開始使用 [免費試用版](https://azure.microsoft.com/pricing/free-trial/) 或瀏覽 [購買選項](https://azure.microsoft.com/pricing/purchase-options/)。

如需儲存體帳戶的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。 

#### <a name="azure-clitabazure-cli"></a>[Azure CLI](#tab/azure-cli)

1. 登入您的 Azure 帳戶。

    ```azurecli-interactive
    az login
    ```
  
1. 建立 Azure 儲存體帳戶。 如果您已經有儲存體帳戶，請移至下一個步驟。 下列命令會在美國東部區域建立名為 `<backupStorage>` 的儲存體帳戶。  
  
    ```azurecli-interactive
    az storage account create -n <backupStorage> -l "eastus" --resource-group <resourceGroup>
    ```  
    
1. 建立名為 `<backupContainer>` 的 Blob 容器以用於備份檔案。
  
    ```azurecli-interactive
    $keys = az storage account keys list --account-name <backupStorage> --resource-group <resourceGroup> | ConvertFrom-Json
    az storage container create --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value 
    ```  
  
1. 產生共用存取簽章 (SAS) 以存取容器。 下列命令可為將於一年內過期的 `<backupContainer>` Blob 容器建立 SAS 權杖。  
  
    ```azurecli-interactive 
    az storage container generate-sas --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value
    ```

#### <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

1. 下列命令可登入您的 Azure 帳戶。

    ```azurepowershell-interactive
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscriptionId>"
    ```
  
1. 建立 Azure 儲存體帳戶。 如果您已經有儲存體帳戶，請移至下一個步驟。 下列命令會在美國東部區域建立名為 `<backupStorage>` 的儲存體帳戶。  
  
    ```azurepowershell-interactive
    New-AzStorageAccount -StorageAccountName <backupStorage> -Location "EAST US" -ResourceGroupName <resourceGroup> -SkuName Standard_GRS
    ```   
  
1. 建立名為 `<backupContainer>` 的 Blob 容器以用於備份檔案。  
  
    ```azurepowershell-interactive
    $context = New-AzStorageContext -StorageAccountName <backupStorage> -StorageAccountKey (Get-AzStorageAccountKey -Name <backupStorage> -ResourceGroupName <resourceGroup>).Value[0]  
    New-AzStorageContainer -Name <backupContainer> -Context $context  
    ```  
  
1. 產生共用存取簽章 (SAS) 以存取容器。 下列命令可為將於一年內過期的 `<backupContainer>` Blob 容器建立 SAS 權杖。
  
    ```azurepowershell-interactive 
    New-AzStorageContainerSASToken -Name <backupContainer> -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context 
    ```

* * *

> [!NOTE]
> 您也可以使用 [Azure 入口網站](https://portal.azure.com/)來完成這些步驟。

輸出將包含容器和/或 SAS 權杖的 URL。 以下是一個範例：  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
如果其中包含 URL，請使用問號將其和 SAS 權杖分隔 (不包含問號)。 例如，上述輸出會產生下列這兩個值。  
  
|||  
|-|-|  
|**容器 URL**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**SAS 權杖**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
記下容器 URL 和 SAS，以便在建立 SQL 認證時使用。 如需 SAS 的詳細資訊，請參閱[共用存取簽章，第 1 部分：了解 SAS 模型](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。  
  
## <a name="enable-managed-backup-to-azure"></a>啟用 Azure 受控備份
  
1.  **建立適用於 SAS URL 的 SQL 認證：** 使用 SAS 權杖來建立適用於 Blob 容器 URL 的 SQL 認證。 在 SQL Server Management Studio 中，使用下列 TRANSACT-SQL 查詢，根據下列範例來建立適用於 Blob 容器 URL 的認證：  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Server Agent 設定為自動執行，以確保備份作業定期執行。  
  
3.  **決定保留期限：** 決定備份檔案的保留期限。 保留週期的指定單位為天，範圍從 1 到 30。  
  
4.  **啟用及設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：** 啟動 SQL Server Management Studio 並連線到目標 SQL Server 執行個體。 在您根據每個需求修改資料庫名稱、容器 URL及保留週期的值之後，從查詢視窗中執行下列陳述式：  
  
    > [!IMPORTANT]  
    >  若要在執行個體層級啟用受管理的備份，請針對 `NULL` 參數指定 `database_name` 。  
  
    ```sql  
    USE msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 已在您指定的資料庫上啟用。 資料庫上的備份作業可能需要 15 分鐘才會開始執行。  
  
5.  **檢閱延伸事件預設設定：** 執行下列 Transact-SQL 陳述式，以檢閱擴充事件設定。  
  
    ```sql
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     預設會顯示已經啟用 Admin、Operational 和 Analytical 通道事件，且無法予以停用。 這應該足以監視需要手動介入的事件。  您可以啟用偵錯事件，不過偵錯通道包含 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 用來偵測及解決問題的資訊和偵錯事件。  
  
6.  **啟用及設定健全狀態通知：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知接收備份錯誤和警告：** 從 [查詢] 視窗中，執行下列 Transact-SQL 陳述式：  
  
        ```sql
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
        ```  
  
7.  **檢視 Azure 儲存體帳戶中的備份檔案：** 從 SQL Server Management Studio 或 Azure 入口網站連線到儲存體帳戶。 您將會看到指定容器中的所有備份檔案。 請注意，您可能會在針對資料庫啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的 5 分鐘內，看到資料庫和記錄備份。  
  
8.  **監視健康狀態：** 您可以透過先前設定的電子郵件通知進行監視，或主動監視記錄的事件。 以下是用於檢視事件的一些 Transact-SQL 陳述式範例：  
  
    ```sql  
    --  view all admin events  
    USE msdb;  
    GO  
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
  
    ```sql  
    -- to enable debug events  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
    ```sql  
    --  View all events in the current week  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
本節所描述的步驟是針對第一次在資料庫上設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 您可以使用相同的系統預存程序來修改現有的組態並提供新值。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 到 Azure 的受控備份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
