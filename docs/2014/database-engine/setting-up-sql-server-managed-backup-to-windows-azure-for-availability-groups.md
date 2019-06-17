---
title: 設定可用性群組的 SQL Server Managed Backup to Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a67b2331959dbc3087f6282be05de90b42443c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843564"
---
# <a name="setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups"></a>針對可用性群組設定 SQL Server Managed Backup 到 Windows Azure
  本主題是設定參與 AlwaysOn 可用性群組之資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之教學課程。  
  
## <a name="availability-group-configurations"></a>可用性群組組態  
 可用性群組資料庫支援使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，不論複本全都設定為內部部署或是全部都在 Windows Azure 上，還是在內部部署與一部或多部 Windows Azure 虛擬機器之間的混合式實作。 但是，您可能必須針對一個或多個實作考量以下事項：  
  
-   記錄備份頻率：記錄備份的頻率會隨著時間和記錄而增加。 例如，系統會每隔兩個小時取得一次記錄備份，除非在這兩個小時內使用的記錄空間為 5 MB 或更多。 這適用於所有實作，不論是內部部署、雲端還是混合式。  
  
-   網路頻寬：這適用於複本的位置在不同的實體位置，例如混合式雲端中或跨雲端的唯一組態中的不同 Windows Azure 區域的實作。 網路頻寬可能會影響次要複本的延遲，而且如果次要複本設定為同步複寫，這可能會導致主要複本上的記錄增加。 如果次要複本設定為同步複寫，次要複本可能會因為網路延遲的緣故而跟不上同步，萬一容錯移轉到次要複本就可能會發生資料遺失。  
  
### <a name="configuring-includesssmartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>設定可用性資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
 **權限：**  
  
-   需要的成員資格**db_backupoperator**資料庫角色，使用**ALTER ANY CREDENTIAL**權限，並`EXECUTE`的權限**sp_delete_backuphistory**預存程序。  
  
-   需要**選取** 權限 **smart_admin.fn_get_current_xevent_settings** 函式。  
  
-   需要`EXECUTE`權限**smart_admin.sp_get_backup_diagnostics**預存程序。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  
  
-   需要`EXECUTE`權限`smart_admin.sp_set_instance_backup`和`smart_admin.sp_backup_master_switch`預存程序。  
  
 以下是使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定 AlwaysOn 可用性群組的基本步驟。 本主題稍後將說明詳細的逐步教學課程。  
  
1.  建立可用性群組之後，請設定慣用的備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會使用可用性群組的這項設定來決定用於備份的複本。 如需如何設定備份喜好設定的逐步指示，請參閱[可用性複本上的 備份設定&#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。  如果您要建立新的 AlwaysOn 可用性群組，請參閱[開始使用 AlwaysOn 可用性群組&#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)。  
  
2.  設定次要複本的唯讀連接存取。 如需如何設定的逐步指示唯讀存取，請參閱 <<c0> [ 可用性複本設定唯讀存取&#40;SQL Server&#41;</c0>](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
3.  指定備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會使用慣用的備份複本設定來決定用於排程備份的資料庫。  若要判斷目前的複本是否為慣用的備份複本，請使用[sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函式。  
  
4.  執行每個複本上[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]資料庫使用的組態**智慧 admin.sp_set_db_backup**預存程序。  
  
     **[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 在容錯移轉之後的行為：** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會繼續運作，並在容錯移轉事件之後保留備份複本和復原能力。 在容錯移轉之後，不需要採取特定的動作。  
  
#### <a name="considerations-and-requirements"></a>考量和需求：  
 針對參與 AlwaysOn 可用性群組的資料庫設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]需要進行特定考量並符合特定需求。 以下是考量與需求清單：  
  
-   參與相同可用性群組之所有 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 節點上的所有資料庫，都應該具有相同的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]組態設定。 您可以在資料庫層級針對主要及所有複本設定相同的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態，或在參與可用性群組的所有節點上設定相同的預設[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定，來達成此目的。 建議在資料庫設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，因為在資料庫層級設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，可讓您將資料庫與變更的設定，與會影響執行個體上所有其他資料庫的預設值相隔開。  
  
-   指定備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會利用慣用的備份複本，排定備份時程。 若要判斷目前的複本是否為慣用的備份複本，請使用[sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函式。  
  
-   如果將次要複本設定為慣用的複本，請將此複本設定為至少具有唯讀連接存取。 不支援無法對次要資料庫進行連接存取的可用性群組。  如需詳細資訊，請參閱 [設定可用性複本上的唯讀存取 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
-   如果在設定可用性群組之後設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會嘗試複製以此可用性群組為基礎的所有現有備份，並複製到儲存體容器。  如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]找不到或無法存取現有的備份，則會排程進行完整資料庫備份。 這樣做的原因主要是為了最佳化可用性群組資料庫的備份作業。  
  
-   您可能要考慮停用的執行個體層級設定，如果您要建立新的可用性資料庫，而且您不想要套用至資料庫的執行個體層級設定  
  
-   當使用加密時，請針對所有複本使用相同的憑證。 這樣萬一容錯移轉或還原到不同的複本時，有助於進行持續和不中斷的備份作業。  
  
#### <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>啟用及設定可用性資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 此教學課程說明為電腦 Node1 和 Node2 上資料庫 (AGTestDB) 啟用及設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的步驟，後面接著啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]健康情況之監視功能的步驟。  
  
1.  **建立 Windows Azure 儲存體帳戶：** 備份會儲存在 Windows Azure Blob 儲存體服務。 如果您目前沒有 Windows Azure 儲存體帳戶，您必須先建立一個帳戶。 如需詳細資訊，請參閱 <<c0> [ 建立 Windows Azure 儲存體帳戶](http://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)。 記下儲存體帳戶的儲存體帳戶名稱、存取金鑰和 URL。 儲存體帳戶名稱和存取金鑰資訊可用來建立 SQL 認證。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會在備份作業期間使用 SQL 認證來驗證儲存體帳戶。  
  
2.  **建立 SQL 認證：** 建立 SQL 認證，使用做為身分識別和儲存體存取金鑰的儲存體帳戶的名稱，做為密碼。  
  
3.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Agent 設定為自動執行，以確保能定期執行備份作業。  
  
4.  **決定保留期限：** 決定您想要備份檔案的保留期限。 保留週期的指定單位為天，範圍從 1 到 30。 保留週期可決定資料庫的復原能力時間範圍。  
  
5.  **建立要用於備份期間加密憑證或非對稱金鑰：** 上的第一個節點 Node1，建立憑證，然後將它匯出至檔案，使用[BACKUP CERTIFICATE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)... 在 Node2 上，使用從 Node1 匯出的檔案建立憑證。 如需有關如何從檔案建立憑證的詳細資訊，請參閱中的範例[CREATE CERTIFICATE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)。  
  
6.  **啟用及設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]Node1 上的 AGTestDB 的：** 啟動 SQL Server Management Studio 並連接到 Node1 安裝可用性資料庫上的執行個體。 在您根據需求修改資料庫名稱、儲存體 URL、SQL 認證和保留週期的值之後，從查詢視窗執行下列陳述式：  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     如需有關建立憑證以進行加密的詳細資訊，請參閱 <<c0>  **建立備份憑證**中的步驟[Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)。  
  
7.  **啟用及設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]Node2 上的 AGTestDB:** 啟動 SQL Server Management Studio 並連接到 Node2 上安裝可用性資料庫的執行個體。 在您根據需求修改資料庫名稱、儲存體 URL、SQL 認證和保留週期的值之後，從查詢視窗執行下列陳述式：  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 已在您指定的資料庫上啟用。 資料庫上的備份作業可能需要 15 分鐘才會開始執行。 此備份會在慣用的備份複本上進行。  
  
8.  **檢閱延伸事件預設設定：** 在複本上執行下列 TRANSACT-SQL 陳述式，以檢閱擴充事件組態[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用來排程備份。 這通常是資料庫所屬之可用性群組的慣用備份複本設定。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     預設會顯示已經啟用 Admin、Operational 和 Analytical 通道事件，且無法予以停用。 這應該足以監視需要手動介入的事件。  您可以啟用偵錯事件，不過這些通道包含[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用來偵測及解決問題的資訊和偵錯事件。 如需詳細資訊，請參閱 <<c0> [ 監視 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
9. **啟用及設定健全狀態通知：** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。  若要接收這類通知，必須啟用 [執行預存程序]，以建立 SQL Server Agent 工作。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知接收備份錯誤和警告：** 從 [查詢] 視窗中，執行下列 TRANSACT-SQL 陳述式：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         如需完整的範例指令碼和詳細資訊，請參閱[監視 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
10. **檢視 Windows Azure 儲存體帳戶中的備份檔案：** 從 SQL Server Management Studio 或 Azure 管理入口網站連接到儲存體帳戶。 您會看到裝載設定為使用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的資料庫之 SQL Server 執行個體的容器。 您也會在啟用資料庫之 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的 15 分鐘內，看到資料庫和記錄備份。  
  
11. **監視健康狀態：** 您可以透過先前設定的電子郵件通知進行監視，或主動監視記錄的事件。 以下是用於檢視事件的一些 Transact-SQL 陳述式範例：  
  
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
    event varchar (512),  
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
  
 本節所描述的步驟是針對第一次在資料庫上設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 您可以修改現有的組態使用相同的系統預存程序**smart_admin.sp_set_db_backup**並提供新的值。 如需詳細資訊，請參閱 < [SQL Server Managed Backup to Windows Azure-Retention and Storage Settings](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>從 AlwaysOn 可用性群組組態移除資料庫時的考量  
 如果資料庫從 AlwaysOn 可用性群組組態移除，且現在是獨立的資料庫，建議您這麼做設定使用的備份[smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)。 當您以此方式建立資料庫備份時，其會建立新的備份鏈結，且檔案會置於執行個體專屬的容器中，而不是放在可用性容器中 (當資料庫是可用性群組的一部分時，備份會儲存於其中)。  
  
> [!WARNING]  
>  在此情況下，從可用性群組狀態有所變更前的備份來復原資料庫的能力，則無法保證。  
  
  
