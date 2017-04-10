---
title: "建立發送訂閱 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "push subscriptions [SQL Server replication], creating"
  - "merge replication subscribing [SQL Server replication], push subscriptions"
  - "subscriptions [SQL Server replication], push"
  - "snapshot replication [SQL Server], subscribing"
  - "異動複寫, 訂閱"
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 建立發送訂閱
  本主題描述如何建立發送訂閱中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，[!INCLUDE[tsql](../../includes/tsql-md.md)], ，或 Replication Management Objects (RMO)。 如需建立發送訂閱非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，請參閱 [為非 SQL Server 訂閱者建立訂閱](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
 
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增訂閱精靈」在「發行者」或「訂閱者」端建立發送訂閱。 依照精靈中各頁面進行：  
  
-   指定發行者和發行集。  
  
-   選取要執行複寫代理程式的位置。 發送訂閱，請選取 **執行所有代理程式在散發者 （發送訂閱）** 上 **散發代理程式位置** 頁面或 **合併代理程式位置** ] 頁面上，視發行集類型而定。  
  
-   指定訂閱者與訂閱資料庫。  
  
-   指定複寫代理程式要連接用的登入和密碼：  
  
    -   針對快照集和交易式發行集的訂閱，請於 **[散發代理程式安全性]** 頁面指定認證。  
  
    -   針對合併式發行集的訂閱，請於 **[合併代理程式安全性]** 頁面指定認證。  
  
     每個代理程式所需的權限的相關資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
-   指定同步處理排程，以及訂閱者要初始化的時間。  
  
-   指定合併式發行集的其他選項：訂閱類型以及參數化篩選的值。  
  
-   為交易式發行集指定其他選項，以允許更新訂閱：訂閱者是否應立即在發行者端認可變更，或者應寫入佇列；認證用來連接訂閱者和發行者。  
  
-   選擇性的編寫訂閱指令碼。  
  
#### 若要從發行者端建立發送訂閱  
  
1.  連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要建立一個或多個訂閱，並按一下 [發行的集 **新訂閱**。  
  
4.  在新增訂閱精靈中完成頁面。  
  
#### 若要從訂閱者建立發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **本機訂閱** 資料夾，然後再按一下 **新訂閱**。  
  
4.  在 **發行集** 頁面的 [新增訂閱精靈、 選取 **\< 尋找 SQL Server 發行者>** 或 **\< 尋找 Oracle 發行者>** 從 **發行者** 下拉式清單。  
  
5.  連接到 **[連接到伺服器]** 對話方塊中的發行者。  
  
6.  選取 **[發行集]** 頁面上的發行集。  
  
7.  在新增訂閱精靈中完成頁面。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立發送訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
> **重要！** 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### 若要建立快照式或交易式發行集的發送訂閱  
  
1.  在發行集資料庫的發行者，請確認發行集支援發送訂閱，藉由執行 [sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)。  
  
    -   如果值 **allow_push** 是 **1**, ，支援發送訂閱。  
  
    -   如果值 **allow_push** 是 **0**, ，執行 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，並指定 **allow_push** 的 **@property** 和 **true** 的 **@value**。  
  
2.  在發行集資料庫的發行者，執行 [sp_addsubscription](https://msdn.microsoft.com/library/ms181702.aspx)。 指定 **@publication**, ，**@subscriber** 和 **@destination_db**。 指定的值為 **推播** 的 **@subscription_type**。 如需有關如何更新訂閱的資訊，請參閱 [建立交易式發行集的可更新訂閱](https://msdn.microsoft.com/library/ms152769.aspx)。  
  
3.  在發行集資料庫的發行者，執行 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定下列項目：  
  
    -    **@Subscriber**, ，**@subscriber_db**, ，和 **@publication** 參數。  
  
    -   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 散發代理程式在散發者上執行的 Windows 認證 **@job_login** 和 **@job_password**。  
  
        > **注意︰** 一律使用 Windows 整合式驗證進行連接會使用指定的 Windows 認證 **@job_login** 和 **@job_password**。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。  
  
    -   （選擇性）值為 **0** 的 **@subscriber_security_mode** 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@subscriber_login** 和 **@subscriber_password**。 如果您在連接到「訂閱者」時需要使用「SQL Server 驗證」，請指定這些參數。  
  
    -   此訂閱之散發代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > **重要！！** 發行者與遠端散發者，提供給所有參數的值來建立發送訂閱時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 若要建立合併式發行集的發送訂閱  
  
1.  在發行集資料庫的發行者，請確認發行集支援發送訂閱，藉由執行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。  
  
    -   如果值 **allow_push** 是 **1**, ，發行集支援發送訂閱。  
  
    -   如果值 **allow_push** 不 **1**, ，執行 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，並指定 **allow_push** 的 **@property** 和 **true** 的 **@value**。  
  
2.  在發行集資料庫的發行者，執行 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md), ，指定下列參數︰  
  
    -   **@publication**。 這是發行集的名稱。  
  
    -   **@subscriber_type**。 將客訂閱指定為 **local** ，並將主訂閱指定為 **global**。  
  
    -   **@subscription_priority**。 主訂閱指定訂閱的優先權 (**0.00** 至 **99.99**)。  
  
         如需詳細資訊，請參閱 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
3.  在發行集資料庫的發行者，執行 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)。 指定下列項目：  
  
    -   **@Subscriber**, ，**@subscriber_db**, ，和 **@publication** 參數。  
  
    -   Windows 認證的合併代理程式在散發者端執行 **@job_login** 和 **@job_password**。  
  
        > **注意︰**  一律使用 Windows 整合式驗證進行連接會使用指定的 Windows 認證 **@job_login** 和 **@job_password**。 「合併代理程式」一律使用「Windows 整合式驗證」建立到「散發者」的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。  
  
    -   （選擇性）值為 **0** 的 **@subscriber_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@subscriber_login** 和 **@subscriber_password**。 如果您在連接到「訂閱者」時需要使用「SQL Server 驗證」，請指定這些參數。  
  
    -   （選擇性）值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 如果您在連接到「發行者」時需要使用「SQL Server 驗證」，請指定這些值。  
  
    -   此訂閱之「合併代理程式」作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > **重要！！** 發行者與遠端散發者，提供給所有參數的值來建立發送訂閱時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立交易式發行集的發送訂閱。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_1.sql)]  
  
 下列範例會建立合併式發行集的發送訂閱。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式建立發送訂閱。 用於建立發送訂閱的 RMO 類別依該訂閱所屬的發行集類型而定。  
  
> **重要！** 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### 若要建立快照式或交易式發行集的發送訂閱  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別使用步驟 1 中的發行者連接。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，則表示步驟 2 中指定的屬性不正確，或伺服器上不存在該發行集。  
  
4.  執行位元邏輯 AND (**&** Visual C# 和 **和** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, ，請將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 的位元邏輯 OR 結果 (**|** Visual C# 和 **或者** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>。 然後，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用發送訂閱。  
  
5.  如果訂閱資料庫不存在，建立使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別。 如需詳細資訊，請參閱 [建立、 改變及移除資料庫](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別。  
  
7.  設定下列訂閱屬性：  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 到 「 發行者 」 中建立步驟 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   訂閱資料庫的名稱 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>。  
  
    -   針對訂閱者 」 名稱 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>。  
  
    -   發行集資料庫的名稱 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>。  
  
    -   發行集名稱 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 散發者端的散發代理程式執行的 Windows 帳戶。 此帳戶用於建立到「散發者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > **注意︰** 設定 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 的成員所建立的訂閱時，就不需要 **sysadmin** 固定伺服器角色，但還是建議。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）值為 **true** （預設值） 的 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 來建立用來同步處理訂閱的代理程式作業。 如果指定 **false**，則只能以程式設計的方式同步處理訂閱。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 時使用 SQL Server 驗證連接到 「 訂閱者 」。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > **重要!!**發行者與遠端散發者，提供給所有屬性的值來建立發送訂閱時包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, ，傳送到 「 散發者 」，以純文字。 您應該先加密 「 發行者 」 之前，先呼叫其遠端散發者之間連接 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 若要建立合併式發行集的發送訂閱  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別使用步驟 1 中的發行者連接。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，則表示步驟 2 中指定的屬性不正確，或伺服器上不存在該發行集。  
  
4.  執行位元邏輯 AND (**&** Visual C# 和 **和** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, ，請將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 的位元邏輯 OR 結果 (**|** Visual C# 和 **或者** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>。 然後，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用發送訂閱。  
  
5.  如果訂閱資料庫不存在，建立使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別。 如需詳細資訊，請參閱 [建立、 改變及移除資料庫](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別。  
  
7.  設定下列訂閱屬性：  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 到 「 發行者 」 中建立步驟 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   訂閱資料庫的名稱 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>。  
  
    -   針對訂閱者 」 名稱 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>。  
  
    -   發行集資料庫的名稱 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>。  
  
    -   發行集名稱 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 散發者端的合併代理程式執行的 Windows 帳戶。 此帳戶用於建立到「散發者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > **注意︰** 設定 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 的成員所建立的訂閱時，就不需要 **sysadmin** 固定伺服器角色，但還是建議。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）值為 **true** （預設值） 的 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 來建立用來同步處理訂閱的代理程式作業。 如果指定 **false**，則只能以程式設計的方式同步處理訂閱。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 時使用 SQL Server 驗證連接到 「 訂閱者 」。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 使用 SQL Server 驗證連接到 「 發行者 」 時。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > **重要！**  發行者與遠端散發者，提供給所有屬性的值來建立發送訂閱時包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, ，傳送到 「 散發者 」，以純文字。 您應該先加密 「 發行者 」 之前，先呼叫其遠端散發者之間連接 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立交易式發行集的新發送訂閱。 用於執行「散發代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 此範例會建立合併式發行集的新發送訂閱。 用於執行「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## 另請參閱  
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Replication Management Objects 概念。](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [以指令碼變數使用 sqlcmd](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  