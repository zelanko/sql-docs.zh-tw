---
title: 建立發送訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e723c42dd41c21abb2c11059b8706a098f7fcfd9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353346"
---
# <a name="create-a-push-subscription"></a>建立發送訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來建立 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的發送訂閱。 如需為非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者建立發送訂閱的資訊，請參閱[為非 SQL Server 訂閱者建立訂閱](create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增訂閱精靈」在「發行者」或「訂閱者」端建立發送訂閱。 依照精靈中各頁面進行：  
  
-   指定發行者和發行集。  
  
-   選取要執行複寫代理程式的位置。 對於發送訂閱，根據發行集的類型在 **[散發代理程式位置]** 頁面或 **[合併代理程式位置]** 頁面上選取 **[在散發者端執行所有代理程式 (發送訂閱)]** 。  
  
-   指定訂閱者與訂閱資料庫。  
  
-   指定複寫代理程式要連接用的登入和密碼：  
  
    -   針對快照集和交易式發行集的訂閱，請於 **[散發代理程式安全性]** 頁面指定認證。  
  
    -   針對合併式發行集的訂閱，請於 **[合併代理程式安全性]** 頁面指定認證。  
  
     如需有關各代理程式需要的權限資訊，請參閱＜ [複寫代理程式安全性模型](security/replication-agent-security-model.md)＞。  
  
-   指定同步處理排程，以及訂閱者要初始化的時間。  
  
-   指定合併式發行集的其他選項：訂閱類型以及參數化篩選的值。  
  
-   為交易式發行集指定其他選項，以允許更新訂閱：訂閱者是否應立即在發行者端認可變更，或者應寫入佇列；認證用來連接訂閱者和發行者。  
  
-   選擇性的編寫訂閱指令碼。  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>若要從發行者端建立發送訂閱  
  
1.  連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要建立一個或多個訂閱的發行集，然後按一下 **[新增訂閱]**。  
  
4.  在新增訂閱精靈中完成頁面。  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>若要從訂閱者建立發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **[區域訂閱]** 資料夾，然後按一下 **[新增訂閱]**。  
  
4.  在 [新增訂閱精靈] 的 [發行集] 頁面上，從 [發行者] 下拉式清單中選取 [\<尋找 SQL Server 發行者>] 或 [\<尋找 Oracle 發行者>]。  
  
5.  連接到 **[連接到伺服器]** 對話方塊中的發行者。  
  
6.  選取 **[發行集]** 頁面上的發行集。  
  
7.  在新增訂閱精靈中完成頁面。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立發送訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>若要建立快照式或交易式發行集的發送訂閱  
  
1.  在發行集資料庫的「發行者」上，確認發行集確實是藉由執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來支援發送訂閱。  
  
    -   如果 **allow_push** 的值為 **1**，則發送訂閱受到支援。  
  
    -   如果值**allow_push**是**0**，執行[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並指定**allow_push**如 **@property**並`true`for **@value**。  
  
2.  在發行集資料庫的「發行者」上，執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定 **@publication**或 Replication Management Objects (RMO) 來建立 **@subscriber** ，並將 **@destination_db**＞。 將 **@subscription_type** 指定為 **@subscription_type**＞。 如需有關如何更新訂用帳戶的資訊，請參閱[建立交易式發行集的可更新訂閱](create-updatable-subscription-transactional-publication-transact-sql.md)  
  
3.  在發行集資料庫的「發行者」上，執行 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定下列項目：  
  
    -   將 **@subscriber**或 Replication Management Objects (RMO) 來建立 **@subscriber_db**和 **@publication** 參數。  
  
    -   將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認證，「散發者」上的「散發代理程式」執行時會針對 **@job_login** ，並將 **@job_password**＞。  
  
        > [!NOTE]  
        >  使用「Windows 整合式驗證」建立的連接一律使用由 **@job_login** 及 **@job_password**中針對非 SQL Server 訂閱者建立訂閱。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。  
  
    -   (選擇性) **0** 指定為 **@subscriber_security_mode** ，以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@subscriber_login** ，並將 **@subscriber_password**＞。 如果您在連接到「訂閱者」時需要使用「SQL Server 驗證」，請指定這些參數。  
  
    -   此訂閱之散發代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  利用遠端「散發者」來建立「發行者」上的發送訂閱時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字格式傳給「散發者」。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>若要建立合併式發行集的發送訂閱  
  
1.  在發行集資料庫的「發行者」上，確認發行集確實是藉由執行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)來支援發送訂閱。  
  
    -   如果 **allow_push** 的值為 **1**，則發行集支援發送訂閱。  
  
    -   如果值**allow_push**不是**1**，執行[sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，並指定**allow_push**如**@property** 並`true`如**@value**。  
  
2.  在發行集資料庫的「發行者」上，執行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)並指定下列參數：  
  
    -   **@publication**＞。 這是發行集的名稱。  
  
    -   **@subscriber_type**＞。 將客訂閱指定為 **local** ，並將主訂閱指定為 **global**。  
  
    -   **@subscription_priority**＞。 指定主訂閱的訂閱優先權 (從**0.00** 到 **99.99**)。  
  
         如需詳細資訊，請參閱 [進階合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
3.  在發行集資料庫的「發行者」上，執行 [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)。 指定下列項目：  
  
    -   將 **@subscriber**或 Replication Management Objects (RMO)，在 **@subscriber_db**和 **@publication** 參數。  
  
    -   Windows 認證，「散發者」上的「合併代理程式」執行時會針對 **@job_login** ，並將 **@job_password**＞。  
  
        > [!NOTE]  
        >  使用「Windows 整合式驗證」建立的連接一律使用由 **@job_login** 及 **@job_password**中針對非 SQL Server 訂閱者建立訂閱。 「合併代理程式」一律使用「Windows 整合式驗證」建立到「散發者」的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。  
  
    -   (選擇性) **0** 指定為 **@subscriber_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@subscriber_login** ，並將 **@subscriber_password**＞。 如果您在連接到「訂閱者」時需要使用「SQL Server 驗證」，請指定這些參數。  
  
    -   (選擇性) **0** 指定為 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** ，並將 **@publisher_password**＞。 如果您在連接到「發行者」時需要使用「SQL Server 驗證」，請指定這些值。  
  
    -   此訂閱之「合併代理程式」作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  利用遠端「散發者」來建立「發行者」上的發送訂閱時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字格式傳給「散發者」。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立交易式發行集的發送訂閱。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpushsub.sql#sp_addtranpushsubscription_agent)]  
  
 下列範例會建立合併式發行集的發送訂閱。 登入和密碼值是在執行階段使用 **sqlcmd** 指令碼變數所提供。  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepushsub.sql#sp_addmergepushsubscriptionagent)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式建立發送訂閱。 用於建立發送訂閱的 RMO 類別依該訂閱所屬的發行集類型而定。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>若要建立快照式或交易式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，則表示步驟 2 中指定的屬性不正確，或伺服器上不存在該發行集。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之間執行位元運算邏輯 AND (Visual C# 中的 `&` 和 Visual Basic 中的 `And`)。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，則將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 設為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之間位元運算邏輯 OR (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`) 的結果。 然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用發送訂閱。  
  
5.  如果訂閱資料庫不存在，可使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別建立它。 如需詳細資訊，請參閱[建立、改變和移除資料庫](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別的執行個體。  
  
7.  設定下列訂閱屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設為到步驟 1 中建立之「發行者」的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>設為訂閱資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>設為「訂閱者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>設為發行集資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>設為發行集的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (或 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) 欄位，為「散發代理程式」在「散發者」上執行時所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶提供認證。 此帳戶用於建立到「散發者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  當訂閱是由 `sysadmin` 固定伺服器角色的成員建立時，不需要設定 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>，但還是建議您對其進行設定。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 的 `true` 值 (預設值)，以建立用於同步處理訂閱的代理程式作業。 如果指定 `false`，則只能以程式設計的方式同步處理訂閱。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「訂閱者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ) 欄位。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > [!IMPORTANT]  
    >  利用遠端「散發者」來建立「發行者」上的發送訂閱時，提供給所有屬性的值 (包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) 都會以純文字的方式傳給「散發者」。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>若要建立合併式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，則表示步驟 2 中指定的屬性不正確，或伺服器上不存在該發行集。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之間執行位元運算邏輯 AND (Visual C# 中的 `&` 和 Visual Basic 中的 `And`)。 如果結果為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，則將 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 設為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之間位元運算邏輯 OR (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`) 的結果。 然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以啟用發送訂閱。  
  
5.  如果訂閱資料庫不存在，可使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別建立它。 如需詳細資訊，請參閱[建立、改變和移除資料庫](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  建立 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別的執行個體。  
  
7.  設定下列訂閱屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設為到步驟 1 中建立之「發行者」的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>設為訂閱資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>設為「訂閱者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>設為發行集資料庫的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>設為發行集的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (或 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) 欄位，為「合併代理程式」在「散發者」上執行時所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶提供認證。 此帳戶用於建立到「散發者」的本機連接，以及使用「Windows 驗證」建立遠端連接。  
  
        > [!NOTE]  
        >  當訂閱是由 `sysadmin` 固定伺服器角色的成員建立時，不需要設定 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>，但還是建議您對其進行設定。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 的 `true` 值 (預設值)，以建立用於同步處理訂閱的代理程式作業。 如果指定 `false`，則只能以程式設計的方式同步處理訂閱。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「訂閱者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ) 欄位。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「發行者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ) 欄位。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > [!IMPORTANT]  
    >  利用遠端「散發者」來建立「發行者」上的發送訂閱時，提供給所有屬性的值 (包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) 都會以純文字的方式傳給「散發者」。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立交易式發行集的新發送訂閱。 用於執行「散發代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 此範例會建立合併式發行集的新發送訂閱。 用於執行「合併代理程式」作業的 Windows 帳戶認證是在執行階段傳遞的。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發送訂閱屬性](view-and-modify-push-subscription-properties.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [同步處理發送訂閱](synchronize-a-push-subscription.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [以指令碼變數使用 sqlcmd](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
