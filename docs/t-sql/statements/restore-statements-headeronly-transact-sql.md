---
title: RESTORE HEADERONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
caps.latest.revision: 95
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 41f8c9931419d9fb2ba6baa52f01432e8b44b510
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="restore-statements---headeronly-transact-sql"></a>RESTORE 陳述式 - HEADERONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中含有特定備份裝置上的所有備份組之所有備份標頭資訊的結果集。 

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)] 
  
> [!NOTE]  
>  如需引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>引數  
 如需 RESTORE HEADERONLY 引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
## <a name="result-sets"></a>結果集  
 對於給定裝置中的每個備份，伺服器都會傳送一個含有下列資料行的標頭資訊資料列：  
  
> [!NOTE]  
>  RESTORE HEADERONLY 會查看媒體中的所有備份組。 因此，當使用高容量磁帶機時，產生這個結果集可能需要一些時間。 若要快速瀏覽媒體，而不需要取得每個備份組的相關資訊，請使用 RESTORE LABELONLY 或指定 FILE **=** *backup_set_file_number*。  
  
> [!NOTE]  
>  由於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format 本質的緣故，來自其他軟體程式的備份組有可能佔用與 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份組相同媒體上的空間。 RESTORE HEADERONLY 傳回的結果集會針對每個這些其他備份組，各包括一個資料列。  
  
|資料行名稱|資料類型|SQL Server 備份組的描述|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar(128)**|備份組名稱|  
|**BackupDescription**|**nvarchar(255)**|備份組描述|  
|**BackupType**|**smallint**|備份類型：<br /><br /> **1** = 資料庫<br /><br /> **2** = 交易記錄<br /><br /> **4** = 檔案<br /><br /> **5** = 差異資料庫<br /><br /> **6** = 差異檔案<br /><br /> **7** = 部分<br /><br /> **8** = 差異部分|  
|**ExpirationDate**|**datetime**|備份組的到期日。|  
|**Compressed**|**BYTE(1)**|是否利用以軟體為基礎的壓縮來壓縮備份組：<br /><br /> **0** = 否<br /><br /> **1** = 是|  
|**位置**|**smallint**|備份組在磁碟區中的位置 (用來搭配 FILE = 選項)。|  
|**DeviceType**|**tinyint**|備份作業所用裝置的對應號碼。<br /><br /> 磁碟：<br /><br /> **2** = 邏輯<br /><br /> **102** = 實體<br /><br /> 磁帶：<br /><br /> **5** = 邏輯<br /><br /> **105** = 實體<br /><br /> 虛擬裝置：<br /><br /> **7** = 邏輯<br /><br /> **107** = 實體<br /><br /> 邏輯裝置名稱和裝置號碼在 **sys.backup_devices** 中；如需詳細資訊，請參閱 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)。|  
|**UserName**|**nvarchar(128)**|執行備份作業的使用者名稱。|  
|**ServerName**|**nvarchar(128)**|寫入備份組的伺服器名稱。|  
|**DatabaseName**|**nvarchar(128)**|備份的資料庫名稱。|  
|**DatabaseVersion**|**int**|建立備份的來源資料庫版本。|  
|**DatabaseCreationDate**|**datetime**|建立資料庫的日期和時間。|  
|**BackupSize**|**numeric(20,0)**|備份的大小 (以位元組為單位)。|  
|**FirstLSN**|**numeric(25,0)**|備份組中第一個記錄的記錄序號。|  
|**LastLSN**|**numeric(25,0)**|備份組之後下一個記錄檔記錄的記錄序號。|  
|**CheckpointLSN**|**numeric(25,0)**|在建立備份時，最近的檢查點之記錄序號。|  
|**DatabaseBackupLSN**|**numeric(25,0)**|最近的完整資料庫備份之記錄序號。<br /><br /> **DatabaseBackupLSN** 是備份啟動時所觸發的「檢查點起點」。 如果備份是在資料庫閒置時進行的，且沒有設定任何複寫，這個 LSN 就會與 **FirstLSN** 一致。|  
|**BackupStartDate**|**datetime**|備份作業開始的日期和時間。|  
|**BackupFinishDate**|**datetime**|備份作業完成的日期和時間。|  
|**SortOrder**|**smallint**|伺服器排序順序。 這個資料行只對資料庫備份有效。 提供這個項目的目的，是為了與舊版相容。|  
|**CodePage**|**smallint**|伺服器所用的伺服器字碼頁或字元集。|  
|**UnicodeLocaleId**|**int**|用來排序 Unicode 字元資料的伺服器 Unicode 地區設定識別碼組態選項。 提供這個項目的目的，是為了與舊版相容。|  
|**UnicodeComparisonStyle**|**int**|伺服器 Unicode 比較樣式組態選項，用來提供其他 Unicode 資料排序控制。 提供這個項目的目的，是為了與舊版相容。|  
|**CompatibilityLevel**|**tinyint**|建立備份的來源資料庫相容性層級設定。|  
|**SoftwareVendorId**|**int**|軟體供應商識別碼。 就 SQL Server 而言，這個號碼是 **4608** (或十六進位的 **0x1200**)。|  
|**SoftwareVersionMajor**|**int**|建立備份組的伺服器之主要版本號碼。|  
|**SoftwareVersionMinor**|**int**|建立備份組的伺服器之次要版本號碼。|  
|**SoftwareVersionBuild**|**int**|建立備份組的伺服器之組建編號。|  
|**MachineName**|**nvarchar(128)**|執行備份作業的電腦名稱。|  
|**旗標**|**int**|若設為 **1**，個別旗標位元意義如下：<br /><br /> **1** = 記錄備份包含大量記錄作業。<br /><br /> **2** = 快照集備份。<br /><br /> **4** = 備份時，資料庫是唯讀的。<br /><br /> **8** = 備份時，資料庫處於單一使用者模式。<br /><br /> **16** = 備份包含備份總和檢查碼。<br /><br /> **32** = 備份時，資料庫損毀，但要求備份作業忽略錯誤並繼續執行。<br /><br /> **64** = 結尾記錄備份。<br /><br /> **128** = 含不完整中繼資料的結尾記錄備份。<br /><br /> **256** = 使用 NORECOVERY 來進行的結尾記錄備份。<br /><br /> **重要：**建議您不要使用 **Flags**，而是改用個別的布林值資料行 (下列從 **HasBulkLoggedData** 開始到 **IsCopyOnly** 結束的布林資料行)。|  
|**BindingID**|**uniqueidentifier**|資料庫的繫結識別碼。 這會與 **sys.database_recovery_status****database_guid** 對應。 當還原資料庫時，會指派一個新值。 另請參閱 **FamilyGUID** (下方)。|  
|**RecoveryForkID**|**uniqueidentifier**|結尾復原分岔的識別碼。 這個資料行會與 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 資料表中的 **last_recovery_fork_guid**對應。<br /><br /> 就資料備份而言，**RecoveryForkID** 等於 **FirstRecoveryForkID**。|  
|**定序**|**nvarchar(128)**|資料庫所用的定序。|  
|**FamilyGUID**|**uniqueidentifier**|在建立之時，原始資料庫的識別碼。 當還原資料庫時，這個值會維持不變。|  
|**HasBulkLoggedData**|**bit**|**1** = 包含大量記錄作業的記錄備份。|  
|**IsSnapshot**|**bit**|**1** 快照集備份。|  
|**IsReadOnly**|**bit**|**1** = 備份時，資料庫是唯讀的。|  
|**IsSingleUser**|**bit**|**1** = 備份時，資料庫是單一使用者。|  
|**HasBackupChecksums**|**bit**|**1** = 備份包含備份總和檢查碼。|  
|**IsDamaged**|**bit**|**1** = 備份時，資料庫損毀，但要求備份作業忽略錯誤並繼續執行。|  
|**BeginsLogChain**|**bit**|**1** = 這是連續記錄備份鏈結中的第一個記錄備份。 記錄鏈結的開頭是建立資料庫之後，或從簡單復原模式切換到完整或大量記錄復原模式之後，所取出的第一個記錄備份。|  
|**HasIncompleteMetaData**|**bit**|**1** = 含不完整中繼資料的結尾記錄備份。<br /><br /> 如需有關含不完整備份中繼資料之結尾記錄備份的資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。|  
|**IsForceOffline**|**bit**|**1** = 使用 NORECOVERY 來進行的備份；資料庫因備份而離線。|  
|**IsCopyOnly**|**bit**|**1** = 僅限複製的備份。<br /><br /> 僅限複製備份並不會影響資料庫的整體備份和還原程序。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。|  
|**FirstRecoveryForkID**|**uniqueidentifier**|起始復原分岔的識別碼。 這個資料行會與 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 資料表中的 **first_recovery_fork_guid**對應。<br /><br /> 就資料備份而言，**FirstRecoveryForkID** 等於 **RecoveryForkID**。|  
|**ForkPointLSN**|**numeric(25,0)** NULL|如果 **FirstRecoveryForkID** 不等於 **RecoveryForkID**，這就是分岔點的記錄序號。 否則，這個值是 NULL。|  
|**RecoveryModel**|**nvarchar(60)**|這是資料庫的復原模式，它有下列幾種：<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|如果是單一基底差異備份，這個值就等於差異基底的 **FirstLSN**；LSN 大於或等於 **DifferentialBaseLSN** 的變更會納入差異備份中。<br /><br /> 如果是多重基底差異備份，這個值就是 NULL，基底 LSN 必須取決於檔案層級。 如需詳細資訊，請參閱 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。<br /><br /> 如果是非差異備份類型，這個值一律是 NULL。<br /><br /> 如需詳細資訊，請參閱 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。|  
|**DifferentialBaseGUID**|**uniqueidentifier**|如果是單一基底差異備份，這個值就是差異基底的唯一識別碼。<br /><br /> 如果是多重基底差異備份，這個值就是 NULL，差異基底必須取決於個別檔案。<br /><br /> 如果是非差異備份類型，這個值就是 NULL。|  
|**BackupTypeDescription**|**nvarchar(60)**|這是字串備份類型，它有下列幾種：<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** NULL|在媒體中，用來識別備份組的唯一識別碼。|  
|**CompressedBackupSize**|**bigint**|備份組的位元組計數。 就未壓縮的備份而言，這個值會與 **BackupSize** 相同。<br /><br /> 若要計算壓縮比，請使用 **CompressedBackupSize** 和 **BackupSize**。<br /><br /> 在 **msdb** 升級期間，這個值會設定為符合 **BackupSize** 資料行的值。|  
|**containment**|**tinyint** not NULL|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指示資料庫的內含項目狀態。<br /><br /> 0 = 資料庫內含項目已關閉<br /><br /> 1 = 資料庫內含項目是部分|  
|**KeyAlgorithm**|**nvarchar(32)**|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至目前的版本)。<br /><br /> 用於加密備份的加密演算法。 NO_Encryption 表示備份未加密。 無法判斷正確的值時，該值應該是 NULL。|  
|**EncryptorThumbprint**|**varbinary(20)**|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至目前的版本)。<br /><br /> 加密程式指模，可用來尋找資料庫中的憑證或非對稱金鑰。 備份未加密時，這個值會是 NULL。|  
|**EncryptorType**|**nvarchar(32)**|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) 至目前的版本)。<br /><br /> 使用的加密程式類型：憑證或非對稱金鑰。 備份未加密時，這個值會是 NULL。|  
  
> [!NOTE]  
>  如果定義了備份組的密碼，RESTORE HEADERONLY 只會顯示密碼符合命令指定的 PASSWORD 選項的備份組。 另外，RESTORE HEADERONLY 也只會顯示未受保護之備份組的完整資訊。 媒體上其他受密碼保護之備份組的 **BackupName** 資料行會設定為 '***受密碼保護\*\*\*'，所有其他資料行則為 NULL。  
  
## <a name="general-remarks"></a>一般備註  
 用戶端可以利用 RESTORE HEADERONLY 來擷取特定備份裝置上的所有備份之所有備份標頭資訊。 對於備份裝置中的每個備份，伺服器會將標頭資訊當做一個資料列來傳送。  
  
## <a name="security"></a>Security  
 備份作業可以選擇性地指定媒體集的密碼及 (或) 備份組的密碼。 當在媒體集或備份組上定義密碼時，您必須在 RESTORE 陳述式中，指定一個或多個正確的密碼。 這些密碼可以防止他人利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具，在未經授權的情況下，對媒體執行還原作業及附加備份組。 不過，密碼無法防止使用者利用 BACKUP 陳述式的 FORMAT 選項來覆寫媒體。  
  
> [!IMPORTANT]  
>  這個密碼所提供的保護很弱。 這是為了防止已獲授權或未獲授權的使用者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具進行不正確的還原。 它無法防止透過其他方式或以取代密碼的方式來讀取備份資料。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]保護備份的最佳做法是將備份磁帶存放在安全位置，或備份至受適當存取控制清單 (ACL) 保護的磁碟檔案中。 ACL 應該設在備份建立所在的根目錄下。  
  
### <a name="permissions"></a>Permissions  
 取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回磁碟檔 `C:\AdventureWorks-FullBackup.bak` 標頭中的資訊。  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [在備份或還原期間啟用或停用備份總和檢查碼 &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
