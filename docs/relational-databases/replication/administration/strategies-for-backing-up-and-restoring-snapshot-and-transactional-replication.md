---
title: "備份與還原快照式和異動複寫的策略 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "備份 [SQL Server 複寫], 快照式複寫"
  - "還原 [SQL Server 複寫], 異動複寫"
  - "快照式複寫 [SQL Server], 備份與還原"
  - "還原 [SQL Server 複寫], 快照式複寫"
  - "復原 [SQL Server 複寫], 異動複寫"
  - "異動複寫，備份與還原"
  - "復原 [SQL Server 複寫], 快照式複寫"
  - "與備份同步 [SQL Server 複寫]"
  - "備份 [SQL Server 複寫], 異動複寫"
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# 備份與還原快照式和異動複寫的策略
  當為快照式及異動複寫設計備份與還原策略時，需要考慮三個方面：  
  
-   要備份的資料庫。  
  
-   異動複寫的備份設定。  
  
-   還原資料庫的必要步驟。 這些步驟是根據複寫類型和所選擇的選項而不同。  
  
 本主題在接下來的三節中對這些方面一一進行說明。 如需 Oracle 發行的備份和還原資訊，請參閱 [備份和還原 Oracle 發行者](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md)。  
  
## 備份資料庫  
 對於快照式及異動複寫，您應定期備份下列資料庫：  
  
-   在「發行者」端的發行集資料庫。  
  
-   在「散發者」端的散發資料庫。  
  
-   在每個「訂閱者」端的訂閱資料庫。  
  
-   發行者、散發者及所有訂閱者端的 **master** 與 **msdb** 系統資料庫。 這些資料庫應與其他每個及相關的複寫資料庫同時備份。 例如，備份 **主要** 和 **msdb** 您備份發行集資料庫的同時發行者端資料庫。 如果還原發行集資料庫時，請確定 **主要** 和 **msdb** 資料庫會與複寫組態和設定發行集資料庫一致。  
  
 如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果不執行記錄備份，則每當與複寫相關的設定發生變更時，便應該執行備份。 如需詳細資訊，請參閱 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)。  
  
## 異動複寫的備份設定  
 異動複寫包含使用 **與備份同步** 選項時，可以在散發資料庫與發行集資料庫上設定︰  
  
-   建議在所有情況下，於散發資料庫上設定此選項。  
  
     在散發資料庫上設定此選項，可確保發行集資料庫記錄檔中的交易在散發資料庫中備份之前，不會被截斷。 散發資料庫可以還原到上次備份時的狀況，任何遺漏的交易都會從發行集資料庫傳遞到散發資料庫。 複寫會繼續，不受影響。  
  
     在散發資料庫上設定此選項不會影響複寫延遲。 不過，此選項會延遲截斷發行集資料庫上的記錄的時間，使其在散發資料庫中相對應的交易備份之前，不會被截斷  (這可能會造成發行集資料庫中存有較大的交易記錄)。  
  
-   如果您的應用程式允許額外的延遲，則建議在發行集資料庫上設定此選項。  
  
     在發行集資料庫上設定此選項，可確保交易在發行集資料庫中備份之前，不會傳遞到散發資料庫。 最近一次的發行集資料庫備份這時可以在「發行者」端還原，同時不會出現這種情況：散發資料庫擁有的交易，在還原的發行集資料庫中不存在。  
  
     延遲和輸送量會受到影響，因為交易在「發行者」端備份之前，不能傳遞到散發資料庫。 例如，如果交易記錄檔每五分鐘備份一次，則「發行者」端正在認可的交易與正在傳遞到散發資料庫 (繼而傳遞到「訂閱者」端) 的交易之間會存在額外的五分鐘延遲。  
  
    > [!NOTE]  
    >   **與備份同步** 選項可確保發行集資料庫與散發資料庫之間的一致性，但此選項並不保證資料不會遺失。 例如，如果交易記錄檔遺失，則自最後一次交易記錄檔備份以後才認可的交易，在發行集資料庫或散發資料庫中都不可用。 這是與非複寫資料庫相同的行為。  
  
 **若要設定 sync with backup 選項**  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計︰ [適用於交易式複寫和 #40; 啟用協調備份複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md)  
  
## 還原複寫中牽涉到的資料庫  
 如果最近的備份可用並遵循適當的步驟，則可以還原複寫拓撲中的所有資料庫。 發行集資料庫的還原步驟取決於所使用的複寫類型和選項，但是所有其他資料庫的還原步驟與複寫類型和選項無關。  
  
 複寫支援將複寫資料庫還原到與原先建立備份的同一個伺服器與資料庫。 如果您將複寫資料庫的備份還原到另一個伺服器或資料庫，將無法保留複寫設定。 在此情況下，您必須在還原備份之後，重新建立所有發行集和訂閱。  
  
### 發行者  
 對以下類型的複寫提供有還原步驟：  
  
-   快照式複寫  
  
-   唯讀異動複寫  
  
-   具有可更新訂閱的異動複寫  
  
-   點對點異動複寫  
  
 在還原 **msdb** 和 **主要** 資料庫，也會包含在這個區段，也適用於所有的四種類型。  
  
#### 發行集資料庫：快照式複寫   
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  發行集資料庫備份是否包含所有發行集和訂閱的最新組態？ 若為是，則還原已經完成。 若為否，請移至步驟 3。  
  
3.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 還原即可完成。  
  
     如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
#### 發行集資料庫：唯讀異動複寫  
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  已 **與備份同步** 啟用發行集資料庫在失敗前設定嗎？ 若為是，請移至步驟 3；若為否，請移至步驟 5。  
  
     如果設定已啟用，`SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` 查詢會傳回 '1'。  
  
3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則還原已經完成。 若為否，請移至步驟 4。  
  
4.  已還原發行集資料庫中的組態資訊並非最新； 因此，您必須確定「訂閱者」擁有散發資料庫中的所有未處理命令，然後再卸除及重新建立複寫組態。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有命令會使用都傳遞給訂閱者 **未散發的命令** 索引標籤，在複寫監視器中，或藉由查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 散發資料庫中的檢視。 移至步驟 b。  
  
         如需如何執行散發代理程式的詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
         如需如何確認命令的詳細資訊，請參閱 [檢視複寫命令和在散發資料庫和 #40; 中的其他資訊複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) 和 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
    2.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
5.   **與備份同步** 發行集資料庫上未設定選項。 因此，沒有包含在還原備份中的交易可能尚未傳遞到散發者和訂閱者。 您必須確定「訂閱者」已經擁有散發資料庫中的所有未處理命令，然後再手動將任何未包含在所還原備份中的交易，套用到發行集資料庫：  
  
    > [!IMPORTANT]  
    >  執行此程序可能會造成已發行資料表的還原時間點，比備份中所還原的其他未發行資料表還要新。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有命令會使用都傳遞給訂閱者 **未散發的命令** 索引標籤，在複寫監視器中，或藉由查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 散發資料庫中的檢視。 移至步驟 b。  
  
         如需如何執行散發代理程式的詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
         如需如何確認命令的詳細資訊，請參閱 [檢視複寫命令和在散發資料庫和 #40; 中的其他資訊複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) 和 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
    2.  使用 [tablediff 公用程式](../../../tools/tablediff-utility.md) 或其他工具來手動同步化 「 發行者 」 與 「 訂閱者 」。 如此可讓您從訂閱資料庫中，復原沒有包含在發行集資料庫備份中的資料。 移至步驟 c。  
  
         如需詳細資訊 **tablediff** 公用程式，請參閱 [比較複寫資料表差異 & #40。複寫程式設計 & #41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 如果是，執行 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 預存程序重新同步處理與散發者端中繼資料的 「 發行者 」 中繼資料。 還原即可完成。 若為否，請移至步驟 d。  
  
    4.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
#### 發行集資料庫：具有可更新訂閱的異動複寫  
  
1.  還原最新的發行集資料庫備份。 移至步驟 2。  
  
2.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有命令會使用都傳遞給訂閱者 **未散發的命令** 索引標籤，在複寫監視器中，或藉由查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 散發資料庫中的檢視。 移至步驟 3。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
     如需如何確認命令的詳細資訊，請參閱 [檢視複寫命令和在散發資料庫和 #40; 中的其他資訊複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) 和 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
3.  如果您使用佇列更新訂閱，每個訂閱者連接，並且刪除所有的資料列 [MSreplication_queue & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) 訂閱資料庫中的資料表。 移至步驟 4。  
  
    > [!NOTE]  
    >  如果您正使用佇列更新訂閱以及包含識別欄位的任何資料表，則必須確保在還原後指派正確的識別範圍。 如需詳細資訊，請參閱 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
4.  您必須確定「訂閱者」已經擁有散發資料庫中的所有未處理命令，然後再手動將任何未包含在所還原備份中的交易，套用到發行集資料庫：  
  
    > [!IMPORTANT]  
    >  執行此程序可能會造成已發行資料表的還原時間點，比備份中所還原的其他未發行資料表還要新。  
  
    1.  執行散發代理程式，直到所有訂閱者與散發資料庫中的未處理命令均已同步處理。 確認所有命令都傳遞給訂閱者使用複寫監視器或藉由查詢 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 散發資料庫中的檢視。 移至步驟 b。  
  
    2.  使用 [tablediff 公用程式](../../../tools/tablediff-utility.md) 或其他工具來手動同步化 「 發行者 」 與 「 訂閱者 」。 如此可讓您從訂閱資料庫中，復原沒有包含在發行集資料庫備份中的資料。 移至步驟 c。  
  
         如需詳細資訊 **tablediff** 公用程式，請參閱 [比較複寫資料表差異 & #40。複寫程式設計 & #41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 如果是，執行 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 預存程序重新同步處理與散發者端中繼資料的 「 發行者 」 中繼資料。 還原即可完成。 若為否，請移至步驟 d。  
  
    4.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
         如需如何移除複寫的詳細資訊，請參閱和 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
#### 發行集資料庫：點對點異動複寫  
 在下列步驟中，發行集資料庫 **A**, ，**B**, ，和 **C** 端對端交易式複寫拓撲中。 資料庫 **A** 和 **C** 線上且正常運作; 資料庫 **B** 是要還原的資料庫。 此處所述的程序 (尤其是步驟 7、10 和 11)，與在點對點拓撲中加入節點的程序非常類似。 執行這些步驟最直接的方法是使用「設定點對點拓撲精靈」，但是您也可以使用預存程序。  
  
1.  執行散發代理程式，同步處理資料庫中的訂閱 **A** 和 **C**。移至步驟 2。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
2.  如果散發資料庫 **B** 是仍然可用，執行散發代理程式同步處理訂閱資料庫之間 **B** 和 **A** 和資料庫而且 B 和 **C**。移至步驟 3。  
  
3.  資料庫中移除中繼資料從發佈 **B** 使用藉由執行 [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) 散發資料庫 **B**。移至步驟 4。  
  
4.  在資料庫 **A** 和 **C**, ，在資料庫中卸除發行集的訂閱 **B**。移至步驟 5。  
  
     如需如何卸除訂閱的詳細資訊，請參閱 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)。  
  
5.  執行記錄備份或完整資料庫備份 **A**。移至步驟 6。  
  
6.  還原資料庫備份 **A** 資料庫 **B**。資料庫 **B** 現在具有來自資料庫的資料 **A**, ，但是沒有複寫組態。 當您將備份還原到另一部伺服器時，會移除複寫。因此，已從資料庫移除複寫 **B**。移至步驟 7。  
  
7.  重新建立發行集之資料庫 **B**, ，然後再重新建立訂閱資料庫之間 **A** 和 **B**。(牽涉到資料庫的訂閱 **C** 在稍後階段處理。)。  
  
    1.  重新建立發行集之資料庫 **B**。移至步驟 b。  
  
    2.  重新建立資料庫的訂閱 **B** 的發行集資料庫之 **的**, ，指定應該初始化的訂閱，以備份 (值為 **的備份初始化** 的 **@sync_type** 參數 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md))。 移至步驟 c。  
  
    3.  重新建立資料庫的訂閱 **A** 的發行集資料庫之 **B**, ，指定 「 訂閱者 」 已經擁有該資料 (值為 **僅支援複寫** 的 **@sync_type** 參數 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md))。 移至步驟 8。  
  
8.  執行散發代理程式，同步處理資料庫中的訂閱 **A** 和 **B**。如果已發行資料表中有任何識別資料行，則移至步驟 9。 若為否，請移至步驟 10。  
  
9. 在還原之後，您指派給資料庫中的每個資料表的識別範圍 **A** 也會在資料庫中用於 **B**。請確定已還原的資料庫 **B** 已收到來自失敗資料庫的所有變更 **B** 中已傳播至資料庫 **A** 和資料庫 **C**; 以及每個資料表的識別範圍重設種子資料。  
  
    1.  執行 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 資料庫 **B** 並擷取輸出參數 **@request_id**。 移至步驟 b。  
  
    2.  依預設，「散發代理程式」設定為連續執行；因此 Token 應該會自動傳送到所有的節點。 如果散發代理程式並非以連續模式執行，請執行代理程式。 如需詳細資訊，請參閱 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 或 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。 移至步驟 c。  
  
    3.  執行 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), ，提供 **@request_id** 步驟 b 中擷取值。 請稍候，直到所有節點都指示已經收到對等要求為止。 移至步驟 d。  
  
    4.  使用 [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) 來重新植入資料庫中的每個資料表 **B** 來確定使用適當的範圍。 移至步驟 10。  
  
     如需如何管理識別範圍的詳細資訊，請參閱 「 指派為手動識別範圍管理的範圍 」 一節 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
10. 此時，資料庫 **B** 和資料庫 **C** 未直接連線，但透過資料庫的變更將會收到 **A**。如果拓撲包含任何正在執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的節點，請移至步驟 11；否則請移至步驟 12。  
  
11. 停止系統，然後再重新建立訂閱資料庫之間 **B** 和 **C**。停止系統包括停止所有節點上已發行資料表的活動，並確定每個節點都已收到來自其他所有節點的所有變更。  
  
    1.  停止點對點拓撲中已發行資料表上的所有活動。 移至步驟 b。  
  
    2.  執行 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 資料庫 **B** 並擷取輸出參數 **@request_id**。 移至步驟 c。  
  
    3.  依預設，「散發代理程式」設定為連續執行；因此 Token 應該會自動傳送到所有的節點。 如果散發代理程式並非以連續模式執行，請執行代理程式。 移至步驟 d。  
  
    4.  執行 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), ，提供 **@request_id** 步驟 b 中擷取值。 請稍候，直到所有節點都指示已經收到對等要求為止。 移至步驟 e。  
  
    5.  重新建立資料庫的訂閱 **B** 的發行集資料庫之 **C**, ，指定 「 訂閱者 」 已經擁有該資料。 移至步驟 b。  
  
    6.  重新建立資料庫的訂閱 **C** 的發行集資料庫之 **B**, ，指定 「 訂閱者 」 已經擁有該資料。 移至步驟 13。  
  
12. 重新建立訂閱資料庫之間 **B** 和 **C**:  
  
    1.  在資料庫 **B**, ，查詢 [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) 資料表，以擷取的記錄序號 (LSN) 的最新的交易資料庫 **B** 已收到來自資料庫 **C**。  
  
    2.  重新建立資料庫的訂閱 **B** 的發行集資料庫之 **C**, ，指定應該初始化的訂閱會依據 LSN (值為 **初始化從 lsn** 的 **@sync_type** 參數 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md))。 移至步驟 b。  
  
    3.  重新建立資料庫的訂閱 **C** 的發行集資料庫之 **B**, ，指定 「 訂閱者 」 已經擁有該資料。 移至步驟 13。  
  
13. 執行散發代理程式，同步處理資料庫中的訂閱 **B** 和 **C**。還原即可完成。  
  
#### msdb 資料庫 (發行者)  
  
1.  最新的備份還原 **msdb** 資料庫。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  從您的複寫指令碼重新建立訂閱清除作業。 復原即可完成。  
  
#### Master 資料庫 (發行者)  
  
1.  最新的備份還原 **主要** 資料庫。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
### 散發者端的資料庫  
  
#### 散發資料庫  
  
1.  還原散發資料庫的最新一次備份。  
  
2.  已 **與備份同步** 失敗前對散發資料庫上啟用的設定嗎？ 若為是，請移至步驟 3；若為否，請移至步驟 4。  
  
     如果設定已啟用，`SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` 查詢會傳回 '1'。  
  
3.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 4。  
  
4.  還原的散發資料庫中的組態資訊不是最新狀態，或 **與備份同步** 散發資料庫未設定選項。 (在還原之後，散發資料庫可能會遺失在「發行者」端認可，但尚未傳遞到「訂閱者」的交易)。卸除並重新建立複寫，然後執行驗證。  
  
    1.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 移至步驟 b。  
  
         如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
         如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
    2.  標示所有發行集以供驗證。 將未通過驗證的任何訂閱重新初始化。 復原即可完成。  
  
         如需有關驗證的詳細資訊，請參閱 [驗證複寫資料](../../../relational-databases/replication/validate-replicated-data.md)。 如需重新初始化的詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### msdb 資料庫 (散發者)  
  
1.  最新的備份還原 **msdb** 資料庫。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有發行集和訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  從「發行者」、「散發者」及「訂閱者」端移除複寫組態，然後重新建立組態。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 移至步驟 4。  
  
     如需如何移除複寫的詳細資訊，請參閱 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)。  
  
     如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
4.  標示所有發行集以供驗證。 將未通過驗證的任何訂閱重新初始化。 復原即可完成。  
  
     如需有關驗證的詳細資訊，請參閱 [驗證複寫資料](../../../relational-databases/replication/validate-replicated-data.md)。 如需重新初始化的詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### Master 資料庫 (散發者)  
  
1.  最新的備份還原 **主要** 資料庫。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
### 訂閱者端的資料庫  
  
#### 訂閱資料庫  
  
1.  最新的訂閱資料庫備份是否比散發資料庫上的最低散發保留設定還新？ (這點將決定「散發者」是否仍具有更新「訂閱者」的所有必要命令)。如果是，則移至步驟 2。 如果否，請重新初始化該項訂閱。 復原即可完成。  
  
     若要判斷最大散發保留設定，請執行 [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 並從中擷取值 **max_distretention** 資料行 （此值是以小時為單位）。  
  
     如需如何重新初始化訂閱的詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-a-subscription.md)。  
  
2.  還原最新一次訂閱資料庫備份。 移至步驟 3。  
  
3.  如果訂閱資料庫僅包含發送訂閱，請移至步驟 4。 如果訂閱資料庫包含任何提取訂閱，請提出以下問題：訂閱資訊是最新的嗎？ 資料庫包含所有在失敗時所設定的資料表和選項嗎？ 如果是，則移至步驟 4。 如果否，請重新初始化該項訂閱。 復原即可完成。  
  
4.  若要同步處理「訂閱者」，請執行「散發代理程式」。 復原即可完成。  
  
     如需如何執行散發代理程式的詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
#### msdb 資料庫 (訂閱者)  
  
1.  最新的備份還原 **msdb** 資料庫。 此「訂閱者」端是否使用提取訂閱？ 如果不是，則還原已完成。 如果是，則移至步驟 2。  
  
2.  還原的備份是否完整且為最新狀態？ 該備份是否包含所有提取訂閱的最新組態？ 若為是，則復原已經完成。 若為否，請移至步驟 3。  
  
3.  卸除並重新建立提取訂閱。 重新建立訂閱時，請指定「訂閱者」已經擁有該資料。 還原即可完成。  
  
     如需如何卸除訂閱的詳細資訊，請參閱 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)。  
  
     如需如何指定 「 訂閱者 」 已經擁有該資料的詳細資訊，請參閱 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)。  
  
#### Master 資料庫 (訂閱者)  
  
1.  最新的備份還原 **主要** 資料庫。  
  
2.  確定資料庫和發行集資料庫內的複寫組態與設定一致。  
  
## 另請參閱  
 [SQL Server 資料庫的備份與還原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [設定散發](../../../relational-databases/replication/configure-distribution.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)   
 [初始化訂閱](../../../relational-databases/replication/initialize-a-subscription.md)   
 [同步處理資料](../../../relational-databases/replication/synchronize-data.md)  
  
  