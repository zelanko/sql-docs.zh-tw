---
title: sp_delete_backup （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67941827"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  從指定的資料庫中，刪除組成快照集備份組的所有快照和備份檔案。 這個系統預存程式是唯一建議用來管理快照集備份組的方法。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>引數  
 *[ @backup_url =] backup_meta_file_url*  
 要刪除之備份的 URL，這會刪除組成指定備份組的所有快照，包括備份檔案本身。  
  
 *[ @db_name =] database_name*  
 包含要刪除之快照集的資料庫名稱。 提供資料庫名稱時，系統會驗證所提供的備份 URL 是指定資料庫的備份 URL，並使用[sp_delete_backup_file_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)來刪除每個快照集。 如果未提供任何資料庫名稱，則不會執行此資料庫檢查。  
  
## <a name="permissions"></a>權限  
 需要指定資料庫的 ALTER ANY DATABASE 許可權或 ALTER 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
