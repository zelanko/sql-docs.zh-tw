---
title: 檢視訂閱代理程式的資訊並執行工作 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0f0770d113a78eb3fe9df5cb8d9ad54d719aecd
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353060"
---
# <a name="view-information-and-perform-tasks-for-subscription-agents"></a>檢視訂閱代理程式的資訊並執行工作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「複寫監視器」提供了兩種索引標籤，可讓您存取與訂閱相關聯的代理程式之資訊：  
  
-   **所有訂閱**  
  
     這個索引標籤會顯示有關選取之發行集的所有訂閱資訊。  
  
-   **訂閱監看清單**  
  
     這個索引標籤的用途，是要顯示有錯誤、警告或效能最差的發行者上，所有可用之發行集的訂閱相關資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的散發者不會顯示這個索引標籤。  
  
 如需有關各索引標籤選項的資訊，請按一下右窗格的索引標籤，然後按一下功能表上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>若要檢視與訂閱相關聯之代理程式的資訊並執行工作 (所有訂閱索引標籤)  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤以檢視有關訂閱的資訊。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：  
  
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。 詳細的資訊包括：代理程式記錄與錯誤訊息；異動複寫的效能統計資料；以及合併式複寫的發行項層級同步處理統計資料。  
  
         在詳細資料視窗中啟動的索引標籤視訂閱類型而定：對於快照式訂閱，此索引標籤為 **[散發者到訂閱者記錄]**；對於交易式訂閱，此索引標籤為 **[發行者到散發者記錄]**、 **[散發者到訂閱者記錄]** 以及 **[未散發的命令]**；對於合併式訂閱，此索引標籤為 **[同步處理記錄]**。  
  
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。  
  
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]**。  
  
    -   若要驗證單一合併訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[驗證訂閱]**。 若要驗證合併發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證所有訂閱]**；若要驗證交易式發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證訂閱]**。  
  
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]**。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>若要檢視與訂閱相關聯之代理程式的資訊並執行工作 (訂閱監看清單索引標籤)  
  
1.  在左窗格中展開發行者群組，然後按一下發行者。  
  
2.  按一下 **[訂閱監看清單]** 索引標籤以檢視有關訂閱的資訊。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：  
  
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。 詳細的資訊包括：代理程式記錄與錯誤訊息；異動複寫的效能統計資料；以及合併式複寫的發行項層級同步處理統計資料。  
  
         在詳細資料視窗中啟動的索引標籤視訂閱類型而定：對於快照式訂閱，此索引標籤為 **[散發者到訂閱者記錄]**；對於交易式訂閱，此索引標籤為 **[發行者到散發者記錄]**、 **[散發者到訂閱者記錄]** 以及 **[效能]**；對於合併式訂閱，此索引標籤為 **[同步處理記錄]**。  
  
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。  
  
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]**。  
  
    -   若要驗證單一合併訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[驗證訂閱]**。 若要驗證合併發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證所有訂閱]**；若要驗證交易式發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證訂閱]**。  
  
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]**。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視訂閱的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
