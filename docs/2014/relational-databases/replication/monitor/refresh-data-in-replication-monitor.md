---
title: 在複寫監視器中重新整理資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d632da029905c4ce914c843a2ea1319e780ac735
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060767"
---
# <a name="refresh-data-in-replication-monitor"></a>在複寫監視器中重新整理資料
  在「複寫監視器」中，主視窗與詳細資料視窗 (這些視窗可從主視窗中啟動) 可自動或手動重新整理。 若要手動重新整理視窗，請按 F5。 依預設，主視窗將每隔五秒鐘自動重新整理；可以為每個「發行者」自訂重新整理速率。  
  
 在「複寫監視器」中顯示的資料可以透過快取查詢；如需快取與重新整理「複寫監視器」之間的關聯性，請參閱[快取、重新整理和複寫監視器效能](caching-refresh-and-replication-monitor-performance.md)。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](start-the-replication-monitor.md)。  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>若要為複寫監視器設定重新整理選項  
  
1.  以滑鼠右鍵按一下「複寫監視器」左窗格中的「發行者」，然後按一下 **[發行者設定]** 。  
  
2.  在 **[發行者設定]** 對話方塊中，設定 **[自動重新整理]** 與 **[重新整理的速率]** 選項。 **[自動重新整理]** 設定會影響「複寫監視器」中的主視窗。 **[重新整理的速率]** 設定也可以影響所有設定為自動重新整理的詳細資料視窗 (設定的變更僅影響在變更後開啟的詳細資料視窗)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>若要指定詳細資料視窗應自動重新整理  
  
1.  在「複寫監視器」中開啟詳細資料視窗。 例如：  
  
    1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
    2.  按一下 **[所有訂閱]** 索引標籤。  
  
    3.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]** 。  
  
2.  在 [**訂閱 \<SubscriptionName> **詳細資料] 視窗中，按一下 [**動作**]，然後按一下 [**自動**重新整理]。 重新整理速率將由 **[發行者設定]** 對話方塊中的 **[重新整理的速率]** 設定決定。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../monitoring-replication.md)  
  
  
