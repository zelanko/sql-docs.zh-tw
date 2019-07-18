---
title: 執行複寫維護作業 (SQL Server Management Studio) | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f294ad3868670783d3010498dd0ba89e1e6a48be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127058"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>執行複寫維護作業 (SQL Server Management Studio)
  複寫會使用下列維護作業：  
  
-   **重新初始化具有資料驗證失敗的訂閱**
-   **代理程式記錄清除：散發**
-   **散發的複寫監視重新整理器。**
-   **檢查複寫代理程式**
-   **散發清除：散發**
-   **清除已過期的訂閱**  
  
 請從  中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from the **Agents** tab in Replication Monitor. 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../monitor/start-the-replication-monitor.md)。 在 [作業屬性 - \<作業>]  對話方塊中檢視及修改各作業的屬性，該對話方塊位於相同的資料夾和索引標籤中。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>在 Management Studio 中啟動或停止複寫維護作業  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下作業，然後按一下 **[啟動作業]** 或 **[停止作業]** 。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>在複寫監視器中啟動或停止複寫維護作業  
  
1.  在複寫監視器中展開發行者群組，然後選取發行者。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  以滑鼠右鍵按一下方格中的作業，然後按一下 **[啟動作業]** 或 **[停止作業]** 。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>在 Management Studio 中檢視及修改複寫維護作業的屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下作業，然後按一下 **[屬性]** 。  
  
4.  在 [作業屬性 - \<作業>]  對話方塊中，視需要修改任何屬性，然後按一下 [確定]  。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>在複寫監視器中檢視及修改複寫維護作業的屬性  
  
1.  在複寫監視器中展開發行者群組，然後選取發行者。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  以滑鼠右鍵按一下方格中的作業，再按一下 **[屬性]** 。  
  
4.  在 [作業屬性 - \<作業>]  對話方塊中，視需要修改任何屬性，然後按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [使用複寫監視器來檢視資訊及執行工作](../monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [複寫代理程式管理](../agents/replication-agent-administration.md)  
  
  
