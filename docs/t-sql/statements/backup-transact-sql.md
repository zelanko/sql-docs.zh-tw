---
title: BACKUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
caps.latest.revision: 275
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7775dbaa4a8c28d9e7124b94c73f3b87c9e68838
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2018
ms.locfileid: "36943174"
---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  備份完整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以建立資料庫備份，或備份資料庫的一或多個檔案或檔案群組以建立檔案備份 (BACKUP DATABASE)。 同時，可在完整復原模式或大量記錄復原模式下備份資料庫的交易記錄，以建立記錄備份 (BACKUP LOG)。 

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL -- Not supporterd in SQL Database Managed Instance
           | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG -- Not supported in SQL Database Managed Instance
  { database_name | @database_name_var }  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | {   DISK -- Not supported in SQL Database Managed Instance
     | TAPE -- Not supported in SQL Database Managed Instance
     | URL } =   
     { 'physical_device_name' | @physical_device_name_var | 'NUL' }  
 }   
  
<MIRROR TO clause>::=  
 MIRROR TO <backup_device> [ ,...n ]  
  
<file_or_filegroup>::=  
 {  
   FILE = { logical_file_name | @logical_file_name_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
 }   
  
<read_only_filegroup>::=  
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
  
<general_WITH_options> [ ,...n ]::=   
--Backup Set Options  
   COPY_ONLY -- Only backup set option supported by SQL Database Managed Instance  
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  --Not supported in SQL Database Managed Instance
 | { EXPIREDATE = { 'date' | @date_var }   
        | RETAINDAYS = { days | @days_var } }   
  
--Media Set Options  
   { NOINIT | INIT }   
 | { NOSKIP | SKIP }   
 | { NOFORMAT | FORMAT }   
 | MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
  
--Tape Options. These are not supported in SQL Database Managed Instance
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options. These are not supported in SQL Database Managed Instance 
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>引數  

DATABASE  
 指定完整的資料庫備份。 如果指定了檔案和檔案群組清單，就只會備份這些檔案和檔案群組。 在完整或差異資料庫備份期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會備份足夠的交易記錄，以便在還原備份時，產生一致的資料庫。  
  
 當您還原 BACKUP DATABASE 所建立的備份 (「資料備份」) 時，就會還原整個備份。 只有記錄備份可以還原至備份內的特定時間或交易。  
  
> [!NOTE]  
> **master** 資料庫上只能執行完整資料庫備份。  
  
LOG **適用於：** SQL Server

 指定只備份交易記錄。 記錄的備份是從最後執行成功的記錄備份至目前的記錄結尾。 您必須先建立完整備份，才能建立第一個記錄備份。  
  
 您可以透過在 [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中指定 `WITH STOPAT`、`STOPATMARK` 或 `STOPBEFOREMARK`，以將記錄備份還原至備份內的特定時間或交易。  
  
> [!NOTE]  
>  建立典型的記錄備份之後，除非您指定 `WITH NO_TRUNCATE` 或 `COPY_ONLY`，否則有些交易記錄檔記錄會變成非使用中狀態。 當一個或多個虛擬記錄檔案中的所有記錄變成非使用中狀態之後，記錄會發生截斷。 如果記錄在例行的記錄備份之後並未截斷，可能會發生延遲記錄截斷。 如需詳細資訊，請參閱[可能會延遲記錄截斷的因素](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)。  
  
 { *database_name* | **@***database_name_var* } 是要備份交易記錄、部分資料庫或完整資料庫的來源資料庫。如果這個名稱是以變數 (**@***database_name_var*) 提供，就可將它指定為字串常數 (**@***database_name_var***=***database name*) 或字元字串資料類型的變數，但 **ntext** 或 **text** 資料類型除外。  
  
> [!NOTE]  
> 資料庫鏡像合作關係中的鏡像資料庫無法備份。  
  
\<file_or_filegroup> [ **,**...*n* ]  
 只能搭配 BACKUP DATABASE 使用，可用來指定要包含在檔案備份中的資料庫檔案或檔案群組，或是指定要包含在部分備份中的唯讀檔案或檔案群組。  
  
 FILE **=** { *logical_file_name* | **@***logical_file_name_var* }  
 這是指要包含在備份中的檔案邏輯名稱，或是其值等於該檔案邏輯名稱的變數。  
  
 FILEGROUP **=** { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
 這是指要包含在備份中的檔案群組邏輯名稱，或是其值等於該檔案群組邏輯名稱的變數。 在簡單復原模式之下，只允許唯讀檔案群組使用檔案群組備份。  
  
> [!NOTE]  
> 當資料庫備份因資料庫大小和效能需求而不可行時，請考慮使用檔案備份。 NUL 裝置可用來測試備份的效能，但不應用於生產環境。
  
 *n*  
 這是一個預留位置，表示可以在逗號分隔清單中指定多個檔案和檔案群組。 數目沒有限制。 
  
 如需詳細資訊，請參閱[完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 與[備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)。  
  
 READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { *logical_filegroup_name* | **@***logical_filegroup_name_var* } [ **,**...* n* ] ]  
 指定部分備份。 部分備份包含資料庫中所有的讀取/寫入檔案：主要檔案群組和任何一種讀取/寫入次要檔案群組，以及任何指定的唯讀檔案或檔案群組。  
  
 READ_WRITE_FILEGROUPS  
 指定要在部分備份進行備份的所有讀取/寫入檔案群組。 如果資料庫是唯讀的，READ_WRITE_FILEGROUPS 只會包括主要檔案群組。  
  
> [!IMPORTANT]  
> 使用 FILEGROUP 取代 READ_WRITE_FILEGROUPS 來明確列出讀取/寫入檔案群組，以建立檔案備份。  
  
 FILEGROUP = { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
這是指要包含在部分備份中的唯讀檔案群組邏輯名稱，或是其值等於該唯讀檔案群組邏輯名稱的變數。 如需詳細資訊，請參閱本主題前面的 "\<file_or_filegroup>"。
  
 *n*  
 這是一個預留位置，表示可以在逗號分隔清單中指定多個唯讀檔案群組。  
  
 如需部份備份的詳細資訊，請參閱[部份備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)。  
  
TO \<backup_device> [ **,**...*n* ] 指出隨附的[備份裝置](../../relational-databases/backup-restore/backup-devices-sql-server.md)集是未鏡像的媒體集，或是鏡像媒體集內的前幾個鏡像 (已針對其宣告了一或多個 MIRROR TO 子句)。  
  
\<backup_device> **適用於：** SQL Server 指定要針對備份作業使用的邏輯或實體備份裝置。  
  
 { *logical_device_name* | **@***logical_device_name_var* } **適用於：** SQL Server 是用來備份資料庫之備份裝置的邏輯名稱。邏輯名稱必須遵照識別碼的規則。如果備份裝置名稱是以變數 (@* logical_device_name_var *) 提供，就可將它指定為字串常數 (@* logical_device_name_var***=**) 或任何字元字串資料類型的變數，但 **ntext** 或 **text** 資料類型除外。  
  
 { DISK | TAPE | URL} **=** { **'***physical_device_name***'** | **@***physical_device_name_var* | 'NUL' } **適用於：** 磁碟、磁帶和 URL 適用於 SQL Server。 只有 URL 適用於 SQL Database 受控執行個體。指定磁碟檔案或磁帶裝置，或是 Windows Azure Blob 儲存體服務。 URL 格式可用來建立備份至 Windows Azure 儲存體服務。 如需詳細資訊和範例，請參閱[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。 如需教學課程，請參閱[教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)。 

> [!NOTE] 
> NUL 磁碟裝置將捨棄傳送給它的所有資訊，而且只應用於測試。 這不適用於生產環境。
  
> [!IMPORTANT]  
> 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 開始至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，當您備份至 URL 時，可以只備份到單一裝置。 為了在備份到 URL 時能夠備份到多部裝置，您必須使用 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，而且必須使用共用存取簽章 (SAS) 權杖。 如需建立共用存取簽章的範例，請參閱 [SQL Server 備份至 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) 和[在 Azure 儲存體上使用 Powershell 搭配共用存取簽章 (SAS) 權杖來簡化 SQL 認證的建立](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx) \(英文\)。  
  
**URL 適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 和 SQL Database 受控執行個體。  
  
 在 BACKUP 陳述式內指定磁碟裝置之前，該裝置不需要存在。 如果實體裝置存在，且 BACKUP 陳述式並未指定 INIT 選項，就會將備份附加至裝置中。  
 
> [!NOTE] 
> NUL 裝置將捨棄傳送到此檔案的所有輸入，不過，備份仍會將所有頁面標記為已備份。
  
 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。  
  
> [!NOTE]  
> 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將移除 TAPE 選項。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 *n*  
 這是一個預留位置，表示可以在逗號分隔清單中指定最多達 64 個備份裝置。  
  
MIRROR TO \<backup_device> [ **,**...*n* ] 指定一組最多三個的次要備份裝置，其中每個裝置都會鏡像處理 TO 子句中所指定的備份裝置。 MIRROR TO 子句必須指定與 TO 子句相同的備份裝置類型和數目。 最大 MIRROR TO 子句數目是 3。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Enterprise 版本才提供這個選項。  
  
> [!NOTE]  
> 如果 MIRROR TO = DISK，BACKUP 會自動判斷磁碟裝置的適當區塊大小。 如需有關區塊大小的詳細資訊，請參閱這份資料表稍後的 "BLOCKSIZE"。  
  
\<backup_device> 請參閱本節前面的 "\<backup_device>"。
  
 *n*  
 這是一個預留位置，表示可以在逗號分隔清單中指定最多達 64 個備份裝置。 MIRROR TO 子句中的裝置數目必須等於 TO 子句中的裝置數目。  
  
 如需詳細資訊，請參閱本主題稍後[備註](#general-remarks)一節中的＜鏡像媒體集中的媒體家族＞。  
  
 [ *next-mirror-to* ]  
 這是一個預留位置，表示單一 BACKUP 陳述式除了可以包含單一 TO 子句，還可以包含最多 3 個 MIRROR TO 子句。  
  
### <a name="with-options"></a>WITH 選項  
 指定要搭配備份作業使用的選項。  
  
 CREDENTIAL  
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 和 SQL Database 受控執行個體。  
 只有當建立備份到 Windows Azure Blob 儲存服務時才使用。  
  
 FILE_SNAPSHOT **適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。

 使用 Azure Blob 儲存體服務來儲存所有 SQL Server 資料庫檔案時，用來建立資料庫檔案的 Azure 快照集。 如需詳細資訊，請參閱 [Microsoft Azure 中的 SQL Server 資料檔案](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 快照集備份會以一致的狀態建立資料庫檔案 (資料和記錄檔) 的 Azure 快照集。 一組一致的 Azure 快照集會組成一個備份，並記錄於備份檔案中。 `BACKUP DATABASE TO URL WITH FILE_SNAPSHOT` 和 `BACKUP LOG TO URL WITH FILE_SNAPSHOT` 之間的唯一差異是，後者也會截斷交易記錄，但前者不會。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 快照集備份，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立備份鏈結所需的初始完整備份之後，只需使用單一交易記錄備份就能將資料庫還原至交易記錄備份的時間點。 此外，只需要兩個交易記錄備份，就能將資料庫還原至這兩個交易記錄備份時間之間的時間點。  
    
 DIFFERENTIAL  
**適用於：** 只能搭配 BACKUP DATABASE 使用，可用來指定資料庫或檔案備份應該只含有資料庫或檔案在前次完整備份之後又變更過的部分。 差異備份所用的空間通常會比完整備份少。 使用這個選項，便不需要套用自前次完整備份之後所執行的所有個別記錄備份。  
  
> [!NOTE]  
> 根據預設，`BACKUP DATABASE` 會建立完整備份。  
  
 如需詳細資訊，請參閱 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  
  
 ENCRYPTION  
 用來指定備份的加密。 您可以指定加密演算法來加密備份，或指定 `NO_ENCRYPTION` 不加密備份。 加密是有助於保護備份檔案的建議作法。 您可以指定的演算法清單包括：  
  
-   `AES_128`  
-   `AES_192`  
-   `AES_256`  
-   `TRIPLE_DES_3KEY`  
-   `NO_ENCRYPTION`    

如果您選擇加密，則也需要使用加密程式選項指定加密程式：  
  
-   SERVER CERTIFICATE = Encryptor_Name  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
> [!WARNING]  
> 搭配 `FILE_SNAPSHOT` 引數使用加密時，中繼資料檔案本身會使用指定的加密演算法進行加密，而系統會確認已針對資料庫完成[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。 對於資料本身則不會進行任何其他加密。 如果未加密資料庫，或者發出備份陳述式之前未完成加密，備份就會失敗。  
  
**備份組選項**  
  
這些選項會處理這個備份作業所建立的備份組。  
  
> [!NOTE]  
> 若要指定還原作業的備份組，請使用 `FILE = <backup_set_file_number>` 選項。 如需如何指定備份組的詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md) 中的＜指定備份組＞。
  
 COPY_ONLY **適用於：** SQL Server 和 SQL Server 受控執行個體。指定備份為「僅複製備份」，這不會影響正常的備份順序。 僅複製備份的建立與定期排程的傳統備份無關。 僅複製備份並不會影響資料庫的整體備份和還原程序。  
  
 僅複製備份應該用於需要執行備份來達成特定用途的情況 (例如，在線上檔案還原之前備份記錄檔)。 通常，僅複製記錄備份用過一次後便會刪除。  
  
-   搭配 `BACKUP DATABASE` 使用時，`COPY_ONLY` 選項會建立無法作為差異基底使用的完整備份。 差異點陣圖不會更新，而且差異備份的行為會如同僅複製備份並不存在。 後續的差異備份會使用最新的傳統完整備份做為其基底。  
  
    > [!IMPORTANT]  
    > 如果同時使用 `DIFFERENTIAL` 和 `COPY_ONLY`，即會忽略 `COPY_ONLY` 並建立差異備份。  
  
-   搭配 `BACKUP LOG` 使用時，`COPY_ONLY` 選項會建立「僅複製記錄備份」，這不會截斷交易記錄。 僅複製記錄備份不會影響記錄檔鏈結，而且其他記錄備份的行為會如同僅複製備份並不存在。  
  
如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  
  
{ COMPRESSION | NO_COMPRESSION }  
只有在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 及更新版本中，才指定是否要在此備份上執行[備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)，以覆寫伺服器層級的預設值。  
  
進行安裝時，預設行為是不壓縮備份。 但是，您可以設定 [backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 伺服器設定選項來變更此預設值。 如需檢視此選項目前值的詳細資訊，請參閱[檢視或變更伺服器屬性 &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)。  

如需搭配已啟用[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 之資料庫使用備份壓縮的相關資訊，請參閱[備註](#general-remarks)一節。
  
COMPRESSION  
明確啟用備份壓縮。  
  
NO_COMPRESSION  
明確停用備份壓縮。  
  
DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
指定描述備份組的自由形式文字。 這個字串最多可有 255 個字元。  
  
NAME **=** { *backup_set_name* | **@***backup_set_var* }  
指定備份組的名稱。 名稱最多可有 128 個字元。 如果未指定 NAME，它就是空白。  
  
{ EXPIREDATE **='***date***'** | RETAINDAYS **=** *days* }  
指定何時可以覆寫這個備份的備份組。 如果同時使用這兩個選項，RETAINDAYS 會優先於 EXPIREDATE。  
  
如果沒有指定任何選項，便會由 **mediaretention** 組態設定來決定到期日。 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。   
  
> [!IMPORTANT]  
> 這些選項只會防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 覆寫檔案。 您可以利用其他方法來清除磁帶，並利用作業系統來刪除磁碟檔案。 如需有關期限驗證的詳細資訊，請參閱這個主題中的 SKIP 和 FORMAT。  
  
EXPIREDATE **=** { **'***date***'** | **@***date_var* } 指定備份組到期且可加以覆寫的時間。如果這個日期是以變數 (@* date_var*) 提供，則它必須遵照所設定的系統 **datetime** 格式，且必須指定為下列其中一項：  
  
-   字串常數 (@*date_var* **=** date)  
-   字元字串資料類型的變數 (**ntext** 或 **text** 資料類型除外)  
-   **smalldatetime**  
-   **datetime** 變數  
  
例如：  
  
-   `'Dec 31, 2020 11:59 PM'`  
-   `'1/1/2021'`  
  
如需如何指定 **datetime** 值的相關資訊，請參閱[日期和時間類型](../../t-sql/data-types/date-and-time-types.md)。  
  
> [!NOTE]  
> 若要忽略到期日，請使用 `SKIP` 選項。  
  
RETAINDAYS **=** { *days* | **@***days_var* } 指定必須經過多少天之後，才能覆寫這個備份媒體集。如果是以變數 (**@***days_var*) 提供，就必須將它指定為整數。  
  
**媒體集選項**  
  
這些選項會處理整個媒體集。  
  
{ **NOINIT** | INIT }  
 控制備份作業要附加還是覆寫至備份媒體上的現有備份組。 預設是附加至媒體上的最新備份組 (NOINIT)。  
  
> [!NOTE]  
> 如需 { **NOINIT** | INIT } 與 { **NOSKIP** | SKIP } 間之互動的相關資訊，請參閱本主題稍後的[備註](#general-remarks)。  
  
NOINIT  
 指出將備份組附加至指定的媒體集，以保留現有的備份組。 如果定義了媒體集的媒體密碼，您就必須提供密碼。 NOINIT 是預設值。  
  
如需詳細資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
INIT  
 指定應該覆寫所有備份組，但保留媒體標頭。 如果指定 INIT，就會覆寫這個裝置中任何現有的備份組 (如果條件允許)。 依預設，BACKUP 會檢查下列狀況，如果任何一種狀況存在，就不會覆寫備份媒體：  
  
-   有尚未到期的備份組。 如需詳細資訊，請參閱 `EXPIREDATE` 和 `RETAINDAYS` 選項。  
-   BACKUP 陳述式所提供的備份組名稱 (如果有提供) 不符合備份媒體中的名稱。 如需詳細資訊，請參閱本節前面的 NAME 選項。  
  
若要覆寫這些檢查，請使用 `SKIP` 選項。  
  
如需詳細資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
{ **NOSKIP** | SKIP }  
控制備份作業在覆寫媒體上的備份組之前是否要先檢查備份組的到期日和時間。  
  
> [!NOTE]  
> 如需 { **NOINIT** | INIT } 與 { **NOSKIP** | SKIP } 間之互動的相關資訊，請參閱本主題稍後的＜備註＞。  
  
NOSKIP  
指示 BACKUP 陳述式先檢查媒體中所有備份組的到期日，才允許覆寫它們。 這是預設行為。  
  
SKIP  
停用通常是由 BACKUP 陳述式所執行的備份組期限和名稱的檢查，以防止覆寫備份組。 如需有關 { INIT | NOINIT } 和 { NOSKIP | SKIP } 之間互動的詳細資訊，請參閱本主題稍後的＜備註＞一節。  
若要檢視備份組的到期日，請查詢 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 記錄資料表的 **expiration_date** 資料行。  
  
{ **NOFORMAT** | FORMAT }  
指定是否要將媒體標頭寫入這項備份作業所使用的磁碟區，以覆寫任何現有的媒體標頭和備份組。  
  
NOFORMAT  
指定備份作業保留這項備份作業所使用之媒體磁碟區上的現有媒體標頭和備份組。 這是預設行為。  
  
FORMAT  
指定建立新的媒體集。 FORMAT 會導致備份作業在備份作業使用的所有媒體磁碟區中寫入新的媒體標頭。 磁碟區的現有內容會變成無效，因為任何現有的媒體標頭和備份組都會遭到覆寫。  
  
> [!IMPORTANT]  
> 請謹慎使用 `FORMAT`。 格式化媒體集的任何磁碟區，會使得整個媒體集無法使用。 例如，如果您初始化屬於現有等量媒體集的單一磁帶，整個媒體集都會變成無法使用。  
  
指定 FORMAT 意味著 `SKIP`；您不需要明確指示 `SKIP`。  
  
MEDIADESCRIPTION **=** { *text* | **@***text_variable* }  
指定媒體集自由形式的文字描述，最多 255 個字元。  
  
MEDIANAME **=** { *media_name* | **@***media_name_variable* }  
指定整個備份媒體集的媒體名稱。 媒體名稱不能超出 128 個字元，如果指定 `MEDIANAME`，它必須符合先前所指定且已存在備份磁碟區的媒體名稱。 如果未指定或指定了 SKIP 選項，就不會進行媒體名稱的驗證檢查。  
  
BLOCKSIZE **=** { *blocksize* | **@***blocksize_variable* }  
指定實體區塊大小 (以位元組為單位)。 支援的大小為 512、1024、2048、4096、8192、16384、32768 和 65536 (64 KB) 位元組。 磁帶裝置的預設值為 65536，其他裝置則為 512。 一般而言這個選項是不必要的，因為 BACKUP 會自動選取裝置適用的區塊大小。 明確指出區塊大小會覆寫自動選取的區塊大小。  
  
如果採用的備份是要複製到 CD-ROM 然後再從中還原，請指定 BLOCKSIZE=2048。  
  
> [!NOTE]  
> 一般而言，只有在寫入磁帶裝置時，這個選項才會對效能造成影響。  
  
**資料轉送選項**  
  
BUFFERCOUNT **=** { *buffercount* | **@***buffercount_variable* }  
指定要用於備份作業的 I/O 緩衝區總數。 您可以指定任何正整數，不過，緩衝區的數目很大時，可能會因為 Sqlservr.exe 處理序中的虛擬位址空間不足而造成「記憶體不足」錯誤。  
  
緩衝區所使用的總空間可由下列公式判斷：*buffercount/maxtransfersize*。  
  
> [!NOTE]  
> 如需使用 `BUFFERCOUNT` 選項的重要資訊，請參閱[不正確的 BufferCount 資料傳輸選項可能導致 OOM 狀況](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) \(英文\) 部落格文章。  
  
MAXTRANSFERSIZE **=** { *maxtransfersize* | ***@** maxtransfersize_variable* } 以位元組為單位，指定要用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和備份媒體之間的最大傳輸單位。 可能的值是 65536 位元組 (64 KB) 的倍數，最大可達 4194304 位元組 (4 MB)。  

> [!NOTE]  
> 使用 SQL 寫入器服務建立備份時，如果已為資料庫設定 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md)，或該資料庫包含[記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)，則在還原期間的 `MAXTRANSFERSIZE` 應該大於或等於建立備份時所使用的 `MAXTRANSFERSIZE`。 

> [!NOTE]  
> 針對含有單一資料檔案且已啟用[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 的資料庫，預設的 `MAXTRANSFERSIZE` 為 65536 (64 KB)。 針對非 TDE 加密的資料庫，使用備份至 DISK 時，預設的 `MAXTRANSFERSIZE` 為 1048576 (1 MB)，而使用 VDI 或 TAPE 時為 65536 (64 KB)。
> 如需搭配 TDE 加密的資料庫使用備份壓縮的詳細資訊，請參閱[備註](#general-remarks)一節。
  
**錯誤管理選項**  
  
這些選項可讓您決定是否要針對備份作業啟用備份總和檢查碼，以及作業是否會在發生錯誤時停止。  
  
{ **NO_CHECKSUM** | CHECKSUM }  
 控制是否要啟用備份總和檢查碼。  
  
NO_CHECKSUM  
明確地停用產生備份總和檢查碼 (以及驗證頁面總和檢查碼)。 這是預設行為。  
  
CHECKSUM  
如果備份作業已啟用且可供使用，指定備份作業要驗證每個頁面的總和檢查碼及損毀頁，並產生整個備份的總和檢查碼。  
  
使用備份總和檢查碼，可能會影響工作負載和備份的輸送量。  
  
如需詳細資訊，請參閱[在備份和還原期間可能發生的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
控制備份作業在發生頁面總和檢查碼錯誤之後要停止或繼續。  
  
STOP_ON_ERROR  
指示 BACKUP 在頁面總和檢查碼未驗證時便失敗。 這是預設行為。  
  
CONTINUE_AFTER_ERROR  
指示儘管發生總和檢查碼無效或損毀頁之類的錯誤，BACKUP 仍繼續作業。  
  
如果您在資料庫損毀時無法使用 NO_TRUNCATE 選項來備份記錄的結尾，您可以指定 CONTINUE_AFTER_ERROR 取代 NO_TRUNCATE 來嘗試進行[結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
如需詳細資訊，請參閱[在備份和還原期間可能發生的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
**相容性選項**  
  
RESTART  
從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，沒有任何作用。 這個版本接受這個選項的目的，是為了與舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相容。  
  
**監視選項**  
  
STATS [ **=** *percentage* ]  
 每次另一個 *percentage* 完成時就會顯示一則訊息，用來量測進度。 如果省略 *percentage*，每完成 10%，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都會顯示一則訊息。  
  
STATS 選項報告到達下一個間隔之報告臨界值的完成百分比。 大約會以指定的百分比為間隔；例如，當 STATS=10，如果完成的量是 40%，這個選項可能顯示 43%。 對大型備份組而言，這不成問題，因為在已完成的 I/O 呼叫之間，百分比完成的移動非常緩慢。  
  
**磁帶選項**  
**適用於：** SQL Server  
這些選項僅適用於「磁帶」裝置。 如果所使用的不是磁帶裝置，將忽略這些選項。  
  
{ **REWIND** | NOREWIND }  
REWIND **適用於：** SQL Server。指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會釋放和倒轉磁帶。 REWIND 是預設值。  
  
NOREWIND **適用於：** SQL Server。指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在備份作業之後，讓磁帶維持在開啟狀態。 對磁帶執行多次備份作業時，可以使用這個選項來改善效能。  
  
NOREWIND 隱含 NOUNLOAD，而這些選項在單一的 BACKUP 陳述式內不相容。  
  
> [!NOTE]  
> 如果您使用 `NOREWIND`，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體會保有磁帶機的擁有權，直到在相同處理序中執行的 BACKUP 或 RESTORE 陳述式使用 `REWIND` 或 `UNLOAD` 選項，或是伺服器執行個體關閉為止。 保留磁帶的開啟狀態可以防止其他處理序存取這個磁帶。 如需如何顯示開啟的磁帶清單及關閉開啟的磁帶之詳細資訊，請參閱[備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)。  
  
{ **UNLOAD** | NOUNLOAD }    
**適用於：** SQL Server 
> [!NOTE]  
> `UNLOAD` 和 `NOUNLOAD` 是工作階段設定，會在工作階段的存留期間保持不變，直到指定其他設定進行重設為止。  
  
UNLOAD **適用於：** SQL Server   
 指定在備份完成之後，便自動倒轉和卸載磁帶。 UNLOAD 是在工作階段開始時的預設值。 
  
NOUNLOAD **適用於：** SQL Server。指定在 BACKUP 作業之後，磁帶仍會在磁帶機上保持載入。  
  
> [!NOTE]  
> 如果要備份到磁帶備份裝置，`BLOCKSIZE` 選項會影響備份作業的效能。 一般而言，只有在寫入磁帶裝置時，這個選項才會對效能造成影響。  
  
**記錄特定選項**  
**適用於：** SQL Server  
這些選項只能搭配 `BACKUP LOG` 使用。  
  
> [!NOTE]  
> 如果您不想要取得記錄備份，請使用簡單復原模式。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
{ NORECOVERY | STANDBY **=** *undo_file_name* }  
  NORECOVERY **適用於：** SQL Server   
  它會備份記錄的結尾，並將資料庫保留在 RESTORING 狀態。 當進行容錯移轉，將工作交給次要資料庫時，或在 RESTORE 作業之前儲存記錄結尾時，NORECOVERY 非常有用。  
  
  若要執行略過記錄截斷的最大速率記錄備份，然後使資料庫自動進入 RESTORING 狀態，請同時使用 `NO_TRUNCATE` 和 `NORECOVERY` 選項。  
  
  STANDBY **=** *standby_file_name* 
**適用於：** SQL Server   
  備份記錄的結尾，並將資料庫保留在唯讀和 STANDBY 狀態。 STANDBY 子句會寫入待命資料 (執行回復，但使用進一步還原的選項)。 使用 STANDBY 選項相當於使用 BACKUP LOG WITH NORECOVERY，後面接著 RESTORE WITH STANDBY。  
  
  使用待命模式需要 *standby_file_name* 所指定的待命資料庫檔案，它的位置儲存在資料庫記錄中。 如果指定的檔案已存在，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會覆寫它；如果檔案不存在，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會建立它。 待命檔案會成為資料庫的一部分。  
  
  這個檔案會保留已回復的變更，如果之後要套用 RESTORE LOG 作業，就必須保留這些變更。 您必須有足以供待命檔案成長的磁碟空間，它才能夠包含資料庫中，因回復未認可的交易而修改過的所有相異頁面。  
  
NO_TRUNCATE  
**適用於：** SQL Server  
指定不截斷記錄，並使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 嘗試進行備份，而不論資料庫狀態為何。 因此，利用 `NO_TRUNCATE` 建立的備份可能會有不完整的中繼資料。 在資料庫已損毀的情況下，您可以利用這個選項來進行記錄的備份。  
  
BACKUP LOG 的 NO_TRUNCATE 選項相當於同時指定 COPY_ONLY 和 CONTINUE_AFTER_ERROR。  
  
未使用 `NO_TRUNCATE` 選項時，資料庫必須處於 ONLINE 狀態。 如果資料庫處於 SUSPENDED 狀態，您就能透過指定 `NO_TRUNCATE` 來建立備份。 但是，如果資料庫處於 OFFLINE 或 EMERGENCY 狀態，即使設定了 `NO_TRUNCATE`，也不允許 BACKUP。 如需資料庫狀態的相關資訊，請參閱[資料庫狀態](../../relational-databases/databases/database-states.md)。  
  
## <a name="about-working-with-sql-server-backups"></a>關於使用 SQL Server 備份  
 本節介紹下列必要的備份概念：  
  
 [備份類型](#Backup_Types)  
 [交易記錄截斷](#Tlog_Truncation)  
 [將備份媒體格式化](#Formatting_Media)  
 [使用備份裝置和媒體集](#Backup_Devices_and_Media_Sets)  
 [還原 SQL Server 備份](#Restoring_Backups)  
  
> [!NOTE]  
> 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中備份的簡介，請參閱[備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)。  
  
###  <a name="Backup_Types"></a> 備份類型  
 支援的備份類型需視資料庫的復原模式而定，如下所示：  
  
-   所有復原模式都支援完整和差異的資料備份。  
  
    |備份範圍|備份類型|  
    |---------------------|------------------|  
    |整個資料庫|[資料庫備份](../../relational-databases/backup-restore/full-database-backups-sql-server.md)會包含整個資料庫。<br /><br /> 或者，每個資料庫備份都可作為一系列一或多個[差異資料庫備份](../../relational-databases/backup-restore/differential-backups-sql-server.md)的基底。|  
    |部分資料庫|[部份備份](../../relational-databases/backup-restore/partial-backups-sql-server.md)包含讀取/寫入檔案群組，可能的話，還會包含一或多個唯讀檔案或檔案群組。<br /><br /> 或者，每個部份備份都可作為一系列一或多個[差異部份備份](../../relational-databases/backup-restore/differential-backups-sql-server.md)的基底。|  
    |檔案或檔案群組|[檔案備份](../../relational-databases/backup-restore/full-file-backups-sql-server.md)包含一或多個檔案或檔案群組，而且只會與包含多個檔案群組的資料庫有關。 在簡單復原模式下，檔案備份基本上會限制用於唯讀的次要檔案群組。<br /> 或者，每個檔案備份都可作為一系列一或多個[差異檔案備份](../../relational-databases/backup-restore/differential-backups-sql-server.md)的基底。|  
  
-   在完整復原模式或大量記錄復原模式下，傳統備份也必須包含循序的「交易記錄備份」 (或「記錄備份」)。 每個記錄備份都包含建立備份時為使用中的交易記錄部分，而且會包含上一次記錄備份沒有備份的所有記錄檔記錄。  
  
     若要將遺失工作的風險降到最低 (但會耗用管理負擔成本)，您應該排定經常性的記錄備份。 在完整備份之間排定差異備份，可減少您在還原資料後必須還原的記錄備份數目，從而減少還原時間。  
  
     我們建議您將記錄備份放在個別的磁碟區上，而不是進行資料庫備份。  
  
    > [!NOTE]  
    > 您必須先建立完整備份，才能建立第一個記錄備份。  
  
-   「僅複製備份」是特殊用途的完整備份或記錄備份，與傳統備份的正常順序無關。 若要建立僅複製備份，請在 BACKUP 陳述式中指定 COPY_ONLY 選項。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  
  
###  <a name="Tlog_Truncation"></a> 交易記錄截斷  
 為避免填滿資料庫的交易記錄，例行備份相當重要。 在簡單復原模式下，記錄截斷會自動在備份資料庫後發生，而在完整復原模式下，則會自動在備份交易記錄後發生。 不過，有時候您可以延遲截斷處理作業。 如需延遲記錄截斷可能因素的相關資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
> [!NOTE]  
> `BACKUP LOG WITH NO_LOG` 和 `WITH TRUNCATE_ONLY` 選項已中止。 如果您要使用完整復原模式或大量記錄復原模式，而且您必須從資料庫移除記錄備份鏈結，請切換到簡單復原模式。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
###  <a name="Formatting_Media"></a> 將備份媒體格式化  
 只有下列其中一種情況成立，BACKUP 陳述式才會將備份媒體格式化：  
  
-   已指定 `FORMAT` 選項。  
-   媒體是空的。  
-   作業正在寫入接續磁帶。  
  
###  <a name="Backup_Devices_and_Media_Sets"></a> 使用備份裝置和媒體集  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>等量媒體集 (等量集) 中的備份裝置  
 「等量集」是一組磁碟檔案，其中的資料會分成幾個區塊，並依照固定順序散發。 等量集中所使用的備份裝置數目必須維持相同 (除非使用 `FORMAT` 來將媒體重新初始化)。  
  
 下列範例會將 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫的備份寫入使用三個磁碟檔案的新等量媒體集。  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'  
WITH FORMAT,  
   MEDIANAME = 'AdventureWorksStripedSet0',  
   MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database;  
GO  
```  
  
 在備份裝置定義成等量集的一部分之後，除非指定 FORMAT，否則，單一裝置備份便無法使用它。 同樣地，除非指定 FORMAT，否則，等量集也無法使用包含非等量備份的備份裝置。 若要分割等量備份組，請使用 FORMAT。  
  
 寫入媒體標頭時，如果既未指定 MEDIANAME，也未指定 MEDIADESCRIPTION，對應至空白項目的媒體標頭欄位就是空的。  
  
#### <a name="working-with-a-mirrored-media-set"></a>使用鏡像媒體集  
 一般而言，備份並無鏡像，而且 BACKUP 陳述式只會包含 TO 子句。 但是，每個媒體集總共可以包含四個鏡像。 如果是鏡像媒體集，備份作業會寫入多個備份裝置群組。 每個備份裝置群組都會在鏡像媒體集中包含單一鏡像。 每個鏡像都必須使用相同數量和類型的實體備份裝置，而且必須全部具備相同的屬性。  
  
 若要備份鏡像媒體集，所有鏡像都必須存在。 若要備份到鏡像媒體集，請指定 `TO` 子句來指定第一個鏡像，並為每個其他鏡像指定 `MIRROR TO` 子句。  
  
 針對鏡像媒體集，每個 `MIRROR TO` 子句都必須列出與 TO 子句相同的裝置數目和類型。 下列範例會寫入含有兩個鏡像，且每個鏡像都使用三個裝置的鏡像媒體集中：  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'  
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';  
GO  
```  
  
> [!IMPORTANT]  
> 這個範例的設計，是為了讓您在本機系統中進行測試。 實際上，在相同磁碟機上備份多個裝置可能會降低效能，而且可能會減損鏡像媒體集原先設計的備援性。  
  
##### <a name="media-families-in-mirrored-media-sets"></a>鏡像媒體集中的媒體家族  
 在 BACKUP 陳述式之 `TO` 子句中指定的每個備份裝置都對應到一個媒體家族。 例如，如果 `TO` 子句列出三個裝置，BACKUP 就會將資料寫入三個媒體家族。 在鏡像媒體集中，每個鏡像都必須包含每個媒體家族的複本。 這就是為什麼每個鏡像必須具有相同的裝置數目。  
  
 當各個鏡像分別列出多個裝置時，裝置順序會決定要將哪個媒體家族寫入特定裝置。 例如，在各份裝置清單中，第二個裝置都會對應到第二個媒體家族。 對於上面範例中的裝置，下表會說明這些裝置和媒體家族間的對應關係。  
  
|鏡像|媒體家族 1|媒體家族 2|媒體家族 3|  
|---------|---------|---------|---------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|@shouldalert|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 媒體家族必須永遠備份到特定鏡像中的相同裝置。 因此，您每次使用現有媒體集時，都必須依照建立該媒體集時所指定的相同順序來列出每一個鏡像的裝置。  
  
 如需鏡像媒體集的詳細資訊，請參閱 [鏡像備份媒體集 &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)的使用者閱讀。 如需媒體集和媒體家族的詳細資訊，請參閱[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
###  <a name="Restoring_Backups"></a> 還原 SQL Server 備份  
 若要還原資料庫，並選擇性地復原它以使其上線，或是還原檔案或檔案群組，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **還原**工作。 如需詳細資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
##  <a name="Additional_Considerations"></a> 關於 BACKUP 選項的其他考量  
  
###  <a name="Interactions_SKIP_etc"></a> SKIP、NOSKIP、INIT 和 NOINIT 的互動  
 下列表格描述 { **NOINIT** | INIT } 與 { **NOSKIP** | SKIP } 選項之間的互動。  
  
> [!NOTE]  
> 如果磁帶媒體是空的，或磁碟備份檔案不存在，所有這些互動都會寫入媒體標頭，並繼續作業。 如果媒體不是空的，但缺少有效媒體標頭，這些作業會回應指出這不是有效的 MTF 媒體，而且備份作業將會中止。  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|如果磁碟區包含有效的媒體標頭，確認媒體名稱符合指定的 `MEDIANAME` (如果有的話)。 如果相符，則附加備份組，保留所有現有的備份組。<br /> 如果磁碟區並未包含有效的媒體標頭，便會發生錯誤。|如果磁碟區包含有效的媒體標頭，則執行下列檢查：<br /><ul><li>如果指定了 `MEDIANAME`，確認指定的媒體名稱符合媒體標頭的媒體名稱。<sup>1</sup></li><li>確認媒體中沒有出現任何非預期的備份組。 如果有，則結束備份。</li></ul><br />如果通過這些檢查，則覆寫媒體中的任何備份組，只保留媒體標頭。<br /> 如果磁碟區未包含有效的媒體標頭，使用指定的 `MEDIANAME` 和 `MEDIADESCRIPTION` (如果有的話) 產生一個。|  
|SKIP|如果磁碟區包含有效的媒體標頭，則附加備份組，保留所有現有的備份組。|如果磁碟區包含有效<sup>2</sup>的媒體標頭，則覆寫媒體上的任何備份組，只保留媒體標頭。<br /> 若媒體是空的，就使用指定的 `MEDIANAME` 和 `MEDIADESCRIPTION` (如果有的話) 來產生媒體標頭。|  

<sup>1</sup> 使用者必須屬於適當的固定資料庫或伺服器角色，才能執行備份作業。    

<sup>2</sup> 有效性包括 MTF 版本號碼和其他標頭資訊。 如果不支援指定的版本，或它不是預期的值，就會發生錯誤。  
  
## <a name="compatibility"></a>相容性  
  
> [!CAUTION]  
> 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，無法還原較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本所建立的備份。  
  
BACKUP 支援 `RESTART` 選項，以提供與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的回溯相容性。 但 RESTART 卻沒有任何作用。  
  
## <a name="general-remarks"></a>一般備註  
您可以將資料庫或記錄備份附加至任何磁碟或磁帶裝置，以便將資料庫及其交易記錄保留在單一實體位置中。  
  
在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。  
  
只要作業系統支援資料庫的定序，便可以執行跨平台的備份作業，即使在不同類型的處理器之間，也是如此。  
 
搭配含有單一資料檔案且已啟用[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 的資料庫使用備份壓縮時，建議使用**大於 65536 (64 KB)** 的 `MAXTRANSFERSIZE` 設定。   
從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，這會針對 TDE 加密的資料庫啟用最佳化壓縮演算法，此演算法會先將頁面解密、將其壓縮，然後再次加密。 如果使用 `MAXTRANSFERSIZE = 65536` (64 KB)，搭配 TDE 加密資料庫的備份壓縮就會直接壓縮加密的頁面，可能不會產生良好的壓縮率。 如需詳細資訊，請參閱[適用於已啟用 TDE 之資料庫的備份壓縮](http://blogs.msdn.microsoft.com/sqlcat/2016/06/20/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases/) \(英文\)。

> [!NOTE]  
> 某些情況下，預設值 `MAXTRANSFERSIZE` 大於 64K：
> * 當資料庫已建立多個資料檔案時，它會使用 `MAXTRANSFERSIZE` > 64K
> * 執行備份至 URL 時，預設 `MAXTRANSFERSIZE = 1048576` (1MB)
>   
> 即使其中一個條件適用，您也必須在備份命令中明確設定 `MAXTRANSFERSIZE` 大於 64K，以取得新的備份壓縮演算法。
  
根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
## <a name="interoperability"></a>互通性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用線上備份程序，使您能夠在使用資料庫時，備份資料庫。 在備份期間，您可以執行大部分的作業；例如，在備份作業期間，您可以執行 INSERT、UPDATE 或 DELETE 陳述式。  
  
 資料庫或交易記錄備份期間所無法執行的作業包括：  
  
-   檔案管理作業，例如，搭配 `ADD FILE` 或 `REMOVE FILE` 選項的 `ALTER DATABASE` 陳述式。  
  
-   壓縮資料庫或壓縮檔案的作業。 其中包括自動壓縮作業。  
  
如果備份作業與檔案管理或壓縮作業重疊，便會發生衝突。 不論是哪一項衝突作業在前面，第二項作業都會等待第一項作業所設定的鎖定逾時 (逾時期間由工作階段逾時設定來控制)。 如果在逾時期間解除鎖定，第二項作業就會繼續下去。 如果鎖定逾時，第二項作業就會失敗。  

## <a name="limitations-for-sql-database-managed-instance"></a>SQL Database 受控執行個體的限制
SQL Database 受控執行個體可以將資料庫備份到具有最多 32 個等量磁碟區的備份，這對於使用備份壓縮的情況，已足夠應付最多 4 TB 的資料庫。

備份等量磁碟區大小上限為 195 GB (最大 Blob 大小)。 在備份命令中增加等量磁碟區的數目，以減少個別的等量磁碟區大小並維持在這項限制內。

> [!NOTE]
> 若要在內部解決這項限制，請備份至 `DISK` 而不要備份至 `URL`、將備份檔案上傳至 Blob，然後還原。 還原支援更大的檔案，因為使用了不同的 Blob 類型。

 
## <a name="metadata"></a>中繼資料  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括下列備份記錄資料表，其會追蹤備份活動：  
  
-   [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
-   [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
-   [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
-   [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
執行還原時，如果備份組尚未記錄於 **msdb** 資料庫，就表示備份記錄資料表可能已修改過。  
  
## <a name="security"></a>Security  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，建立備份的 `PASSWORD` 和 `MEDIAPASSWORD` 選項已遭到停用。 仍然可以還原以密碼建立的備份。  
  
### <a name="permissions"></a>Permissions  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="examples"></a> 範例  
 本節包含下列範例：  
  
-   A. [備份完整資料庫](#backing_up_db)  
-   B. [備份資料庫和記錄](#backing_up_db_and_log)  
-   C. [建立次要檔案群組的完整檔案備份](#full_
-   file_backup)  
-   D. [建立次要檔案群組的差異檔案備份](#differential_file_backup)  
-   E. [建立和備份至單一家族鏡像媒體集](#create_single_family_mirrored_media_set)  
-   F. [建立和備份至多重家族鏡像媒體集](#create_multifamily_mirrored_media_set)  
-   G. [備份至現有的鏡像媒體集](#existing_mirrored_media_set)  
-   H. [在新的媒體集中建立壓縮備份](#creating_compressed_backup_new_media_set)  
-   I. [備份至 Microsoft Azure Blob 儲存體服務](#url)  
  
> [!NOTE]  
> 備份的使用說明主題包含了其他的範例。 如需詳細資訊，請參閱 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)。  
  
###  <a name="backing_up_db"></a> A. 備份完整資料庫  
 下列範例會將 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫備份到磁碟檔案。  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. 備份資料庫和記錄  
 下列範例會備份 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫，依預設採用簡單復原模式。 為了支援記錄備份，[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫會修改成使用完整復原模式。  
  
 接著，範例會使用 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)，建立邏輯[備份裝置](../../relational-databases/backup-restore/backup-devices-sql-server.md)來備份資料 (`AdvWorksData`)，並建立另一個邏輯備份裝置來備份記錄 (`AdvWorksLog`)。  
  
 這個範例接著會建立 `AdvWorksData` 的完整資料庫備份，並且在更新活動一段時間之後，將記錄備份到 `AdvWorksLog`。  
  
```sql  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
   SET RECOVERY FULL;  
GO  
-- Create AdvWorksData and AdvWorksLog logical backup devices.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'Z:\SQLServerBackups\AdvWorksData.bak';  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',   
'X:\SQLServerBackups\AdvWorksLog.bak';  
GO  
  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;  
GO  
-- Back up the AdventureWorks2012 log.  
BACKUP LOG AdventureWorks2012  
   TO AdvWorksLog;  
GO  
```  
  
> [!NOTE]  
>  如果是實際執行的資料庫，請定期備份記錄。 記錄的備份頻率必須足以保護資料不會遺失。  
  
###  <a name="full_file_backup"></a> C. 建立次要檔案群組的完整檔案備份  
 下列範例會為兩個次要檔案群組中的每個檔案建立完整檔案備份。  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> D. 建立次要檔案群組的差異檔案備份  
 下列範例會為兩個次要檔案群組中的每個檔案建立差異檔案備份。  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
###  <a name="create_single_family_mirrored_media_set"></a> E. 建立和備份至單一家族的鏡像媒體集中  
 下列範例會建立一個鏡像媒體集，其中包含單一媒體家族和四個鏡像，且會將 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫備份至其中。  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0'  
MIRROR TO TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2'  
MIRROR TO TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet0';  
```  
  
###  <a name="create_multifamily_mirrored_media_set"></a> F. 建立和備份至多重家族的鏡像媒體集中  
 下列範例會建立一個鏡像媒體集，其中的每個鏡像都由兩個媒體家族組成。 之後，這個範例會將 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫備份在這兩個鏡像中。  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a> G. 備份至現有的鏡像媒體集中  
 下列範例會將備份組附加至先前範例所建立的媒體集中。  
  
```sql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  NOINIT 是預設值，這裡顯示它是為了更加清楚。  
  
###  <a name="creating_compressed_backup_new_media_set"></a> H. 在新的媒體集中建立壓縮備份  
 下列範例會將媒體格式化、建立新的媒體集，並執行 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫的完整壓縮備份。  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a> I. 備份至 Microsoft Azure Blob 儲存體服務 
下列範例會為 `Sales` 執行完整資料庫備份以將它備份到 Microsoft Azure Blob 儲存體服務。  儲存體帳戶名稱為 `mystorageaccount`。  容器名稱為 `myfirstcontainer`。  已建立具有讀取、寫入、刪除和列出權限的預存存取原則。  已使用與預存存取原則相關聯的共用存取簽章來建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。  如需將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份至 Windows Azure Blob 儲存體服務的相關資訊，請參閱[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)和 [SQL Server 備份至 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [分次還原具有記憶體最佳化資料表的資料庫](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  
