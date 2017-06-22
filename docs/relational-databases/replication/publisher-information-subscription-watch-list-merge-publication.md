---
title: "發行者資訊，訂閱監看清單 (合併式發行集) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1a6afe57c26dcf92aa82a9542cd65f9f3997d44
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="publisher-information-subscription-watch-list-merge-publication"></a>發行者資訊，訂閱監看清單 (合併式發行集)
  執行 **和更新版本的散發者可以使用** [訂閱監看清單] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 索引標籤。這個索引標籤的用途是顯示選取發行者端之所有可用發行集的相關訂閱資訊。 您可以篩選訂閱清單以查看錯誤、警告以及任何執行不良的訂閱。 此索引標籤為管理員提供監視發行者端所有複寫活動的單一位置：複寫監視器會根據選取的複寫類型和 **[顯示]** 下拉式清單方塊中選擇的選項，顯示需要注意的所有訂閱。 由於此索引標籤上顯示的項目會依據目前的狀態與效能，因此唯有在目前符合 **[顯示]** 清單方塊中之選項的訂閱，才會在這個頁面上顯示。  
  
## <a name="options"></a>選項  
 如需詳細資訊以及與訂閱相關的工作，請以滑鼠右鍵按一下該訂閱的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 **[排序資料行]** 對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及在 **[選擇資料行]** 對話方塊中顯示這些資料行所依循的順序。  
  
-   **篩選**：根據 **[篩選設定]** 對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **顯示合併訂閱**  
 針對選取之發行者，選取要顯示的訂閱類型 (交易式、快照式或合併式)。  
  
 **[顯示]**  
 針對選取之訂閱類型，選取要顯示的訂閱狀態。 例如，您可以選取只顯示有錯誤的訂閱。  
  
 **狀態**  
 每一個訂閱的狀態，是由合併代理程式的狀態決定。  
  
 依預設，包含訂閱資訊的方格是依 **[狀態]** 資料行排序 (然後由具有相同狀態之訂閱的 **[效能]** 資料行排序)。 下列清單顯示可能的狀態值和值的排序順序 (例如，錯誤一律顯示在方格頂端)。  
  
-   錯誤  
  
-   效能嚴重不足  
  
-   長期執行合併  
  
-   即將過期/已過期  
  
-   未初始化的訂閱  
  
-   正在重試失敗的命令  
  
-   正在同步處理  
  
-   未進行同步處理  
  
 當給定訂閱有一個以上的狀態時，排序順序也會決定要顯示哪一個值。 例如，若訂閱有錯誤而且即將過期，則 [狀態]  資料行會顯示 [錯誤] 。  
  
 **[效能嚴重不足]**、 **[長時間執行的合併]**、 **[即將過期/已過期]**和 **[未初始化的訂閱]** 等狀態值均為警告。 如果有顯示警告，則 **[狀態]** 資料行也會顯示代理程式是否為同步處理。 例如，狀態可能是 **[正在同步處理，效能嚴重不足]**。  
  
 只有設定臨界值時，才會顯示 **[即將過期/已過期]** 和 **[長時間執行的合併]** 狀態值。 只有在相同連接類型 (撥號或 LAN) 的訂閱經過五次同步處理之後，才會顯示 **[效能嚴重不足]** 的狀態值。 如需效能測量和設定閾值的資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)和[在複寫監視器中設定閾值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **訂閱**  
 每一個訂閱名稱的格式為：*SubscriberName: SubscriptionDatabaseName*。  
  
 **易記名稱**  
 每一個訂閱的描述。 此描述輸入於 **[訂閱屬性]** 對話方塊中，或以 **@description** 或 [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) 的 [@description](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 使用者通常使用描述作為訂閱的「易記名稱」或暱稱。  
  
 **發行集**  
 與訂閱同步處理的發行集名稱，格式如下： *PublicationDatabaseName: PublicationName*。  
  
 **[效能]**  
 每一個訂閱的效能評比，是以複寫監視器所測量之傳遞速率的最新數據為基礎。 評比會根據相同連接類型 (撥號或 LAN) 的發行集訂閱，進行個別訂閱效能和平均記錄效能的比較來決定。 在相同連接類型上發生過五次同步處理，且每次同步處理都具有 50 或更多個變更之後，複寫監視器才會顯示值。 如果具有 50 或更多個變更的同步處理少於五次，或者最近的同步處理少於 50 個變更，則此資料行為空白。  
  
> [!NOTE]  
>  效能是以 **[連接]** 資料行所顯示的連接類型為基礎；因此，如果第一個訂閱是透過較慢速連接進行同步處理，則傳遞速率較低的訂閱有可能顯示比另一個訂閱更好的效能評比。  
  
 效能評比是下列其中一個值：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
 如需如何定義效能評比和如何設定效能閾值的詳細資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **傳遞速率**  
 合併代理程式每秒處理的資料列數目。  
  
 **上次同步處理日期**  
 合併代理程式上次執行的時間。 在這次同步處理期間不一定有處理變更。 如果正在進行同步處理，就會顯示完成百分比值。  
  
 **有效期間**  
 合併代理程式在上次同步處理期間執行的時間量。 如果合併代理程式目前正在進行同步處理，則時間代表經過時間，如果合併代理程式先前已同步處理，則時間代表總共花費的時間。  
  
 **[連接]**  
 訂閱者和發行者之間的連接類型。 可能的值為 **[LAN]**、 **[撥號]**和 **[網際網路]**。 如果訂閱使用 Web 同步處理，則會顯示 **[網際網路]** 值。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視發行者的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
