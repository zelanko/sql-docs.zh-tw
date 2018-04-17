---
title: sp_delete_backup (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26f0dde7c29de4e9ded31217f5da6fdff952def2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  刪除所有快照集和備份檔案，其中包含從指定的資料庫設定的快照集備份。 此系統預存程序是用於管理快照集備份組的唯一建議的方法。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>引數  
 *[ @backup_url = ] backup_meta_file_url*  
 這會刪除所有快照集包含指定的備份組包括備份檔案本身要刪除、 備份的 URL。  
  
 *[ @db_name =] 資料庫名稱*  
 包含要刪除的快照集之資料庫的名稱。 資料庫名稱時提供，系統會驗證備份 URL 提供備份 URL 指定的資料庫，然後再使用[sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)刪除每個快照集。 如果沒有資料庫提供名稱，此資料庫的檢查不會執行。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY DATABASE 權限或 ALTER 權限指定的資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_db_backup_file_snapshots &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
