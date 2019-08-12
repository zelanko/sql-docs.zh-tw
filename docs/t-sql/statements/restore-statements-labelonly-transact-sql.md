---
title: RESTORE LABELONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4d763ccf2799ea72a1882a576e4b17ef839e3f1e
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742954"
---
# <a name="restore-statements---labelonly-transact-sql"></a>RESTORE 陳述式 - LABELONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]
  傳回含有給定備份裝置所識別的備份媒體之相關資訊的結果集。  
  
> [!NOTE]  
>  如需引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
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
 如需 RESTORE LABELONLY 引數的描述，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
## <a name="result-sets"></a>結果集  
 RESTORE LABELONLY 的結果集由單一資料列和這項資訊組成。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**MediaName**|**nvarchar(128)**|媒體名稱。|  
|**MediaSetId**|**uniqueidentifier**|媒體集的唯一識別碼。|  
|**FamilyCount**|**int**|媒體集中的媒體家族數目。|  
|**FamilySequenceNumber**|**int**|這個家族的序號。|  
|**MediaFamilyId**|**uniqueidentifier**|媒體家族的唯一識別碼。|  
|**MediaSequenceNumber**|**int**|這個媒體在媒體家族中的序號。|  
|**MediaLabelPresent**|**tinyint**|媒體描述是否包含：<br /><br /> **1** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format 媒體標籤<br /><br /> **0** = 媒體描述|  
|**MediaDescription**|**nvarchar(255)**|媒體描述 (自由形式文字) 或這個磁帶格式媒體標籤。|  
|**SoftwareName**|**nvarchar(128)**|寫入標籤的備份軟體名稱。|  
|**SoftwareVendorId**|**int**|寫入備份的軟體供應商之唯一供應商識別碼。|  
|**MediaDate**|**datetime**|標籤的寫入日期和時間。|  
|**Mirror_Count**|**int**|媒體集中的鏡像數目 (1-4)。<br /><br /> 注意:針對相同媒體集中不同鏡像而寫入的標籤都相同。|  
|**IsCompressed**|**bit**|備份是否經過壓縮：<br /><br /> 0 = 未壓縮<br /><br /> 1 = 已壓縮|  
  
> [!NOTE]  
>  如果定義了媒體集的密碼，只有在命令的 MEDIAPASSWORD 選項指定了正確的媒體密碼時，RESTORE LABELONLY 才會傳回資訊。  
  
## <a name="general-remarks"></a>一般備註  
 執行 RESTORE LABELONLY 是快速了解備份媒體包含哪些項目的方式。 由於 RESTORE LABELONLY 只會讀取媒體標頭，因此，即便使用高容量的磁帶裝置，這個陳述式的完成速度也很快。  
  
## <a name="security"></a>Security  
 備份作業可以選擇性地指定媒體集的密碼。 定義了媒體集的密碼之後，您必須在 RESTORE 陳述式中指定正確的密碼。 該密碼可以防止他人利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具，在未獲授權的情況下，在媒體上執行還原作業及附加備份組。 不過，密碼無法防止使用者利用 BACKUP 陳述式的 FORMAT 選項來覆寫媒體。  
  
> [!IMPORTANT]  
>  這個密碼所提供的保護很弱。 這是為了防止已獲授權或未獲授權的使用者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具進行不正確的還原。 它無法防止透過其他方式或以取代密碼的方式來讀取備份資料。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]保護備份的最佳做法是將備份磁帶存放在安全位置，或備份至受適當存取控制清單 (ACL) 保護的磁碟檔案中。 ACL 應該設在備份建立所在的根目錄下。  
  
### <a name="permissions"></a>權限  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中，取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
