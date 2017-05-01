---
title: "散發者資訊、代理程式 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.Distributor.commonjobs..f1
ms.assetid: 5d601a64-6af0-42f9-81b1-cf0087f1c50d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5b1db16b9faf24e2255857203ac4a685d5326ca3
ms.lasthandoff: 04/11/2017

---
# <a name="distributor-information-agents"></a>散發者資訊，代理程式
  **[代理程式]** 索引標籤會顯示與發行者和訂閱者相關聯之代理程式和維護作業的相關資訊。  
  
 專供「散發者」檢視中的「散發者」使用的代理程式會位於 **[代理程式]** 索引標籤中，當中包含了可供「發行者」使用且位於 **[代理程式]** 索引標籤中的所有代理程式。 但是，專供「散發者」檢視中之「散發者」使用的 **[代理程式]** 索引標籤也會包含「散發者代理程式」和「合併代理程式」。  
  
 如需有關「快照集」、「佇列讀取器代理程式」和維護作業的詳細資訊，請參閱＜ [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md)＞。 請注意，當您在 **[代理程式]** 索引標籤上檢視「散發者」的代理程式資訊時，「發行者」資訊也會顯示，以供「快照集」和「記錄讀取器」代理程式使用。 但是，在專供「散發者」檢視中之「散發者」使用的 **[代理程式]** 索引標籤中，您也可以選取 **[散發者代理程式]** 和 **[合併代理程式]**。  
  
## <a name="options"></a>選項  
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
  
 **訂閱**  
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
  
### <a name="merge-agent"></a>[合併代理程式]  
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
  
 **訂閱**  
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
 [檢視發行者的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
