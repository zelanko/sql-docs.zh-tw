---
title: 在複寫監視器中重新整理資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c63d6b2f113ba5d9f3d3d2cfed201f9a6535b74f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915130"
---
# <a name="refresh-data-in-replication-monitor"></a>在複寫監視器中重新整理資料
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  在「複寫監視器」中，主視窗與詳細資料視窗 (這些視窗可從主視窗中啟動) 可自動或手動重新整理。 若要手動重新整理視窗，請按 F5。 依預設，主視窗將每隔五秒鐘自動重新整理；可以為每個「發行者」自訂重新整理速率。  
  
 在「複寫監視器」中顯示的資料可以透過快取查詢；如需快取與重新整理「複寫監視器」之間的關聯性，請參閱[快取、重新整理和複寫監視器效能](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>若要為複寫監視器設定重新整理選項
  
1.  以滑鼠右鍵按一下「複寫監視器」左窗格中的「發行者」，然後按一下 **[發行者設定]** 。  
  
2.  在 **[發行者設定]** 對話方塊中，設定 **[自動重新整理]** 與 **[重新整理的速率]** 選項。 **[自動重新整理]** 設定會影響「複寫監視器」中的主視窗。 **[重新整理的速率]** 設定也可以影響所有設定為自動重新整理的詳細資料視窗 (設定的變更僅影響在變更後開啟的詳細資料視窗)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>若要指定詳細資料視窗應自動重新整理  
  
1.  在「複寫監視器」中開啟詳細資料視窗。 例如：  
  
    1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
    2.  按一下 **[所有訂閱]** 索引標籤。  
  
    3.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]** 。  
  
2.  在 [訂閱 \<SubscriptionName>] 詳細資料視窗中，按一下 [動作]，然後按一下 [自動重新整理]。 重新整理速率將由 **[發行者設定]** 對話方塊中的 **[重新整理的速率]** 設定決定。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
