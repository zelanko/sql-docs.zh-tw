---
title: "建立發行集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publications [SQL Server replication], creating"
  - "articles [SQL Server replication], defining"
  - "adding articles"
  - "發行項 [SQL Server 複寫], 加入"
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 建立發行集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO) 來建立 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中的發行集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要建立發行集並定義發行項，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   發行集與發行項名稱不能包含任何下列字元: %、 \* , ，[，]，|，:，"，？ 、'、\、/、\<、>。 如果資料庫中的物件包含下列任何字元，而且您想要複寫它們，您必須指定發行項名稱中的物件名稱與不同 **發行項屬性-\< 發行項>** 對話方塊中，可從 **文章** 精靈中的頁面。  
  
###  <a name="Security"></a> 安全性  
 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」建立發行集並定義發行項。 在建立發行集之後，檢視及修改發行集屬性，在 **發行集屬性-\< 發行集>** 對話方塊。 從 Oracle 資料庫建立發行集的詳細資訊，請參閱 [從 Oracle 資料庫建立發行集](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
#### 建立發行集並定義發行項  
  
1.  連接到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]的發行者，然後展開伺服器節點。  
  
2.  展開 **複寫** 資料夾，然後再以滑鼠右鍵按一下 **本機發行集** 資料夾。  
  
3.  按一下 **[新增發行集]**。  
  
4.  遵循「新增發行集精靈」中的頁面，執行：  
  
    -   如果尚未在伺服器上設定散發，則請指定「散發者」。 如需有關如何設定散發的詳細資訊，請參閱 [設定發行與散發](../../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
         如果您指定在 **散發者** 發行者伺服器作為本身的散發者 （本機散發者），以及將伺服器不設定為散發者 」、 「 新增發行集精靈 」 會將伺服器設定的頁面。 您將在 **[快照集資料夾]** 頁面，為「散發者」指定預設快照集資料夾。 快照集資料夾只是指定為共用的目錄；讀取並寫入此資料夾的代理程式必須具有足夠的權限才能對其進行存取。 如需有關適當地設定資料夾的詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
         如果指定另一台伺服器扮演「散發者」角色，則必須在 **[管理密碼]** 頁面輸入密碼才能從「發行者」連接到「散發者」。 此密碼必須符合發行者於遠端散發者啟用時所指定的密碼。  
  
         如需詳細資訊，請參閱 [設定散發](../../../relational-databases/replication/configure-distribution.md)。  
  
    -   選擇發行集資料庫。  
  
    -   選取發行集類型。 如需詳細資訊，請參閱 [類型的複寫](../../../relational-databases/replication/types-of-replication.md)。  
  
    -   指定要發行的資料和資料庫物件；從資料表發行項選擇性地篩選資料行，並設定發行項屬性。  
  
    -   從資料表發行項中選擇性地篩選資料列。 如需詳細資訊，請參閱 [篩選已發佈資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
    -   設定「快照集代理程式」的排程。  
  
    -   指定下列複寫代理程式執行時使用的認證，並建立連接：  
  
         \- 所有發行集的快照集代理程式。  
  
         \- 記錄所有交易式發行集的讀取器代理程式。  
  
         \- 允許更新訂閱的交易式發行集的佇列讀取器代理程式。  
  
         如需相關資訊，請參閱 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 以及 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
    -   選擇性地編寫發行集的指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
    -   指定發行集的名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立發行集。 使用哪些預存程序取決於所要建立的發行集類型而定。  
  
#### 建立快照式或交易式發行集  
  
1.  在發行集資料庫的發行者，執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要啟用目前的資料庫使用快照式或交易式複寫的發行集。  
  
2.  如果是交易式發行集，請判斷發行集資料庫是否有記錄讀取器代理程式作業存在 (快照式發行集不需要這個步驟)。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 3。  
  
    -   如果您不確定是否記錄讀取器代理程式作業存在已發行的資料庫，執行 [sp_helplogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 在發行集資料庫上的 「 發行者 」。  
  
    -   如果結果集是空的，請建立記錄讀取器代理程式作業。 在 「 發行者 」 執行 [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 代理程式執行的 Windows 認證 **@job_name** 和 **@password**。 如果代理程式將使用 SQL Server 驗證連接到發行者時，您也必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 請繼續進行步驟 3。  
  
3.  在 「 發行者 」 執行 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定的發行集名稱 **@publication**, ，並針對 **@repl_freq** 參數，指定其值為 **快照集** 快照式發行集的值為 **連續** 交易式發行集。 指定任何其他發行集選項。 這樣會定義此發行集。  
  
    > [!NOTE]  
    >  發行集名稱不能包含下列字元：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  在 「 發行者 」 執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定發行集名稱，如步驟 3 中使用 **@publication** 和 Windows 認證的快照集代理程式執行 **@snapshot_job_name** 和 **@password**。 如果代理程式將使用 SQL Server 驗證連接到發行者時，您也必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
5.  將發行項加入至發行集。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
6.  啟動快照集代理程式作業來產生此發行集的初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
#### 建立合併式發行集  
  
1.  在 「 發行者 」 執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要啟用發行集使用合併式複寫的目前資料庫。  
  
2.  在發行集資料庫的發行者，執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 針對 **@publication** 指定發行集的名稱，並指定其他任何發行集選項。 這樣會定義此發行集。  
  
    > [!NOTE]  
    >  發行集名稱不能包含下列字元：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  在 「 發行者 」 執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定發行集名稱，如步驟 2 中使用 **@publication** 和 Windows 認證的快照集代理程式執行 **@snapshot_job_name** 和 **@password**。 如果代理程式將使用 SQL Server 驗證連接到發行者時，您也必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
4.  將發行項加入至發行集。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
5.  啟動快照集代理程式作業來產生此發行集的初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立交易式發行集。 指令碼變數是用來傳遞建立快照集代理程式作業和記錄讀取器代理程式作業所需的 Windows 認證。  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 此範例會建立合併式發行集。 指令碼變數是用來傳遞建立快照集代理程式作業所需的 Windows 認證。  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式建立發行集。 用來建立發行集的 RMO 類別，將取決於所建立的發行集類型而定。  
  
#### 建立快照式或交易式發行集  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別發行集資料庫中，設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 的執行個體的內容 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 從步驟 1，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 傳回 **false**, ，確認資料庫是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 屬性是 **false**, ，將它設定為 **true**。  
  
4.  交易式發行集，檢查的值 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> 屬性。 如果這個屬性為 **true**，則表示記錄讀取器代理程式作業已存在此資料庫中。 如果這個屬性為 **false**，請執行下列動作：  
  
    -   設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶下執行 「 記錄讀取器代理程式。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> 建立發行集的成員時，就不需要 **sysadmin** 固定的伺服器角色。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> 使用 SQL Server 驗證連接到 「 發行者 」 時。  
  
    -   呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> 方法來建立資料庫的記錄讀取器代理程式作業。  
  
5.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別，並設定此物件的下列屬性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   針對已發行的資料庫名稱 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   發行集的名稱 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -   A <xref:Microsoft.SqlServer.Replication.PublicationType> 的 <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> 或 <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 提供快照集代理程式所執行的 Windows 帳戶的認證。 當快照集代理程式要連接本機散發者及進行任何遠端連接 (使用 Windows 驗證) 時，也會使用此帳戶。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 建立發行集的成員時，就不需要 **sysadmin** 固定的伺服器角色。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性） <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> 使用 SQL Server 驗證連接到 「 發行者 」 時。  
  
    -   （選擇性）使用包含的邏輯 OR 運算子 (**|** Visual C# 中和 **或者** Visual Basic 中) 和排除的邏輯 OR 運算子 (**^** Visual C# 和 **Xor** Visual Basic 中) 來設定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。  
  
    -   （選擇性）發行者名稱 <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> 當發行者為非 SQL Server 發行者。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有屬性的值來設定發行者時包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，傳送到 「 散發者 」，以純文字。 您應該先加密 「 發行者 」 之前，先呼叫其遠端散發者之間連接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法來建立發行集的快照集代理程式作業。  
  
#### 建立合併式發行集  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別發行集資料庫中，設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 的執行個體的內容 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 從步驟 1，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 傳回 **false**, ，確認資料庫是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 屬性是 **false**, ，將它設定為 **true**, ，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別，並設定此物件的下列屬性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   針對已發行的資料庫名稱 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   發行集的名稱 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 提供快照集代理程式所執行的 Windows 帳戶的認證。 當快照集代理程式要連接本機散發者及進行任何遠端連接 (使用 Windows 驗證) 時，也會使用此帳戶。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 建立發行集的成員時，就不需要 **sysadmin** 固定的伺服器角色。 如需相關資訊，請參閱 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （選擇性）使用包含的邏輯 OR 運算子 (**|** Visual C# 中和 **或者** Visual Basic 中) 和排除的邏輯 OR 運算子 (**^** Visual C# 和 **Xor** Visual Basic 中) 來設定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有屬性的值來設定發行者時包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，傳送到 「 散發者 」，以純文字。 您應該先加密 「 發行者 」 之前，先呼叫其遠端散發者之間連接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法來建立發行集的快照集代理程式作業。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會針對交易式發行啟用 AdventureWorks 資料庫、定義記錄讀取器代理程式作業，並建立 AdvWorksProductTran 發行集。 必須為此發行集定義發行項。 建立記錄讀取器代理程式作業和快照集代理程式作業所需的 Windows 帳戶認證是在執行階段所傳遞。 若要了解如何使用 RMO 來定義快照發行項和交易式發行項，請參閱＜ [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)＞。  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 此範例會針對合併發行啟用 AdventureWorks 資料庫，並建立 AdvWorksSalesOrdersMerge 發行集。 仍然必須為此發行集定義發行項。 建立快照集代理程式作業所需的 Windows 帳戶認證是在執行階段所傳遞。 若要了解如何使用 RMO 來定義合併發行項，請參閱＜ [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)＞。  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## 另請參閱  
 [以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Management Objects 概念。](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)   
 [檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [設定散發](../../../relational-databases/replication/configure-distribution.md)   
 [保護散發者](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  