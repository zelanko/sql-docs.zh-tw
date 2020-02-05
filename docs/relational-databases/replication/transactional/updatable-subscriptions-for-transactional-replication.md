---
title: 可更新的訂閱 (交易式)
description: 說明 SQL Server 中可用於異動複寫的可更新訂閱功能。
ms.custom: seo-lt-2019
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7baa131caa531038d8764c070ebd00ba44147c54
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321426"
---
# <a name="updatable-subscriptions---for-transactional-replication"></a>可更新訂閱 - 異動複寫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  這項功能在 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012 到 2016 的版本中仍然受到支援。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 異動複寫透過可更新訂閱和點對點複寫支援在訂閱者端的更新。 以下是兩種可以更新的訂閱類型：  
  
-   立即更新。 發行者和訂閱者必須連接，以便更新訂閱者端的資料。  
  
-   佇列更新。發行者和訂閱者不必連接，即可更新訂閱者端的資料。 更新可在訂閱者或發行者離線時進行。  
  
 當資料在訂閱者端更新時，它會先傳播至發行者，然後再傳播至其他訂閱者。 如果使用立即更新，則透過使用兩階段認可通訊協定，變更會立即傳播。 如果使用佇列更新，則變更會儲存於佇列中；然後，佇列交易會在網路連接可用時，在發行者端上非同步套用。 因為更新會非同步地傳播到「發行者」，因此相同的資料可能已經被「發行者」或另一個「訂閱者」更新過，所以在套用更新時可能會出現衝突。 衝突會偵測出來，並且根據建立發行集時設定的衝突解決原則來解決。  
  
 如果在「新增發行集精靈」中建立具有可更新訂閱的交易式發行集，則會啟用立即更新和佇列更新。 如果以預存程序建立發行集，則可啟用一個或兩個選項。 建立發行集的訂閱時，則需指定要使用的更新模式。 必要時，可切換更新模式。 如需詳細資訊，請參閱下面的＜切換更新模式＞一節。  
  
 若要為交易式發行集啟用可更新的訂閱，請參閱＜ [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)＞。  
  
 若要為交易式發行集建立可更新的訂閱，請參閱[建立交易式發行集的可更新訂閱 (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) 
  
## <a name="switching-between-update-modes"></a>切換更新模式  
 使用可更新訂閱時，可以指定訂閱應使用一個更新模式，如果應用程式有所要求，再切換至另一個更新模式。 例如，您可以指定訂閱應使用立即更新，但是如果系統錯誤造成失去網路連接，則切換至佇列更新。  
  
> [!NOTE]  
>  複寫不會自動切換更新模式。 您必須透過 SQL Server Management Studio 設定更新模式，或者您的應用程式必須呼叫 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md) 模式，才能在兩種模式之間切換。  
  
 如果從立即更新切換至佇列更新，則在「訂閱者」和「發行者」連接，且「佇列讀取器代理程式」將佇列中所有暫止訊息套用至「發行者」之前，無法切換回立即更新。  
  
 **切換更新模式**  
  
 若要切換更新模式，則必須啟用兩種更新模式的發行集和訂閱，然後必要時在它們之間進行切換。 如需相關資訊，請參閱  
[切換可更新之交易式訂閱的更新模式](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>使用可更新訂閱之考量  
  
-   在更新訂閱或佇列更新訂閱啟用發行集後，則無法停用該發行集的選項 (雖然訂閱不需要使用該選項)。 若要停用該選項，則必須刪除發行集並建立一個新的發行集。  
  
-   不支援重新發行資料。  
  
-   複寫將 **msrepl_tran_version** 資料行加入已發行的資料表中，用來進行追蹤。 因為這是新增的資料行，所以所有 **INSERT** 陳述式均應包含資料行清單。  
  
-   若要在支援更新訂閱的發行集之資料表中進行結構描述變更，則必須停止「發行者」和「訂閱者」上所有資料表的活動，且暫止資料變更必須在進行任何結構描述變更前傳播至所有節點。 這會確保未處理完畢的交易不與暫止結構描述變更發生衝突。 結構描述變更傳播至所有節點之後，可於已發行的資料表上繼續進行活動。 如需詳細資訊，請參閱[停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
-   如果計劃切換更新模式，則「佇列讀取器代理程式」在訂閱初始化後必須至少執行一次 (依預設，「佇列讀取器代理程式」會持續執行)。  
  
-   如果「訂閱者」資料庫是水平分割，且在此分割中有存在於訂閱者端，而非在發行者端的資料列，則訂閱者無法更新這些已經存在的資料列。 嘗試更新這些資料列會傳回錯誤。 資料列應該從資料表刪除，然後在發行者端加入。  

-   使用唯一篩選索引時，含有佇列可更新訂閱者的異動複寫可能會導致效能變慢。 若在具有唯一篩選索引的發行項上發生衝突，則解決衝突會導致在訂閱者上針對唯一篩選索引未涵蓋的資料列進行額外的刪除和插入。
  
### <a name="updates-at-the-subscriber"></a>在訂閱者端的更新  
  
-   即使訂閱已過期或為非使用中，訂閱者端的更新也會傳播至發行者。 請確定所有此類訂閱都已卸除或重新初始化。  
  
-   若使用 **TIMESTAMP** 或 **IDENTITY** 資料行，且這兩個資料行在複寫時成為其基底資料類型，就不應更新訂閱者中這些資料行中的值。  
  
-   因為訂閱者無法從複寫變更追蹤觸發器中所插入或刪除的資料表中讀取 **text**、 **ntext** 或 **image** 值，所以訂閱者無法更新或插入這些值。 因為資料會由發行者所覆寫，所以訂閱者也同樣無法使用 **WRITETEXT** 或 **UPDATETEXT** 更新或插入 **text** 或 **image** 值。 您反而可以將 **text** 及 **image** 資料行分割到不同的資料表，並在交易中修改這兩個資料表。  
  
     若要更新訂閱者中的大型物件，請使用資料類型 **varchar(max)** 、 **nvarchar(max)** 、 **varbinary(max)** ，而不要個別使用 **text**、 **ntext**及 **image** 資料類型。  
  
-   若更新專用索引鍵 (包含主索引鍵) 會造成重複 (例如更新格式 `UPDATE <column> SET <column> =<column>+1` )，將無法執行此作業，而且會因為違反不重複原則而遭到拒絕。 這是因為在訂閱者進行的設定更新，會在每個資料列受到影響時，透過複寫方式個別的 **UPDATE** 陳述式進行傳播。  
  
-   如果「訂閱者」資料庫是水平分割，且在此分割中有存在於「訂閱者」端，而非在「發行者」端的資料列，則「訂閱者」無法更新這些已經存在的資料列。 嘗試更新這些資料列會傳回錯誤。 資料列應該從資料表刪除，然後再次插入。  
  
### <a name="user-defined-triggers"></a>使用者自訂觸發程序  
  
-   若應用程式在訂閱者需要觸發器，便應使用 `NOT FOR REPLICATION` 選項同時在發行者與訂閱者定義觸發器。 這會確保觸發器僅為原始資料變更而引發，而不會在複寫變更時引發。  
  
     請確保複寫觸發器更新資料表時不會引發使用者自訂的觸發器。 這可藉由在使用者定義的觸發程式主體中呼叫 **sp_check_for_sync_trigger** 程序達成。 如需詳細資訊，請參閱 [sp_check_for_sync_trigger &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md)。  
  
### <a name="immediate-updating"></a>立即更新  
  
-   對於立即更新訂閱，「訂閱者」端的變更會傳播至「發行者」，並使用「Microsoft 分散式交易協調器」(MS DTC) 來套用。 請確定已在「發行者」和「訂閱者」端安裝並設定了 MS DTC。 如需詳細資訊，請參閱 Windows 文件集。  
  
-   立即更新訂閱使用的觸發器要求連接到「發行者」以複寫變更。  
  
-   如果發行集允許立即更新訂閱，且發行集中的發行項具有資料行篩選，則無法篩選無預設值的不可為 Null 資料行。  
  
### <a name="queued-updating"></a>佇列更新  
  
-   包含在合併式發行集的資料表也無法發行為允許佇列更新訂閱的部分交易式發行集。  
  
-   在使用佇立更新時，不建議更新主索引鍵資料行，這是因為主索引鍵是所有查詢的記錄定位器。 若衝突解決原則是設為「訂閱者優先」，則應在更新主索引鍵時多加注意。 若「發行者」與「訂閱者」的主索引鍵均更新，則結果將會是有著不同主索引鍵的兩資料列。  
  
-   對於資料類型為 **SQL_VARIANT**的資料行：當在訂閱者插入或更新資料後，資料會在從訂閱者複製到佇列時，由佇列讀取器代理程式以下列方式加以對應：  
  
    -   **BIGINT**、 **DECIMAL**、 **NUMERIC**、 **MONEY**和 **SMALLMONEY** 對應至 **NUMERIC**。  
  
    -   **BINARY** 和 **VARBINARY** 對應至 **VARBINARY** 資料。  
  
### <a name="conflict-detection-and-resolution"></a>衝突偵測與解決方案  
  
-   對於「訂閱者成功」衝突原則：至主索引鍵資料行的更新不支援衝突解決。  
  
-   複寫不會解決因外部索引鍵條件約束錯誤引起的衝突：  
  
    -   如果衝突是非預期的且資料分割正常 (「訂閱者」不更新相同資料列)，則可使用「發行者」和「訂閱者」上的外部索引鍵條件約束。  
  
    -   如果預期會發生衝突：在使用「訂閱者成功」衝突解決時，不應使用發行者或訂閱者端的外部索引鍵條件約束；在使用「發行者成功」衝突解決時，不應使用訂閱者端的外部索引鍵條件約束。  
  
## <a name="see-also"></a>另請參閱  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [異動複寫](../../../relational-databases/replication/transactional/transactional-replication.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
