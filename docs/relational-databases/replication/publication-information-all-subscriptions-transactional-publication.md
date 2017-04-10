---
title: "發行集資訊，所有訂閱 (交易式發行集) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.tran.f1"
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 發行集資訊，所有訂閱 (交易式發行集)
  **[所有訂閱]** 索引標籤會針對選取之交易式發行集的所有訂閱顯示其資訊。  
  
## 選項  
 如需詳細資訊以及與訂閱相關的工作，請以滑鼠右鍵按一下該訂閱的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 **[排序資料行]** 對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及在 **[選擇資料行]** 對話方塊中顯示這些資料行所依循的順序。  
  
-   **篩選**：根據 **[篩選設定]** 對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **顯示**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 針對選取之訂閱類型，選取要顯示的訂閱狀態。 例如，您可以選取只顯示有錯誤的訂閱。  
  
 **狀態**  
 每個訂閱的狀態，這是由散發代理程式或記錄讀取器代理程式的狀態決定 (顯示較高優先權狀態；如果使用佇列更新訂閱，狀態也可以由佇列讀取器代理程式決定)。  
  
 根據預設，包含訂閱資訊的方格依 **狀態** 資料行 (然後再排序所 **效能** 這些訂用帳戶，具有相同狀態的資料行)。 下列清單顯示可能的狀態值和值的排序順序 (例如，錯誤一律顯示在方格頂端)。  
  
-   錯誤  
  
-   效能嚴重不足 (僅限 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   即將過期/已過期 (僅限 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   未初始化的訂閱 (僅限 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   執行中  
  
 當給定訂閱有一個以上的狀態時，排序順序也會決定要顯示哪一個值。 例如，若訂閱有錯誤而且即將過期，則 **[狀態]** 資料行會顯示 **[錯誤]**。  
  
 狀態值 **效能嚴重不足**, ，**即將過期/已過期**, ，和 **未初始化的訂閱** 會出現警告。 顯示警告時，如果代理程式正在執行，則 **[狀態]** 資料行也會顯示。 例如，狀態可能是 **[執行中，效能嚴重不足]**。  
  
 狀態值 **效能嚴重不足** 和 **即將過期/已過期** 閾值設定時，才會顯示。 如需效能測量和設定臨界值，請參閱 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) 和 [設定臨界值和複寫監視器 」 中的警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **訂閱**  
 在表單中的每一個訂閱名稱︰ *SubscriberName: SubscriptionDatabaseName*。  
  
 **效能**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 每個訂閱的效能比是以複寫監視器進行的最近測量為基礎，且不會反映記錄效能。 會針對有定義效能臨界值的發行集訂閱，測量其效能；如果發行集沒有定義效能臨界值，此資料行就會顯示 **[未啟用]**。 效能評比是下列其中一個值：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
-   嚴重  
  
 如果效能嚴重不足， **[狀態]** 資料行中就會顯示 **[效能嚴重不足]** 。 如需有關如何定義效能評比和如何設定效能臨界值的詳細資訊，請參閱 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **延遲**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 在發行者端認可之交易與在訂閱者端認可之對應交易之間經過的平均時間量。 顯示的延遲是以複寫監視器進行的最近測量為基礎。 如需有關測量延遲的詳細資訊，請參閱 [測量延遲及驗證連線的交易式複寫](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## 另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視資訊以及訂閱 & #40; 執行工作複寫監視器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  