---
title: "檢視發行者的資訊並執行工作 (複寫監視器) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Publishers [SQL Server replication], Replication Monitor tasks
- viewing Publisher information
- Publishers [SQL Server replication], viewing information
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad1d0890185e7e9e8066885057742870f48b1acc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="view-information-and-perform-tasks-for-a-publisher-replication-monitor"></a>檢視發行者的資訊並執行工作 (複寫監視器)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 複寫監視器提供下列顯示所選取「發行者」之資訊的索引標籤：  
  
-   **[發行集]**  
  
     此索引標籤會顯示所選取「發行者」端所有發行集的資訊。  
  
-   **訂閱監看清單**  
  
     這個索引標籤的用途，是要顯示有錯誤、警告或效能最差的發行者上，所有可用之發行集的訂閱相關資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的散發者不會顯示這個索引標籤。  
  
-   **[代理程式]** 索引標籤  
  
     此索引標籤會顯示有關所有複寫類型使用之代理程式和工作的詳細資訊。 您也可以用這個索引標籤來啟動和停止每個代理程式和工作。  
  
 若要檢視每一索引標籤上選項的詳細資訊，請按一下右窗格中的索引標籤，然後按一下功能表列上的 **[說明]** 。 如需啟動複寫監視器的資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-a-publisher"></a>若要檢視發行者的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，然後按一下發行者。  
  
2.  若要檢視所有發行集的資訊，請按一下 **[發行集]** 索引標籤。  
  
3.  若要檢視有關訂閱的資訊，請按一下 **[訂閱監看清單]** 索引標籤。也可以從此索引標籤存取詳細資訊，並執行工作：  
  
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。  
  
    -   若要檢視訂閱的屬性，請以滑鼠右鍵按一下訂閱，再按一下 **[屬性]**。  
  
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。  
  
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]**。  
  
4.  若要檢視有關代理程式的詳細資訊，請按一下 **[代理程式]** 索引標籤。您也可以在這個索引標籤上存取更詳細的資訊及執行工作：  
  
    -   若要檢視代理程式的資訊 (例如提示訊息及任何錯誤訊息)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[檢視詳細資料]**。  
  
    -   若要檢視執行代理程式之作業的詳細資訊 (諸如排程、作業步驟詳細資料等)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[屬性]**。  
  
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]**。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
    -   若要啟動尚未執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[啟動代理程式]**。  
  
    -   若要停止正在執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[停止代理程式]**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
