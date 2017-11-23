---
title: "RESTORE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE DATABASE
- RESTORE_TSQL
- RESTORE_DATABASE_TSQL
- RESTORE
- RESTORE_LOG_TSQL
- RESTORE LOG
dev_langs: TSQL
helpviewer_keywords:
- RESTORE DATABASE, see RESTORE statement
- full backups [SQL Server]
- RECOVERY option
- database snapshots [SQL Server], reverting to
- STOPAT syntax
- differential backups, RESTORE statement
- point in time recovery [SQL Server]
- restoring [SQL Server]
- NORECOVERY option
- online restores [SQL Server], RESTORE statement
- moving databases
- RESTORE statement, syntax
- cross-platform restores
- restoring databases [SQL Server], options
- RESTORE statement
- snapshots [SQL Server database snapshots], reverting to
- reverting database snapshots
- transaction log backups [SQL Server], RESTORE statement
- RESTORE LOG, see RESTORE statement
ms.assetid: 877ecd57-3f2e-4237-890a-08f16e944ef1
caps.latest.revision: "248"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b5f6424589d13652095b43ffcefa63e8916ecf39
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="restore-statements-transact-sql"></a>RESTORE 陳述式 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  還原利用 BACKUP 命令取得的備份。 此命令可讓您執行以下還原案例：  
  
-   從完整資料庫備份還原整個資料庫 (完整還原)。  
  
-   還原部分資料庫 (部分還原)。  
  
-   將特定檔案或檔案群組還原到資料庫 (檔案還原)。  
  
-   將特定頁面還原到資料庫 (分頁還原)。  
  
-   將交易記錄還原到資料庫 (交易記錄還原)。  
  
-   將資料庫還原到資料庫快照集所擷取的時間點。  
  
 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]還原案例，請參閱[還原和復原概觀 &#40;SQL Server &#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  如需有關引數說明的詳細資訊，請參閱[RESTORE 引數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).   從另一個執行個體還原資料庫時，請考慮 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)中的資訊。
  
> **注意：**如需從 Windows Azure Blob 儲存體服務進行還原的詳細資訊，請參閱[SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 [ FROM <backup_device> [ ,...n ] ]  
 [ WITH   
   {  
    [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
   | ,  <general_WITH_options> [ ,...n ]  
   | , <replication_WITH_option>  
   | , <change_data_capture_WITH_option>  
   | , <FILESTREAM_WITH_option>  
   | , <service_broker_WITH options>   
   | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence  
-- of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
      ] [ ,...n ]   
[;]  
  
--To Restore Specific Files or Filegroups:   
RESTORE DATABASE { database_name | @database_name_var }   
   <file_or_filegroup> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
   {  
      [ RECOVERY | NORECOVERY ]  
      [ , <general_WITH_options> [ ,...n ] ]  
   } [ ,...n ]   
[;]  
  
--To Restore Specific Pages:   
RESTORE DATABASE { database_name | @database_name_var }   
   PAGE = 'file:page [ ,...n ]'   
 [ , <file_or_filegroups> ] [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
       NORECOVERY     
      [ , <general_WITH_options> [ ,...n ] ]  
[;]  
  
--To Restore a Transaction Log:  
RESTORE LOG { database_name | @database_name_var }   
 [ <file_or_filegroup_or_pages> [ ,...n ] ]  
 [ FROM <backup_device> [ ,...n ] ]   
 [ WITH   
   {  
     [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
    | ,  <general_WITH_options> [ ,...n ]  
    | , <replication_WITH_option>  
    | , \<point_in_time_WITH_options—RESTORE_LOG>   
   } [ ,...n ]  
 ]   
[;]  
  
--To Revert a Database to a Database Snapshot:     
RESTORE DATABASE { database_name | @database_name_var }   
FROM DATABASE_SNAPSHOT = database_snapshot_name   
  
<backup_device>::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
 | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Windows Azure Blob. Although Windows Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seemless restore experince for all the three devices.  
<files_or_filegroups>::=   
{   
   FILE = { logical_file_name_in_backup | @logical_file_name_in_backup_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }   
 | READ_WRITE_FILEGROUPS  
}   
  
<general_WITH_options> [ ,...n ]::=   
--Restore Operation Options  
   MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
 | REPLACE   
 | RESTART   
 | RESTRICTED_USER  | CREDENTIAL  
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
 | BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }   
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
<replication_WITH_option>::=  
 | KEEP_REPLICATION   
  
<change_data_capture_WITH_option>::=  
 | KEEP_CDC  
  
<FILESTREAM_WITH_option>::=  
 | FILESTREAM ( DIRECTORY_NAME = directory_name )  
  
<service_broker_WITH_options>::=   
 | ENABLE_BROKER   
 | ERROR_BROKER_CONVERSATIONS   
 | NEW_BROKER  
  
\<point_in_time_WITH_options—RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options—RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
  
```  
  
## <a name="arguments"></a>引數  
 如需引數的描述，請參閱[RESTORE 引數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="about-restore-scenarios"></a>關於還原狀況  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援各種還原狀況：  
  
-   完整資料庫還原  
  
     還原整個資料庫，從完整資料庫備份開始，後面可能接著還原差異資料庫備份 (和記錄備份)。 如需詳細資訊，請參閱[完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) 或[完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)。  
  
-   檔案還原  
  
     還原多個檔案群組資料庫中的檔案或檔案群組。 請注意，在簡單復原模式之下，檔案必須屬於唯讀檔案群組。 在完整檔案還原之後，便可以還原差異檔案備份。 如需詳細資訊，請參閱[檔案還原 &#40;完整復原模式 &#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)和[檔案還原 &#40;簡單復原模式 &#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md).  
  
-   分頁還原  
  
     還原個別頁面。 只有完整復原模式和大量記錄復原模式會使用分頁還原。 如需詳細資訊，請參閱[還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)。  
  
-   分次還原  
  
     分段還原資料庫，從主要檔案群組及一個或多個次要檔案群組開始。 分次還原從使用 PARTIAL 選項且指定還原一個或多個次要檔案群組的 RESTORE DATABASE 開始。 如需詳細資訊，請參閱[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
-   僅限復原  
  
     復原已與資料庫一致的資料，只需要使其成為可用。 如需詳細資訊，請參閱[復原資料庫而不還原資料 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)。  
  
-   交易記錄還原。  
  
     在完整或大量記錄復原模式之下，您必須還原記錄備份，以到達所需要的復原點。 如需有關還原記錄備份的詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server &#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
-   Always On 可用性群組準備可用性資料庫  
  
     如需詳細資訊，請參閱[針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)。  
  
-   為資料庫鏡像準備鏡像資料庫  
  
     如需詳細資訊，請參閱 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
-   線上還原  
  
    > **注意：**的 Enterprise 版本中才允許線上還原[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     當支援線上還原時，如果資料庫在線上，檔案還原和分頁還原會自動成為線上還原，另外，也會在分次還原的初始階段之後，還原次要檔案群組。  
  
    > **注意：**線上還原可能涉及[延遲交易](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)。  
  
     如需詳細資訊，請參閱[線上還原 &#40;SQL Server &#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
## <a name="additional-considerations-about-restore-options"></a>關於 RESTORE 選項的其他考量  
  
### <a name="discontinued-restore-keywords"></a>已停止的 RESTORE 關鍵字  
 下列關鍵字在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中已停止：  
  
|已停止的關鍵字|取代者|取代關鍵字的範例|  
|--------------------------|------------------|------------------------------------|  
|LOAD|RESTORE|`RESTORE DATABASE`|  
|TRANSACTION|LOG|`RESTORE LOG`|  
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|  
  
### <a name="restore-log"></a>RESTORE LOG  
 RESTORE LOG 可以包括一份檔案清單，讓您在向前復原期間建立檔案。 如果記錄備份包含檔案加入資料庫時所撰寫的記錄檔記錄，便使用這個項目。  
  
> **注意：**對於使用完整或大量記錄復原模式的資料庫，在大部分情況下您必須備份記錄結尾還原資料庫之前。 除非 RESTORE DATABASE 陳述式包含 WITH REPLACE 或 WITH STOPAT 子句 (必須指定在資料備份結束之後發生的時間或交易)，否則如果沒有先備份記錄結尾便還原資料庫，就會產生錯誤。 如需結尾記錄備份的詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
### <a name="comparison-of-recovery-and-norecovery"></a>比較 RECOVERY 和 NORECOVERY  
 RESTORE 陳述式利用 [ RECOVERY | NORECOVERY ] 選項來控制回復：  
  
-   NORECOVERY 指定不進行回復。 這使向前復原能夠繼續循序執行下一個陳述式。  
  
     在這個情況下，還原順序可以還原其他備份，並將它們向前復原。  
  
-   RECOVERY (預設值) 表示在完成目前備份的向前復原之後，應該執行回復。  
  
     復原資料庫需要整個設定所還原的資料 (*向前復原集*) 是與資料庫一致。 如果向前復原集尚未向前復原到足以與資料庫一致的範圍，且指定了 RECOVERY，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會發出錯誤。  
  
## <a name="compatibility-support"></a>相容性支援  
 備份**主要**，**模型**和**msdb**所建立的使用較早版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無法還原[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
> **注意：**否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份還原到較早版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]比建立備份時的版本。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每一個版本都會使用與舊版不同的預設路徑。 因此，若要還原在舊版備份之預設位置中所建立的資料庫，就必須使用 MOVE 選項。 有關新預設路徑的詳細資訊，請參閱[檔案位置的預設和具名執行個體的 SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 將舊版資料庫還原成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，資料庫會自動升級。 通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據  **upgrade_option** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為匯入 (**upgrade_option** = 2) 或重建 (**upgrade_option** = 0)，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 若要變更 **upgrade_option** 伺服器屬性的設定，請使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)。  
  
 當資料庫第一次連接或還原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時，資料庫主要金鑰複本 (由服務主要金鑰加密) 尚未儲存在伺服器中。 您必須利用 **OPEN MASTER KEY** 陳述式來解密資料庫主要金鑰 (DMK)。 DMK 解密之後，您便可以選擇利用 **ALTER MASTER KEY REGENERATE** 陳述式來提供服務主要金鑰 (SMK) 所加密的 DMK 複本給伺服器，以在未來啟用自動解密。 當資料庫從舊版升級時，應該會重新產生 DMK 以使用較新的 AES 演算法。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新產生 DMK 金鑰以升級至 AES 所需的時間是取決於 DMK 所保護的物件數目而定。 重新產生 DMK 金鑰以升級至 AES 只需執行一次，且不會影響金鑰循環策略中後續的重新產生。  
  
## <a name="general-remarks"></a>一般備註  
 在離線還原期間，如果指定的資料庫在使用中，RESTORE 會在一小段延遲之後，強迫使用者結束作業。 如果是非主要檔案群組的線上還原，除非正在還原的檔案群組在離線中，否則，資料庫會保持使用中的狀態。 還原的資料會取代指定之資料庫中的任何資料。  
  
 如需資料庫復原的詳細資訊，請參閱[還原和復原概觀 &#40;SQL Server &#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
 只要作業系統支援資料庫的定序，便可以執行跨平台的還原作業，即使在不同類型的處理器之間，也是如此。  
  
 RESTORE 可以在發生錯誤之後，重新啟動。 另外，您也可以指示 RESTORE 不論是否發生錯誤，一律繼續作業，它會盡可能還原多一點的資料 (請參閱 CONTINUE_AFTER_ERROR 選項)。  
  
 在明確或隱含的交易中，不允許使用 RESTORE。  
  
 還原損毀**主要**資料庫必須利用特殊程序。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
 還原資料庫會清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取。 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
 若要還原可用性資料庫，請先將資料庫還原至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後再將資料庫新增至可用性群組。  
  
## <a name="interoperability"></a>互通性  
  
### <a name="database-settings-and-restoring"></a>資料庫設定和還原  
 在還原期間，大部分可以利用 ALTER DATABASE 來設定的資料庫選項都會重設為備份結束時的有效值。  
  
 不過，使用 WITH RESTRICTED_USER 選項會覆寫使用者存取選項設定的這個行為。 這項設定一律設在 RESTORE 陳述式之後，其中包括 WITH RESTRICTED_USER 選項。  
  
### <a name="restoring-an-encrypted-database"></a>還原加密資料庫  
 若要還原加密的資料庫，您必須能夠存取之前用來加密資料庫的憑證或非對稱金鑰。 如果沒有該憑證或非對稱金鑰，就無法還原資料庫。 因此，只要需要備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>還原啟用 Vardecimal 儲存的資料庫  
 備份和還原可正確地搭配**vardecimal**儲存格式。 如需有關**vardecimal**儲存格式，請參閱[sp_db_vardecimal_storage_format &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
### <a name="restore-full-text-data"></a>還原全文檢索資料  
 在完整還原期間，全文檢索資料會與其他資料庫資料一起還原。 當使用正規 `RESTORE DATABASE database_name FROM backup_device` 語法時，還原資料庫檔也會還原全文檢索檔案。  
  
 您也可以利用 RESTORE 陳述式，將全文檢索資料還原到替代位置，以及執行全文檢索資料的差異還原、檔案和檔案群組還原及差異檔案和檔案群組還原。 另外，RESTORE 只能連同資料庫資料一起還原全文檢索檔案。  
  
> **注意：**全文檢索目錄匯入從[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]仍然會視為資料庫檔案。 對於這些檔案而言，備份全文檢索目錄的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 程序會維持適用狀態，不過不再需要於備份作業期間暫停和繼續。 如需詳細資訊，請參閱[備份與還原全文檢索目錄](http://go.microsoft.com/fwlink/?LinkId=107381)。  
  
## <a name="metadata"></a>中繼資料  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含備份與還原記錄資料表，以便用來為每個伺服器執行個體進行追蹤備份和還原活動。 當執行還原時，也會修改備份記錄資料表。 如需有關這些資料表，請參閱[備份歷程記錄與標頭資訊 &#40;SQL Server &#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md).  
  
##  <a name="REPLACEoption"></a>REPLACE 選項影響  
 REPLACE 不應經常使用，而且只應在審慎考量之後使用。 還原通常可以防止意外將資料庫覆寫成不同資料庫。 如果 RESTORE 陳述式中指定的資料庫已經存在於目前伺服器，而且指定的資料庫系列 GUID 與備份組中記錄的資料庫系列 GUID 不同，將不會還原資料庫。 這是重要的防護措施。  
  
 REPLACE 選項會覆寫還原通常會執行的數項重要安全檢查。 會覆寫的檢查如下：  
  
-   使用從其他資料庫建立的備份來還原現有資料庫。  
  
     使用 REPLACE 選項，即使指定的資料庫名稱與備份組中所記錄的資料庫名稱不同，還原仍可讓您以備份組中的任何資料庫覆寫現有的資料庫。 這可能會導致意外將資料庫覆寫成不同資料庫。  
  
-   使用完整或大量記錄復原模式來還原資料庫，而這兩種模式都未取得結尾記錄備份也未使用 STOPAT 選項。  
  
     使用 REPLACE 選項，您可能會遺失已認可的記錄，因為最近寫入的記錄尚未被備份。  
  
-   覆寫現有的檔案。  
  
     例如，作業失誤可能導致覆寫到錯誤的檔案類型 (例如 .xls 檔案)，或覆寫到其他資料庫 (目前不在線上) 正在使用的檔案。 如果覆寫了現有檔案，即使還原的資料庫是完整的，仍有可能遺失任意資料。  
  
## <a name="redoing-a-restore"></a>重做還原  
 您不可能恢復還原的效果；不過，您可以針對個別檔案重新開始，以消除資料複製和向前復原的效果。 若要重新開始，請還原所需要的檔案，再重新執行向前復原。 例如，如果您不慎還原太多記錄備份，超出您想要的停止點，您就必須重新開始這個順序。  
  
 您可以還原受影響之檔案的整個內容來中止和重新開始還原順序。  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>將資料庫還原為資料庫快照集  
 A*還原資料庫作業*（利用 DATABASE_SNAPSHOT 選項指定） 會採用及時取回完整的來源資料庫還原到資料庫快照集，也就覆寫來源資料庫與點的資料在指定的資料庫快照集中維護的時間。 目前能存在的快照集只限於您要還原的目標快照集。 之後，還原作業會重建記錄檔 (因此，您無法稍後再將還原的資料庫向前復原到發生使用者錯誤的那個時間點)。  
  
 您只會失去建立快照集之後的資料庫更新資料。 還原資料庫的中繼資料與建立快照集時的中繼資料相同。 不過，還原為快照集會卸除所有全文檢索目錄。  
  
 從資料庫快照集還原的用途，並不在於復原媒體。 資料庫快照集不像正規的備份組，它是不完整的資料庫檔案副本。 如果資料庫或資料庫快照集損毀，可能就無法從快照集還原。 此外，即使可以還原，但是在損毀的情況下還原也不太可能會更正問題。  
  
### <a name="restrictions-on-reverting"></a>還原限制  
 在下列狀況下，不支援還原：  
  
-   來源資料庫包含任何唯讀或壓縮的檔案群組。  
  
-   建立快照集時原本處於線上狀態的所有檔案，現在都變成離線狀態。  
  
-   目前已經有一個以上的資料庫快照集。  
  
 如需詳細資訊，請參閱[將資料庫還原成資料庫快照集](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)。  
  
## <a name="security"></a>安全性  
 備份作業可以選擇性地指定媒體集的密碼及 (或) 備份組的密碼。 當在媒體集或備份組上定義密碼時，您必須在 RESTORE 陳述式中，指定一個或多個正確的密碼。 這些密碼可以防止他人利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具，在未獲授權的情況下，在媒體上執行還原作業及附加備份組。 不過，BACKUP 陳述式的 FORMAT 選項可以覆寫密碼所保護的媒體。  
  
> [!IMPORTANT]  
>  這個密碼所提供的保護很弱。 這是為了防止已獲授權或未獲授權的使用者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具進行不正確的還原。 它無法防止透過其他方式或以取代密碼的方式來讀取備份資料。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]保護備份的最佳作法是將備份磁帶存放在安全的位置，或備份至足夠的存取控制清單 (Acl) 所保護的磁碟檔案。 ACL 應該設在備份建立所在的根目錄下。  
>   
>  SQL Server 備份及還原與 Windows Azure Blob 儲存體的特定資訊，請參閱[SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
### <a name="permissions"></a>Permissions  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此，因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="examples"></a> 範例  
 所有範例都假設已執行完整資料庫備份。  
  
 RESTORE 範例包括：  
  
-   A. [還原完整資料庫](#restoring_full_db)  
  
-   B. [還原完整和差異資料庫備份](#restoring_full_n_differential_db_backups)  
  
-   C. [利用 RESTART 語法還原資料庫](#restoring_db_using_RESTART)  
  
-   D. [還原資料庫和移動檔案](#restoring_db_n_move_files)  
  
-   E. [使用備份與還原複製資料庫](#copying_db_using_bnr)  
  
-   F. [使用 STOPAT 還原至時間點](#restoring_to_pit_using_STOPAT)  
  
-   G. [交易記錄還原到標記](#restoring_transaction_log_to_mark)  
  
-   H. [利用 TAPE 語法還原](#restoring_using_TAPE)  
  
-   I. [使用 FILE 和 FILEGROUP 語法還原](#restoring_using_FILE_n_FG)  
  
-   J. [從資料庫快照集還原](#reverting_from_db_snapshot)  
  
-   K. [從 Microsoft Azure Blob 儲存體服務進行還原](#Azure_Blob)  
  
> **注意：**如需其他範例，請參閱還原的如何主題中所列[還原和復原概觀 &#40;SQL Server &#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
###  <a name="restoring_full_db"></a> A. 還原完整資料庫  
 下列範例會從 `AdventureWorksBackups` 邏輯備份裝置還原完整的資料庫備份。 如需建立這個裝置的範例，請參閱[備份裝置](../../relational-databases/backup-restore/backup-devices-sql-server.md)。  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> **注意：**資料庫使用完整或大量記錄復原模式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要在大部分情況下，您還原資料庫之前備份記錄結尾。 如需詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> B. 還原完整和差異資料庫備份  
 下列範例會還原完整資料庫備份，接著再從包含這兩種備份 `Z:\SQLServerBackups\AdventureWorks2012.bak` 備份裝置進行差異備份。 將進行還原的完整備份是裝置上的第六個備份組 (`FILE = 6`)，而差異資料庫備份是裝置上的第九個備份組 (`FILE = 9`)。 只要差異備份一完成復原，資料庫就完成復原。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> C. 使用 RESTART 語法還原資料庫  
 下列範例會利用 `RESTART` 選項來重新啟動因伺服器斷電而中斷的 `RESTORE` 作業。  
  
```  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> D. 還原資料庫和移動檔案  
 下列範例會還原完整的資料庫和交易記錄，並將還原的資料庫移至 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` 目錄。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH NORECOVERY,   
      MOVE 'AdventureWorks2012_Data' TO   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.mdf',   
      MOVE 'AdventureWorks2012_Log'   
TO 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.ldf';  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH RECOVERY;  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="copying_db_using_bnr"></a> E. 使用 BACKUP 和 RESTORE 複製資料庫  
 下列範例使用 `BACKUP` 和 `RESTORE` 陳述式建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的副本。 `MOVE` 陳述式會使資料和記錄檔還原到指定的位置。 `RESTORE FILELISTONLY` 陳述式是用來決定資料庫中所要還原的檔案數目及名稱。 新資料庫複本的名稱是 `TestDB`。 如需詳細資訊，請參閱 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups ;  
  
RESTORE FILELISTONLY   
   FROM AdventureWorksBackups ;  
  
RESTORE DATABASE TestDB   
   FROM AdventureWorksBackups   
   WITH MOVE 'AdventureWorks2012_Data' TO 'C:\MySQLServer\testdb.mdf',  
   MOVE 'AdventureWorks2012_Log' TO 'C:\MySQLServer\testdb.ldf';  
GO  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> F. 使用 STOPAT 還原至時間點  
 下列範例會將資料庫還原至 `12:00 AM` `April 15, 2020` 時的狀態，並顯示含有多個記錄備份的還原作業。 在備份裝置 `AdventureWorksBackups`上，要還原的完整資料庫備份是裝置上的第三個備份組 (`FILE = 3`)，第一個記錄備份是第四個備份組 (`FILE = 4`)，而第二個記錄備份是第五個備份組 (`FILE = 5`)。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a>G. 將交易記錄還原到標記  
 下列範例會將交易記錄還原到名為 `ListPriceUpdate`的標示交易中之標示。  
  
```  
USE AdventureWorks2012  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master;  
GO  
  
RESTORE DATABASE AdventureWorks2012  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'UPDATE Product list prices';  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_using_TAPE"></a>H. 使用 TAPE 語法進行還原  
 下列範例會從 `TAPE` 備份裝置還原完整的資料庫備份。  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a>我。 使用 FILE 與 FILEGROUP 語法進行還原  
 下列範例會還原名為 `MyDatabase` 的資料庫，此資料庫擁有兩個檔案，一個次要檔案群組和一個交易記錄， 而且使用完整復原模式。  
  
 資料庫備份是在名為 `MyDatabaseBackups` 的邏輯備份裝置上，媒體集中的第九個備份組。 接下來是三個記錄備份，它們分別位於 `10` 裝置的後三個備份組中 (`11`、`12` 和 `MyDatabaseBackups`)，並且利用 `WITH NORECOVERY` 而還原。 在還原最後一個記錄備份之後，資料庫就可以復原。  
  
> **注意：**當做個別的步驟，以降低過早復原您執行復原時，已還原之前的所有記錄備份。  
  
 請注意，在 `RESTORE DATABASE` 中有兩種 `FILE` 選項類型。 在備份裝置名稱之前的 `FILE` 選項指定要從備份組還原之資料庫檔案的邏輯檔案名稱；例如，`FILE = 'MyDatabase_data_1'`。 這個備份組並非媒體集中的第一個資料庫備份；因此，它在媒體集中的位置是利用 `FILE` 子句中的 `WITH` 選項 `FILE=9` 指出。  
  
```  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'new_customers'  
   FROM MyDatabaseBackups  
   WITH   
      FILE = 9,  
      NORECOVERY;  
GO  
-- Restore the log backups.  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 10,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 11,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 12,   
      NORECOVERY;  
GO  
--Recover the database:  
RESTORE DATABASE MyDatabase WITH RECOVERY;  
GO  
```  
  
 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a>J. 從資料庫快照集還原  
 下列範例會將資料庫還原到某個資料庫快照集。 這個範例假設資料庫目前只有一個快照集。 如需如何建立這個資料庫快照集的範例，請參閱[建立資料庫快照集 &#40;TRANSACT-SQL &#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
> **注意：**正在還原成快照集卸除所有全文檢索目錄。  
  
```  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
 如需詳細資訊，請參閱[將資料庫還原成資料庫快照集](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)。  

 [&#91;頂端的範例 &#93;](#examples)  
  
###  <a name="Azure_Blob"></a>K。 從 Microsoft Azure Blob 儲存體服務進行還原  
下列範例牽涉到使用 Microsoft Azure 儲存體服務。  儲存體帳戶名稱為 `mystorageaccount`。  資料檔案的容器會呼叫`myfirstcontainer`。  備份檔案的容器會呼叫`mysecondcontainer`。  已建立具有讀取、 寫入、 刪除和清單中，針對每個容器的權限的預存的存取原則。  建立使用共用存取簽章與預存存取原則相關聯的 SQL Server 認證。  SQL Server 備份及還原與 Microsoft Azure Blob 儲存體的特定資訊，請參閱[SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  

**K1。從 Microsoft Azure 儲存體服務還原完整資料庫備份**  
完整資料庫備份，位於`mysecondcontainer`的`Sales`將會還原到`myfirstcontainer`。  `Sales`目前不存在伺服器上。 
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2。從 Microsoft Azure 儲存體服務還原完整資料庫備份至本機儲存體**  
完整資料庫備份，位於`mysecondcontainer`的`Sales`將會還原到本機儲存體。  `Sales`目前不存在伺服器上。
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3。從本機儲存體還原完整資料庫備份至 Microsoft Azure 儲存體服務**  
```
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
 [&#91;頂端的範例 &#93;](#examples)  
  
## <a name="much-more-information"></a>更多的資訊!!  
 - [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [備份和還原系統資料庫 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
 - [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
 - [備份並還原全文檢索目錄與索引](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 - [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 - [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 - [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 - [RESTORE REWINDONLY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 - [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 - [RESTORE FILELISTONLY (TRANSACT-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
 - [RESTORE HEADERONLY (TRANSACT-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
 - [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
