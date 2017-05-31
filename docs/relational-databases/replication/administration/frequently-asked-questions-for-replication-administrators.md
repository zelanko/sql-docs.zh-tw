---
title: "複寫管理員的常見問題集 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b7fd50c53405ab0866e5eca50275531687c7b171
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="frequently-asked-questions-for-replication-administrators"></a>複寫管理員的常見問題集
  透過下列問題和答覆可以了解複寫的資料庫管理員所面臨的各種工作。  
  
## <a name="configuring-replication"></a>設定複寫  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>當活動發行後，是否需要在資料庫中停止該活動？  
 否。 在建立發行集期間，可在資料庫中繼續保留活動。 請注意，產生快照集可能需要大量資源，因此最好在資料庫中活動較少的時間產生快照集 (依預設，在您完成「新增發行集精靈」時產生快照集)。  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>資料表是否在快照集產生期間鎖定？  
 鎖定的時間長短視所用的複寫類型而定：  
  
-   針對合併式發行集，快照集代理程式未使用任何鎖定。  
  
-   對於交易式發行集，依預設，「快照集代理程式」將只在快照集產生的初始階段進行鎖定。  
  
-   對於快照式發行集，「快照集代理程式」會在快照集產生的整個處理過程中進行鎖定。  
  
 由於鎖定可以防止其他使用者更新資料表，因此「快照集代理程式」應排程在資料庫活動較少的時間執行，特別是對於快照式發行集。  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>訂閱何時可用？訂閱資料庫何時可用？  
 訂閱可在快照集套用至訂閱資料庫後使用。 儘管在此之前可以存取訂閱資料庫，但在套用快照集之前不應使用資料庫。 使用「複寫監視器」檢查快照集產生狀態與應用程式：  
  
-   快照集由「快照集代理程式」產生。 在複寫監視器中發行集的 **[代理程式]** 索引標籤上檢視快照集產生狀態。 如需詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
-   快照集由「散發代理程式」或「合併代理程式」套用。 在「複寫監視器」的 **[散發代理程式]** 或 **[合併代理程式]** 頁面中檢視快照集應用程式狀態。 如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>如果當「散發代理程式」或「合併代理程式」啟動時「快照集代理程式」尚未完成，會發生什麼事情？  
 如果「散發代理程式」或「合併代理程式」與「快照集代理程式」同時執行，將不會導致錯誤。 但是，您必須注意下列情況：  
  
-   如果「散發代理程式」或「合併代理程式」設定為連續執行，則代理程式會在「快照集代理程式」完成時自動套用快照集。  
  
-   如果「散發代理程式」或「合併代理程式」設定為根據排程或視需要執行，並且在執行代理程式時沒有可用的快照集，則代理程式將關閉並顯示一則訊息，說明快照集尚無法使用。 您必須在完成「快照集代理程式」後再次執行代理程式以套用快照集。 如需執行代理程式的詳細資訊，請參閱[同步處理發送訂閱](../../../relational-databases/replication/synchronize-a-push-subscription.md)、[同步處理提取訂閱](../../../relational-databases/replication/synchronize-a-pull-subscription.md)和[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
### <a name="should-i-script-my-replication-configuration"></a>我是否應為我的複寫組態編寫指令碼？  
 是的。 編寫複寫組態的指令碼是複寫拓撲之任何損毀復原計劃的主要部分。 如需有關編寫指令碼的詳細資訊，請參閱＜ [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)＞。  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>複寫的資料庫中需要什麼復原模式？  
 使用下列任何一種復原模式的複寫都能正常運作：簡單、大量記錄或完整。 合併式複寫會透過將資訊儲存於中繼資料表來追蹤變更。 異動複寫則透過標記交易記錄來追蹤變更，但此標記處理序不受復原模式影響。  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>複寫為何將資料行新增至複寫的資料表？如果資料表未發行，它是否會被移除？  
 若要追蹤變更，合併式複寫和具有佇列更新訂閱的異動複寫必須可以唯一地識別每個已發行資料表中的每個資料列。 若要完成這個程序：  
  
-   合併式複寫會將此資料行 **rowguid** 新增至每個資料表，除非資料表已經擁有的資料行是包含 **ROWGUIDCOL** 屬性集的 **uniqueidentifier** 資料類型 (在此情況下將使用此資料行)。 若從發行集卸除資料表， **rowguid** 資料行會遭到移除；若現有資料行用來進行追蹤，則不會移除資料行。  
  
-   如果交易式發行集支援佇列更新訂閱，則複寫會將 **msrepl_tran_version** 資料行加入每份資料表中。 如果從發行集中卸除資料表，將不會移除 **msrepl_tran_version** 資料行。  
  
-   篩選不得包含複寫識別資料列所使用的 **rowguidcol** 。 根據預設，這是在您設定合併式複寫時加入，且名稱為 **rowguid**的資料行。  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>如何管理已發行資料表中的條件約束？  
 針對已發行資料表中的條件約束需要考慮許多問題：  
  
-   異動複寫要求在每個已發行資料表中具有主索引鍵條件約束。 合併式複寫不需要主索引鍵，但如果存在主索引鍵，則它必須被複寫。 快照式複寫不需要主索引鍵。  
  
-   依預設，主索引鍵條件約束、索引和檢查條件約束都會複寫至「訂閱者」。  
  
-   依預設，NOT FOR REPLICATION 選項將指定給外部索引鍵條件約束和檢查條件約束；條件約束對使用者作業而非代理程式作業強制執行。  
  
 如需有關設定用於控制是否複寫條件約束之結構描述選項的詳細資訊，請參閱＜ [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md)＞。  
  
### <a name="how-do-i-manage-identity-columns"></a>如何管理識別欄位？  
 複寫為在「訂閱者」端包含更新的複寫拓撲提供自動識別範圍管理。 如需詳細資訊，請參閱[複寫識別資料欄](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>相同的物件是否能發行在不同的發行集中？  
 是，但有一些限制。 如需詳細資訊，請參閱[發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)主題中的＜在多個發行集中發行資料表＞一節。  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>多個發行集是否可以使用相同的散發資料庫？  
 是的。 可以使用相同散發資料庫的發行集沒有數量或類型的限制。 給定「發行者」的所有發行集必須使用相同的「散發者」和散發資料庫。  
  
 如果您有多個發行集，則可在「散發者」端設定多個散發資料庫，以確定每個散發資料庫中的資料流程來自單一發行集。 使用 [散發者屬性] 對話方塊或 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 以新增散發資料庫。 如需存取對話方塊的詳細資訊，請參閱[檢視和修改散發者和發行者屬性](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>如何尋找「散發者」和「發行者」的資訊 (例如，資料庫中哪些物件已發行)？  
 此資訊可透過 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]和數個複寫預存程序獲得。 如需詳細資訊，請參閱 [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)。  
  
### <a name="does-replication-encrypt-data"></a>複寫是否會加密資料？  
 否。 複寫不會對儲存在資料庫或透過網路傳送的資料加密。 如需詳細資訊，請參閱[安全性概觀 &#40;複寫&#41;](../../../relational-databases/replication/security/security-overview-replication.md) 主題中的＜加密＞一節。  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>如何透過網際網路複寫資料？  
 使用下列方式，透過網際網路複寫資料：  
  
-   虛擬私人網路 (VPN)。 如需詳細資訊，請參閱[使用 VPN 透過網際網路發行資料](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)。  
  
-   合併式複寫的 Web 同步處理選項。 如需詳細資訊，請參閱 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
 所有類型的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫都可以透過 VPN 複寫資料，但是您若是使用合併式複寫，則應考慮 Web 同步處理。  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>如果連接斷開，則複寫是否會繼續？  
 是的。 如果連接斷開，複寫處理會從它停止的地方繼續。 如果您在不可靠的網路中使用合併式複寫，請考慮使用邏輯記錄，它可確保相關變更作為一個單位進行處理。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>複寫是否透過低頻寬連接執行？ 它是否使用壓縮？  
 是，複寫透過低頻寬連接執行。 對於透過 TCP/IP 的連接，它使用由通訊協定提供的壓縮，但不提供其他壓縮。 對於透過 HTTPS 的 Web 同步處理連接，它使用由通訊協定提供的壓縮，同時還提供對 XML 檔案 (用於複寫變更) 的其他壓縮。  
  
## <a name="logins-and-object-ownership"></a>登入和物件擁有權  
  
### <a name="are-logins-and-passwords-replicated"></a>登入和密碼是否會被複寫？  
 否。 您可以建立 DTS 封裝以將登入和密碼從「發行者」傳送給一個或多個「訂閱者」。  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>結構描述什麼是以及它們是如何進行複寫的？  
 從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *「結構描述」* 具有兩重含義：  
  
-   物件的定義，例如 CREATE TABLE 陳述式。 依預設，複寫將所有複寫物件的定義複製到「訂閱者」。  
  
-   在其中建立物件的命名空間：\<資料庫>.\<結構描述>.\<物件>。 結構描述使用 CREATE SCHEMA 陳述式來定義。  
  
-   針對結構描述和物件擁有權，複寫在新增複寫精靈中具有下列預設行為：  
  
-   針對合併式發行集內相容性層級等於或超過 90 的發行項、快照集發行集以及交易式發行集：依預設，訂閱者的物件擁有者與發行者內對應物件的擁有者相同。 若擁有物件的結構描述不存在於訂閱者中，則會自動建立。  
  
-   針對相容性層級小於 90 之合併式發行集內的發行項：依預設，會將擁有者保留空白，並在訂閱者上建立物件期間，將其指定為 **dbo** 。  
  
-   針對 Oracle 發行集內的發行項：依預設，會將擁有者指定為 **dbo**。  
  
-   針對使用字元模式快照集之發行集內的發行項 (用於非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者和 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 訂閱者)：依預設，會將擁有者保留空白。 擁有者預設為與散發代理程式或合併代理程式用於連接到訂閱者之帳戶相關聯的擁有者。  
  
 物件擁有者可以透過 **[發行項屬性 -\<**<發行項>**>]** 對話方塊和透過下列預存程序變更︰**sp_addarticle**、**sp_addmergearticle**、**sp_changearticle** 和 **sp_changemergearticle**。 如需詳細資訊，請參閱[檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)、[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)和[檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>如何將訂閱資料庫中的授權設定為與發行集資料庫中的授權相符？  
 依預設，複寫不執行訂閱資料庫中的 GRANT 陳述式。 如果您要使訂閱資料庫中的授權與發行集資料庫中的授權相符，請使用以下其中一種方法：  
  
-   直接在訂閱資料庫執行 GRANT 陳述式。  
  
-   使用後快照集指令碼執行陳述式。 如需詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用預存程序 [sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) 執行陳述式。  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>如果重新初始化訂閱，在訂閱資料庫中的授與權限會發生什麼情況？  
 依預設，當重新初始化訂閱時，「訂閱者」端的物件將卸除並重新建立，這會導致授與這些物件的所有權限被卸除。 有兩種方式可以處理此問題：  
  
-   在重新初始化之後，使用上一節中所述的技術重新套用授權。  
  
-   指定在重新初始化訂閱時不應卸除物件。 在重新初始化之前，執行下列其中一項：  
  
    -   執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 或 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定**sp_changearticle**參數的 'pre_creation_cmd' (**sp_changemergearticle**) 或 'pre_creation_command' ( **@property** )，以及 **@value**。  
  
    -   在 [發行項屬性 - \<發行項>] 對話方塊的 [目的地物件] 區段中，選取 [不要變更現有物件]、[刪除資料。如果發行項有資料列篩選，僅刪除符合篩選的資料。] 或 [截斷現有物件中的所有資料] 作為 [如果名稱使用中，則採取動作] 選項的值。 如需存取這個對話方塊的詳細資訊，請參閱[檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
## <a name="database-maintenance"></a>資料庫維護  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>為何我無法在已發行的資料表中執行 TRUNCATE TABLE？  
 TRUNCATE TABLE 是不會引發觸發程序的非記錄式作業。 因為複寫無法追蹤由此作業導致的變更，所以不允許執行此作業：異動複寫透過交易記錄追蹤變更；合併式複寫透過已發行資料表上的觸發程序追蹤變更。  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>在已複寫資料庫中執行大量插入命令有什麼效果？  
 對於異動複寫，大量插入將被追蹤並同其他插入一樣進行複寫。 對於合併式複寫，您必須確定正確更新變更追蹤中繼資料。  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>是否有任何備份和還原的複寫考量？  
 是的。 對於涉及複寫的資料庫有許多特殊的考量。 如需詳細資訊，請參閱 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>複寫是否會影響交易記錄的大小？  
 合併式複寫和快照式複寫不會影響交易記錄大小，但異動複寫會影響。 如果資料庫包含一個或多個交易式發行集，則除非已將所有與發行集相關的交易傳遞至散發資料庫，否則不會截斷記錄檔。 如果交易記錄變得很大，而且「記錄讀取器代理程式」依排程執行，請考慮縮短兩次執行間的間隔或設定其以連續模式執行。 或者將它設定為以連續模式執行。 如果已將其設定為在連續模式下執行 (預設值)，則請確定它正在執行。 如需檢查記錄讀取器代理程式狀態的詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
 此外，如果您已在發行集資料庫或散發資料庫中設定選項 'sync with backup'，則除非已備份所有交易，否則交易記錄不會被截斷。 如果交易記錄變得很大，並且您已設定此選項，則請考慮縮短兩次交易記錄備份之間的間隔。 如需涉及異動複寫之備份和還原資料庫的詳細資訊，請參閱[備份與還原快照集和異動複寫的策略](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>如何在複寫的資料庫中重建索引或資料表？  
 有各種重建索引的機制。 這些機制在使用時沒有針對複寫的特殊考量，下列情況例外：交易式發行集中的資料表上需要主索引鍵，因此您無法在這些資料表中卸除和重新建立主索引鍵。  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>如何在發行集和訂閱資料庫上新增或變更索引？  
 可以在「發行者」或「訂閱者」端新增索引，而沒有針對複寫的特殊考量 (請注意，索引會影響效能)。 CREATE INDEX 和 ALTER INDEX 不會複寫，因此如果您新增或變更索引 (例如在「發行者」端)，則必須在「訂閱者」端進行同樣的新增或變更 (如果您要在那裡反映出來)。  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>如何移動或重新命名涉及複寫的資料庫？  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，移動或重新命名資料庫檔案需要卸離及重新附加資料庫。 因為複寫的資料庫無法卸離，所以必須先從這些資料庫中移除複寫。 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始，您可以在不卸離或重新附加資料庫的情況下移動或重新命名檔案，而不會影響複寫。 如需移動和重新命名檔案的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>如何卸除正在複寫的資料表？  
 首先使用 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)、[sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 或 [發行集屬性 - \<發行集>] 對話方塊從發行集中卸除發行項，然後使用 `DROP <Object>` 將其從資料庫中卸除。 訂閱已加入之後，不可從快照集或交易式發行集卸除發行項，必須先卸除訂閱。 如需詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>如何在已發行的資料表中新增或卸除資料行？  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援在已發行物件上進行各種結構描述變更，包括新增和卸除資料行。 例如，在發行者端執行 ALTER TABLE ... DROP COLUMN，並將陳述式複寫至訂閱者，然後執行以卸除資料行。 執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本的「訂閱者」支援透過預存程序 [sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) 和 [sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md)新增和卸除資料行。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="replication-maintenance"></a>複寫維護  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>如何確定「訂閱者」端的資料是否與「發行者」端的資料同步？  
 使用驗證。 驗證將報告給定「訂閱者」是否與「發行者」同步。 如需詳細資訊，請參閱[驗證複寫的資料](../../../relational-databases/replication/validate-replicated-data.md)。 驗證不會提供未正確同步之資料列 (若有的話) 的資訊，但 [tablediff 公用程式](../../../tools/tablediff-utility.md) 可以提供。  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>如何將資料表新增至現有的發行集？  
 新增資料表 (或其他物件) 時不必停止發行集或訂閱資料庫中的活動。 透過 [發行集屬性 - \<發行集>] 對話方塊或預存程序 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 和 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)，將資料表新增至發行集。 如需詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>如何從發行集中移除資料表？  
 使用 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)、[sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 或 [發行集屬性 - \<發行集>] 對話方塊從發行集中移除資料表。 訂閱已加入之後，不可從快照集或交易式發行集卸除發行項，必須先卸除訂閱。 如需詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>哪些動作需要重新初始化訂閱？  
 有許多發行項和發行集變更需要重新初始化訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>哪些動作會導致快照集失效？  
 有許多發行項和發行集變更會導致快照集失效，並需要產生新的快照集。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
### <a name="how-do-i-remove-replication"></a>如何移除複寫？  
 從資料庫中移除複寫所需採取的動作視資料庫是否用作發行集資料庫、訂閱資料庫或兩者而定。  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>如何確定是否有要複寫的交易或資料列？  
 對於異動複寫，請使用預存程序或「複寫監視器」中的 **[未散發的命令]** 索引標籤。 如需詳細資訊，請參閱[在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 和[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 對於合併式複寫，請使用預存程序 **sp_showpendingchanges**。 如需詳細資訊，請參閱 [sp_showpendingchanges &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>「散發代理程式」落後多少？ 是否應重新初始化？  
 使用 **sp_replmonitorsubscriptionpendingcmds** 預存程序或「複寫監視器」中的 **[未散發命令]** 索引標籤。 預存程序與索引標籤顯示：  
  
-   散發資料庫中尚未傳遞給選取之訂閱者的命令數目。 由一個 Transact-SQL 資料操作語言 (DML) 陳述式或一個資料定義語言 (DDL) 陳述式組成的命令。  
  
-   估計將命令傳遞給訂閱者所需的時間量。 如果此值大於產生快照集並將其套用至訂閱者所需的時間量，則請考慮重新初始化訂閱者。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
 如需詳細資訊，請參閱 [sp_replmonitorsubscriptionpendingcmds &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) 和[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="replication-and-other-database-features"></a>複寫與其他資料庫功能  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>複寫是否與記錄傳送和資料庫鏡像一起使用？  
 是的。 如需詳細資訊，請參閱[記錄傳送和複寫 &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) 和[資料庫鏡像和複寫 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>複寫是否與群集一起使用？  
 是的。 無需特殊考量，因為所有資料儲存在群集的一組磁碟中。  
  
## <a name="see-also"></a>另請參閱  
 [管理 &#40;複寫&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
