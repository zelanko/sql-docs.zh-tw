---
title: "backupfilegroup (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2787b6a012268378421017c0a2912385c669da17
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對備份時在資料庫中的每個檔案群組，各包含一個資料列。 **backupfilegroup**會儲存在**msdb**資料庫。  
  
> [!NOTE]  
>  **Backupfilegroup**表格顯示的資料庫，而不是備份組的檔案群組組態。 若要識別是否在備份組中包含的檔案，請使用**is_present**資料行[backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)資料表。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|包含這個檔案群組的備份組。|  
|**name**|**sysname**|檔案群組的名稱。|  
|**filegroup_id**|**int**|檔案群組的識別碼，它在資料庫中是唯一的。 對應至**data_space_id**中**sys.filegroups**。|  
|**filegroup_guid**|**uniqueidentifier**|檔案群組的全域唯一識別碼。 可以是 NULL。|  
|**type**|**char(2)**|這是內容類型，它有下列幾種：<br /><br /> FG = "Rows" 檔案群組<br /><br /> SL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔案群組|  
|**type_desc**|**nvarchar(60)**|這是函數類型的描述，它有下列幾種：<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP |  
|**is_default**|**bit**|在 CREATE TABLE 或 CREATE INDEX 中未指定檔案群組時，所使用的預設檔案群組。|  
|**is_readonly**|**bit**|1 = 檔案群組是唯讀的。|  
|**log_filegroup_guid**|**uniqueidentifier**|可以是 NULL。|  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  相同的檔案群組名稱可以出現在不同的資料庫中；每個檔案群組都有它自己的 GUID。 因此， **(backup_set_id，filegroup_guid)**識別中的檔案群組為唯一索引鍵**backupfilegroup**。  
  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY 會的資料行**backupmediaset**媒體集標頭的適當值的資料表。  
  
 若要減少此資料表和其他備份和記錄資料表中的資料列數目，請執行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [備份及還原資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系統資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
