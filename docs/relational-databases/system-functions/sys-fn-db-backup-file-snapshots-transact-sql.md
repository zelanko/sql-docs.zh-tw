---
title: sys.databases fn_db_backup_file_snapshots （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: d6944817524a339eb8e48aa223c291cef1de1879
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052748"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>sys.databases fn_db_backup_file_snapshots （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  傳回與資料庫檔案相關聯的 Azure 快照集。 如果找不到指定的資料庫，或資料庫檔案未儲存在 Microsoft Azure Blob 儲存體服務中，則不會傳回任何資料列。 請使用此系統函數搭配**sys. sp_delete_backup_file_snapshot**系統預存程式，來識別和刪除孤立的備份快照集。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>引數  
 *Database_name*  
 正在查詢之資料庫的名稱。 如果是 Null，則會在目前的資料庫範圍中執行此函式。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|file_id|**int**|資料庫的檔案識別碼。 不可為 Null。|  
|snapshot_time|**nvarchar(260)**|REST API 所傳回之快照集的時間戳記。 如果沒有快照集存在，則傳回 Null。|  
|snapshot_url|**nvarchar(360)**|檔案快照集的完整 URL。 如果沒有快照集存在，則傳回 Null。|  
  
## <a name="permissions"></a>權限  
 需要資料庫的 VIEW DATABASE STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_backup_file_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
