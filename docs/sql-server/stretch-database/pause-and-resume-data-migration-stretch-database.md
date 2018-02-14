---
title: "暫停和繼續資料移轉 (Stretch Database) | Microsoft Docs"
ms.custom: 
ms.date: 06/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, pausing and resuming
- pausing Stretch Database
- resuming Stretch Database
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a668af6406490e36584d9ad7754f4f783b8b0be
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="pause-and-resume-data-migration-stretch-database"></a>暫停和繼續資料移轉 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要暫停或繼續將資料移轉至 Azure，請在 SQL Server Management Studio 中的資料表選取 [延展]，然後選取 [暫停] 以暫停資料移轉，或選取 [繼續] 以繼續資料移轉。 您也可以使用 Transact-SQL 來暫停或繼續資料移轉。  
  
 當您要對本機伺服器的問題進行疑難排解，或將可用的網路頻寬最大化時，請在個別的資料表上暫停資料移轉。  

## <a name="pause-data-migration"></a>暫停資料移轉  
  
### <a name="use-sql-server-management-studio-to-pause-data-migration"></a>使用 SQL Server Management Studio 暫停資料移轉  
  
1.  在 SQL Server Management Studio 的 [物件總管] 中，選取您要暫停資料移轉的已啟用 Stretch 的資料表。  
  
2.  按一下滑鼠右鍵並選取 [延展]，然後選取 [暫停]。  
  
### <a name="use-transact-sql-to-pause-data-migration"></a>使用 Transact-SQL 暫停資料移轉  
 執行下列命令。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## <a name="resume-data-migration"></a>繼續資料移轉  
  
### <a name="use-sql-server-management-studio-to-resume-data-migration"></a>使用 SQL Server Management Studio 繼續資料移轉  
  
1.  在 SQL Server Management Studio 的 [物件總管] 中，選取您要繼續資料移轉的已啟用 Stretch 的資料表。  
  
2.  按一下滑鼠右鍵並選取 [延展]，然後選取 [繼續]。  
  
### <a name="use-transact-sql-to-resume-data-migration"></a>使用 Transact-SQL 繼續資料移轉  
 執行下列命令。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## <a name="check-whether-migration-is-active-or-paused"></a>檢查移轉為使用中或已暫停

### <a name="use-sql-server-management-studio-to-check-whether-migration-is-active-or-paused"></a>使用 SQL Server Management Studio 以檢查移轉為使用中或已暫停
在 SQL Server Management Studio 中，開啟 [Stretch Database 監視器]，並檢查 [移轉狀態] 資料行的值。 如需詳細資訊，請參閱[監視及疑難排解資料移轉](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)。

### <a name="use-transact-sql-to-check-whether-migration-is-active-or-paused"></a>使用 Transact-SQL 以檢查移轉為使用中或已暫停
查詢 **sys.remote_data_archive_tables** 目錄檢視，並檢查 **is_migration_paused** 資料行的值。 如需詳細資訊，請參閱 [sys.remote_data_archive_tables](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)。

## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[監視及疑難排解資料移轉](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  
