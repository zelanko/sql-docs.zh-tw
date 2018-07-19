---
title: sp_delete_backup & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2955570ee99eaa05d9a689ccbe62973af3208d80
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054445"
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  刪除所有快照集和備份檔案包含從指定的資料庫設定的快照集備份。 此系統預存程序是唯一的建議的方法，來管理快照集備份組。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>引數  
 *[ @backup_url = ] backup_meta_file_url*  
 備份會遭到刪除，這會刪除所有快照集，其中包含指定的備份組包括備份檔案本身的 URL。  
  
 *[ @db_name =] 資料庫名稱*  
 包含要刪除的快照集之資料庫的名稱。 當資料庫已提供名稱，系統會驗證備份 URL 提供指定之資料庫的備份 URL，並使用[sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)來刪除每個快照集。 如果沒有提供資料庫名稱時，不會執行這項資料庫檢查。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY DATABASE 權限或指定的資料庫上的 ALTER 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_db_backup_file_snapshots &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
