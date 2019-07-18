---
title: 發行者資訊，發行集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: deb1f9af6d006ff9e524d2f91d61af6269737079
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62752775"
---
# <a name="publisher-information-publications"></a>發行者資訊，發行集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[發行集]** 索引標籤可以提供在左窗格中所選取發行者之所有發行集的摘要資訊。  
  
## <a name="options"></a>選項。  
 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 [排序資料行]  對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及這些資料行在 [選擇資料行]  對話方塊中的顯示順序。  
  
-   **篩選**：根據 [篩選設定]  對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **狀態**  
 每一個發行集的狀態，由訂閱的最高優先權狀態來決定。 依預設，包含發行集資訊的方格會依 **[狀態]** 資料行排序。 下列清單會顯示可能的狀態值，以及值的排序順序 (例如，錯誤會一律顯示在方格頂端)：  
  
-   錯誤  
  
-   效能嚴重不足  
  
-   正在重試失敗的命令  
  
-   [確定]  
  
 **[效能嚴重不足]** 狀態值與交易式訂閱和合併訂閱有關；對交易式訂閱而言，唯有已設定臨界值時，才會顯示此狀態值。 如需效能測量和設定閾值的資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)和[在複寫監視器中設定閾值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **發行集**  
 每個發行集的名稱，格式為 *PublicationDatabaseName:PublicationName*。  
  
 **訂閱**  
 每一個發行集的訂閱數目。  
  
 **正在同步處理**  
 目前正在進行同步處理之每一個發行集的訂閱數目：  
  
-   對異動複寫而言，「正在同步處理」表示散發代理程式正在執行，但不一定正在複寫資料。  
  
-   對合併式複寫而言，「正在同步處理」表示全併代理程式正在執行，且目前正在複寫資料。  
  
-   對快照式複寫而言，「正在同步處理」表示散發代理程式正在執行，且目前正在複寫資料。  
  
 **目前的平均效能** 和 **目前最差效能**  
 僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 分別代表發行集之所有訂閱的平均效能評比和最差效能評比。 評比是以複寫監視器最近使用的度量單位為基礎，並不反映訂閱經過一段時間的效能。  
  
 對異動複寫而言，複寫監視器只會顯示已定義效能臨界值之發行集的值。 如果發行集未定義效能臨界值，則此資料行會顯示 **[未啟用]** 。 對合併式複寫而言，在相同連接類型 (撥號或 LAN) 上發生過五次同步處理，且每次同步處理都具有 50 或更多個變更之後，複寫監視器才會顯示值。 如果具有 50 或更多個變更的同步處理少於五次，或者最近的同步處理少於 50 個變更，則此資料行為空白。  
  
 效能評比是下列其中一個值：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
-   嚴重  
  
 如需如何定義效能評比和如何設定效能閾值的詳細資訊，請參閱[使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視發行者的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
