---
title: sp_delete_backup_file_snapshot & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66099ab0821bcccf399b353207c09b9571130736
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718656"
---
# <a name="spdeletebackupfilesnapshot-transact-sql"></a>sp_delete_backup_file_snapshot & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  從指定的資料庫中刪除指定的備份快照集。 使用此系統預存程序搭配**sys.fn_db_backup_file_snapshots**系統函式，來找出並刪除孤立的備份快照集。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N’<database_name>  
    , [ @snapshot_url = ] N’<snapshot_url>  
```  
  
## <a name="arguments"></a>引數  
 *[ @db_name =] 資料庫名稱*  
 包含要刪除、 提供做為 Unicode 字串的快照集之資料庫的名稱。  
  
 *[ @snapshot_url = ] snapshot_url*  
 若要刪除，做為 Unicode 字串提供快照集的 URL。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY DATABASE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_db_backup_file_snapshots &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
