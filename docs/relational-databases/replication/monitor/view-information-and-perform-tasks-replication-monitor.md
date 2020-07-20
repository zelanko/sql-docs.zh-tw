---
title: 檢視資訊與執行工作 (複寫監視器)
description: 了解如何在 SQL Server Management Studio (SSMS) 中使用複寫監視器來檢視資訊及執行各種工作。
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: be851d2ff0919125699a4e33c4b4d1d6445c0fc6
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159626"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>使用複寫監視器來檢視資訊及執行工作
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
複寫監視器提供一些索引標籤和選項，來檢視資訊及執行各種工作。 本文說明使用「複寫監視器」時，可以檢視和完成的各種不同項目。 


## <a name="for-a-publication"></a>針對發行集

### <a name="view-information"></a>檢視資訊
「複寫監視器」提供下列包含所選取發行集之資訊的索引標籤：  
  
-   **所有訂閱** - 此索引標籤會顯示與所選發行集的所有訂閱相關的資訊。  
  
-   **代理程式** - 此索引標籤會顯示與發行集所使用的所有代理程式相關的資訊：   
    -   所有發行集所使用的快照集代理程式。   
    -   所有交易式發行集所使用的記錄讀取器代理程式。   
    -   「佇列讀取器代理程式」，由已佇列更新訂閱的交易式發行集使用。  
  
-   **警告** - 此索引標籤可讓您為代理程式指定警告和警示。  
  
-   **追蹤 Token** - (僅限異動複寫) 此索引標籤可讓您測量延遲，亦即「發行者」端所認可之交易與「訂閱者」端所認可之對應交易之間經過的時間。  
  
 如需有關每個索引標籤上選項的詳細資訊，請在右窗格中選取索引標籤，然後選取功能表列上的 [說明]。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="perform-tasks"></a>執行工作
  
1.  在左窗格中依序展開某個「發行者」群組和「發行者」，然後選取發行集。   
2.  若要檢視及修改發行集屬性，請在發行集上按一下滑鼠右鍵，然後選取 [屬性]。    
3.  若要檢視有關訂閱的資訊，請選取 [所有訂閱] 索引標籤，在訂閱上按一下滑鼠右鍵，然後選取 [屬性]。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 
4.  若要檢視有關代理程式的資訊，請選取 [代理程式] 索引標籤。您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 
5.  若要檢視有關代理程式警告和閾值的資訊，請選取 [警告] 索引標籤。如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
6.  若要檢視有關追蹤 Token 的資訊，請選取 [追蹤 Token] 索引標籤。如需如何使用追蹤 Token 的詳細資訊，請參閱＜ [針對異動複寫測量延遲及驗證連接](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)＞。  
  
## <a name="for-a-publisher"></a>針對發行者 

### <a name="view-information"></a>檢視資訊
「複寫監視器」提供下列顯示所選取「發行者」之資訊的索引標籤：   
-   **發行集** - 顯示與所選「發行者」的所有發行集相關的資訊。   
-   **訂閱監看清單** - 顯示與所選「發行者」之所有可用發行集內有錯誤、警告或效能最差的訂閱相關的資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前版本的散發者不會顯示這個索引標籤。    
-   **代理程式**索引標籤 - 顯示與所有複寫類型所使用的代理程式和作業相關的詳細資訊。 您也可以用這個索引標籤來啟動和停止每個代理程式和工作。 若要檢視每一索引標籤上選項的詳細資訊，請按一下右窗格中的索引標籤，然後按一下功能表列上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="perform-tasks"></a>執行工作
  
1.  在左窗格中展開發行者群組，然後按一下發行者。   
2.  若要檢視所有發行集的資訊，請按一下 **[發行集]** 索引標籤。    
3.  若要檢視有關訂閱的資訊，請按一下 **[訂閱監看清單]** 索引標籤。也可以從此索引標籤存取詳細資訊，並執行工作：   
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]** 。    
    -   若要檢視訂閱的屬性，請以滑鼠右鍵按一下訂閱，再按一下 **[屬性]** 。    
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]** 。   
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]** 。   
4.  若要檢視有關代理程式的詳細資訊，請按一下 **[代理程式]** 索引標籤。您也可以在這個索引標籤上存取更詳細的資訊及執行工作：    
    -   若要檢視代理程式的資訊 (例如提示訊息及任何錯誤訊息)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[檢視詳細資料]** 。  
    -   若要檢視執行代理程式之作業的詳細資訊 (諸如排程、作業步驟詳細資料等)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[屬性]** 。    
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]** 。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。    
    -   若要啟動尚未執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[啟動代理程式]** 。  
    -   若要停止正在執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[停止代理程式]** 。  


## <a name="for-a-subscription"></a>針對訂閱 

### <a name="view-information"></a>檢視資訊
  複寫監視器提供下列包含有訂閱資訊的索引標籤：    
-   **所有訂閱** - 顯示與所選發行集的所有訂閱相關的資訊。   
-   **訂閱監看清單** - 顯示與所選「發行者」之所有可用發行集內有錯誤、警告或效能最差的訂閱相關的資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前版本的散發者不會顯示這個索引標籤。 如需有關各索引標籤選項的資訊，請按一下右窗格的索引標籤，然後按一下功能表上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="perform-tasks"></a>執行工作
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。   
2.  若要檢視有關訂閱的資訊，請按一下 **[所有訂閱]** 索引標籤。若只要檢視給定狀態中的訂閱，如同步處理，請從 **[顯示]** 下拉式清單中選取某選項。    
3.  若要檢視和修改訂閱屬性，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]** 。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>若要在訂閱監看清單索引標籤中針對訂閱檢視資訊並執行工作  
  
1.  在左窗格中展開發行者群組，然後按一下發行者。    
2.  若要檢視有關訂閱的資訊，請按一下 **[訂閱監看清單]** 索引標籤。    
3.  從 [顯示 \<SubscriptionType> 訂閱] 下拉式清單中選取要顯示的訂閱類型。 若只要檢視給定狀態中的訂閱，如同步處理，請從 **[顯示]** 下拉式清單中選取某選項。    
4.  若要檢視和修改訂閱屬性，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]** 。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 
  
  
## <a name="for-publication-agents"></a>針對發行集代理程式
複寫監視器提供 **[代理程式]** 索引標籤，其中包含與選取的發行集相關聯之代理程式的資訊。 「散發代理程式」和「合併代理程式」都與訂閱相關。 
  
### <a name="view-information"></a>檢視資訊
 這個索引標籤會顯示下列代理程式的相關資訊：  
  
-   所有發行集所使用的快照集代理程式。  
-   所有交易式發行集所使用的記錄讀取器代理程式。  
-   針對佇列更新訂閱啟用之交易式發行集所使用的佇列讀取器代理程式。 
  
 若要檢視有關這個索引標籤之選項的詳細資訊，請按一下功能表列上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>若要檢視與發行集相關聯之代理程式的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。    
2.  若要檢視代理程式的相關資訊，請按一下 **[代理程式]** 索引標籤。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：    
    -   若要檢視代理程式的資訊 (例如提示訊息及任何錯誤訊息)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[檢視詳細資料]** 。  
    -   若要檢視執行代理程式之作業的詳細資訊 (諸如排程、作業步驟詳細資料等)，請以滑鼠右鍵按一下該代理程式，然後按一下 **[屬性]** 。    
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]** 。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。   
    -   若要啟動尚未執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[啟動代理程式]** 。   
    -   若要停止正在執行的代理程式，請以滑鼠右鍵按一下該代理程式，然後按一下 **[停止代理程式]** 。  
  
## <a name="for-subscription-agents"></a>針對訂閱代理程式

### <a name="view-information"></a>檢視資訊
-   **所有訂閱** - 顯示與所選發行集的所有訂閱相關的資訊。  
  
-   **訂閱監看清單** - 用來顯示與所選「發行者」之所有可用發行集內有錯誤、警告或效能最差的訂閱相關的資訊。 執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前版本的散發者不會顯示這個索引標籤。 如需有關各索引標籤選項的資訊，請按一下右窗格的索引標籤，然後按一下功能表上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="perform-tasks"></a>執行工作
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。    
2.  按一下 **[所有訂閱]** 索引標籤以檢視有關訂閱的資訊。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：   
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]** 。 詳細的資訊包括：代理程式記錄與錯誤訊息；異動複寫的效能統計資料；以及合併式複寫的發行項層級同步處理統計資料。  
  
         在詳細資料視窗中啟動的索引標籤視訂閱類型而定：對於快照式訂閱，此索引標籤為 **[散發者到訂閱者記錄]** ；對於交易式訂閱，此索引標籤為 **[發行者到散發者記錄]** 、 **[散發者到訂閱者記錄]** 以及 **[未散發的命令]** ；對於合併式訂閱，此索引標籤為 **[同步處理記錄]** 。  
  
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]** 。    
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]** 。    
    -   若要驗證單一合併訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[驗證訂閱]** 。 若要驗證合併發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證所有訂閱]** ；若要驗證交易式發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證訂閱]** 。    
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]** 。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
### <a name="subscription-watch-list-tab"></a>[訂閱監看清單] 索引標籤 
  
1.  在左窗格中展開發行者群組，然後按一下發行者。    
2.  按一下 **[訂閱監看清單]** 索引標籤以檢視有關訂閱的資訊。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：   
    -   若要檢視有關與訂閱相關聯之代理程式的詳細資訊，請以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]** 。 詳細的資訊包括：代理程式記錄與錯誤訊息；異動複寫的效能統計資料；以及合併式複寫的發行項層級同步處理統計資料。    
         在詳細資料視窗中啟動的索引標籤視訂閱類型而定：對於快照式訂閱，此索引標籤為 **[散發者到訂閱者記錄]** ；對於交易式訂閱，此索引標籤為 **[發行者到散發者記錄]** 、 **[散發者到訂閱者記錄]** 以及 **[效能]** ；對於合併式訂閱，此索引標籤為 **[同步處理記錄]** 。  
  
    -   若要同步處理發送訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]** 。    
    -   若要重新初始化訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化訂閱]** 。    
    -   若要驗證單一合併訂閱，請以滑鼠右鍵按一下訂閱，然後按一下 **[驗證訂閱]** 。 若要驗證合併發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證所有訂閱]** ；若要驗證交易式發行集的所有訂閱，請以滑鼠右鍵按一下發行集，然後按一下 **[驗證訂閱]** 。    
    -   若要管理代理程式的設定檔，請以滑鼠右鍵按一下代理程式，然後按一下 **[代理程式設定檔]** 。 如需詳細資訊，請參閱 [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  

    


## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [檢視及修改發送訂閱屬性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
 [在複寫監視器中設定閾值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)    
  
  
