---
title: "指定同步處理排程 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1d131e8e7aee66186245b0d69acb1b5c10285cf3
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="specify-synchronization-schedules"></a>指定同步處理排程
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中指定同步處理排程。 當您建立訂閱時，可以定義一個同步排程，以控制訂閱的複寫代理程式將於何時執行。 如果不指定排程參數，訂閱將使用預設排程。  
  
 訂閱是由散發代理程式 (適用於快照式與異動複寫) 或合併代理程式 (適用於合併式複寫) 同步處理。 代理程式可以繼續執行、視需要執行，或是依照排程執行。  
  
 **本主題內容**  
  
-   **若要指定同步處理排程，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增訂閱精靈」的 **[同步排程]** 頁面中指定同步排程。 如需有關存取這個精靈的詳細資訊，請參閱＜ [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) ＞與＜ [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)＞。  
  
 在 **[作業排程屬性]** 對話方塊中修改同步處理排程，您可從 **的** [作業] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資料夾和「複寫監視器」的代理程式詳細資料視窗中取得此對話方塊。 如需啟動複寫監視器的資訊，請參閱[啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
 如果從 **[作業]** 資料夾指定排程，請使用下列資料表以決定代理程式作業的名稱。  
  
|代理程式|作業名稱|  
|-----------|--------------|  
|提取訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<訂閱資料庫>-\<整數>**|  
|發送訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|  
|發送訂閱的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>** <sup>1</sup>|  
|提取訂閱的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<訂閱資料庫>-\<GUID>** <sup>2</sup>|  
|發送訂閱至非 SQL Server 訂閱者的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|  
  
 <sup>1</sup> 如果是 Oracle 發行集的發送訂閱，其作業名稱會是 [\<發行者>-\<發行者>]，而不是 [\<發行者>-\<發行集資料庫>]。  
  
 <sup>2</sup> 如果是 Oracle 發行集的提取訂閱，其作業名稱會是 [\<發行者>-\<散發資料庫>]，而不是 [\<發行者>-\<發行集資料庫>]。  
  
#### <a name="to-specify-synchronization-schedules"></a>若要指定同步排程  
  
1.  在 [新增訂閱精靈] 的 [同步排程] 頁面，從 [代理程式排程] 下拉式清單中為您正建立的每個訂閱選取下列值的其中之一：  
  
    -   **連續執行**  
  
    -   **[視需要執行]**  
  
    -   **\<定義排程…>**  
  
2.  如果您選取 [\<定義排程...>]，則在 [作業排程屬性] 對話方塊中指定排程，然後按一下 [確定]。  
  
3.  完成精靈。  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>若要在「複寫監視器」中修改發送訂閱的同步排程  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。  
  
4.  在 [訂閱 <訂閱名稱>] 視窗中，按一下 [動作]，然後按一下 [\<代理程式名稱> 作業屬性]。  
  
5.  在 [作業屬性 - \<工作名稱>] 對話方塊的 [排程] 頁面，按一下 [編輯]。  
  
6.  在 **[作業排程屬性]** 對話方塊中，從 **[排程類型]** 下拉式清單內選取一個值：  
  
    -   若要指定代理程式應持續執行，請選取 **[當 SQL Server Agent 啟動時自動啟動]**。  
  
    -   若要指定代理程式應於排程上執行，請選取 **[重複執行]**。  
  
    -   若要指定代理程式應視需要執行，請選取 **[執行一次]**。  
  
7.  若您選取 **[重複執行]**，請為代理程式指定排程。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>若要在 Management Studio 中修改發送訂閱的同步排程  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下與訂閱相關聯的散發代理程式或合併代理程式的作業，然後按一下 **[屬性]**。  
  
4.  在 [作業屬性 - \<工作名稱>] 對話方塊的 [排程] 頁面，按一下 [編輯]。  
  
5.  在 **[作業排程屬性]** 對話方塊中，從 **[排程類型]** 下拉式清單內選取一個值：  
  
    -   若要指定代理程式應持續執行，請選取 **[當 SQL Server Agent 啟動時自動啟動]**。  
  
    -   若要指定代理程式應於排程上執行，請選取 **[重複執行]**。  
  
    -   若要指定代理程式應視需要執行，請選取 **[執行一次]**。  
  
6.  若您選取 **[重複執行]**，請為代理程式指定排程。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>若要在 Management Studio 修改提取訂閱的同步排程  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下與訂閱相關聯的散發代理程式或合併代理程式的作業，然後按一下 **[屬性]**。  
  
4.  在 [作業屬性 - \<工作名稱>] 對話方塊的 [排程] 頁面，按一下 [編輯]。  
  
5.  在 **[作業排程屬性]** 對話方塊中，從 **[排程類型]** 下拉式清單內選取一個值：  
  
    -   若要指定代理程式應持續執行，請選取 **[當 SQL Server Agent 啟動時自動啟動]**。  
  
    -   若要指定代理程式應於排程上執行，請選取 **[重複執行]**。  
  
    -   若要指定代理程式應視需要執行，請選取 **[執行一次]**。  
  
6.  若您選取 **[重複執行]**，請為代理程式指定排程。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式定義同步排程。 使用哪些預存程序要依複寫的類型和訂閱的類型 (提取訂閱或發送訂閱) 而定。  
  
 排程是由下列排程參數所定義，其行為是繼承自 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)：  
  
-   **@frequency_type** - 在排程代理程式時所使用的頻率類型。  
  
-   **@frequency_interval** - 代理程式執行之一週中的日子。  
  
-   **@frequency_relative_interval** - 當代理程式排定為要每月執行時，給定月份的週。  
  
-   **@frequency_recurrence_factor** - 在同步處理之間發生的頻率類型單位數目。  
  
-   **@frequency_subday** - 代理程式執行頻率超過一天一次以上時的頻率單位。  
  
-   **@frequency_subday_interval** - 代理程式執行頻率超過一天一次以上時，執行之間的頻率單位數目。  
  
-   **@active_start_time_of_day** - 代理程式在給定日子開始執行的最早時間。  
  
-   **@active_end_time_of_day** - 代理程式在給定日子開始執行的最晚時間。  
  
-   **@active_start_date** - 代理程式排程開始生效的第一天。  
  
-   **@active_end_date** - 代理程式排程有效的最後一天。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>針對交易式發行集的提取訂閱定義同步排程  
  
1.  建立交易式發行集的新提取訂閱。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在訂閱者端，執行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**或 Replication Management Objects (RMO)，在 **@publication**以及針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_name **@job_name** ＞與＜ **@password**＞。 指定以上詳述的同步處理參數，這些參數會針對同步處理訂閱的散發代理程式作業定義排程。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>針對交易式發行集的發送訂閱定義同步排程  
  
1.  建立交易式發行集的新發送訂閱。 如需詳細資訊，請參閱 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在訂閱者端，執行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定 **@subscriber**或 Replication Management Objects (RMO)，在 **@subscriber_db**或 Replication Management Objects (RMO)，在 **@publication**以及針對 **@job_name** ＞與＜ **@password**＞。 指定以上詳述的同步處理參數，這些參數會針對同步處理訂閱的散發代理程式作業定義排程。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>針對合併式發行集的提取訂閱定義同步排程  
  
1.  建立合併式發行集的新提取訂閱。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在訂閱者上，執行 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**或 Replication Management Objects (RMO)，在 **@publication**以及針對 **@job_name** ＞與＜ **@password**＞。 指定以上詳述的同步處理參數，這些參數會針對同步處理訂閱的合併代理程式作業定義排程。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>針對合併式發行集的發送訂閱定義同步排程  
  
1.  建立合併式發行集的新發送訂閱。 如需詳細資訊，請參閱 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在訂閱者上，執行 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)。 指定 **@subscriber**或 Replication Management Objects (RMO)，在 **@subscriber_db**或 Replication Management Objects (RMO)，在 **@publication**以及針對 **@job_name** ＞與＜ **@password**＞。 指定以上詳述的同步處理參數，這些參數會針對同步處理訂閱的合併代理程式作業定義排程。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 複寫會使用 SQL Server Agent 來排程定期發生之活動的作業，例如快照集的產生和訂閱同步處理。 您可以使用Replication Management Objects (RMO)，以程式設計方式指定複寫代理程式作業的排程。  
  
> [!NOTE]  
>  當您建立訂閱，並針對 **false** (提取訂閱的預設行為) 指定 **CreateSyncAgentByDefault** 的值時，不會建立代理程式作業，而且會忽略排程屬性。 在此情況下，同步排程必須由應用程式來決定。 如需相關資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 及 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>當您建立交易式發行集的發送訂閱時，定義複寫代理程式排程  
  
1.  為您所建立的訂閱建立 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別的執行個體。 如需詳細資訊，請參閱 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在您呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 之前，請設定 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 屬性的下列一或多個欄位：  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 排定代理程式時所使用的頻率類型 (如每天或每週)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 代理程式在一週的哪一天執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 代理程式排定為每月執行時，於所指定月份的哪一週執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同步處理之間發生的頻率類型單位數目。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 代理程式一天執行多次時的頻率單位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 代理程式一天執行多次時，各執行之間的頻率單位數。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 代理程式開始執行的那一天的最早時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 代理程式開始執行的那一天的最晚時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 代理程式排程生效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 代理程式排程生效的最後一天。  
  
    > [!NOTE]  
    >  若未指定這些屬性的其中一個，則會設定預設值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法來建立訂閱。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>當您建立交易式發行集的提取訂閱時，定義複寫代理程式排程  
  
1.  為您所建立的訂閱建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在您呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 之前，請設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 屬性的下列一或多個欄位：  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 排定代理程式時所使用的頻率類型 (如每天或每週)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 代理程式在一週的哪一天執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 代理程式排定為每月執行時，於所指定月份的哪一週執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同步處理之間發生的頻率類型單位數目。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 代理程式一天執行多次時的頻率單位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 代理程式一天執行多次時，各執行之間的頻率單位數。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 代理程式開始執行的那一天的最早時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 代理程式開始執行的那一天的最晚時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 代理程式排程生效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 代理程式排程生效的最後一天。  
  
    > [!NOTE]  
    >  若未指定這些屬性的其中一個，則會設定預設值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法來建立訂閱。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>當您建立合併式發行集的提取訂閱時，定義複寫代理程式排程  
  
1.  為您所建立的訂閱建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在您呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 之前，請設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 屬性的下列一或多個欄位：  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 排定代理程式時所使用的頻率類型 (如每天或每週)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 代理程式在一週的哪一天執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 代理程式排定為每月執行時，於所指定月份的哪一週執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同步處理之間發生的頻率類型單位數目。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 代理程式一天執行多次時的頻率單位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 代理程式一天執行多次時，各執行之間的頻率單位數。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 代理程式開始執行的那一天的最早時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 代理程式開始執行的那一天的最晚時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 代理程式排程生效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 代理程式排程生效的最後一天。  
  
    > [!NOTE]  
    >  若未指定這些屬性的其中一個，則會設定預設值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法來建立訂閱。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>當您建立合併式發行集的發送訂閱時，定義複寫代理程式排程  
  
1.  為您所建立的訂閱建立 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別的執行個體。 如需詳細資訊，請參閱 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在您呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 之前，請設定 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 屬性的下列一或多個欄位：  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - 排定代理程式時所使用的頻率類型 (如每天或每週)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - 代理程式在一週的哪一天執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - 代理程式排定為每月執行時，於所指定月份的哪一週執行。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同步處理之間發生的頻率類型單位數目。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - 代理程式一天執行多次時的頻率單位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - 代理程式一天執行多次時，各執行之間的頻率單位數。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - 代理程式開始執行的那一天的最早時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - 代理程式開始執行的那一天的最晚時間。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - 代理程式排程生效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - 代理程式排程生效的最後一天。  
  
    > [!NOTE]  
    >  若未指定這些屬性的其中一個，則會設定預設值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法來建立訂閱。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立合併式發行集的發送訂閱，並指定同步處理此訂閱所依據的排程。  
  
 [!code-cs[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>另請參閱  
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)  
  
  

