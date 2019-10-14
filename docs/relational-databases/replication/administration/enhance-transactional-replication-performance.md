---
title: 增強異動複寫效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: f50978c19295f5973e787bdaab46efea6367308a
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710383"
---
# <a name="enhance-transactional-replication-performance"></a>增強異動複寫效能
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  除了考慮＜ [增強一般複寫效能](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)＞中所述的一般效能提示之外，還要考慮異動複寫特定的以下幾個其他方面。  
  
## <a name="database-design"></a>資料庫設計  
  
-   將應用程式設計中的交易量最小化。  
  
     依預設，異動複寫會根據交易界限傳播變更。 如果交易較小，便不太可能發生「散發代理程式」因網路問題而必須重新傳送交易的情況。 如果需要代理程式來重新傳送交易，則傳送的資料量較小。 

  
## <a name="distributor-configuration"></a>散發者組態  
  
-   在專用伺服器上設定散發者。  
  
     透過設定遠端「散發者」可以降低「發行者」端的處理負擔。 如需詳細資訊，請參閱 [Configure Distribution](../../../relational-databases/replication/configure-distribution.md)＞。  
  
-   適當調整散發資料庫的大小。  
  
     用一般負載量為系統測試複寫，以決定需要多少空間儲存命令。 確認資料庫大小足夠儲存命令，且無須經常自動成長。 如需變更資料庫大小的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="publication-design"></a>發行集設計  
  
-   批次更新到已發行資料表時，複寫預存程序執行。  
  
     如果您的批次更新偶而會影響到訂閱者的大量資料列，則應該考慮使用預存程序來更新發行的資料表，並發行預存程序的執行。 「散發代理程式」不會傳送每一個受影響資料列的更新或刪除，卻會使用相同的參數值在「訂閱者」端執行相同的程序。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   跨多發行集傳播發行項。  
  
     如果您無法使用 [ **-SubscriptionStreams** 參數](#subscriptionstreams)，請考慮建立多個發行集。 在這些發行集間分散發行項允許複寫將變更平行套用到各個「訂閱者」。  
  
## <a name="subscription-considerations"></a>訂閱考量因素  
  
-   如果您在同一「發行者」端有多個發行集，請使用獨立代理程式而非共用代理程式 (此為「新增發行集精靈」的預設值)。  
  
-   連續執行代理程式來代替頻繁的排程執行。  
  
     將代理程式設定為連續執行來代替建立頻繁的排程 (例如每分鐘) 可提升複寫效能，因為代理程式不必啟動和停止。 當您將「散發代理程式」設定為連續執行時，變更將以低度延遲傳播到拓撲中連接的其他伺服器。 如需詳細資訊，請參閱：  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[指定同步處理排程](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>散發代理程式和記錄讀取器代理程式參數  
代理程式設定檔參數會經常調整，目的是要讓「記錄讀取器」和「散發代理程式」的輸送量與高流量 OLTP 系統一同增加。 

進行測試的目的是要決定最合適的值，以提高「記錄讀取器」和「散發代理程式」的效能。 此測試的結論是：工作負載已成為值在何種情況下才有效的決定性因素了，因此，不可能只調整單一值就改善每種情況下的效能。 

結果： 
- 若「記錄讀取器代理程式」  具有較小型交易的工作負載 (少於 500 個命令) 時，**ReadBatchSize** 較高的值可能會對輸送量產生有利的影響。 不過，針對具有大型交易的工作負載，變更這值不會改善效能。 
    - 當同一個伺服器上有多個「記錄讀取器代理程式」和多個「散發代理程式」平行執行時，**ReadBatchSize** 較大的值會導致散發資料庫出現爭用的狀況。 
- 針對「散發代理程式」 
    - 增加 **CommitBatchSize** 可以改善輸送量。 缺點是，如果發生失敗，「散發代理程式」必須復原並從頭再次套用更大的交易量。 
    - 增加 **SubscriptionStreams** 值有助於提升「散發代理程式」的整體輸送量，因為多個訂閱者連線會平行套用變更批次。 不過，根據處理器數目以及其他中繼資料的條件 (例如主索引鍵、外部索引鍵、唯一限制式和索引)，SubscriptionStreams 較高的值，實際上可能會有不利的影響。 此外，如果資料流無法執行或認可，則「散發代理程式」會退而使用單一資料流來重試失敗的批次。


如需有關這項測試的詳細資訊，請參閱部落格[最佳化複寫代理程式設定檔參數以提升效能](https://blogs.msdn.microsoft.com/sql_server_team/optimizing-replication-agent-profile-parameters-for-better-performance/) \(英文\)。


### <a name="log-reader-agent"></a>記錄讀取器代理程式

#### <a name="readbatchsize"></a>ReadBatchSize
- 為「記錄讀取器代理程式」增加 **-ReadBatchSize** 參數的值。  
  
「記錄讀取器代理程式」與「散發代理程式」支援交易讀取與認可作業的批次大小。 批次大小的預設值是 500 項交易。 「記錄讀取器代理程式」會從記錄檔中讀取特定數量的交易，無論這些交易是否都標示為複寫。 當大量交易寫入發行集資料庫，但標示要複寫的只是其中小部分子集時，您就應該使用 **-ReadBatchSize** 參數來增加「記錄讀取器代理程式」的讀取批次大小。 此參數不會套用至 Oracle 發行者。  

   - 當 **ReadBatchSize** 增加到 5000 時，較小型交易的工作負載 (少於 500 個的命令) 每秒處理的命令數會增加。 
   - 至於較大型的工作負載 (具有 500 到 1000 個命令的交易)，增加 **ReadBatchSize** 會稍提改善效能。 增加 **ReadBatchSize** 會導致大量交易被一次性寫入散發資料庫。 這會增加「散發代理程式」看到交易和命令的時間，讓複寫處理產生延遲。  

#### <a name="pollinginterval"></a>PollingInterval
- 為「記錄讀取器代理程式」減少 **-PollingInterval** 參數的值。  
  
**-PollingInterval** 參數指定針對待複寫交易查詢已發行資料庫之交易記錄檔的頻率。 預設值是 5 秒。 如果減小此值，記錄檔輪詢將更頻繁，這會降低從發行集資料庫到散發資料庫之交易傳遞的延遲。 但是，您應在降低延遲需求和因更頻繁地輪詢而導致伺服器負載增加之間進行平衡。   
  
#### <a name="maxcmdsintran"></a>MaxCmdsInTran
- 若要解決意外的一次性瓶頸，請針對記錄讀取器代理程式使用 **–MaxCmdsInTran** 參數。  
  
**–MaxCmdsInTran** 參數指定當「記錄讀取器」將命令寫入散發資料庫時，分組到某交易內的最大陳述式數量。 使用此參數可讓「記錄讀取器代理程式」和「散發作業代理程式」在「訂閱者」端套用命令時，於「發行者」端將大型交易 (由許多命令組成) 分割成幾個較小的交易。 指定此參數可以降低「散發者」的競爭，並減少「發行者」和「訂閱者」之間的延遲。 因為原始交易是以較小的單位來套用，所以「訂閱者」在原始交易結束之前可以存取大量的邏輯「發行者」交易資料列，打破了嚴格的交易不可部份完成性。 預設值為 **0**，保留「發行者」的交易界限。 此參數不會套用至 Oracle 發行者。  
  
   > [!WARNING]  
   >  **MaxCmdsInTran** 的設計不是為了要永遠開啟。 其存在的目的是為了解決有人不小心在單一交易中執行大量 DML 作業的狀況 (使得整筆交易在散發資料庫之前延遲命令的散發、鎖定持有等等)。 如果您經常地遇到這個狀況，請檢閱您的應用程式，並找出減少交易大小的方法。  
  
### <a name="distribution-agent"></a>散發代理程式

#### <a name="subscriptionstreams"></a>SubscriptionStreams
- 增加「散發代理程式」的 **–SubscriptionStreams** 參數。  
  
**–SubscriptionStreams** 參數可大幅提升彙總複寫輸送量。 它允許至「訂閱者」的多個連接平行套用批次變更，同時在使用單一執行緒時維護現有的許多交易特性。 如果有一個連接無法執行或認可，則所有連接都將中止目前批次，且代理程式將使用單一資料流重試失敗的批次。 在此重試階段完成之前，「訂閱者」端可能會出現暫時的交易不一致性。 成功認可失敗的批次後，「訂閱者」將返回交易一致性的狀態。  
  
此代理程式參數值可以使用 [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 `@subscriptionstreams` 來指定。  

如需有關實作訂用帳戶資料流的詳細資訊，請參閱[瀏覽 SQL 複寫 subscriptionStream 設定](https://blogs.msdn.microsoft.com/repltalk/2010/03/01/navigating-sql-replication-subscriptionstreams-setting) \(英文\)。
  
### <a name="blocking-monitor-thread"></a>封鎖監視執行緒

散發代理程式會維護在兩個工作階段之間偵測封鎖的封鎖監視執行緒。 如果封鎖監視執行緒在兩個工作階段之間偵測到封鎖，散發代理程式就會切換為使用一個工作階段，以重新套用先前無法套用的目前命令批次。

封鎖監視執行緒可在散發代理程式工作階段之間偵測封鎖。 不過，封鎖監視執行緒在下列情況無法偵測封鎖：
- 發生封鎖的其中一個工作階段不是散發代理程式工作階段。
- 工作階段死結凍結了散發代理程式的活動。

在這種情況下，散發代理程式會協調所有工作階段，使其在命令執行時一併認可。 如果滿足下列條件，工作階段中的死結就會發生：

- 封鎖發生在散發代理程式工作階段與不是散發代理程式工作階段的工作階段之間。
- 散發代理程式在等候所有工作階段完成執行其命令，之後散發代理程式才協調所有工作階段，使其一併認可。

例如，您將 *SubscriptionStreams* 參數設為 8。 工作階段 10 到工作階段 17 為散發代理程式工作階段。 工作階段 18 不是散發代理程式工作階段。 工作階段 18 封鎖了工作階段 10，而工作階段 11 封鎖了工作階段 18。 另外，工作階段 10 和工作階段 11 必須一併認可。 不過，因為封鎖的關係，散發代理程式無法一併認可工作階段 10 和工作階段 11。 因此，在工作階段 10 和工作階段 11 執行其命令之前，散發代理程式無法協調這八個工作階段，使其一併認可。

這個例子導致了沒有任何工作階段執行其命令的狀態。 當達到 **QueryTimeout** 屬性中指定的時間時，散發代理程式就會取消所有工作階段。

> [!Note]
> 根據預設，**QueryTimeout** 屬性的值為 5 分鐘。

在這段查詢逾時期間，您可能會注意到散發代理程式效能計數器有下列趨勢： 

- **Dist:Delivered Cmds/sec** 效能計數器的值一律為 0。
- **Dist:Delivered Trans/sec** 效能計數器的值一律為 0。
- **Dist:Delivery Latency** 效能計數器會回報值增加的情況，直到執行緒死結解決為止。

《SQL Server 線上叢書》中的＜複寫散發代理程式＞主題包含 *SubscriptionStreams* 參數的下列描述：「如果有無法執行或認可某個連線，則所有連線都將中止目前批次，且代理程式將使用單一資料流重試失敗的批次。」

散發代理程式會使用一個工作階段來重試無法套用的批次。 在散發代理程式成功套用批次之後，散發代理程式會繼續使用多個工作階段，而不會重新啟動。

#### <a name="commitbatchsize"></a>CommitBatchSize
- 為「散發代理程式」增加 **-CommitBatchSize** 參數的值。  
  
認可一組交易的負擔是固定的；透過以較低頻率認可較大的交易量，負擔會分散到較大量的資料。  增加 CommitBatchSize (最多到 200) 可以改善效能，因為可提交更多的交易給訂閱者。 但是，由於套用變更的成本還受限於其他因素，例如包含記錄檔之磁碟的最大 I/O，因此增加此參數的好處不那麼明顯。 此外，還要考慮以下的權衡得失：任何導致「散發代理程式」重新啟動的失敗都必須復原，並重新套用更大的交易數。 對於不穩定的網路，當發生錯誤時，值越低導致的錯誤就越少，要復原並重新套用的交易數也越少。  
  

## <a name="see-more"></a>查看更多
  
[處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
[檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
