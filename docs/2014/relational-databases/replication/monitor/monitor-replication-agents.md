---
title: 監視複寫代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b176e84d15daa2471014ebf90a6a72a683cdc29a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107460"
---
# <a name="monitor-replication-agents"></a>監視複寫代理程式
  「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器」可全面檢視複寫活動，但也可以直接尋找特定代理程式的資訊。 下列清單包含每個代理程式、可以在複寫監視器上找到的索引標籤，以及到說明如何存取這些索引標籤之主題的連結：  
  
-   下列代理程式與複寫監視器中的發行集相關聯：  
  
    -   快照集代理程式  
  
    -   記錄讀取器代理程式  
  
    -   佇列讀取器代理程式  
  
     透過下列索引標籤，存取與這些代理程式相關聯的資訊和工作： **[代理程式]** (每個發行者和發行集都可使用) 和 **[警告]** (每個發行集都可使用)。 如需詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-publication-agents.md)。  
  
-   下列代理程式與複寫監視器中的訂閱相關聯：  
  
    -   散發代理程式  
  
    -   [合併代理程式]  
  
     透過下列索引標籤，存取與這些代理程式相關聯的資訊和工作： **[訂閱監看清單]** (每個發行者皆可用) 或者 **[所有訂閱]** 索引標籤 (每個發行者皆可用)。 如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>使用 SQL Server Management Studio 監視複寫代理程式  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 提供下列用於監視複寫代理程式的對話方塊：  
  
-   **[檢視快照集代理程式的狀態]** (針對所有發行集)  
  
-   **[檢視記錄讀取器代理程式的狀態]** (針對所有交易式發行集)  
  
-   **[檢視同步處理的狀態]** (針對所有訂閱；此對話方塊允許存取「散發代理程式」與「合併代理程式」)  
  
 「複寫監視器」提供每個代理程式的其他資訊，並提供對「佇列讀取器代理程式」的監視(如果使用的話)。 如需詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-publication-agents.md)、[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-publication-agents.md) 和[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-subscription-agents.md)。  
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>若要監視快照集代理程式和記錄讀取器代理程式  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下發行集，然後按一下 **[檢視記錄讀取器代理程式的狀態]** 或 **[檢視快照集代理程式的狀態]**。  
  
4.  在 **[檢視記錄讀取器代理程式的狀態]** 或 **[檢視快照集代理程式的狀態]** 對話方塊中：  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   按一下 **[監視器]** 以啟動 **[複寫監視器]**。  
  
5.  按一下 [ **關閉**]。  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>若要監視散發代理程式與合併代理程式 (從發行者)  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開要監視之訂閱的發行集。  
  
4.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視同步處理的狀態]**。  
  
5.  在 **[檢視同步處理的狀態]** 對話方塊：  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   對於發送訂閱，按一下 **[監視器]** 以啟動 **[複寫監視器]**。  
  
    -   對於提取訂閱，按一下 **[檢視作業記錄]** 以啟動 **[記錄檔檢視器]**，該檢視器會顯示代理程式記錄的輸出。  
  
6.  按一下 [ **關閉**]。  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>若要監視散發代理程式與合併代理程式 (從訂閱者)  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要監視的訂閱，然後按一下 **[檢視同步處理的狀態]**。  
  
4.  在 **[檢視同步處理的狀態]** 對話方塊：  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   按一下 **[檢視作業記錄]** 以啟動 **[記錄檔檢視器]**，該檢視器會顯示代理程式記錄的輸出。  
  
5.  按一下 [ **關閉**]。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../monitoring-replication.md)   
 [複寫代理程式概觀](../agents/replication-agents-overview.md)  
  
  
