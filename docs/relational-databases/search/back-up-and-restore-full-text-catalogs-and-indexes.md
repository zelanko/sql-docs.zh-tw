---
title: 備份並還原全文檢索目錄與索引 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
caps.latest.revision: 62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 92cfb3b9b67b622c82031dde7d43f497a2714d07
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>備份並還原全文檢索目錄與索引。
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題說明如何備份和還原在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中建立的全文檢索索引。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，全文檢索目錄是邏輯概念，而且不會位於檔案群組中。 因此，若要備份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的全文檢索目錄，您必須識別包含屬於此目錄之全文檢索索引的每個檔案群組。 然後，您必須逐一備份這些檔案群組。  
  
> [!IMPORTANT]  
>  您可以在升級 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫時，匯入全文檢索目錄。 每個匯入的全文檢索目錄都是其檔案群組中的資料庫檔案。 若要備份匯入的目錄，只要備份其檔案群組即可。 如需詳細資訊，請參閱《 [線上叢書》中的](http://go.microsoft.com/fwlink/?LinkID=121052)備份和還原 SQL Server 2008 全文檢索目錄 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
##  <a name="backingup"></a> 備份全文檢索目錄的全文檢索索引  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> 尋找全文檢索目錄的全文檢索索引  
 您可以使用下列 [SELECT](../../t-sql/queries/select-transact-sql.md) 陳述式 (從 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) 和 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 目錄檢視中選取資料行) 來擷取全文檢索索引的屬性。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  
  
###  <a name="Find_FG_of_FTI"></a> 尋找包含全文檢索索引的檔案群組或檔案  
 建立全文檢索索引時，它會放置於下列其中一個位置：  
  
-   使用者指定的檔案群組。  
  
-   與基底資料表或檢視表相同的檔案群組 (若為非資料分割資料表)。  
  
-   主要檔案群組 (若為資料分割資料表)。  
  
> [!NOTE]  
>  如需建立全文檢索索引的相關資訊，請參閱[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)和 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
 若要針對某個資料表或檢視表尋找全文檢索索引的檔案群組，請使用下列查詢，其中 *object_name* 是資料表或檢視表的名稱：  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  
  
###  <a name="Back_up_FTIs_of_FTC"></a> 備份包含全文檢索索引的檔案群組  
 尋找包含全文檢索目錄之索引的檔案群組之後，您必須備份每個檔案群組。 在備份程序期間，您可能無法卸除或加入全文檢索目錄。  
  
 檔案群組的第一個備份必須是完整檔案備份。 建立檔案群組的完整檔案備份之後，您就可以透過建立一系列的一個或多個差異檔案備份 (以完整檔案備份為基礎)，僅備份檔案群組中的變更。  
  
 **備份檔案與檔案群組**  
  
-   [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  
##  <a name="Restore_FTI"></a> 還原全文檢索索引  
 還原備份的檔案群組就會還原全文檢索索引檔案，以及檔案群組中的其他檔案。 根據預設，檔案群組會還原至備份檔案群組所在的磁碟位置。  
  
 如果建立備份時，全文檢索索引資料表已在線上，而且正在進行母體擴展，就會在還原之後繼續進行母體擴展。  
  
 **還原檔案群組**  
  
-   [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [以覆蓋現有檔案的方式還原檔案與檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [將檔案還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
## <a name="see-also"></a>另請參閱  
 [管理及監視伺服器執行個體的全文檢索搜尋](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
