---
title: "檢視訂閱的資訊並執行工作 (複寫監視器) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "訂閱 [SQL Server 複寫], 檢視資訊"
  - "訂閱 [SQL Server 複寫], 複寫監視器工作"
  - "檢視訂閱資訊"
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 檢視訂閱的資訊並執行工作 (複寫監視器)
  複寫監視器提供下列包含有訂閱資訊的索引標籤：  
  
-   **所有訂閱**  
  
     這個索引標籤會顯示有關選取之發行集的所有訂閱資訊。  
  
-   **訂閱監看清單**  
  
     這個索引標籤的用途，是要顯示有錯誤、警告或效能最差的發行者上，所有可用之發行集的訂閱相關資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的散發者不會顯示這個索引標籤。  
  
 如需有關每個索引標籤上的選項的詳細資訊，請按一下右窗格中的索引標籤，然後按一下 [ **協助** 在功能表列上。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 若要在所有訂閱索引標籤中針對訂閱檢視資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視訂閱的相關資訊，請按一下 [ **所有訂閱** ] 索引標籤。 若要檢視這些訂用帳戶中指定的狀態，例如同步處理，請選取從選項 **顯示** 下拉式清單。  
  
3.  若要檢視及修改訂閱屬性，以滑鼠右鍵按一下訂閱，以及 [ **屬性**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
### 若要在訂閱監看清單索引標籤中針對訂閱檢視資訊並執行工作  
  
1.  在左窗格中展開發行者群組，然後按一下發行者。  
  
2.  若要檢視有關訂閱的資訊，請按一下 **[訂閱監看清單]** 索引標籤。  
  
3.  選取要顯示的訂閱類型 **顯示 \< SubscriptionType> 訂閱** 下拉式清單。 若要檢視這些訂用帳戶中指定的狀態，例如同步處理，請選取從選項 **顯示** 下拉式清單。  
  
4.  若要檢視及修改訂閱屬性，以滑鼠右鍵按一下訂閱，以及 [ **屬性**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 另請參閱  
 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  