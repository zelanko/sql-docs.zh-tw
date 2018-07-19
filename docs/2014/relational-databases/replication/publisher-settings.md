---
title: 發行者設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abcedc479df197258b9ad836a3dd62430fb1c69b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301838"
---
# <a name="publisher-settings"></a>發行者設定
  **[發行者設定]** 對話方塊，可讓您針對已加入至複寫監視器之左窗格的發行者變更設定。  
  
## <a name="options"></a>選項。  
 **發行者連接**  
 按一下即可啟動 **[連接到伺服器]** 對話方塊，可讓您檢視和變更連接屬性以及複寫監視器用來連接到發行者的認證。  
  
 **散發者連接**  
 只有在發行者使用遠端散發者時才會顯示此選項。 按一下即可啟動 **[連接到伺服器]** 對話方塊，可讓您檢視和變更連接屬性以及複寫監視器用來連接到遠端散發者的認證。  
  
 **啟動複寫監視器時自動連接**  
 選取即可讓複寫監視器自動連接到散發者，並擷取在對話方塊頂端方格中選取之發行者的狀態資訊。 如果清除此核取方塊，您必須在啟動複寫監視器後手動連接：以滑鼠右鍵按一下複寫監視器之左窗格中的發行者，然後按一下 **[連接]**。  
  
 **自動重新整理此發行者和其發行集的狀態**  
 選取即可讓複寫監視器自動重新整理在對話方塊頂端方格中選取之發行者的狀態。 如果選取此選項，複寫監視器就會輪詢散發者，以取得發行者和其發行集的狀態資訊。 輪詢間隔會由 **[重新整理的頻率]** 選項設定。 如需複寫監視器中之重新整理的詳細資訊，請參閱[快取、重新整理和複寫監視器效能](monitor/caching-refresh-and-replication-monitor-performance.md)。  
  
 **[重新整理的頻率]**  
 輸入一個值 (以秒為單位)，來指定複寫監視器應輪詢散發者以取得狀態的頻率。 較低的值會產生較頻繁的輪詢，如果您監視大量的發行者，這會影響散發者端的效能。 建議您測試自己的系統，以決定適當的值。 如果您在複寫監視器的任何一個詳細資料視窗中選取 **[自動重新整理]** ，也會使用 **[重新整理的頻率]** 設定。  
  
 **在下列群組中顯示此發行者**  
 從清單中選取一個發行者群組。 發行者會在左窗格中的這個群組之下顯示。 群組提供組織發行者的一種方式，對於複寫的運作方式沒有影響。  
  
 **新增群組**  
 按一下即可建立新的發行者群組。 發行者群組提供在複寫監視器內組織發行者的一種便利方式。 群組不會影響資料的複寫，也不會影響複寫拓撲中各伺服器間的關聯性。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)  
  
  
