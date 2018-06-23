---
title: 檢視資訊並執行 a Publication (Replication Monitor) 相關聯的代理程式工作 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 38
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2a82df3ae01b49d8ad7c8b48c5a07d6f57d2dbe8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022854"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-publication-replication-monitor"></a>檢視與發行集相關聯之代理程式的資訊並執行工作 (複寫監視器)
  複寫監視器提供 **[代理程式]** 索引標籤，其中包含與選取的發行集相關聯之代理程式的資訊。 散發代理程式和合併代理程式與訂閱建立關聯；如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 這個索引標籤會顯示下列代理程式的相關資訊：  
  
-   所有發行集所使用的快照集代理程式。  
  
-   所有交易式發行集所使用的記錄讀取器代理程式。  
  
-   針對佇列更新訂閱啟用之交易式發行集所使用的佇列讀取器代理程式。  
  
 若要檢視有關這個索引標籤之選項的詳細資訊，請按一下功能表列上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>若要檢視與發行集相關聯之代理程式的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視代理程式的相關資訊，請按一下 **[代理程式]** 索引標籤。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：  
  
    -   若要檢視代理程式的資訊 (例如提示訊息及任何錯誤訊息)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[檢視詳細資料]**。  
  
    -   若要檢視執行代理程式之作業的詳細資訊 (諸如排程、作業步驟詳細資料等)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[屬性]**。  
  
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]**。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../agents/replication-agent-profiles.md)。  
  
    -   若要啟動尚未執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[啟動代理程式]**。  
  
    -   若要停止正在執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[停止代理程式]**。  
  
## <a name="see-also"></a>另請參閱  
 [在複寫監視器中設定閾值和警告](set-thresholds-and-warnings-in-replication-monitor.md)   
 [檢視發行集的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [複寫代理程式管理](../agents/replication-agent-administration.md)   
 [監視複寫](../monitoring-replication.md)  
  
  