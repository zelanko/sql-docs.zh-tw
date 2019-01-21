---
title: 發行集資訊，所有訂閱 (交易式發行集) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.allsubscriptions.tran.f1
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd2053774f8a42aaeb0146c13ee7d302e9ac0b74
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128198"
---
# <a name="publication-information-all-subscriptions-transactional-publication"></a>發行集資訊，所有訂閱 (交易式發行集)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[所有訂閱]** 索引標籤會針對選取之交易式發行集的所有訂閱顯示其資訊。  
  
## <a name="options"></a>選項。  
 如需詳細資訊以及與訂閱相關的工作，請以滑鼠右鍵按一下該訂閱的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 [排序資料行] 對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及這些資料行在 [選擇資料行] 對話方塊中的顯示順序。  
  
-   **篩選**：根據 [篩選設定] 對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **顯示**  
 僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 針對選取之訂閱類型，選取要顯示的訂閱狀態。 例如，您可以選取只顯示有錯誤的訂閱。  
  
 **狀態**  
 每個訂閱的狀態，這是由散發代理程式或記錄讀取器代理程式的狀態決定 (顯示較高優先權狀態；如果使用佇列更新訂閱，狀態也可以由佇列讀取器代理程式決定)。  
  
 依預設，包含訂閱資訊的方格是依 **[狀態]** 資料行排序 (然後由具有相同狀態之訂閱的 **[效能]** 資料行排序)。 下列清單顯示可能的狀態值和值的排序順序 (例如，錯誤一律顯示在方格頂端)。  
  
-   錯誤  
  
-   效能嚴重不足 (僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   即將過期/已過期 (僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   未初始化的訂閱 (僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   執行中  
  
 當給定訂閱有一個以上的狀態時，排序順序也會決定要顯示哪一個值。 例如，若訂閱有錯誤而且即將過期，則 **[狀態]** 資料行會顯示 **[錯誤]**。  
  
 **[效能嚴重不足]**、 **[即將過期/已過期]** 和 **[未初始化的訂閱]** 狀態值均為警告。 顯示警告時，如果代理程式正在執行，則 **[狀態]** 資料行也會顯示。 例如，狀態可能是 **[執行中，效能嚴重不足]**。  
  
 唯有設定了臨界值，才會顯示狀態值 **[效能嚴重不足]** 和 **[即將過期/已過期]** 。 如需效能測量和設定閾值的資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)和[在複寫監視器中設定閾值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **訂閱**  
 每一個訂閱的名稱，格式為：*SubscriberName:SubscriptionDatabaseName*。  
  
 **[效能]**  
 僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 每個訂閱的效能比是以複寫監視器進行的最近測量為基礎，且不會反映記錄效能。 會針對有定義效能臨界值的發行集訂閱，測量其效能；如果發行集沒有定義效能臨界值，此資料行就會顯示 **[未啟用]**。 效能評比是下列其中一個值：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
-   嚴重  
  
 如果效能嚴重不足， **[狀態]** 資料行中就會顯示 **[效能嚴重不足]** 。 如需如何定義效能評比和如何設定效能閾值的詳細資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **延遲**  
 僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 在發行者端認可之交易與在訂閱者端認可之對應交易之間經過的平均時間量。 顯示的延遲是以複寫監視器進行的最近測量為基礎。 如需測量延遲的詳細資訊，請參閱[針對異動複寫測量延遲及驗證連線](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [使用複寫監視器來檢視資訊及執行工作](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
