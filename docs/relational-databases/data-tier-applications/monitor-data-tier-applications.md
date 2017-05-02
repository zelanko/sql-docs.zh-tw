---
title: "監視資料層應用程式 |Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f7949096021314093ef63877175ceddf77e4cf0e
ms.lasthandoff: 04/11/2017

---
# <a name="monitor-data-tier-applications"></a>監視資料層應用程式
  您可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中的 [公用程式總管]**** 與 [物件總管]**** 以及系統檢視表和資料表中監視資料層應用程式 (DAC)。 此外，包含在 DAC 中之資料庫內的所有物件都可以使用標準資料庫與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 監視技術進行監視。  
  
## <a name="before-you-begin"></a>開始之前  
 若您將 DAC 部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的受管理執行個體，下次從執行個體將公用程式收集組傳送到公用程式控制點時，部署 DAC 的相關資訊就會合併至 SQL Server 公用程式。 然後，您可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **[公用程式總管]**，檢視 DAC 的基本健全狀況資訊。  
  
 SSMS 的 **[物件總管]** 會顯示部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體之每個 DAC 的基本組態資訊，而不論是否在 SQL Server 公用程式中管理執行個體。 而且，可以使用監視任何資料庫的相同程序，來監視與部署 DAC 相關聯的資料庫。  
  
## <a name="using-the-sql-server-utility"></a>使用 SQL Server 公用程式  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 公用程式總管****中的 [部署的資料層應用程式]**** 詳細資料頁面會顯示一個儀表板，這個儀表板會報告已部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之受管理執行個體的所有 DAC 資源使用情況。 詳細資料頁面的上方窗格會列出每個已部署的 DAC 以及視覺指標，顯示其 CPU 的使用量與檔案資源是否超出針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所定義的原則之外。 如果您選取清單檢視中的任何 DAC，在頁面下方窗格的索引標籤中會顯示其他詳細資料。 如需詳細資料頁面上所呈現之資訊的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
 使用 [部署的資料層應用程式]**** 詳細資料頁面快速識別使用不足或其硬體資源負荷過重的 DAC 之後，您可以做出處理所有問題的計畫。 未充分使用其目前硬體資源的多個 DAC 可以合併到單一伺服器，釋出部分伺服器做為其他用途使用。 如果 DAC 在目前伺服器上的資源負荷過重，可以將 DAC 移到更大的伺服器，或者將額外的資源加入至目前的伺服器。  
  
 資源使用量的上下限是由 **[公用程式管理]** 詳細資料頁面中所定義的應用程式監視原則定義的。 資料庫管理員可以量身訂作這些原則，以符合其組織所設立的限制。 例如，某家公司可能會設定 75% 做為 DAC 的 CPU 使用量上限，而另一家公司則可能將上限設定為 80%。 如需有關設定應用程式監視原則的詳細資訊，請參閱[公用程式管理 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)。  
  
 若要檢視 [部署的資料層應用程式]**** 詳細資料頁面：  
  
1.  選取 [檢視/公用程式總管]**** 功能表。  
  
2.  將 [公用程式總管]**** 連接至公用程式控制點 (UCP)。  
  
3.  選取 [檢視/公用程式總管詳細資料]**** 功能表。  
  
4.  選取 [公用程式總管]**** 中的 [部署的資料層應用程式]**** 節點。  
  
 [部署的資料層應用程式]**** 詳細資料頁面中的資訊來自公用程式管理資料倉儲中的資料，此資料倉儲預設每 15 分鐘收集資料一次。 其間隔可以使用 **[公用程式管理]** 詳細資料頁面自訂。  
  
## <a name="using-object-explorer"></a>使用物件總管  
 SSMS 的 **[物件總管]** 會顯示有關部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體之每個 DAC 的基本組態資訊。 這同時包括已經在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中註冊的受管理的執行個體，以及無法在 [公用程式總管]**** 中檢視的獨立執行個體。  
  
 若要檢視部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體之 DAC 的詳細資料：  
  
1.  選取 [檢視/物件總管]**** 功能表。  
  
2.  從 [物件總管] 窗格連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
3.  選取 [檢視/物件總管詳細資料]**** 功能表。  
  
4.  在 [物件總管]**** 中，選取對應至執行個體的伺服器節點，然後導覽至 [管理\資料層應用程式]**** 節點。  
  
5.  在詳細資料頁面上方窗格中的清單檢視會列出部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的每個 DAC。 選取 DAC 以便在頁面底部的詳細資料窗格中顯示資訊。  
  
 [資料層應用程式]**** 節點的滑鼠右鍵功能表也會用來部署新的 DAC 或刪除現有的 DAC。  
  
## <a name="using-the-dac-system-views-and-tables"></a>使用 DAC 系統檢視表與資料表  
 msdb.dbo.sysdac_history_internal 系統資料表會記錄針對 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體執行的所有 DAC 管理動作成功或失敗。 資料表會記錄每個動作發生的時間，以及起始動作的登入。 如需詳細資訊，請參閱 [sysdac_history_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal.md)。  
  
 DAC 系統檢視表會報告基本目錄資訊。 如需詳細資訊，請參閱[資料層應用程式檢視表 &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)。  
  
## <a name="monitoring-dac-databases"></a>監視 DAC 資料庫  
 成功部署 DAC 之後，包含在 DAC 中的資料庫會與其他任何資料庫的運作方式相同。 使用標準 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 技術與工具來監視資料庫的效能、記錄、事件與資源使用情況。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [部署資料層應用程式](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  
