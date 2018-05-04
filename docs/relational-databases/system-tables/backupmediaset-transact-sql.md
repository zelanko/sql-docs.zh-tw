---
title: backupmediaset (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f394fc3ece4b7eb6c0a5b333ac597effe5c1dcc5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每個備份組各含一個資料列。 這份資料表儲存在**msdb**資料庫。  
 
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|唯一媒體集識別碼。 識別，主索引鍵。|  
|**media_uuid**|**uniqueidentifier**|媒體集的 UUID。 所有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]媒體集都有一個 UUID。<br /><br /> 舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不過，如果媒體集包含僅由一個媒體家族**media_uuid**資料行可能是 NULL (**media_family_count**為 1)。|  
|**media_family_count**|**tinyint**|媒體集中的媒體家族數目。 可以是 NULL。|  
|**name**|**nvarchar(128)**|媒體集的名稱。 可以是 NULL。<br /><br /> 如需詳細資訊，請參閱 MEDIANAME 和 MEDIADESCRIPTION 中的[備份&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。|  
|**描述**|**nvarchar(255)**|媒體集的文字描述。 可以是 NULL。<br /><br /> 如需詳細資訊，請參閱 MEDIANAME 和 MEDIADESCRIPTION 中的[備份&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。|  
|**software_name**|**nvarchar(128)**|寫入媒體標籤的備份軟體名稱。 可以是 NULL。|  
|**software_vendor_id**|**int**|寫入備份媒體標籤的軟體供應商識別碼。 可以是 NULL。<br /><br /> 值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是十六進位 0x1200。|  
|**MTF_major_version**|**tinyint**|用來產生這個媒體集之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format 的主要版本號碼。 可以是 NULL。|  
|**mirror_count**|**tinyint**|媒體集中的鏡像數目。|  
|**is_password_protected**|**bit**|這是指媒體集是否有密碼保護：<br /><br /> 0 = 無保護<br /><br /> 1 = 保護|  
|**is_compressed**|**bit**|備份是否經過壓縮：<br /><br /> 0 = 未壓縮<br /><br /> 1 = 已壓縮<br /><br /> 期間**msdb**升級時，此值設為 NULL。 這表示非壓縮的備份。|  
|**is_encrypted**|**Bit**|備份是否經過加密：<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密|  
  
## <a name="remarks"></a>備註  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY 會的資料行**backupmediaset**媒體集標頭的適當值的資料表。  
  
 若要減少此資料表和其他備份和記錄資料表中的資料列數目，請執行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [備份與還原資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
