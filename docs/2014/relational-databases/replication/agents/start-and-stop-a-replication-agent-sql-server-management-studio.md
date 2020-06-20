---
title: 啟動及停止複寫代理程式 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b9074ab3ac56f3457f4ab5ffb877e63a66a1c783
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068704"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>啟動及停止複寫代理程式 (SQL Server Management Studio)
  從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [作業]**** 資料夾和 [複寫]**** 資料夾，以及從複寫監視器啟動及停止代理程式。 啟動和停止下列代理程式和作業：  
  
-   所有發行集所使用的快照集代理程式。  
  
-   所有交易式發行集所使用的記錄讀取器代理程式。  
  
-   針對佇列更新訂閱啟用之交易式發行集所使用的佇列讀取器代理程式。  
  
-   散發代理程式，同步處理交易式和快照式發行集的訂閱。  
  
-   合併代理程式，同步處理合併式發行集的訂閱。  
  
-   複寫維護作業。  
  
 如需啟動合併代理程式和散發代理程式的詳細資訊，請參閱[同步處理發送訂閱](../synchronize-a-push-subscription.md)和[同步處理提取訂閱](../synchronize-a-pull-subscription.md)。 如需維護作業的詳細資訊，請參閱[執行複寫維護作業 &#40;SQL Server Management Studio&#41;](../../../ssms/sql-server-management-studio-ssms.md)。  
  
 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../monitor/start-the-replication-monitor.md)。  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>若要從 Management Studio 啟動和停止快照集代理程式或記錄讀取器代理程式  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的「發行者」，然後展開伺服器節點和 **[複寫]** 資料夾。  
  
2.  展開 **[本機發行集]** 資料夾，然後以滑鼠右鍵按一下發行集。  
  
3.  按一下 **[檢視快照集代理程式的狀態]** 或 **[檢視記錄讀取器代理程式的狀態]**。  
  
4.  按一下 **[啟動]** 或 **[停止]**。  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>若要從 Management Studio 啟動和停止「佇列讀取器代理程式」  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下代理程式的作業，再按一下 **[啟動作業]** 或 **[停止作業]**。 佇列讀取器代理程式的作業名稱格式為 **[ \<Distributor> ]. \<integer> **。  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>若要從「複寫監視器」啟動和停止「快照集代理程式」、「記錄讀取器代理程式」或「佇列讀取器代理程式」  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  以滑鼠右鍵按一下代理程式，然後按一下 **[啟動代理程式]** 或 **[停止代理程式]**。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../monitoring-replication.md)   
 [複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)   
 [複寫代理程式概觀](replication-agents-overview.md)  
  
  
