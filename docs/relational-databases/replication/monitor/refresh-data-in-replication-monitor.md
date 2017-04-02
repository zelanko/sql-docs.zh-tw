---
title: "在複寫監視器中重新整理資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "重新整理資料"
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 在複寫監視器中重新整理資料
  在「複寫監視器」中，主視窗與詳細資料視窗 (這些視窗可從主視窗中啟動) 可自動或手動重新整理。 若要手動重新整理視窗，請按 F5。 依預設，主視窗將每隔五秒鐘自動重新整理；可以為每個「發行者」自訂重新整理速率。  
  
 複寫監視器中顯示的資料會查詢從快取。快取和重新整理複寫監視器之間的關聯性的相關資訊，請參閱 [快取、 重新整理和複寫監視效能](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 若要為複寫監視器設定重新整理選項  
  
1.  以滑鼠右鍵按一下複寫監視器的左窗格中的發行者，然後按一下 **發行者設定**。  
  
2.  在 **發行者設定** ] 對話方塊中，將 **自動重新整理** 和 **重新整理的頻率** 選項。  **自動重新整理** 設定會影響複寫監視器 」 中的主視窗。  **重新整理的頻率** 設定也會影響任何設定為自動重新整理的詳細資料視窗 （設定的變更只會影響在變更後開啟詳細資料視窗）。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 若要指定詳細資料視窗應自動重新整理  
  
1.  在「複寫監視器」中開啟詳細資料視窗。 例如：  
  
    1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
    2.  按一下 **[所有訂閱]** 索引標籤。  
  
    3.  訂閱中，按一下滑鼠右鍵，然後按一下 **檢視詳細資料**。  
  
2.  在 **訂閱 \< SubscriptionName>** 詳細資料視窗中，按一下 **動作**, ，然後按一下 [ **自動重新整理**。 重新整理的頻率由 **重新整理的頻率** 中設定 **發行者設定** 對話方塊。  
  
## 另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  