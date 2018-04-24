---
title: 檢視訂閱的資訊並執行工作 (複寫監視器) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], viewing information
- subscriptions [SQL Server replication], Replication Monitor tasks
- viewing subscription information
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 214901cd0160c4df35e0f0e92560977d4bd1780d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="view-information-and-perform-tasks-for-a-subscription-replication-monitor"></a>檢視訂閱的資訊並執行工作 (複寫監視器)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫監視器提供下列包含有訂閱資訊的索引標籤：  
  
-   **所有訂閱**  
  
     這個索引標籤會顯示有關選取之發行集的所有訂閱資訊。  
  
-   **訂閱監看清單**  
  
     這個索引標籤的用途，是要顯示有錯誤、警告或效能最差的發行者上，所有可用之發行集的訂閱相關資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的散發者不會顯示這個索引標籤。  
  
 如需有關各索引標籤選項的資訊，請按一下右窗格的索引標籤，然後按一下功能表上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-all-subscriptions-tab"></a>若要在所有訂閱索引標籤中針對訂閱檢視資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視有關訂閱的資訊，請按一下 **[所有訂閱]** 索引標籤。若只要檢視給定狀態中的訂閱，如同步處理，請從 **[顯示]** 下拉式清單中選取某選項。  
  
3.  若要檢視和修改訂閱屬性，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>若要在訂閱監看清單索引標籤中針對訂閱檢視資訊並執行工作  
  
1.  在左窗格中展開發行者群組，然後按一下發行者。  
  
2.  若要檢視有關訂閱的資訊，請按一下 **[訂閱監看清單]** 索引標籤。  
  
3.  從 [顯示 \<訂閱類型> 訂閱] 下拉式清單中選取要顯示的訂閱類型。 若只要檢視給定狀態中的訂閱，如同步處理，請從 **[顯示]** 下拉式清單中選取某選項。  
  
4.  若要檢視和修改訂閱屬性，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發送訂閱屬性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
