---
title: "增強異動複寫效能 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 441ae5e2f835146f3d25bda645c44b33fa0146d2
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="enhance-transactional-replication-performance"></a>增強異動複寫效能
  除了考慮＜ [增強一般複寫效能](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)＞中所述的一般效能提示之外，還要考慮異動複寫特定的以下幾個其他方面。  
  
## <a name="database-design"></a>資料庫設計  
  
-   將應用程式設計中的交易量最小化。  
  
     依預設，異動複寫會根據交易界限傳播變更。 如果交易較小，便不太可能發生「散發代理程式」因網路問題而必須重新傳送交易的情況。 如果需要代理程式來重新傳送交易，則傳送的資料量較小。  
  
## <a name="distributor-configuration"></a>散發者組態  
  
-   在專用伺服器上設定散發者。  
  
     透過設定遠端「散發者」可以降低「發行者」端的處理負擔。 如需詳細資訊，請參閱[設定散發](../../../relational-databases/replication/configure-distribution.md)。  
  
-   適當調整散發資料庫的大小。  
  
     用一般負載量為系統測試複寫，以決定需要多少空間儲存命令。 確認資料庫大小足夠儲存命令，且無須經常自動成長。 如需變更資料庫大小的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="publication-design"></a>發行集設計  
  
-   批次更新到已發行資料表時，複寫預存程序執行。  
  
     如果您的批次更新偶而會影響到訂閱者的大量資料列，則應該考慮使用預存程序來更新發行的資料表，並發行預存程序的執行。 「散發代理程式」不會傳送每一個受影響資料列的更新或刪除，卻會使用相同的參數值在「訂閱者」端執行相同的程序。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   跨多發行集傳播發行項。  
  
     如果您無法使用 **-SubscriptionStreams** 參數 (本主題中稍後將進行討論)，請考慮建立多個發行集。 在這些發行集間分散發行項允許複寫將變更平行套用到各個「訂閱者」。  
  
## <a name="subscription-considerations"></a>訂閱考量因素  
  
-   如果您在同一「發行者」端有多個發行集，請使用獨立代理程式而非共用代理程式 (此為「新增發行集精靈」的預設值)。  
  
-   連續執行代理程式來代替非常頻繁的排程執行。  
  
     將代理程式設定為連續執行來代替建立頻繁的排程 (例如每分鐘) 可提升複寫效能，因為代理程式不必啟動和停止。 當您將「散發代理程式」設定為連續執行時，變更將以低度延遲傳播到拓撲中連接的其他伺服器。 如需詳細資訊，請參閱：  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[指定同步處理排程](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>散發代理程式和記錄讀取器代理程式參數  
  
-   若要解決意外的一次性瓶頸，請針對記錄讀取器代理程式使用 **–MaxCmdsInTran** 參數。  
  
     **–MaxCmdsInTran** 參數指定當「記錄讀取器」將命令寫入散發資料庫時，分組到某交易內的最大陳述式數量。 使用此參數可讓「記錄讀取器代理程式」和「散發作業代理程式」在「訂閱者」端套用命令時，於「發行者」端將大型交易 (由許多命令組成) 分割成幾個較小的交易。 指定此參數可以降低「散發者」的競爭，並減少「發行者」和「訂閱者」之間的延遲。 因為原始交易是以較小的單位來套用，所以「訂閱者」在原始交易結束之前可以存取大量的邏輯「發行者」交易資料列，打破了嚴格的交易不可部份完成性。 預設值為 **0**，保留「發行者」的交易界限。 此參數不會套用至 Oracle 發行者。  
  
    > [!WARNING]  
    >  **MaxCmdsInTran** 的設計不是為了要永遠開啟。 其存在的目的是為了解決有人不小心在單一交易中執行大量 DML 作業的狀況 (使得整筆交易在散發資料庫之前延遲命令的散發、鎖定持有等等)。 如果您習慣性地遇到這個狀況，您應該檢閱您的應用程式，並找出減少交易大小的方法。  
  
-   使用「散發代理程式」的 **–SubscriptionStreams** 參數。  
  
     **–SubscriptionStreams** 參數可大幅提升彙總複寫輸送量。 它允許至「訂閱者」的多個連接平行套用批次變更，同時在使用單一執行緒時維護現有的許多交易特性。 如果有一個連接無法執行或認可，則所有連接都將中止目前批次，且代理程式將使用單一資料流重試失敗的批次。 在此重試階段完成之前，「訂閱者」端可能會出現暫時的交易不一致性。 成功認可失敗的批次後，「訂閱者」將返回交易一致性的狀態。  
  
     此代理程式參數的值可以使用 [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@subscriptionstreams** 來指定。  
  
-   為「記錄讀取器代理程式」增加 **-ReadBatchSize** 參數的值。  
  
     「記錄讀取器代理程式」與「散發代理程式」支援交易讀取與認可作業的批次大小。 批次大小的預設值是 500 項交易。 「記錄讀取器代理程式」會從記錄檔中讀取特定數量的交易，無論這些交易是否都標示為複寫。 當大量交易寫入發行資料庫，但標示要複寫的只是其中小部分子集時，您就應該使用 **-ReadBatchSize** 參數來增加「記錄讀取器代理程式」的讀取批次大小。 此參數不會套用至 Oracle 發行者。  
  
-   為「散發代理程式」增加 **-CommitBatchSize** 參數的值。  
  
     認可一組交易的負擔是固定的；透過以較低頻率認可較大的交易量，負擔會分散到較大量的資料。 但是，由於套用變更的成本還受限於其他因素，例如包含記錄檔之磁碟的最大 I/O，因此增加此參數的好處不那麼明顯。 此外，還要考慮反向作用：任何導致散發代理程式重新啟動的失敗都必須回復，並重新套用更大量的交易。 對於不穩定的網路，當發生錯誤時，值越低導致的錯誤就越少，要回復並重新套用的交易數也越少。  
  
-   為「記錄讀取器代理程式」減少 **-PollingInterval** 參數的值。  
  
     **-PollingInterval** 參數指定針對待複寫交易查詢已發行資料庫之交易記錄檔的頻率。 預設值是 5 秒。 如果減小此值，記錄檔輪詢將更頻繁，這會降低從發行集資料庫到散發資料庫之交易傳遞的延遲。 但是，您應在降低延遲需求和因更頻繁地輪詢而導致伺服器負載增加之間進行平衡。  
  
 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱：  
  
-   [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
