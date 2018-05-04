---
title: restorehistory (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
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
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6216c36edeb2fac643e9ad28f5e823f39945456d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每項還原作業都有一個資料列。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|用來識別每項還原作業的唯一識別碼。 識別，主索引鍵。|  
|**restore_date**|**datetime**|還原作業的完成日期和時間。 可以是 NULL。|  
|**destination_database_name**|**nvarchar(128)**|還原作業的目的地資料庫名稱。 可以是 NULL。|  
|**user_name**|**nvarchar(128)**|執行還原作業的使用者名稱。 可以是 NULL。|  
|**backup_set_id**|**int**|用來識別還原的備份組的唯一識別碼。 參考**backupset （backup_set_id)**。|  
|**restore_type**|**char(1)**|還原作業的類型：<br /><br /> D = 資料庫<br /><br /> F = 檔案<br /><br /> G = 檔案群組<br /><br /> I = 差異<br /><br /> L = 記錄<br /><br /> V = 僅驗證<br /><br /> 可以是 NULL。|  
|**replace**|**bit**|指出還原作業是否指定了 REPLACE 選項：<br /><br /> 1 = 已指定<br /><br /> 0 = 未指定<br /><br /> 可以是 NULL。<br /><br /> 當資料庫還原到某個資料庫快照集時，0 是唯一選項。|  
|**recovery**|**bit**|指出還原作業指定了 RECOVERY 或 NORECOVERY 選項：<br /><br /> 1 = RECOVERY<br /><br /> 可以是 NULL。<br /><br /> 當資料庫還原成資料庫快照集時，1 是唯一的選項。<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|指出還原作業是否指定了 RESTART 選項：<br /><br /> 1 = 已指定<br /><br /> 0 = 未指定<br /><br /> 可以是 NULL。<br /><br /> 當資料庫還原到某個資料庫快照集時，0 是唯一選項。|  
|**stop_at**|**datetime**|復原資料庫的時間點。 可以是 NULL。|  
|**device_count**|**tinyint**|還原作業所涉及的裝置數目。 這個數目可以小於備份媒體家族的數目。 可以是 NULL。<br /><br /> 當資料庫還原到某個資料庫快照集時，這個數目一律是 1。|  
|**stop_at_mark_name**|**nvarchar(128)**|指出復原到包含具名標示的交易。 可以是 NULL。<br /><br /> 當資料庫還原到某個資料庫快照集時，這個值是 NULL。|  
|**stop_before**|**bit**|指出復原是否包含具名標示的交易：<br /><br /> 0 = 復原暫停在標示交易之前。<br /><br /> 1 = 復原包括標示的交易。<br /><br /> 可以是 NULL。<br /><br /> 當資料庫還原到某個資料庫快照集時，這個值是 NULL。|  
  
## <a name="remarks"></a>備註  
 若要減少此資料表和其他備份和記錄資料表中的資料列數目，請執行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [備份與還原資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
