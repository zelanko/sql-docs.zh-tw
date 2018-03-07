---
title: "RESTORE FILELISTONLY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6776115033e6e7222abc610673dd8b0aaff81dc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTORE 陳述式-FILELISTONLY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回含有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫清單的結果集及備份組所包含的記錄檔。  
  
> [!NOTE]  
>  如需引數的描述，請參閱[RESTORE 引數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
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
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>引數  
 如需 RESTORE FILELISTONLY 引數的描述，請參閱[RESTORE 引數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>結果集  
 用戶端可以利用 RESTORE FILELISTONLY 來取得備份組所包含的檔案清單。 這項資訊會當做結果集傳回，其中針對每個檔案各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-|-|-|  
|LogicalName|**nvarchar(128)**|檔案的邏輯名稱。|  
|PhysicalName|**nvarchar(260)**|檔案的實體或作業系統名稱。|  
|型別|**char(1)**|這是檔案的類型，它有下列幾種：<br /><br /> **L** = Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔<br /><br /> **D**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料檔案<br /><br /> **F** = 全文檢索目錄<br /><br /> **S** = FileStream、 FileTable 或[!INCLUDE[hek_2](../../includes/hek-2-md.md)]容器|  
|FileGroupName|**nvarchar(128)**|檔案所在的檔案群組名稱。|  
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
|LogGroupGUID|**uniqueidentifier NULL**|NULL。|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|差異備份，變更的記錄序號大於或等於**DifferentialBaseLSN**隨附的差異。<br /><br /> 如果是其他備份類型，這個值就是 NULL。|  
|DifferentialBaseGUID|**uniqueidentifier**|如果是差異備份，就是差異基底的唯一識別碼。<br /><br /> 如果是其他備份類型，這個值就是 NULL。|  
|IsReadOnly|**bit**|**1** = 檔案是唯讀的。|  
|IsPresent|**bit**|**1** = 檔案存在於在備份中。|  
|TDEThumbprint|**varbinary(32)**|顯示資料庫加密金鑰的指模。 加密程式指模是用來加密金鑰的憑證 SHA-1 雜湊。 資料庫加密的相關資訊，請參閱[透明資料加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).|  
|SnapshotURL|**nvarchar(360)**|FILE_SNAPSHOT 備份中包含的資料庫檔案 Azure 快照集 URL。 如果沒有 FILE_SNAPSHOT 備份，則傳回 NULL。|  
  
## <a name="security"></a>Security  
 備份作業可以選擇性地指定媒體集的密碼及 (或) 備份組的密碼。 當在媒體集或備份組上定義密碼時，您必須在 RESTORE 陳述式中，指定一個或多個正確的密碼。 這些密碼防止未經授權的還原作業，而且未經授權的附加至媒體使用的備份組[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]工具。 不過，密碼無法防止使用者利用 BACKUP 陳述式的 FORMAT 選項來覆寫媒體。  
  
> [!IMPORTANT]  
>  這個密碼所提供的保護很弱。 這是為了防止已獲授權或未獲授權的使用者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具進行不正確的還原。 它無法防止透過其他方式或以取代密碼的方式來讀取備份資料。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 保護備份的最佳作法是將備份磁帶存放在安全位置，或備份至適當的存取控制清單 (ACL) 所保護的磁碟檔案中。 ACL 應該設在備份建立所在的根目錄下。  
  
### <a name="permissions"></a>Permissions  
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
  
  
