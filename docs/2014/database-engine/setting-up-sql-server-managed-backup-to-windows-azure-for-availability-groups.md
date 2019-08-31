---
title: 針對可用性群組設定 SQL Server 受控備份至 Azure |Microsoft Docs
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
ms.openlocfilehash: aa2cbce81827c9085f87112b366d532077915f58
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176094"
---
# <a name="setting-up-sql-server-managed-backup-to-azure-for-availability-groups"></a>針對可用性群組設定 SQL Server 受控備份至 Azure
  本主題是設定參與 AlwaysOn 可用性群組之資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之教學課程。  
  
## <a name="availability-group-configurations"></a>可用性群組組態  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可用性群組資料庫支援, 不論複本是設定在內部部署或完全在 Azure 上, 或是在內部部署與一或多個 Azure 虛擬機器之間的混合式執行。 但是，您可能必須針對一個或多個實作考量以下事項：  
  
-   記錄備份頻率:記錄備份的頻率同時是時間和記錄檔的成長。 例如，系統會每隔兩個小時取得一次記錄備份，除非在這兩個小時內使用的記錄空間為 5 MB 或更多。 這適用於所有實作，不論是內部部署、雲端還是混合式。  
  
-   網路頻寬:這適用于複本位於不同實體位置 (例如在混合式雲端中), 或僅限雲端設定中不同 Azure 區域的執行。 網路頻寬可能會影響次要複本的延遲，而且如果次要複本設定為同步複寫，這可能會導致主要複本上的記錄增加。 如果次要複本設定為同步複寫，次要複本可能會因為網路延遲的緣故而跟不上同步，萬一容錯移轉到次要複本就可能會發生資料遺失。  
  
### <a name="configuring-includess_smartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>設定可用性資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
 **權限：**  
  
-   需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權`EXECUTE` , 以及**sp_delete_backuphistory**預存程式的許可權。  
  
-   需要**選取** 權限 **smart_admin.fn_get_current_xevent_settings** 函式。  
  
-   需要`EXECUTE` **smart_admin 的 sp_get_backup_diagnostics**預存程式的許可權。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  
  
-   需要`EXECUTE` `smart_admin.sp_set_instance_backup`和預`smart_admin.sp_backup_master_switch`存程式的許可權。  
  
 以下是使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定 AlwaysOn 可用性群組的基本步驟。 本主題稍後將說明詳細的逐步教學課程。  
  
1.  建立可用性群組之後，請設定慣用的備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會使用可用性群組的這項設定來決定用於備份的複本。 如需如何設定備份喜好設定的逐步指示, 請參閱[在可用性複本&#40; &#41;上設定備份 SQL Server](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。  如果您要建立新的 AlwaysOn 可用性群組, 請參閱[具有 AlwaysOn 可用性群組&#40;SQL Server&#41;的消費者入門](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)。  
  
2.  設定次要複本的唯讀連接存取。 如需如何設定唯讀存取的逐步指示, 請參閱[設定可用性複本&#40;的唯讀存取 SQL Server&#41; ](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
3.  指定備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會使用慣用的備份複本設定來決定用於排程備份的資料庫。  若要判斷目前的複本是否為慣用的備份複本, 請使用[fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函數。  
  
4.  在每個複本[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上, 使用 sp_set_db_backup 預存**程式**來執行資料庫的設定。  
  
     [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] **故障[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]轉移後的行為:** 將會繼續運作, 並在容錯移轉事件之後維護備份副本和復原能力。 在容錯移轉之後，不需要採取特定的動作。  
  
#### <a name="considerations-and-requirements"></a>考量和需求：  
 針對參與 AlwaysOn 可用性群組的資料庫設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]需要進行特定考量並符合特定需求。 以下是考量與需求清單：  
  
-   參與相同可用性群組之所有 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 節點上的所有資料庫，都應該具有相同的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]組態設定。 您可以在資料庫層級針對主要及所有複本設定相同的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態，或在參與可用性群組的所有節點上設定相同的預設[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定，來達成此目的。 建議在資料庫設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，因為在資料庫層級設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，可讓您將資料庫與變更的設定，與會影響執行個體上所有其他資料庫的預設值相隔開。  
  
-   指定備份複本。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會利用慣用的備份複本，排定備份時程。 若要判斷目前的複本是否為慣用的備份複本, 請使用[fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)函數。  
  
-   如果將次要複本設定為慣用的複本，請將此複本設定為至少具有唯讀連接存取。 不支援無法對次要資料庫進行連接存取的可用性群組。  如需詳細資訊，請參閱 [設定可用性複本上的唯讀存取 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
-   如果在設定可用性群組之後設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會嘗試複製以此可用性群組為基礎的所有現有備份，並複製到儲存體容器。  如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]找不到或無法存取現有的備份，則會排程進行完整資料庫備份。 這樣做的原因主要是為了最佳化可用性群組資料庫的備份作業。  
  
-   如果您要建立新的可用性資料庫, 而且不打算將實例層級設定套用至資料庫, 您可以考慮停用實例層級設定。  
  
-   當使用加密時，請針對所有複本使用相同的憑證。 這樣萬一容錯移轉或還原到不同的複本時，有助於進行持續和不中斷的備份作業。  
  
#### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>啟用及設定可用性資料庫的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 此教學課程說明為電腦 Node1 和 Node2 上資料庫 (AGTestDB) 啟用及設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的步驟，後面接著啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]健康情況之監視功能的步驟。  
  
1.  **建立 Azure 儲存體帳戶：** 這些備份會儲存在 Azure Blob 儲存體服務中。 如果您還沒有 Azure 儲存體帳戶, 您必須先建立它。 如需詳細資訊, 請參閱[建立 Azure 儲存體帳戶](http://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)。 記下儲存體帳戶的儲存體帳戶名稱、存取金鑰和 URL。 儲存體帳戶名稱和存取金鑰資訊可用來建立 SQL 認證。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會在備份作業期間使用 SQL 認證來驗證儲存體帳戶。  
  
2.  **建立 SQL 認證:** 使用儲存體帳戶的名稱做為身分識別, 並使用儲存體存取金鑰做為密碼, 以建立 SQL 認證。  
  
3.  **確認 SQL Server Agent 服務已啟動且在執行中：** 如果目前尚未執行 SQL Server Agent，請加以啟動。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 需要在執行個體上執行 SQL Server Agent，才能執行備份作業。  您可能需要將 SQL Agent 設定為自動執行，以確保能定期執行備份作業。  
  
4.  **決定保留期限：** 決定您想要用於備份檔案的保留期限。 保留週期的指定單位為天，範圍從 1 到 30。 保留週期可決定資料庫的復原能力時間範圍。  
  
5.  **建立要在備份期間用於加密的憑證或非對稱金鑰:** 在第一個節點節點1上建立憑證, 然後使用[備份憑證&#40;transact-sql&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)將它匯出至檔案。 在 Node2 上，使用從 Node1 匯出的檔案建立憑證。 如需從檔案建立憑證的詳細資訊, 請參閱[建立憑證&#40;transact-sql&#41;](/sql/t-sql/statements/create-certificate-transact-sql)中的範例。  
  
6.  **針對節點 1 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上的 AGTestDB 啟用和設定:** 啟動 SQL Server Management Studio, 然後連接到已安裝可用性資料庫之節點上的實例。 在您根據需求修改資料庫名稱、儲存體 URL、SQL 認證和保留週期的值之後，從查詢視窗執行下列陳述式：  
  
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
  
     如需建立憑證以進行加密的詳細資訊, 請參閱[建立加密備份](../relational-databases/backup-restore/create-an-encrypted-backup.md)中的**建立備份憑證**步驟。  
  
7.  **在節點 2 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上啟用和設定 AGTestDB:** 啟動 SQL Server Management Studio, 並連接到已安裝可用性資料庫之節點2上的實例。 在您根據需求修改資料庫名稱、儲存體 URL、SQL 認證和保留週期的值之後，從查詢視窗執行下列陳述式：  
  
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
  
8.  **檢閱延伸事件預設設定：** 在用來排程備份的複本[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上執行下列 transact-sql 語句, 以檢查擴充事件設定。 這通常是資料庫所屬之可用性群組的慣用備份複本設定。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     預設會顯示已經啟用 Admin、Operational 和 Analytical 通道事件，且無法予以停用。 這應該足以監視需要手動介入的事件。  您可以啟用偵錯事件，不過這些通道包含[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用來偵測及解決問題的資訊和偵錯事件。 如需詳細資訊, 請參閱[監視 SQL Server 受控備份至 Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
9. **啟用及設定健全狀態通知：** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的預存程序會建立代理程式作業，以針對可能需要注意的錯誤或警告傳送電子郵件通知。  若要接收這類通知，必須啟用 [執行預存程序]，以建立 SQL Server Agent 工作。 下列步驟描述啟用及設定電子郵件通知的程序：  
  
    1.  如果執行個體上尚未啟用，請設定 Database Mail。 如需詳細資訊，請參閱＜ [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)＞。  
  
    2.  設定 SQL Server Agent 通知使用 Database Mail。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
    3.  **啟用電子郵件通知接收備份錯誤和警告：** 從 [查詢] 視窗中，執行下列 Transact-SQL 陳述式：  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         如需詳細資訊和完整的範例腳本, 請參閱[監視 SQL Server 受控備份至 Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
10. **查看 Azure 儲存體帳戶中的備份檔案:** 從 SQL Server Management Studio 或 Azure 管理入口網站連線到儲存體帳戶。 您會看到裝載設定為使用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的資料庫之 SQL Server 執行個體的容器。 您也會在啟用資料庫之 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的 15 分鐘內，看到資料庫和記錄備份。  
  
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
  
 本節所描述的步驟是針對第一次在資料庫上設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 您可以使用相同的系統預存程式**smart_admin**來修改現有的設定, 並提供新的值。 如需詳細資訊, 請參閱[SQL Server 受控備份至 Azure-保留和儲存體設定](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>從 AlwaysOn 可用性群組組態移除資料庫時的考量  
 如果資料庫已從 AlwaysOn 可用性群組設定中移除, 而且現在是獨立的資料庫, 我們建議使用[smart_admin. sp_backup_on_demand &#40; &#41;transact-sql](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)來進行備份。 當您以此方式建立資料庫備份時，其會建立新的備份鏈結，且檔案會置於執行個體專屬的容器中，而不是放在可用性容器中 (當資料庫是可用性群組的一部分時，備份會儲存於其中)。  
  
> [!WARNING]  
>  在此情況下，從可用性群組狀態有所變更前的備份來復原資料庫的能力，則無法保證。  
  
  
