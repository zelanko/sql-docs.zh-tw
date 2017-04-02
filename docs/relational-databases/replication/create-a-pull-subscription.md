---
title: "建立提取訂閱 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "提取訂閱 [SQL Server 複寫], 建立"
  - "合併式複寫訂閱 [SQL Server 複寫], 提取訂閱"
  - "訂閱 [SQL Server 複寫], 提取"
  - "快照式複寫 [SQL Server], 訂閱"
  - "異動複寫, 訂閱"
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 建立提取訂閱
  本主題說明如何建立提取訂閱中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，[!INCLUDE[tsql](../../includes/tsql-md.md)], ，或 Replication Management Objects (RMO)。  
  
 為 P2P 複寫設定提取訂閱可透過指令碼來進行，但無法透過精靈進行。  
 
  ##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增訂閱精靈」在「發行者」或「訂閱者」端建立提取訂閱。 依照精靈中各頁面進行：  
  
-   指定發行者和發行集。  
  
-   選取要執行複寫代理程式的位置。 提取訂閱，請選取 **執行每個代理程式在其訂閱者 」 （提取訂閱）** 上 **散發代理程式位置** 頁面或 **合併代理程式位置**  頁面上，視發行集類型而定。  
  
-   指定訂閱者與訂閱資料庫。  
  
-   指定複寫代理程式要連接用的登入和密碼：  
  
    -   針對快照集和交易式發行集的訂閱，請於 **[散發代理程式安全性]** 頁面指定認證。  
  
    -   針對合併式發行集的訂閱，請於 **[合併代理程式安全性]** 頁面指定認證。  
  
     每個代理程式所需的權限的相關資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
-   指定同步處理排程，以及訂閱者要初始化的時間。  
  
-   指定合併式發行集的其他選項：訂閱類型；參數化篩選的值；以及如果針對 Web 同步處理啟用該發行集時，透過 HTTPS 同步處理的資訊。  
  
-   為交易式發行集指定其他選項，以允許更新訂閱：訂閱者是否應立即在發行者端認可變更，或者應寫入佇列；認證用來連接訂閱者和發行者。  
  
-   選擇性的編寫訂閱指令碼。  
  
#### 若要從發行者建立提取訂閱  
  
1.  連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要建立一個或多個訂閱，並按一下 發行的集 **新訂閱**。  
  
4.  在新增訂閱精靈中完成頁面。  
  
#### 若要從訂閱者建立提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **本機訂閱** 資料夾，然後再按一下 **新訂閱**。  
  
4.  在 **發行集** 頁面的 新增訂閱精靈、 選取 **\< 尋找 SQL Server 發行者>** 或 **\< 尋找 Oracle 發行者>** 從 **發行者** 下拉式清單。  
  
5.  連接到 **[連接到伺服器]** 對話方塊中的發行者。  
  
6.  選取 **[發行集]** 頁面上的發行集。  
  
7.  在新增訂閱精靈中完成頁面。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立提取訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### 若要建立快照式或交易式發行集的提取訂閱  
  
1.  在發行者上，確認發行集支援提取訂閱，藉由執行 [sp_helppublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)。  
  
    -   如果值 **allow_pull** 結果集是 **1**, ，則發行集支援提取訂閱。  
  
    -   如果值 **allow_pull** 是 **0**, ，執行 [sp_changepublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，並指定 **allow_pull** 的 **@property** 和 **true** 的 **@value**。  
  
2.  在 「 訂閱者 」 執行 [sp_addpullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication**。 如需更新訂閱的相關資訊，請參閱 [建立交易式發行集的可更新訂閱](https://msdn.microsoft.com/library/ms152769.aspx)。  
  
3.  在 「 訂閱者 」 執行 [sp_addpullsubscription_agent &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定下列項目：  
  
    -   **@Publisher**, ，**@publisher_db**, ，和 **@publication** 參數。  
  
    -   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訂閱者 的 散發代理程式執行的 Windows 認證 **@job_login** 和 **@job_password**。  
  
        > [!NOTE]  
        >  一律使用 Windows 整合式驗證進行連接會使用指定的 Windows 認證 **@job_login** 和 **@job_password**。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到「散發者」。  
  
    -   （選擇性）值為 **0** 的 **@distributor_security_mode** 和 SQL Server 登入資訊 **@distributor_login** 和 **@distributor_password**, ，如果您需要使用 SQL Server 驗證連接到散發者時。  
  
    -   此訂閱之散發代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
4.  在 「 發行者 」 執行 [sp_addsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 若要註冊提取訂閱。 指定 **@publication**, ，**@subscriber**, ，和 **@destination_db**。 指定的值為 **提取** 的 **@subscription_type**。  
  
#### 若要建立合併式發行集的提取訂閱  
  
1.  在發行者上，確認發行集支援提取訂閱，藉由執行 [sp_helpmergepublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。  
  
    -   如果值 **allow_pull** 結果集是 **1**, ，則發行集支援提取訂閱。  
  
    -   如果值 **allow_pull** 是 **0**, ，執行 [sp_changemergepublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，並指定 **allow_pull** 的 **@property** 和 **true** 的 **@value**。  
  
2.  在 「 訂閱者 」 執行 [sp_addmergepullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，以及下列參數︰  
  
    -   **@subscriber_type** – 指定 **本機** 客訂閱和 **全域** 伺服器訂閱。  
  
    -   **@subscription_priority** – 指定訂閱的優先權 (**0.00** 至 **99.99**)。 只需要對主訂閱執行此動作。  
  
         如需詳細資訊，請參閱 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
3.  在 「 訂閱者 」 執行 [sp_addmergepullsubscription_agent &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)。 指定下列參數：  
  
    -   **@publisher**, ，**@publisher_db**, ，和 **@publication**。  
  
    -   Windows 認證的 「 訂閱者 」 的 「 合併代理程式執行 **@job_login** 和 **@job_password**。  
  
        > [!NOTE]  
        >  一律使用 Windows 整合式驗證進行連接會使用指定的 Windows 認證 **@job_login** 和 **@job_password**。 「合併代理程式」一律使用「Windows 整合式驗證」建立到「訂閱者」的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到「發行者」。  
  
    -   （選擇性）值為 **0** 的 **@distributor_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@distributor_login** 和 **@distributor_password**, ，如果您需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到散發者時。  
  
    -   （選擇性）值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**, ，如果您需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到 「 發行者 」 時。  
  
    -   此訂閱之「合併代理程式」作業的排程。 如需詳細資訊，請參閱 [建立交易式發行集的可更新訂閱](https://msdn.microsoft.com/library/ms152769.aspx)。  
  
4.  在 「 發行者 」 執行 [sp_addmergesubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, ，而值為 **提取** 的 **@subscription_type**。 如此會註冊提取訂閱。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立交易式發行集的提取訂閱。 第一批次在「訂閱者」上執行，而第二批次在「發行者」上執行。 登入和密碼值是在執行階段使用 sqlcmd 指令碼變數提供的。  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
  
-- At the subscription database, create a pull subscription   
-- to a transactional publication.  
USE [AdventureWorksReplica]  
EXEC sp_addpullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.  
EXEC sp_addpullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password);  
GO  
```  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Publisher.  
DECLARE @publication AS sysname;  
DECLARE @subscriber AS sysname;  
DECLARE @subscriptionDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @subscriber = $(SubServer);  
SET @subscriptionDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
EXEC sp_addsubscription   
  @publication = @publication,   
  @subscriber = @subscriber,   
  @destination_db = @subscriptionDB,   
  @subscription_type = N'pull',  
  @status = N'subscribed';  
GO  
  
```  
  
 下列範例會建立合併式發行集的提取訂閱。 第一批次在「訂閱者」上執行，而第二批次在「發行者」上執行。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
DECLARE @hostname AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
SET @hostname = N'adventure-works\david8';  
  
-- At the subscription database, create a pull subscription   
-- to a merge publication.  
USE [AdventureWorksReplica]  
EXEC sp_addmergepullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.   
EXEC sp_addmergepullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password),  
  @hostname = @hostname;  
GO  
```  
  
```  
-- Execute this batch at the Publisher.  
DECLARE @myMergePub  AS sysname;  
DECLARE @mySub       AS sysname;  
DECLARE @mySubDB     AS sysname;  
  
SET @myMergePub = N'AdvWorksSalesOrdersMerge';  
SET @mySub = N'MYSUBSERVER';  
SET @mySubDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
USE [AdventureWorks]  
EXEC sp_addmergesubscription @publication = @myMergePub,   
@subscriber = @mySub, @subscriber_db = @mySubDB,   
@subscription_type = N'pull';  
GO  
```  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於建立提取訂閱的 RMO 類別依該訂閱所屬的發行集類型而定。  
  
#### 若要建立快照式或交易式發行集的提取訂閱  
  
1.  建立連接到 「 訂閱者 」 與 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別使用步驟 1 中的發行者連接。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果這個方法傳回 **false**，則表示步驟 2 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
4.  執行位元邏輯 AND (**&** Visual C# 和 **和** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, ，請將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 的位元邏輯 OR 結果 (**|** Visual C# 和 **或者** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>。 然後，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 啟用提取訂閱。  
  
5.  如果訂閱資料庫不存在，建立使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別。 如需詳細資訊，請參閱 [建立、 改變及移除資料庫](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別。  
  
7.  設定下列訂閱屬性：  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 到 「 訂閱者 」 中建立步驟 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   訂閱資料庫的名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>。  
  
    -   名稱為 「 發行者 」 的 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>。  
  
    -   發行集資料庫的名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>。  
  
    -   發行集名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訂閱者的散發代理程式執行的 Windows 帳戶。 此帳戶用於建立到「訂閱者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 的成員所建立的訂閱時，就不需要 **sysadmin** 固定伺服器角色，但還是建議。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）值為 **true** 的 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 來建立用來同步處理訂閱的代理程式作業。 如果您指定 **false** （預設值），只會同步處理訂閱以程式設計的方式，您必須指定的其他屬性 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 當您存取此物件從 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 屬性。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
        > [!NOTE]  
        >  並非所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。 當您為 Express 訂閱者指定值 **true** 時，不會建立代理程式作業。 不過，在「訂閱者」上會儲存重要的訂閱相關中繼資料。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 使用 SQL Server 驗證連接到散發者時。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法。  
  
9. 使用的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別從步驟 2，呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> 方法來與 「 發行者 」 註冊提取訂閱。 如果此註冊已存在，則會發生例外狀況。  
  
#### 若要建立合併式發行集的提取訂閱  
  
1.  建立連接到 「 訂閱者 」 與 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別使用步驟 1 中的發行者連接。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果這個方法傳回 **false**，則表示步驟 2 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
4.  執行位元邏輯 AND (**&** Visual C# 和 **和** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, ，請將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 的位元邏輯 OR 結果 (**|** Visual C# 和 **或者** 在 Visual Basic 中) 之間 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>。 然後，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 啟用提取訂閱。  
  
5.  如果訂閱資料庫不存在，建立使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別。 如需詳細資訊，請參閱 [建立、 改變及移除資料庫](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別。  
  
7.  設定下列訂閱屬性：  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 到 「 訂閱者 」 中建立步驟 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   訂閱資料庫的名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>。  
  
    -   名稱為 「 發行者 」 的 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>。  
  
    -   發行集資料庫的名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>。  
  
    -   發行集名稱 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訂閱者的合併代理程式執行的 Windows 帳戶。 此帳戶用於建立到「訂閱者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 的成員所建立的訂閱時，就不需要 **sysadmin** 固定伺服器角色，但還是建議。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）值為 **true** 的 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 來建立用來同步處理訂閱的代理程式作業。 如果您指定 **false** （預設值），只會同步處理訂閱以程式設計的方式，您必須指定的其他屬性 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 當您存取此物件從 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 屬性。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 使用 SQL Server 驗證連接到散發者時。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 使用 SQL Server 驗證連接到 「 發行者 」 時。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法。  
  
9. 使用的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別從步驟 2，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> 方法來與 「 發行者 」 註冊提取訂閱。 如果此註冊已存在，則會發生例外狀況。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立交易式發行集的提取訂閱。 用於建立「散發代理程式」作業的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶認證是在執行階段傳遞的。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksProductTran";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
TransPublication publication;  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Publisher and Subscriber.  
    subscriberConn.Connect();  
    publisherConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new TransPublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.IsExistingObject)  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new TransPullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // By default, subscriptions to transactional publications are synchronized   
        // continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (TransSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                TransSubscriberType.ReadOnly);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As TransPublication  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Publisher and Subscriber.  
    subscriberConn.Connect()  
    publisherConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New TransPublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.IsExistingObject Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New TransPullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.Description = "Pull subscription to " + publicationDbName _  
        + " on " + subscriberName + "."  
  
        ' Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' By default, subscriptions to transactional publications are synchronized   
        ' continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As TransSubscription In publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName And _  
                existing.SubscriptionDBName = subscriptionDbName Then  
                registered = True  
            End If  
        Next existing  
        If Not registered Then  
            ' Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             TransSubscriberType.ReadOnly)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
  
```  
  
 此範例會建立合併式發行集的提取訂閱。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
```cpp#  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 這個範例會建立合併式發行集的提取訂閱，而不需建立關聯的代理程式作業和訂閱中的中繼資料 [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify that an agent job not be created for this subscription. The  
        // subscription can only be synchronized by running the Merge Agent directly.  
        // Subscripition metadata stored in MSsubscription_properties will not  
        // be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = false;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
  
        ' Specify that an agent job not be created for this subscription. The  
        ' subscription can only be synchronized by running the Merge Agent directly.  
        ' Subscripition metadata stored in MSsubscription_properties will not  
        ' be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = False  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 此範例會建立合併式發行集的提取訂閱，使用 Web 同步處理可以從網際網路對其進行同步處理。 用於建立「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/WebSync/replisapi.dll";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions and Web synchronization.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
        if ((publication.Attributes & PublicationAttributes.AllowWebSynchronization) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowWebSynchronization;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Enable Web synchronization.  
        subscription.UseWebSynchronization = true;  
        subscription.InternetUrl = webSyncUrl;  
  
        // Specify the same Windows credentials to use when connecting to the  
        // Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication;  
        subscription.InternetLogin = winLogin;  
        subscription.InternetPassword = winPassword;  
  
        // Ensure that we create a job for this subscription.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/WebSync/replisapi.dll"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions and Web synchronization.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
        If (publication.Attributes And PublicationAttributes.AllowWebSynchronization) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowWebSynchronization  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Enable Web synchronization.  
        subscription.UseWebSynchronization = True  
        subscription.InternetUrl = webSyncUrl  
  
        ' Specify the same Windows credentials to use when connecting to the  
        ' Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication  
        subscription.InternetLogin = winLogin  
        subscription.InternetPassword = winPassword  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
## 另請參閱  
 [Replication Management Objects 概念。](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  