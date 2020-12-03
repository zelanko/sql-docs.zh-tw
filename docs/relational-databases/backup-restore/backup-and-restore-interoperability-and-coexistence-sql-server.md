---
title: 備份與還原：功能互通性
description: 本文描述 SQL Server 中的備份與還原功能，包括資料庫啟動、線上還原和停用的索引，以及資料庫鏡像。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server], related features
- restoring [SQL Server], files
- restoring files [SQL Server], related features
- backups [SQL Server], files or filegroups
- file backups [SQL Server], related features
ms.assetid: 69f212b8-edcd-4c5d-8a8a-679ced33c128
author: cawrites
ms.author: chadam
ms.openlocfilehash: 106773df7a5e9f88c123b614688ca19722613d7f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130538"
---
# <a name="backup-and-restore-interoperability-and-coexistence-sql-server"></a>備份與還原：互通性與共存性 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本主題描述 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中數個功能的備份和還原考量。 這些功能包括：檔案還原和資料庫啟動、線上還原和停用的索引、資料庫鏡像，以及分次還原和全文檢索索引。  
  
 **本主題內容：**  
  
-   [檔案還原與資料庫啟動](#FileRestoreAndDbStartup)  
  
-   [線上還原和停用的索引](#OnlineRestoreAndDisabledIndexes)  
  
-   [資料庫鏡像與備份和還原](#DbMandBnR)  
  
-   [分次還原和全文檢索索引](#PiecemealAndFTIndexes)  
  
-   [檔案備份以及還原與壓縮](#FileBnRandCompression)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="file-restore-and-database-startup"></a><a name="FileRestoreAndDbStartup"></a> 檔案還原與資料庫啟動  
 本節僅與包含多個檔案群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。  
  
> [!NOTE]  
>  當資料庫啟動時，只有在資料庫關閉時其檔案仍在線上的檔案群組才會復原並回到線上。  
  
 如果在資料庫啟動期間發生問題，復原會失敗，且會將資料庫標示為 SUSPECT。 如果將問題隔離到檔案，資料庫管理員就可以使檔案離線，並嘗試重新啟動資料庫。 若要使檔案離線，您可以使用下列 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式：  
  
 ALTER DATABASE *database_name* MODIFY FILE (NAME **='** _filename_*_'_*, OFFLINE)  
  
 如果啟動成功，任何包含離線檔案的檔案群組都會保持離線。  
  
##  <a name="online-restore-and-disabled-indexes"></a><a name="OnlineRestoreAndDisabledIndexes"></a> 線上還原和停用的索引  
 本節僅與包含多個檔案群組 (在簡單復原模式下，至少有一個唯讀檔案群組) 的資料庫有關。  
  
 在這些案例中，如果資料庫在線上，則只有在保有索引任一部分的所有檔案群組都在線上時，才可以建立、卸除、啟用或停用索引。  
  
 如需還原離線檔案群組的相關資訊，請參閱[線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)。  
  
##  <a name="database-mirroring-and-backup-and-restore"></a><a name="DbMandBnR"></a> 資料庫鏡像與備份和還原  
 本節僅與包含多個檔案群組的完整模式資料庫有關。  
  
> [!NOTE]  
>  未來的 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本將移除資料庫鏡像功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。  
  
 資料庫鏡像是增加資料庫可用性的軟體方案。 鏡像是以每個資料庫為基準實作，只適用於使用完整復原模式的資料庫。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
> [!NOTE]  
>  若要散發資料庫中檔案群組子集的副本，請使用複寫：請只複寫檔案群組中您要複製到其他伺服器的物件。 如需複寫的詳細資訊，請參閱 [SQL Server 複寫](../../relational-databases/replication/sql-server-replication.md)。  
  
### <a name="creating-the-mirror-database"></a>建立鏡像資料庫  
 鏡像資料庫是透過在鏡像伺服器上還原 (但不復原) 主體資料庫備份的方式所建立。 還原必須保留相同的資料庫名稱。 如需詳細資訊，請參閱 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
 您可以使用分次還原順序來建立鏡像資料庫 (只要有支援)。 不過，要等到還原了所有檔案群組，而且通常還要在時間點上將記錄備份還原到夠接近主體資料庫的時間點之後，才能開始進行鏡像。 如需詳細資訊，請參閱[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
### <a name="restrictions-on-backup-and-restore-during-mirroring"></a>鏡像期間備份和還原的限制  
 資料庫鏡像工作階段使用中時，將套用下列限制：  
  
-   不允許備份和還原鏡像資料庫。  
  
-   允許備份主體資料庫，但不允許 BACKUP LOG WITH NORECOVERY。  
  
-   不允許還原主體資料庫。  
  
##  <a name="piecemeal-restore-and-full-text-indexes"></a><a name="PiecemealAndFTIndexes"></a> 分次還原和全文檢索索引  
 本節只與包含多個檔案群組的資料庫有關，而在簡單模式資料庫中僅與唯讀檔案群組相關。  
  
 全文檢索索引會儲存在資料庫檔案群組中，而且可能會受到分次還原的影響。 如果全文檢索索引與任何相關聯的資料表資料位於相同的檔案群組中，分次還原就會依照預期方式運作。  
  
> [!NOTE]  
>  若要檢視包含全文檢索索引之檔案群組的檔案群組識別碼，請選取 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)的 data_space_id 資料行。  
  
### <a name="full-text-indexes-and-tables-in-separate-filegroups"></a>個別檔案群組中的全文檢索索引和資料表  
 如果全文檢索索引與所有相關聯的資料表資料位於不同的檔案群組中，則分次還原的行為會取決於第一個還原且上線的檔案群組而定：  
  
-   如果包含全文檢索索引的檔案群組在包含相關聯資料表資料的檔案群組之前還原並上線，一旦全文檢索索引上線時，全文檢索搜尋就會依照預期方式運作。  
  
-   如果包含資料表資料的檔案群組在包含全文檢索索引的檔案群組之前還原並上線，則全文檢索行為可能會受到影響。 這是因為在索引上線之前，觸發母體擴展、重建目錄或重新組織目錄的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式都會失敗。 這些陳述式包括 CREATE FULLTEXT INDEX、ALTER FULLTEXT INDEX、DROP FULLTEXT INDEX 和 ALTER FULLTEXT CATALOG。  
  
     在此情況下，下列因素就很重要：  
  
    -   如果全文檢索索引具有變更追蹤，在索引檔案群組上線之前，使用者 DML 將會失敗。 此外，在索引檔案群組上線之前，刪除作業也會失敗。  
  
    -   無論變更追蹤與否，全文檢索查詢都會失敗，因為無法使用索引。 如果在包含全文檢索索引的檔案群組離線時，嘗試全文檢索查詢，將會傳回錯誤。  
  
    -   只有當狀態函數 (例如 FULLTEXTCATALOGPROPERTY) 不需要存取全文檢索索引時，這些函數才會成功。 例如，存取任何線上全文檢索中繼資料都會成功，但是 **uniquekeycount、itemcount** 卻會失敗。  
  
     在全文檢索索引檔案群組還原並上線之後，索引資料與資料表資料就會一致。  
  
 一旦資料表檔案群組和群組檢索索引檔案群組都上線時，任何暫停的全文檢索母體擴展就會繼續進行。  
  
##  <a name="file-backup-and-restore-and-compression"></a><a name="FileBnRandCompression"></a> 檔案備份以及還原與壓縮  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援唯讀檔案群組及唯讀資料庫的 NTFS 檔案系統資料壓縮。  
  
 壓縮的 NTFS 檔案支援唯讀檔案群組中的檔案還原。 這些檔案群組的備份與還原，本質上與任何唯讀檔案群組相同，但有下列例外狀況：  
  
-   將讀寫檔案 (包括讀寫資料庫的主要檔案或記錄檔) 還原至壓縮磁碟區會失敗，並顯示錯誤。  
  
-   允許將唯讀資料庫還原至壓縮磁碟區。  
  
> [!NOTE]  
>  讀取/寫入資料庫的記錄檔絕不可放在壓縮檔案系統上。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [備份並還原全文檢索目錄與索引](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
[使用中次要：在次要複本上備份 \(Always On 可用性群組\)](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
