---
title: RESTORE FILELISTONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 892b18ac9780054cafe90d62569afb63f8261b3e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68742983"
---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTORE 陳述式 - FILELISTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]


  傳回含有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫清單的結果集及備份組所包含的記錄檔。  

> [!NOTE]  
>  如需引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE FILELISTONLY   
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
   | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  

> [!NOTE] 
> URL 是用來指定 Microsoft Azure Blob 儲存體位置和檔案名稱的格式，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 開始支援。 雖然 Microsoft Azure 儲存體是一項服務，但其實作方式類似於磁碟和磁帶，以便為這三種裝置提供一致且順暢的還原體驗。

## <a name="arguments"></a>引數  
 如需 RESTORE FILELISTONLY 引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
## <a name="result-sets"></a>結果集  
 用戶端可以利用 RESTORE FILELISTONLY 來取得備份組所包含的檔案清單。 這項資訊會當做結果集傳回，其中針對每個檔案各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-|-|-|  
|LogicalName|**nvarchar(128)**|檔案的邏輯名稱。|  
|PhysicalName|**nvarchar(260)**|檔案的實體或作業系統名稱。|  
|類型|**char(1)**|這是檔案的類型，它有下列幾種：<br /><br /> **L** = Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔<br /><br /> **D** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔<br /><br /> **F** = 全文檢索目錄<br /><br /> **S** = FileStream、FileTable 或 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 容器|  
|FileGroupName|**nvarchar(128)** NULL|檔案所在的檔案群組名稱。|  
|大小|**numeric(20,0)**|目前的大小 (以位元組為單位)。|  
|MaxSize|**numeric(20,0)**|允許的大小上限 (以位元組為單位)。|  
|FileID|**bigint**|檔案的識別碼，它在資料庫中是唯一的。|  
|CreateLSN|**numeric(25,0)**|建立檔案的記錄序號。|  
|DropLSN|**numeric(25,0)** NULL|卸除檔案的記錄序號。 如果檔案尚未卸除，這個值就是 NULL。|  
|UniqueID|**uniqueidentifier**|檔案的全域唯一識別碼。|  
|ReadOnlyLSN|**numeric(25,0) NULL**|包含從讀寫改成唯讀 (最近的變更) 的檔案之檔案群組所在的記錄序號。|  
|ReadWriteLSN|**numeric(25,0)** NULL|包含從唯讀改成讀寫 (最近的變更) 的檔案之檔案群組所在的記錄序號。|  
|BackupSizeInBytes|**bigint**|這個檔案的備份大小 (以位元組為單位)。|  
|SourceBlockSize|**int**|檔案所在實體裝置 (不是備份裝置) 的區塊大小 (以位元組為單位)。|  
|FileGroupID|**int**|檔案群組的識別碼。|  
|LogGroupGUID|**uniqueidentifier** NULL|NULL。|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|如果是差異備份，記錄序號大於或等於 **DifferentialBaseLSN** 的變更會併入差異備份中。<br /><br /> 如果是其他備份類型，這個值就是 NULL。|  
|DifferentialBaseGUID|**uniqueidentifier** NULL|如果是差異備份，就是差異基底的唯一識別碼。<br /><br /> 如果是其他備份類型，這個值就是 NULL。|  
|IsReadOnly|**bit**|**1** = 檔案唯讀。|  
|IsPresent|**bit**|**1** = 檔案在備份中。|  
|TDEThumbprint|**varbinary(32)** NULL|顯示資料庫加密金鑰的指模。 加密程式指模是用來加密金鑰的憑證 SHA-1 雜湊。 如需資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。|  
|SnapshotURL|**nvarchar(360)** NULL|FILE_SNAPSHOT 備份中包含之資料庫檔案的 Azure 快照集 URL。 如果沒有 FILE_SNAPSHOT 備份，則傳回 NULL。|  
  
## <a name="security"></a>安全性  
 備份作業可以選擇性地指定媒體集的密碼及 (或) 備份組的密碼。 當在媒體集或備份組上定義密碼時，您必須在 RESTORE 陳述式中，指定一個或多個正確的密碼。 這些密碼可以防止他人使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具，在未獲授權的情況下，在媒體上執行還原作業及附加備份組。 不過，密碼無法防止使用者利用 BACKUP 陳述式的 FORMAT 選項來覆寫媒體。  
  
> [!IMPORTANT]  
>  這個密碼所提供的保護很弱。 這是為了防止已獲授權或未獲授權的使用者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具進行不正確的還原。 它無法防止透過其他方式或以取代密碼的方式來讀取備份資料。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 保護備份的最佳作法是將備份磁帶存放在安全位置，或備份至適當的存取控制清單 (ACL) 所保護的磁碟檔案中。 ACL 應該設在備份建立所在的根目錄下。  
  
### <a name="permissions"></a>權限  
 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會從名稱為 `AdventureWorksBackups` 的備份裝置傳回資訊。 此範例使用 `FILE` 選項指定裝置的第二個備份組。  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
