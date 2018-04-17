---
title: managed_backup.fn_available_backups (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_available_backups
- smart_admin.fn_available_backups_TSQL
- fn_available_backups_TSQL
- fn_available_backups
dev_langs:
- TSQL
helpviewer_keywords:
- fn_available_backups
- smart_admin.fn_available_backups
ms.assetid: 7aa84474-16e5-49bd-a703-c8d1408ef107
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a86ac3447c3bdefbef53fc23acd303502b40f22
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="managedbackupfnavailablebackups-transact-sql"></a>managed_backup.fn_available_backups (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  傳回指定資料庫之可用備份檔案的資料表，內含 0、1 或更多資料列。 傳回的備份檔案是 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 建立的備份。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.fn_available_backups ([@database_name = ] 'database name')  
```  
  
##  <a name="Arguments"></a> 引數  
 @database_name  
 資料庫的名稱。 @database_name是 nvarchar （512）。  
  
## <a name="table-returned"></a>傳回的資料表  
 資料表已啟用唯一的叢集條件約束 (database_guid、backup_start_date、first_lsn 和 backup_type)。   
如果卸除資料庫再重新建立，則會傳回所有資料庫的備份組。 此輸出是依照可唯一識別每個資料庫的 database_guid 排序。   
如果 LSN 有間距，表示記錄鏈結中斷，資料表將針對每個遺漏的 LSN 區段各包含一個特殊資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|Backup_path|NVARCHAR(260) COLLATE Latin1_General_CI_AS_KS_WS|備份檔案的 URL。|  
|backup_type|NVARCHAR(6)|'DB' 表示資料庫備份，'LOG' 表示記錄備份|  
|expiration_date|DATETIME|此檔案預期要刪除的日期。 這會根據復原資料庫的能力設定為指定保留期限內的時間點。|  
|database_guid|UNIQUEIDENTIFIER|指定資料庫的 GUID 值。  此 GUID 會唯一識別資料庫。|  
|first_lsn|NUMERIC(25, 0)|備份組中第一個或最舊記錄檔記錄的記錄序號。 可以是 NULL。|  
|last_lsn|NUMERIC(25, 0)|備份組之後下一個記錄檔記錄的記錄序號。 可以是 NULL。|  
|backup_start_date|DATETIME|備份作業開始的日期和時間。|  
|backup_finish_date|NVARCHAR(128)|備份作業完成的日期和時間。|  
|machine_name|NVARCHAR(128)|安裝 SQL Server 執行個體並執行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的電腦名稱。|  
|last_recovery_fork_id|UNIQUEIDENTIFIER|結尾復原分岔的識別碼。|  
|first_recovery_fork_id|UNIQUEIDENTIFIER|起始復原分岔的識別碼。 對於資料備份而言，first_recovery_fork_guid 等於 last_recovery_fork_guid。|  
|fork_point_lsn|NUMERIC(25, 0)|如果 first_recovery_fork_id 不等於 last_recovery_fork_id，這就是分岔點的記錄序號。 否則，這個值是 NULL。|  
|availability_group_guid|UNIQUEIDENTIFIER|如果資料庫是 Alwayson 資料庫，這是可用性群組的 GUID。 否則，這個值是 NULL。|  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要**選取**這個函式上的權限。  
  
## <a name="examples"></a>範例  
 下列範例列出所有可用備份，透過資料庫 'MyDB' 的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 進行備份  
  
```  
SELECT *   
FROM managed_backup.fn_available_backups ('MyDB')  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Managed 的 Backup to Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)   
 [從儲存在 Microsoft Azure 的備份還原](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
