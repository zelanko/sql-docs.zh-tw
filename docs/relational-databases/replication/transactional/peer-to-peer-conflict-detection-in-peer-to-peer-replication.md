---
title: "點對點複寫中的衝突偵測 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c2b248262e1344a7dc4652ed5d48aefa081a2f40
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="peer-to-peer---conflict-detection-in-peer-to-peer-replication"></a>點對點 - 點對點複寫中的衝突偵測
  點對點異動複寫可讓您在拓撲中的任何節點上插入、更新或刪除資料，以及讓資料變更傳播至其他節點。 由於您可以在任何節點上變更資料，因此不同節點的資料變更可能會彼此衝突。 如果在一個以上的節點上修改資料列，它可能會在此資料列傳播到其他節點時，造成衝突或甚至是遺失更新。  
  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 及更新版本中的點對點複寫提供了在點對點拓撲之間啟用衝突偵測的選項。 這個選項可避免因為未偵測到的衝突所導致的問題，包括不一致的應用程式行為和遺失更新。 啟用這個選項時，預設會將衝突的變更視為造成散發代理程式失敗的嚴重錯誤。 在發生衝突時，此拓撲會維持不一致的狀態，直到解決衝突並讓拓撲之間的資料變成一致為止。  
  
> [!NOTE]  
>  若要避免潛在的資料不一致問題，請務必要避免發生點對點拓撲中的衝突，即使是啟用了衝突偵測也一樣。 若要確定只在一個節點上執行特定資料列的寫入作業，存取和變更資料的應用程式必須分割插入、更新和刪除作業。 這樣的分割可確保，從一個節點對給定資料列的修改會在其他節點修改該資料列之前，與拓撲中的所有其他節點同步處理。 如果應用程式需要複雜的衝突偵測與解決功能，請使用合併式複寫。 如需詳細資訊，請參閱[合併式複寫](../../../relational-databases/replication/merge/merge-replication.md)和[偵測及解決合併式複寫衝突](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)。  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>了解衝突和衝突偵測  
 在單一資料庫中，由不同應用程式對相同資料列所做的變更不會導致衝突發生。 這是因為交易是序列化的，而且系統會使用鎖定來處理並行的變更。 在非同步分散式系統 (例如點對點複寫) 中，交易會在每個節點上獨立運作，而且沒有任何機制可序列化多個節點之間的交易。 雖然您可以使用兩階段交易認可之類的通訊協定，但是這樣做會大幅影響效能。  
  
 在點對點複寫等系統中，當系統在個別對等中認可變更時，無法偵測衝突。 不過，當這些變更複寫和套用至其他對等時，就會偵測衝突。 在點對點複寫中，將變更套用至每個節點的預存程序會根據每個已發行資料表中的隱藏資料行來偵測衝突。 這個隱藏資料行會儲存結合了您針對每個節點指定的 *「訂閱者識別碼」* (Originator ID) 與資料列版本的識別碼。 在同步處理期間，散發代理程式會針對每份資料表執行程序。 這些程序會從其他對等套用插入、更新和刪除作業。 如果其中一項程序在讀取隱藏資料行的值時偵測到衝突，它就會引發嚴重性層級為 16 的錯誤 22815：  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 根據預設，這項錯誤會導致散發代理程式停止將變更套用至該節點。 如需有關如何處理偵測之衝突的詳細資訊，請參閱本主題後面的「處理衝突」。  
  
> [!NOTE]  
>  隱藏資料行只能由透過「專用管理員連接」(DAC) 登入的使用者存取。 如需 DAC 的資訊，請參閱[資料庫管理員的診斷連線](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。  
  
 點對點複寫會偵測下列衝突類型：  
  
-   插入對插入  
  
     參與點對點複寫之每份資料表中的所有資料列都會使用主索引鍵值進行唯一識別。 在多個節點上插入具有相同索引鍵值的資料列時，就會發生插入對插入的衝突。  
  
-   更新對更新  
  
     在多個節點上更新相同的資料列時發生。  
  
-   插入對更新  
  
     在某個節點上插入一個資料列，但是在另一個節點上刪除並重新插入相同的資料列時發生。  
  
-   插入對刪除  
  
     在某個節點上刪除一個資料列，但是在另一個節點上刪除並重新插入相同的資料列時發生。  
  
-   更新對刪除  
  
     在某個節點上插入一個資料列，但是在另一個節點上刪除相同的資料列時發生。  
  
-   刪除對刪除  
  
     在多個節點上刪除資料列時發生。  
  
## <a name="enabling-conflict-detection"></a>啟用衝突偵測  
 若要使用衝突偵測，所有節點都必須執行 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 或更新版本，而且您必須針對所有節點啟用偵測。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更新版本中， [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]預設會啟用衝突偵測。 我們建議您啟用偵測，即使是預期不會發生任何衝突的狀況也一樣。 您可以使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 預存程序來啟用和停用衝突偵測：  
  
-   您可以使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] [發行集屬性] **對話方塊的** [訂閱選項] **頁面或「設定點對點拓撲精靈」的** [設定拓撲] **頁面，啟用和停用** 中的偵測。 如需相關資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
     如果您使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]來設定衝突偵測，散發代理程式就會設定為在偵測到衝突時停止套用變更。  
  
-   您也可以使用下列預存程序來啟用和停用偵測： [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 或 [sp_configure_peerconflictdetection](../../../relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql.md)。  
  
     如果您使用預存程序來設定衝突偵測，就可以指定散發代理程式是否應該在偵測到衝突時停止套用變更。 代理程式的預設值為停止。 我們建議您使用預設設定。  
  
## <a name="handling-conflicts"></a>處理衝突  
 在點對點複寫中發生衝突時，系統就會引發點對點衝突偵測警示。 我們建議您設定這個警示，以便在發生衝突時收到通知。 如需警示的詳細資訊，請參閱[使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)。  
  
 在散發代理程式停止並引發警示之後，請使用下列其中一種方法來處理發生的衝突：  
  
-   根據包含必要資料的節點備份，重新初始化偵測到衝突的節點 (建議使用的方法)。 這種方法可確保資料處於一致的狀態。  
  
-   透過讓散發代理程式繼續套用變更，嘗試再次同步處理節點：  
  
    1.  執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)：針對 @property 參數指定 'p2p_continue_onconflict' 而針對 @value 參數指定 **true**。  
  
    2.  重新啟動散發代理程式。  
  
    3.  使用衝突檢視器來確認偵測到的衝突，然後判斷所涉及的資料列、衝突的類型以及成功者。 系統會根據您在組態設定期間指定的訂閱者識別碼值來解決衝突：源自最高識別碼之節點的資料列會在衝突中獲勝。 如需詳細資訊，請參閱[檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)。  
  
    4.  執行驗證，以便確保衝突資料列會正確聚合。 如需詳細資訊，請參閱[驗證複寫的資料](../../../relational-databases/replication/validate-replicated-data.md)。  
  
        > [!NOTE]  
        >  如果進行這個步驟之後資料出現不一致，您就必須手動更新具有最高優先權之節點上的資料列，然後讓變更從這個節點傳播。 如果拓撲中沒有其他進一步的衝突變更，所有節點都會處於一致狀態。  
  
    5.  執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)：針對 @property 參數指定 'p2p_continue_onconflict' 而針對 @value 參數指定 **false**。  
  
## <a name="see-also"></a>另請參閱  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
