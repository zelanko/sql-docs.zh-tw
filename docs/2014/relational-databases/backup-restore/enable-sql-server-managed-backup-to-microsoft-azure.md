---
title: 設定 SQL Server Managed Backup to Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 493f0b885f25cfba956fc8e03505b705c731cf2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875797"
---
# <a name="setting-up-sql-server-managed-backup-to-windows-azure"></a>設定 SQL Server Managed Backup 到 Windows Azure
  本主題包含兩個教學課程：  
  
 在資料庫層級設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、啟用電子郵件通知，以及監視備份活動。  
  
 在執行個體層級設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、啟用電子郵件通知，以及監視備份活動。  
  
 如需設定的教學課程[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]可用性群組，請參閱[可用性群組設定 SQL Server Managed Backup to Microsoft Azure](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)。  
  
## <a name="setting-up-includesssmartbackupincludesss-smartbackup-mdmd"></a>設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
### <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-for-a-database"></a>啟用及設定資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 此教學課程會先說明啟用及設定資料庫 (TestDB) 之 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的必要步驟，然後再說明啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 健全狀態之監視功能的步驟。  
  
 **權限：**  
  
-   需要的成員資格**db_backupoperator**資料庫角色，使用**ALTER ANY CREDENTIAL**權限，並`EXECUTE`的權限**sp_delete_backuphistory**預存程序。  
  
-   需要**選取** 權限 **smart_admin.fn_get_current_xevent_settings** 函式。  
  
-   需要`EXECUTE`權限**smart_admin.sp_get_backup_diagnostics**預存程序。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  
  
-   需要`EXECUTE`權限`smart_admin.sp_set_instance_backup`和`smart_admin.sp_backup_master_switch`預存程序。  


1.  **建立 Microsoft Azure 儲存體帳戶：** 備份會儲存在 Microsoft Azure 儲存體服務。 如果您還沒有帳戶，您必須先建立 Microsoft Azure 儲存體帳戶。
    - SQL Server 2014 使用分頁 blob，其不同於區塊和附加 blob。 因此，您必須建立一般用途的帳戶，而不是 blob 帳戶。 如需詳細資訊，請參閱 <<c0> [ 關於 Azure 儲存體帳戶](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。
    - 記下儲存體帳戶名稱和存取金鑰。 儲存體帳戶名稱和存取金鑰資訊可用來建立 SQL 認證。 SQL 認證會用來驗證儲存體帳戶。  
 
2.  **建立 SQL 認證：** 建立 SQL 認證，使用做為身分識別和儲存體存取金鑰的儲存體帳戶的名稱，做為密碼。  
  
3.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Server Agent 設定為自動執行，以確保備份作業定期執行。  
  
4.  **決定保留期限：** 決定備份檔案的保留期限。 保留週期的指定單位為天，範圍從 1 到 30。  
  
5.  **啟用及設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：** 啟動 SQL Server Management Studio 並連接到安裝資料庫執行個體。 在您根據需要修改資料庫名稱、SQL 認證、保留週期及加密選項的值之後，請在查詢視窗中執行下列陳述式：  
  
     如需有關建立憑證以進行加密的詳細資訊，請參閱 <<c0>  **建立備份憑證**中的步驟[Create an Encrypted Backup](create-an-encrypted-backup.md)。  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 已在您指定的資料庫上啟用。 資料庫上的備份作業可能需要 15 分鐘才會開始執行。  
  
6.  **檢閱延伸事件預設設定：** 執行下列 TRANSACT-SQL 陳述式，以檢閱擴充事件設定。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     預設會顯示已經啟用 Admin、Operational 和 Analytical 通道事件，且無法予以停用。 這應該足以監視需要手動介入的事件。  您可以啟用偵錯事件，不過偵錯通道包含 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 用來偵測及解決問題的資訊和偵錯事件。 如需詳細資訊，請參閱 <<c0> [ 監視 SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
7.  **啟用及設定健全狀態通知：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知接收備份錯誤和警告：** 從 [查詢] 視窗中，執行下列 TRANSACT-SQL 陳述式：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         如需詳細資訊，以及完整的範例指令碼請參閱[監視 SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
8.  **檢視 Microsoft Azure 儲存體帳戶中的備份檔案：** 從 SQL Server Management Studio 或 Azure 管理入口網站連接到儲存體帳戶。 您會看到裝載設定為使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的資料庫之 SQL Server 執行個體的容器。 您也會在啟用資料庫之 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的 15 分鐘內，看到資料庫和記錄備份。  
  
9. **監視健康狀態：** 您可以透過先前設定的電子郵件通知進行監視，或主動監視記錄的事件。 以下是用於檢視事件的一些 Transact-SQL 陳述式範例：  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 本節所描述的步驟是針對第一次在資料庫上設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 您可以修改現有的組態使用相同的系統預存程序**smart_admin.sp_set_db_backup**並提供新的值。 如需詳細資訊，請參閱 < [SQL Server Managed Backup to Microsoft Azure-Retention and Storage Settings](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]使用預設設定啟用執行個體的  
 本教學課程描述啟用及設定步驟[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]執行個體 'MyInstance'，\\。 其中也包括如何啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]健全狀態之監視功能的步驟。  
  
 **權限：**  
  
-   需要的成員資格**db_backupoperator**資料庫角色，使用**ALTER ANY CREDENTIAL**權限，並`EXECUTE`的權限**sp_delete_backuphistory**預存程序。  
  
-   需要**選取** 權限 **smart_admin.fn_get_current_xevent_settings** 函式。  
  
-   需要`EXECUTE`權限**smart_admin.sp_get_backup_diagnostics**預存程序。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  


1.  **建立 Microsoft Azure 儲存體帳戶：** 備份會儲存在 Microsoft Azure 儲存體服務。 如果您還沒有帳戶，您必須先建立 Microsoft Azure 儲存體帳戶。
    - SQL Server 2014 使用分頁 blob，其不同於區塊和附加 blob。 因此，您必須建立一般用途的帳戶，而不是 blob 帳戶。 如需詳細資訊，請參閱 <<c0> [ 關於 Azure 儲存體帳戶](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。
    - 記下儲存體帳戶名稱和存取金鑰。 儲存體帳戶名稱和存取金鑰資訊可用來建立 SQL 認證。 SQL 認證會用來驗證儲存體帳戶。  
  
2.  **建立 SQL 認證：** 建立 SQL 認證，使用做為身分識別和儲存體存取金鑰的儲存體帳戶的名稱，做為密碼。  
  
3.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Server Agent 設定為自動執行，以確保備份作業定期執行。  
  
4.  **決定保留期限：** 決定備份檔案的保留期限。 保留週期的指定單位為天，範圍從 1 到 30。 在執行個體層級啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 並使用預設值之後，所有於此後所新建的資料庫，皆會繼承這些設定。 僅支援設定為完整或大量記錄復原模式的資料庫，並且會自動設定。 如果您不想設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，您可以隨時停用特定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 您也可以在資料庫層級設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，以變更特定資料庫的設定。  
  
5.  **啟用及設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：** 啟動 SQL Server Management Studio 並連接到 SQL Server 執行個體。 在您根據需要修改資料庫名稱、SQL 認證、保留週期及加密選項的值之後，請在查詢視窗中執行下列陳述式：  
  
     如需有關建立憑證以進行加密的詳細資訊，請參閱 <<c0>  **建立備份憑證**中的步驟[Create an Encrypted Backup](create-an-encrypted-backup.md)。  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     現在在執行個體上已啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
6.  執行下列 Transact-SQL 陳述式，以驗證組態設定：  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  在執行個體上建立新的資料庫。 執行下列 Transact-SQL 陳述式，以檢視資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 組態設定：  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     可能需要 15 分鐘才會顯示設定，並開始執行資料庫上的備份作業。  
  
8.  **啟用及設定健全狀態通知：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。  若要接收這類通知，必須啟用 [執行預存程序]，以建立 SQL Server Agent 工作。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知接收備份錯誤和警告：** 從 [查詢] 視窗中，執行下列 TRANSACT-SQL 陳述式：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         如需如何監視，以及完整的範例指令碼的詳細資訊，請參閱[監視 SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)。  
  
9. **檢視 Microsoft Azure 儲存體帳戶中的備份檔案：** 從 SQL Server Management Studio 或 Azure 管理入口網站連接到儲存體帳戶。 您會看到裝載設定為使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的資料庫之 SQL Server 執行個體的容器。 您也會在建立新的資料庫之後的 15 分鐘內，看到資料庫和記錄備份。  
  
10. **監視健康狀態：** 您可以透過先前設定的電子郵件通知進行監視，或主動監視記錄的事件。 以下是用於檢視事件的一些 Transact-SQL 陳述式範例：  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 在資料庫層級明確地配置設定，可以覆寫特定資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 預設設定。 您也可以暫停再繼續執行 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服務。 如需詳細資訊，請參閱[SQL Server Managed Backup to Microsoft Azure-Retention and Storage Settings](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)  
  
  
