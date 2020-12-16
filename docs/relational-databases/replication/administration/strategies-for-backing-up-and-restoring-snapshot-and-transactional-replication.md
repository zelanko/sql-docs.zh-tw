---
title: 備份與還原快照式和異動複寫的策略 | Microsoft Docs
description: 了解在 SQL Server 中為快照式及異動複寫設計備份與還原策略時，所需考量的事項。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 1d395bebae8b009f4e91d8df074401f8659e1748
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467399"
---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>備份與還原快照式和異動複寫的策略
[!INCLUDE[sql-asdb](../../../includes/applies-to-version/sql-asdb.md)]
  當為快照式及異動複寫設計備份與還原策略時，需要考慮三個方面：  
  
-   要備份的資料庫。
-   異動複寫的備份設定。
-   還原資料庫的必要步驟。 這些步驟是根據複寫類型和所選擇的選項而不同。  
  
 本主題在接下來的三節中對這些方面一一進行說明。 如需 Oracle 發行之備份及還原的詳細資訊，請參閱 [Oracle 發行者的備份與還原](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md)。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="backing-up-databases"></a>備份資料庫  
 對於快照式及異動複寫，您應定期備份下列資料庫：  
  
-   在「發行者」端的發行集資料庫。  
  
-   在「散發者」端的散發資料庫。  
  
-   在每個「訂閱者」端的訂閱資料庫。  
  
-   發行者、散發者及所有訂閱者端的 **master** 與 **msdb** 系統資料庫。 這些資料庫應與其他每個及相關的複寫資料庫同時備份。 例如，在您備份發行集資料庫的同時，在「發行者」端備份 **master** 與 **msdb** 資料庫。 如果還原發行集資料庫，請確定 **master** 和 **msdb** 資料庫在複寫組態和設定上與發行集資料庫一致。  
  
 如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果不執行記錄備份，則每當與複寫相關的設定發生變更時，便應該執行備份。 如需相關資訊，請參閱 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)。  
  
## <a name="backup-settings-for-transactional-replication"></a>異動複寫的備份設定  
 異動複寫包含使用 **sync with backup** 選項 (可以在散發資料庫和發行集資料庫上設定)：  
  
-   建議在所有情況下，於散發資料庫上設定此選項。  
  
     在散發資料庫上設定此選項，可確保發行集資料庫記錄檔中的交易在散發資料庫中備份之前，不會被截斷。 散發資料庫可以還原到上次備份時的狀況，任何遺漏的交易都會從發行集資料庫傳遞到散發資料庫。 複寫會繼續，不受影響。  
  
     在散發資料庫上設定此選項不會影響複寫延遲。 不過，此選項會延遲截斷發行集資料庫上的記錄的時間，使其在散發資料庫中相對應的交易備份之前，不會被截斷 (這可能會造成發行集資料庫中存有較大的交易記錄)。  
  
-   如果您的應用程式允許額外的延遲，則建議在發行集資料庫上設定此選項。  
  
     在發行集資料庫上設定此選項，可確保交易在發行集資料庫中備份之前，不會傳遞到散發資料庫。 最近一次的發行集資料庫備份這時可以在「發行者」端還原，同時不會出現這種情況：散發資料庫擁有的交易，在還原的發行集資料庫中不存在。  
  
     延遲和輸送量會受到影響，因為交易在「發行者」端備份之前，不能傳遞到散發資料庫。 例如，如果交易記錄檔每五分鐘備份一次，則「發行者」端正在認可的交易與正在傳遞到散發資料庫 (繼而傳遞到「訂閱者」端) 的交易之間會存在額外的五分鐘延遲。  
  
    > [!NOTE]  
    >  **sync with backup** 選項確保了發行集資料庫與散發資料庫之間的一致性，但該選項不能保證資料不會遺失。 例如，如果交易記錄檔遺失，則自最後一次交易記錄檔備份以後才認可的交易，在發行集資料庫或散發資料庫中都不可用。 這是與非複寫資料庫相同的行為。  
  
 **若要設定 sync with backup 選項**  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計：[為異動複寫啟用協調備份 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>還原複寫中牽涉到的資料庫  
 如果最近的備份可用並遵循適當的步驟，則可以還原複寫拓撲中的所有資料庫。 發行集資料庫的還原步驟取決於所使用的複寫類型和選項，但是所有其他資料庫的還原步驟與複寫類型和選項無關。  
  
 複寫支援將複寫資料庫還原到與原先建立備份的同一個伺服器與資料庫。 如果您將複寫資料庫的備份還原到另一個伺服器或資料庫，將無法保留複寫設定。 在此情況下，您必須在還原備份之後，重新建立所有發行集和訂閱。  
  
### <a name="publisher"></a>發行者  
 對以下類型的複寫提供有還原步驟：  
  
-   快照式複寫  
  
-   唯讀異動複寫  
  
-   具有可更新訂閱的異動複寫  
  
-   點對點異動複寫  
  
 **msdb** 和 **master** 資料庫的還原 (也涵蓋在本節中) 對所有四種類型都相同。  
  
#### <a name="publication-database-snapshot-replication"></a>發行集資料庫：快照式複寫  
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  發行集資料庫備份是否包含所有發行集和訂閱的最新組態？ 若為是，則還原已經完成。 若為否，請移至步驟 3。  
  
3.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 還原即可完成。  
  
     如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
#### <a name="publication-database-read-only-transactional-replication"></a>發行集資料庫：唯讀異動複寫  
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  是否在失敗前對發行集資料庫啟用了 **sync with backup** 設定？ 若為是，請移至步驟 3；若為否，請移至步驟 5。  
  
     如果設定已啟用， `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` 查詢會傳回 '1'。  
  
3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則還原已經完成。 若為否，請移至步驟 4。  
  
4.  已還原發行集資料庫中的組態資訊並非最新； 因此，您必須確定「訂閱者」擁有散發資料庫中的所有未處理命令，然後再卸除及重新建立複寫組態。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有的命令都已傳遞給訂閱者，方法是使用「複寫監視器」中的 **[未散發的命令]** 索引標籤，或是在散發資料庫中查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 檢視。 移至步驟 b。  
  
         如需如何執行散發代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
         如需有關如何確認命令的詳細資訊，請參閱[在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 和[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
    2.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
5.  未在發行集資料庫上設定 **sync with backup** 選項； 因此，沒有包含在還原備份中的交易可能尚未傳遞到散發者和訂閱者。 您必須確定「訂閱者」已經擁有散發資料庫中的所有未處理命令，然後再手動將任何未包含在所還原備份中的交易，套用到發行集資料庫：  
  
    > [!IMPORTANT]  
    >  執行此程序可能會造成已發行資料表的還原時間點，比備份中所還原的其他未發行資料表還要新。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有的命令都已傳遞給訂閱者，方法是使用「複寫監視器」中的 **[未散發的命令]** 索引標籤，或是在散發資料庫中查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 檢視。 移至步驟 b。  
  
         如需如何執行散發代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
         如需有關如何確認命令的詳細資訊，請參閱[在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 和[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
    2.  使用 [tablediff 公用程式](../../../tools/tablediff-utility.md) 或其他工具來手動同步化發行者與訂閱者。 如此可讓您從訂閱資料庫中，復原沒有包含在發行集資料庫備份中的資料。 移至步驟 c。  
  
         如需 **tablediff** 公用程式的詳細資訊，請參閱 [比較複寫資料表的差異 &#40;複寫程式設計&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，請執行 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 預存程序，以重新同步處理「發行者」中繼資料資料與「散發者」中繼資料。 還原即可完成。 若為否，請移至步驟 d。  
  
    4.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>發行集資料庫：具有可更新訂閱的異動複寫  
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有的命令都已傳遞給「訂閱者」，方法是使用「複寫監視器」中的 **[未散發的命令]** 索引標籤，或是在散發資料庫中查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 檢視。 移至步驟 3。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
     如需有關如何確認命令的詳細資訊，請參閱[在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 和[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
3.  如要使用佇列更新訂閱，請連接到各訂閱者，並從訂閱資料庫的 [MSreplication_queue &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) 資料表中刪除所有資料列。 移至步驟 4。  
  
    > [!NOTE]  
    >  如果您正使用佇列更新訂閱以及包含識別欄位的任何資料表，則必須確保在還原後指派正確的識別範圍。 如需詳細資訊，請參閱[複寫識別資料欄](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
4.  您必須確定「訂閱者」已經擁有散發資料庫中的所有未處理命令，然後再手動將任何未包含在所還原備份中的交易，套用到發行集資料庫：  
  
    > [!IMPORTANT]  
    >  執行此程序可能會造成已發行資料表的還原時間點，比備份中所還原的其他未發行資料表還要新。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 透過使用「複寫監視器」，或透過查詢散發資料庫中的 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 檢視，確認所有命令是否已傳遞到「訂閱者」。 移至步驟 b。  
  
    2.  使用 [tablediff Utility](../../../tools/tablediff-utility.md) 或其他工具來手動同步化發行者與訂閱者。 如此可讓您從訂閱資料庫中，復原沒有包含在發行集資料庫備份中的資料。 移至步驟 c。  
  
         如需 **tablediff** 公用程式的詳細資訊，請參閱 [比較複寫資料表的差異 &#40;複寫程式設計&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，請執行 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 預存程序，以重新同步處理「發行者」中繼資料資料與「散發者」中繼資料。 還原即可完成。 若為否，請移至步驟 d。  
  
    4.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>發行集資料庫：@loopback_detection  
 在下列步驟中，發行集資料庫 **A**、 **B** 和 **C** 在點對點異動複寫拓撲中。 資料庫 **A** 和 **C** 在線上並正常運作；資料庫 **B** 則是要還原的資料庫。 此處所述的程序 (尤其是步驟 7、10 和 11)，與在點對點拓撲中加入節點的程序非常類似。 執行這些步驟最直接的方法是使用「設定點對點拓撲精靈」，但是您也可以使用預存程序。  
  
1.  執行散發代理程式，以便同步處理資料庫 **A** 和 **C** 中的訂閱。移至步驟 2。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
2.  如果 **B** 使用的散發資料庫仍然可用，則執行散發代理程式，以便同步處理資料庫 **B** 和 **A** 之間，以及資料庫 B 和 **C** 之間的訂閱。移至步驟 3。  
  
3.  透過在 **B** 的散發資料庫執行 [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md)，從 **B** 使用的散發資料庫中移除中繼資料。移至步驟 4。  
  
4.  在資料庫 **A** 和 **C** 中卸除資料庫 **B** 之發行集的訂閱。移至步驟 5。  
  
     如需有關如何卸除訂閱的詳細資訊，請參閱＜ [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)＞。  
  
5.  執行資料庫 **A** 的記錄備份或完整備份。移至步驟 6。  
  
6.  於資料庫 **B** 中還原資料庫 **A** 的備份。資料庫 **B** 現在擁有來自資料庫 **A** 的資料，但是沒有複寫組態。 當您將備份還原到另一部伺服器時，複寫就會被移除，因此複寫已從資料庫 **B** 中移除。移至步驟 7。  
  
7.  在資料庫 **B** 中重新建立發行集，然後在 **A** 和資料庫 **B** 之間重新建立訂閱。(有關資料庫 **C** 的訂閱將在後續階段中處理)。  
  
    1.  在資料庫 **B** 上重新建立發行集。移至步驟 b。  
  
    2.  重新建立資料庫 **B** 的發行集至資料庫 **A** 的訂閱，指定該訂閱應使用備份 ([sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 之 `@sync_type` 參數的 **initialize with backup** 值) 來初始化。 移至步驟 c。  
  
    3.  重新建立資料庫 **A** 的發行集至資料庫 **B** 的訂閱，指定訂閱者已擁有資料 ( [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 之 `@sync_type` 參數的 **replication support only** 值) 來初始化。 移至步驟 8。  
  
8.  執行散發代理程式，以便同步處理資料庫 **A** 和 **B** 中的訂閱。如果已發行資料表中有任何識別資料行，則移至步驟 9。 若為否，請移至步驟 10。  
  
9. 還原之後，您針對資料庫 **A** 中的每一個資料表指派的識別範圍也會在資料庫 **B** 中使用。請確保還原的資料庫 **B** 已接收到來自失敗資料庫 **B** 中已傳播至資料庫 **A** 和資料庫 **C** 的所有變更；然後為每個資料表的識別範圍重設種子資料。  
  
    1.  在資料庫 **B** 執行 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)，並擷取輸出參數 `@request_id`。 移至步驟 b。  
  
    2.  依預設，「散發代理程式」設定為連續執行；因此 Token 應該會自動傳送到所有的節點。 如果散發代理程式並非以連續模式執行，請執行代理程式。 如需詳細資訊，請參閱[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)或[啟動和停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。 移至步驟 c。  
  
    3.  執行 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)，提供步驟 b 中所擷取的 `@request_id` 值。 請稍候，直到所有節點都指示已經收到對等要求為止。 移至步驟 d。  
  
    4.  使用 [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) 重設資料庫 **B** 上每個資料表的種子資料，以確保使用適當的範圍。 移至步驟 10。  
  
     如需如何管理識別範圍的詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)中的＜為手動識別範圍管理指派範圍＞一節。  
  
10. 此時，資料庫 **B** 和資料庫 **C** 並沒有直接連接，但它們將會透過資料庫 **A** 接收變更。如果拓撲包含任何正在執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的節點，請移至步驟 11；否則請移至步驟 12。  
  
11. 停止系統，然後重新建立資料庫 **B** 和 **C** 之間的訂閱。停止系統包括停止所有節點上已發行資料表的活動，並確定每個節點都已收到來自其他所有節點的所有變更。  
  
    1.  停止點對點拓撲中已發行資料表上的所有活動。 移至步驟 b。  
  
    2.  在資料庫 **B** 執行 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)，並擷取輸出參數 `@request_id`。 移至步驟 c。  
  
    3.  依預設，「散發代理程式」設定為連續執行；因此 Token 應該會自動傳送到所有的節點。 如果散發代理程式並非以連續模式執行，請執行代理程式。 移至步驟 d。  
  
    4.  執行 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)，提供步驟 b 中所擷取的 `@request_id` 值。 請稍候，直到所有節點都指示已經收到對等要求為止。 移至步驟 e。  
  
    5.  重新建立資料庫 **C** 的發行集之資料庫 **B** 的訂閱，指定「訂閱者」已具有資料。 移至步驟 b。  
  
    6.  重新建立資料庫 **B** 的發行集之資料庫 **C** 的訂閱，指定「訂閱者」已具有資料。 移至步驟 13。  
  
12. 重新建立資料庫 **B** 和 **C** 之間的訂閱：  
  
    1.  在資料庫 **B** 中查詢 [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) 資料表，以擷取資料庫 **B** 已從資料庫 **C** 所接收之最新交易的記錄序號。  
  
    2.  重新建立資料庫 **B** 的發行集至資料庫 **C** 的訂閱，指定該訂閱應依據 LSN ( [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 之 `@sync_type` 參數的 **initialize with backup** 值) 來初始化。 移至步驟 b。  
  
    3.  重新建立資料庫 **B** 的發行集之資料庫 **C** 的訂閱，指定「訂閱者」已具有資料。 移至步驟 13。  
  
13. 執行散發代理程式，以便同步處理資料庫 **B** 和 **C** 中的訂閱。還原即可完成。  
  
#### <a name="msdb-database-publisher"></a>msdb 資料庫 (發行者)  
  
1.  還原 **msdb** 資料庫的最新備份。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  從您的複寫指令碼重新建立訂閱清除作業。 復原即可完成。  
  
#### <a name="master-database-publisher"></a>Master 資料庫 (發行者)  
  
1.  還原 **master** 資料庫的最新備份。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
### <a name="databases-at-the-distributor"></a>散發者端的資料庫  
  
#### <a name="distribution-database"></a>散發資料庫  
  
1.  還原散發資料庫的最新一次備份。  
  
2.  是否在失敗前對散發資料庫啟用了 **sync with backup** 設定？ 若為是，請移至步驟 3；若為否，請移至步驟 4。  
  
     如果設定已啟用， `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` 查詢會傳回 '1'。  
  
3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 4。  
  
4.  已還原散發資料庫中的組態資訊不是最新的，或者未在散發資料庫上設定 **sync with backup** 選項 (在還原之後，散發資料庫可能會遺失在「發行者」端認可，但尚未傳遞到「訂閱者」的交易)。卸除並重新建立複寫，然後執行驗證。  
  
    1.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 移至步驟 b。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
    2.  標示所有發行集以供驗證。 將未通過驗證的任何訂閱重新初始化。 復原即可完成。  
  
         如需驗證的相關資訊，請參閱 [Validate Replicated Data](../../../relational-databases/replication/validate-data-at-the-subscriber.md)。 如需詳細資訊，請參閱[重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### <a name="msdb-database-distributor"></a>msdb 資料庫 (散發者)  
  
1.  還原 **msdb** 資料庫的最新備份。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 移至步驟 4。  
  
     如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
     如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
4.  標示所有發行集以供驗證。 將未通過驗證的任何訂閱重新初始化。 復原即可完成。  
  
     如需驗證的相關資訊，請參閱 [Validate Replicated Data](../../../relational-databases/replication/validate-data-at-the-subscriber.md)。 如需詳細資訊，請參閱[重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### <a name="master-database-distributor"></a>Master 資料庫 (散發者)  
  
1.  還原 **master** 資料庫的最新備份。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
### <a name="databases-at-the-subscriber"></a>訂閱者端的資料庫  
  
#### <a name="subscription-database"></a>訂閱資料庫  
  
1.  最新的訂閱資料庫備份是否比散發資料庫上的最低散發保留設定還新？ (這點將決定「散發者」是否仍具有更新「訂閱者」的所有必要命令)。如果是，則移至步驟 2。 如果否，請重新初始化該項訂閱。 復原即可完成。  
  
     若要決定最大散發保留設定，則執行 [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 並從 **max_distretention** 資料行中擷取值 (此值以小時表示)。  
  
     如需有關如何重新初始化訂閱的詳細資訊，請參閱＜ [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md)＞。  
  
2.  還原最新一次訂閱資料庫備份。 移至步驟 3。  
  
3.  如果訂閱資料庫僅包含發送訂閱，請移至步驟 4。 如果訂閱資料庫包含任何提取訂閱，請詢問下列問題：訂閱資訊是最新的嗎？ 資料庫包含所有在失敗時所設定的資料表和選項嗎？ 如果是，則移至步驟 4。 如果否，請重新初始化該項訂閱。 復原即可完成。  
  
4.  若要同步處理「訂閱者」，請執行「散發代理程式」。 復原即可完成。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
#### <a name="msdb-database-subscriber"></a>msdb 資料庫 (訂閱者)  
  
1.  還原 **msdb** 資料庫的最新備份。 此「訂閱者」端是否使用提取訂閱？ 如果不是，則還原已完成。 如果是，則移至步驟 2。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有提取訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  卸除並重新建立提取訂閱。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
     如需有關如何卸除訂閱的詳細資訊，請參閱＜ [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)＞。  
  
     如需有關如何指定訂閱者已經擁有該資料的詳細資訊，請參閱＜ [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
#### <a name="master-database-subscriber"></a>Master 資料庫 (訂閱者)  
  
1.  還原 **master** 資料庫的最新備份。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [[設定散發]](../../../relational-databases/replication/configure-distribution.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [初始化訂閱](../../../relational-databases/replication/initialize-a-subscription.md)   
 [同步處理資料](../../../relational-databases/replication/synchronize-data.md)  
  
  
