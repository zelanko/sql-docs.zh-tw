---
title: 檢視發行集的資訊並執行工作 (複寫監視器) | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 283310364d5ea984960878fd675f9333e7c37a74
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307398"
---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>檢視發行集的資訊並執行工作 (複寫監視器)
  「複寫監視器」提供下列包含所選取發行集之資訊的索引標籤：  
  
-   **所有訂閱**  
  
     這個索引標籤會顯示有關選取之發行集的所有訂閱資訊。  
  
-   **代理程式**  
  
     此索引標籤會顯示複寫所使用之所有代理程式的相關資訊：  
  
    -   所有發行集所使用的快照集代理程式。  
  
    -   所有交易式發行集所使用的記錄讀取器代理程式。  
  
    -   「佇列讀取器代理程式」，由已佇列更新訂閱的交易式發行集使用。  
  
-   **警告** (針對執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新版本的「散發者」)  
  
    -   這個索引標籤可用來為代理程式指定警告和警示。  
  
-   **[追蹤 Token]** (對於執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新版本的「散發者」，僅限於異動複寫)。  
  
     這個索引標籤能讓您測量延遲，在發行者端所認可之交易與在訂閱者端所認可之對應交易之間經過的時間。  
  
 如需有關各索引標籤選項的資訊，請按一下右窗格的索引標籤，然後按一下功能表上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>若要檢視發行集的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視並修改發行集屬性，請以滑鼠右鍵按一下發行集，然後按一下 **[屬性]**。  
  
3.  若要檢視有關訂閱的資訊，請按一下 **[所有訂閱]** 索引標籤。  
  
     若要檢視和修改訂閱屬性，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-subscription-agents.md)。  
  
4.  若要檢視有關代理程式的詳細資訊，請按一下 **[代理程式]** 索引標籤。您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。如需詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-publication-agents.md)。  
  
5.  若要檢視有關代理程式警告與臨界值的詳細資訊，請按一下 **[警告]** 索引標籤。如需詳細資訊，請參閱＜ [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)＞。  
  
6.  若要檢視追蹤 Token 的資訊，請按一下 **[追蹤 Token]** 索引標籤。如需如何使用追蹤 Token 的詳細資訊，請參閱＜ [針對異動複寫測量延遲及驗證連接](measure-latency-and-validate-connections-for-transactional-replication.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../publish/view-and-modify-publication-properties.md)   
 [監視複寫](../monitoring-replication.md)  
  
  
