---
title: 發行集資訊，所有訂閱 (快照式發行集) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.allsubscriptions.snapshot.f1
ms.assetid: 7ce656c2-6e60-4625-8955-1daff641070c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37e3a3fefcbd604774254467e3bc8516716fbcef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701296"
---
# <a name="publication-information-all-subscriptions-snapshot-publication"></a>發行集資訊，所有訂閱 (快照式發行集)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[所有訂閱]** 索引標籤，會顯示所選取快照式發行集之所有訂閱的資訊。  
  
## <a name="options"></a>選項。  
 如需詳細資訊以及與訂閱相關的工作，請以滑鼠右鍵按一下該訂閱的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 **[排序資料行]** 對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及在 **[選擇資料行]** 對話方塊中顯示這些資料行所依循的順序。  
  
-   **篩選**：根據 **[篩選設定]** 對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **顯示**  
 僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 針對選取之訂閱類型，選取要顯示的訂閱狀態。 例如，您可以選取只顯示有錯誤的訂閱。  
  
 **狀態**  
 每個訂閱的狀態，這是由快照集代理程式或散發代理程式的狀態所決定 (會顯示優先權較高的狀態)。  
  
 依預設，包含訂閱資訊的方格會依 **[狀態]** 資料行排序。 下列清單顯示可能的狀態值和值的排序順序 (例如，錯誤一律顯示在方格頂端)。  
  
-   錯誤  
  
-   即將過期/已過期 (僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   未初始化的訂閱 (僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本)  
  
-   正在重試失敗的命令  
  
-   正在同步處理  
  
-   未進行同步處理  
  
 當給定訂閱有一個以上的狀態時，排序順序也會決定要顯示哪一個值。 例如，若訂閱有錯誤而且即將過期，則 **[狀態]** 資料行會顯示 **[錯誤]**。  
  
 **[即將過期/已過期]** 和 **[未初始化的訂閱]** 狀態值均為警告。 顯示警告時，如果代理程式正在執行，則 [狀態]  資料行也會顯示。 例如，狀態可能是 **[執行中，即將過期/已過期]**。  
  
 唯有設定了臨界值時，才會顯示 **[即將過期/已過期]** 狀態值。 如需設定閾值的資訊，請參閱[在複寫監視器中設定閾值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **訂閱**  
 每一個訂閱的名稱，格式為： *SubscriberName: SubscriptionDatabaseName*。  
  
 **上次同步處理日期**  
 散發代理程式上次執行的時間。 如果正在進行同步處理，就會顯示 **[進行中]** 。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視訂閱的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
