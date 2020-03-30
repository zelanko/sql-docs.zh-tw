---
title: 散發者資訊、發行集 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.Distributor.Publications.f1
- sql13.rep.monitor.Distributor.commonjobs..f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 91e4ceeba2e8ec18569c22a886623977402e478a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76284006"
---
# <a name="distributor-information-publications"></a>散發者資訊，發行集
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[發行集]** 索引標籤可以提供在左窗格中所選取「散發者」之所有發行集的摘要資訊。  
  
顯示的資訊會與受到「散發者」支援的發行集相關，當中包括了包含「發行者」之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料行。 否則，當您在複寫監視器的「發行者」檢視中檢視發行集時，所提供的發行集資訊會與此處的發行集資訊相同。 如需有關 **[發行集]** 索引標籤中之資料行的詳細資訊，請參閱＜ [Publisher Information, Publications](../../relational-databases/replication/publisher-information-publications.md)＞。  

## <a name="subscription-watch-list"></a>訂閱監看清單

### <a name="transactional-replication"></a>異動複寫
  交易式訂閱資訊會包括「發行者」的名稱。 否則，這個對話方塊提供的功能和資訊會與在「發行者」檢視相同。 如需如何使用這個對話方塊的詳細資訊，請參閱[發行者資訊、訂閱監看清單 &#40;交易式發行集，SQL Server 2005 和更新版本&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-transactional.md)。 

### <a name="merge-replication"></a>合併式複寫
  合併式發行集的訂閱資訊會包括「發行者」的名稱。 否則，這個對話方塊提供的功能和資訊會與在「發行者」檢視相同。 如需如何使用這個對話方塊的詳細資訊，請參閱[發行者資訊、訂閱監看清單 &#40;合併式發行集，SQL Server 2005 和更新版本&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-merge-publication.md)。  

### <a name="snapshot-replication"></a>快照式複寫 
  快照式發行集的訂閱資訊會包括「發行者」的名稱。 否則，這個對話方塊提供的功能和資訊會與在「發行者」檢視相同。 如需如何使用這個對話方塊的詳細資訊，請參閱[發行者資訊、訂閱監看清單 &#40;快照式發行集，SQL Server 2005 和更新版本&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-snapshot.md)。  

## <a name="agents"></a>代理程式
**[代理程式]** 索引標籤會顯示與發行者和訂閱者相關聯之代理程式和維護作業的相關資訊。  
  
 專供「散發者」檢視中的「散發者」使用的代理程式會位於 **[代理程式]** 索引標籤中，當中包含了可供「發行者」使用且位於 **[代理程式]** 索引標籤中的所有代理程式。 但是，專供「散發者」檢視中之「散發者」使用的 **[代理程式]** 索引標籤也會包含「散發者代理程式」和「合併代理程式」。  
  
 如需有關「快照集」、「佇列讀取器代理程式」和維護作業的詳細資訊，請參閱＜ [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md)＞。 請注意，當您在 **[代理程式]** 索引標籤上檢視「散發者」的代理程式資訊時，「發行者」資訊也會顯示，以供「快照集」和「記錄讀取器」代理程式使用。 但是，在專供「散發者」檢視中之「散發者」使用的 **[代理程式]** 索引標籤中，您也可以選取 **[散發者代理程式]** 和 **[合併代理程式]** 。  
  
### <a name="options"></a>選項。  
 下列各節將描述這個索引標籤上針對「散發者代理程式」和「合併代理程式」顯示的資料。  
  
### <a name="distributor-agent"></a>[散發者代理程式]  
 **狀態**  
 代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤    
-   重試    
-   執行中    
-   未執行   
-   從未啟動  
  
 **發行者**  
 「發行者」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 **發行集**  
 與代理程式相關聯之發行集的名稱。  
  
 **訂用帳戶**  
 訂閱的名稱，格式應該為：[*SubscriberName*].[*Database*]。  
  
 **型別**  
 複寫類型：發送、提取或匿名。  
  
 **上次啟動時間**  
 代理程式上次啟動的時間。  
  
 **有效期間**  
 代理程式已執行的時間長度。 如果代理程式目前正在執行，此時間代表經過時間。如果代理程式先前已執行過，則代表總時間。  
  
 **最後一個動作**  
 代理程式最近一次執行期間執行的最後一個動作。  
  
 **傳遞速率**  
 最近一次代理程式執行期間，在散發資料庫中認可初始化命令的速率 (以每秒命令數為單位)。  
  
 **延遲**  
 在發行集資料庫中認可的最近一次變更與散發資料庫中認可的對應命令之間經過的時間 (以秒為單位)。  
  
 **交易數**  
 最近一次代理程式執行期間，在散發資料庫中認可的交易數目。  
  
 **命令數**  
 最近一次代理程式執行期間，在散發資料庫中認可的命令數目。 命令與資料變更 (例如更新) 相同。  
  
 **平均命令數**  
 最近一次代理程式執行期間，每項交易的平均命令數目。  
  
### <a name="merge-agent"></a>合併代理程式  
 **狀態**  
 代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   重試  
  
-   執行中  
  
-   未執行  
  
-   從未啟動  
  
 **發行者**  
 「發行者」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 **發行集**  
 與代理程式相關聯之發行集的名稱。  
  
 **訂用帳戶**  
 訂閱的名稱，格式應該為：[*SubscriberName*].[*Database*]。  
  
 **型別**  
 複寫類型：發送、提取或匿名。  
  
 **上次啟動時間**  
 代理程式上次啟動的時間。  
  
 **有效期間**  
 代理程式已執行的時間長度。 如果代理程式目前正在執行，此時間代表經過時間。如果代理程式先前已執行過，則代表總時間。  
  
 **最後一個動作**  
 代理程式最近一次執行期間執行的最後一個動作。  
  
 **傳遞速率**  
 在散發資料庫中認可變更的速率 (以每秒命令數為單位)。  
  
 **發行者插入**  
 發行者端所套用的 INSERT 命令數目。  
  
 **發行者更新**  
 發行者端所套用的 UPDATE 命令數目。  
  
 **發行者刪除**  
 發行者端所套用的 DELETE 命令數目。  
  
 **發行者衝突**  
 合併處理期間發行者端每秒所發生的衝突數。  
  
 **訂閱者插入**  
 訂閱者端所套用的 INSERT 命令數目。  
  
 **訂閱者更新**  
 訂閱者端所套用的 UPDATE 命令數目。  
  
 **訂閱者刪除**  
 訂閱者端所套用的 DELETE 命令數目。  
  
 **訂閱者衝突**  
 合併處理期間訂閱者端每秒所發生的衝突數。  

  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
  
  
