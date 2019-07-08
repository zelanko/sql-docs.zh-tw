---
title: 線上還原 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06fb23f63b65d06be6e05569ecd31387830522ae
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581073"
---
# <a name="online-restore-sql-server"></a>線上還原 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 才支援線上還原。 在此版本中，檔案、分頁或分次還原預設都是在線上進行。 本主題僅與包含多個檔案或檔案群組 (若是簡單復原模式，則只有唯讀檔案群組) 的資料庫有關。  
  
 在資料庫還在線上時還原資料，就稱之為 *「線上還原」* 。 即使有一或多個次要檔案群組離線，只要主要檔案群組還在線上，就將資料庫視為在線上。 當資料庫在線上時，您可以在任何復原模式下還原離線的檔案。 當資料庫在線上時，您也可以在完整復原模式下還原頁面。  
  
> [!NOTE]  
>  線上還原會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 版中自動發生，不需要任何使用者動作。 如果您不想要使用線上還原，則可以先使資料庫離線，再啟動還原。 如需詳細資訊，請參閱本主題稍後的「 [使資料庫或檔案離線](#taking_db_or_file_offline)」。  
  
 在線上檔案還原期間，任何即將還原的檔案及其檔案群組都會離線。 當線上還原啟動時，如果這其中還有任何檔案在線上，第一個還原陳述式就會讓檔案的檔案群組離線。 相反地，在線上分頁還原期間，只有頁面會離線。  
  
 每個線上還原實例都包括下列基本步驟：  
  
1.  還原資料。  
  
2.  針對最後一次記錄還原，使用 WITH RECOVERY 來還原記錄。 這會使還原的資料上線。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 有時候會因為回復所需的資料在啟動期間離線，而無法回復未認可的交易。 在此情況下，將會延遲交易。 如需詳細資訊，請參閱 [延遲交易 &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)中無用的檔案群組。  
  
> [!NOTE]  
>  如果資料庫目前正在使用大量記錄復原模式，建議您先切換到完整復原模式，再啟動線上還原。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
> [!IMPORTANT]  
>  如果備份是在附加至伺服器的多個裝置上進行，則在執行線上還原時，必須有相同數目的裝置可用。  
  
> [!CAUTION]  
>  使用快照集備份時，您無法執行「線上還原」  。 如需**快照集備份**的詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
## <a name="log-backups-for-online-restore"></a>線上還原的記錄備份  
 在線上還原中，復原點就是還原的資料變成離線或最後一次設為唯讀的時間點。 能夠重建及包含此復原點的交易記錄備份，必須完整備妥。 一般而言，在該時間點後必須有記錄備份，才能涵蓋檔案的復原點。 唯一的例外就是從資料變成唯讀後建立的資料備份中，對唯讀資料所進行的線上還原。 在這種情況下，您不需要有記錄備份。  
  
 一般而言，即使在還原順序啟動之後，您還是可以在資料庫仍在線上時進行交易記錄備份。 最後記錄備份的時間點取決於要還原之檔案的屬性：  
  
-   對於線上唯讀檔案，您可以在第一個還原順序之前或當中進行復原所需的最後一次記錄備份。 如果是在檔案群組成為唯讀之後進行資料或差異備份，唯讀檔案群組就可以不需要記錄備份。  
  
    > [!NOTE]  
    >  上述資訊也同樣適用於每個離線檔案。  
  
-   比較特殊的情況是，在發出第一個還原陳述式時仍在線上，但之後因該還原陳述式而自動離線的讀取/寫入檔案。 在此情況下，您必須在第一個「還原順序」  (此順序中包含一或多個可還原、向前復原及復原資料的 RESTORE 陳述式) 期間進行記錄備份。 一般而言，必須在還原所有完整備份之後，而且在復原資料之前進行這個記錄備份。 不過，如果特定的檔案群組有多個檔案備份，則記錄備份最晚的時間點是在檔案群組離線之後的時間。 這個資料還原後的記錄備份會擷取檔案離線時的時間點。 資料還原後的記錄備份是必要的，因為 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 無法使用線上記錄進行線上還原。  
  
    > [!NOTE]  
    >  此外，您也可以在還原順序之前手動使檔案離線。 如需詳細資訊，請參閱本主題稍後的「使資料庫或檔案離線」。  
  
##  <a name="taking_db_or_file_offline"></a> 使資料庫或檔案離線  
 如果您不想要使用線上還原，則可以使用下列其中一個方法先讓資料庫離線，再來啟動還原順序：  
  
-   在任何復原模式下，您可以使用下列 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式，讓資料庫離線：  
  
     ALTER DATABASE *database_name* SET OFFLINE  
  
-   或者，也可以在完整復原模式下強制檔案或分頁還原離線，方法是使用下列 [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) 陳述式，將資料庫置於正在還原狀態：  
  
     BACKUP LOG *database_name* WITH NORECOVERY。  
  
 只要資料庫仍然離線，所有的還原就都是離線還原。  
  
## <a name="examples"></a>範例  
  
> [!NOTE]  
>  線上還原順序的語法和離線還原順序的語法相同。  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [範例：線上還原讀取/寫入檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [在不還原資料的情況下復原資料庫 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [移除無用的檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
