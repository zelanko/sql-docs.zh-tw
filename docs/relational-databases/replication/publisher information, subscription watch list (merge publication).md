---
title: "發行者資訊，訂閱監看清單 (合併式發行集，SQL Server 2005 和更新的版本) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1"
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 發行者資訊，訂閱監看清單 (合併式發行集，SQL Server 2005 和更新的版本)
   **訂閱監看清單** ] 索引標籤可供散發者執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本; 它用來顯示所有可用選取發行者端之發行集的訂閱資訊。 您可以篩選訂閱清單以查看錯誤、警告以及任何執行不良的訂閱。 此索引標籤提供系統管理員可以監視所有的複寫活動，在發行者端的單一位置︰ 複寫監視器 」 會顯示所有的訂閱需要注意的地方，根據選取的複寫類型，並在所選擇的選項 **顯示** 下拉式清單方塊。 由於此索引標籤上顯示的項目會依據目前的狀態與效能，因此唯有在目前符合 **[顯示]** 清單方塊中之選項的訂閱，才會在這個頁面上顯示。  
  
## 選項  
 如需詳細資訊以及與訂閱相關的工作，請以滑鼠右鍵按一下該訂閱的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 **[排序資料行]** 對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及在 **[選擇資料行]** 對話方塊中顯示這些資料行所依循的順序。  
  
-   **篩選**：根據 **[篩選設定]** 對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **顯示合併訂閱**  
 針對選取之發行者，選取要顯示的訂閱類型 (交易式、快照式或合併式)。  
  
 **顯示**  
 針對選取之訂閱類型，選取要顯示的訂閱狀態。 例如，您可以選取只顯示有錯誤的訂閱。  
  
 **狀態**  
 每一個訂閱的狀態，是由合併代理程式的狀態決定。  
  
 根據預設，包含訂閱資訊的方格依 **狀態** 資料行 (然後再排序所 **效能** 這些訂用帳戶，具有相同狀態的資料行)。 下列清單顯示可能的狀態值和值的排序順序 (例如，錯誤一律顯示在方格頂端)。  
  
-   錯誤  
  
-   效能嚴重不足  
  
-   長期執行合併  
  
-   即將過期/已過期  
  
-   未初始化的訂閱  
  
-   正在重試失敗的命令  
  
-   正在同步處理  
  
-   未進行同步處理  
  
 當給定訂閱有一個以上的狀態時，排序順序也會決定要顯示哪一個值。 例如，若訂閱有錯誤而且即將過期，則 **[狀態]** 資料行會顯示 **[錯誤]**。  
  
 狀態值 **效能嚴重不足**, ，**長時間執行的合併**, ，**即將過期/已過期**, ，和 **未初始化的訂閱** 會出現警告。 如果有顯示警告，則 **[狀態]** 資料行也會顯示代理程式是否為同步處理。 例如，狀態可能是 **[正在同步處理，效能嚴重不足]**。  
  
 狀態值 **即將過期/已過期** 和 **長時間執行的合併** 閾值設定時，才可以顯示。 狀態值 **效能嚴重不足** 五次同步處理的訂閱，且相同的連接類型 （撥號或 LAN） 後，才可以顯示。 如需效能測量和設定臨界值，請參閱 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) 和 [設定臨界值和複寫監視器 」 中的警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **訂閱**  
 在表單中的每一個訂閱名稱︰*SubscriberName: SubscriptionDatabaseName*。  
  
 **易記名稱**  
 每一個訂閱的描述。 描述輸入於 **訂閱屬性** 對話方塊或指定了 **@description** 參數 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) 或 [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 使用者通常使用描述作為訂閱的「易記名稱」或暱稱。  
  
 **發行集**  
 與訂閱同步處理，在表單中的發行集名稱︰ *PublicationDatabaseName: PublicationName*。  
  
 **效能**  
 每一個訂閱的效能評比，是以複寫監視器所測量之傳遞速率的最新數據為基礎。 評比會根據相同連接類型 (撥號或 LAN) 的發行集訂閱，進行個別訂閱效能和平均記錄效能的比較來決定。 在相同連接類型上發生過五次同步處理，且每次同步處理都具有 50 或更多個變更之後，複寫監視器才會顯示值。 如果具有 50 或更多個變更的同步處理少於五次，或者最近的同步處理少於 50 個變更，則此資料行為空白。  
  
> [!NOTE]  
>  效能根據連線類型顯示在 **連接** 資料行，因此可能會具有較低的傳送速率，以顯示較佳效能等級比另一個訂閱如果透過較慢的連線的第一個訂閱進行同步處理的訂閱。  
  
 效能評比是下列其中一個值：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
 如需有關如何定義效能評比和如何設定效能臨界值的詳細資訊，請參閱 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **傳遞速率**  
 合併代理程式每秒處理的資料列數目。  
  
 **上次同步處理日期**  
 合併代理程式上次執行的時間。 在這次同步處理期間不一定有處理變更。 如果正在進行同步處理，就會顯示完成百分比值。  
  
 **有效期間**  
 合併代理程式在上次同步處理期間執行的時間量。 如果合併代理程式目前正在進行同步處理，則時間代表經過時間，如果合併代理程式先前已同步處理，則時間代表總共花費的時間。  
  
 **連接**  
 訂閱者和發行者之間的連接類型。 可能的值為 **[LAN]**、 **[撥號]**和 **[網際網路]**。 如果訂閱使用 Web 同步處理，則會顯示 **[網際網路]** 值。  
  
## 另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視資訊並執行工作的 「 發行者 」 與 #40;複寫監視器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [合併式複寫的 Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  