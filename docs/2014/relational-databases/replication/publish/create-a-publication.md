---
title: 建立發行集 | Microsoft 文件
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
- adding articles
- articles [SQL Server replication], adding
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ce1f698224a7e1938ac30e94565033e3c32f5c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195568"
---
# <a name="create-a-publication"></a>建立發行集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來建立 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的發行集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要建立發行集並定義發行項，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   發行集與發行項名稱不能包含下列任何字元：%、\*、[、]、|、:、"、? '、 \、 /、 \< ，>。 如果資料庫中的物件包含這些字元的任何一個，而且您要複寫它們，則必須指定一個不同於 [發行項屬性 - \<發行項>] 對話方塊中之物件名稱的發行項名稱，您可以從精靈的 [發行項] 頁面存取此對話方塊。  
  
###  <a name="Security"></a> 安全性  
 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」建立發行集並定義發行項。 建立發行集之後，您可以在 [發行集屬性 - \<發行集>] 對話方塊中，檢視及修改發行集屬性。 如需從 Oracle 資料庫建立發行集的詳細資訊，請參閱[從 Oracle 資料庫建立發行集](create-a-publication-from-an-oracle-database.md)。  
  
#### <a name="to-create-a-publication-and-define-articles"></a>建立發行集並定義發行項  
  
1.  連接到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後以滑鼠右鍵按一下 **[本機發行集]** 資料夾。  
  
3.  按一下 **[新增發行集]**。  
  
4.  遵循「新增發行集精靈」中的頁面，執行：  
  
    -   如果尚未在伺服器上設定散發，則請指定「散發者」。 如需設定散發的詳細資訊，請參閱[設定發行和散發](../configure-publishing-and-distribution.md)。  
  
         如果在 **[散發者]** 頁面指定「發行者」伺服器做為自己的「散發者」(本機散發者)，而不將伺服器設定為「散發者」，則「新增發行集精靈」會設定該伺服器。 您將在 **[快照集資料夾]** 頁面，為「散發者」指定預設快照集資料夾。 快照集資料夾只是指定為共用的目錄；讀取並寫入此資料夾的代理程式必須具有足夠的權限才能對其進行存取。 如需適當地保護資料夾的詳細資訊，請參閱[保護快照集資料夾](../security/secure-the-snapshot-folder.md)。  
  
         如果指定另一台伺服器扮演「散發者」角色，則必須在 **[管理密碼]** 頁面輸入密碼才能從「發行者」連接到「散發者」。 此密碼必須符合發行者於遠端散發者啟用時所指定的密碼。  
  
         如需詳細資訊，請參閱 [Configure Distribution](../configure-distribution.md)＞。  
  
    -   選擇發行集資料庫。  
  
    -   選取發行集類型。 如需詳細資訊，請參閱[複寫類型](../types-of-replication.md)。  
  
    -   指定要發行的資料和資料庫物件；從資料表發行項選擇性地篩選資料行，並設定發行項屬性。  
  
    -   從資料表發行項中選擇性地篩選資料列。 如需詳細資訊，請參閱[篩選發行的資料](filter-published-data.md)。  
  
    -   設定「快照集代理程式」的排程。  
  
    -   指定下列複寫代理程式執行時使用的認證，並建立連接：  
  
         \- 快照集代理程式 (針對所有發行集)。  
  
         \- 記錄讀取器代理程式 (針對所有交易式發行集)。  
  
         \- 佇列讀取器代理程式 (針對允許更新訂閱的交易式發行集)。  
  
         如需相關資訊，請參閱 [Replication Agent Security Model](../security/replication-agent-security-model.md) 以及 [Replication Security Best Practices](../security/replication-security-best-practices.md)。  
  
    -   選擇性地編寫發行集的指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../scripting-replication.md)。  
  
    -   指定發行集的名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式建立發行集。 使用哪些預存程序取決於所要建立的發行集類型而定。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>建立快照式或交易式發行集  
  
1.  在發行集資料庫的發行者端執行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)，以便使用快照式或異動複寫來啟用目前資料庫的發行集。  
  
2.  如果是交易式發行集，請判斷發行集資料庫是否有記錄讀取器代理程式作業存在 (快照式發行集不需要這個步驟)。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 3。  
  
    -   如果您不確定發行的資料庫是否有記錄讀取器代理程式作業存在，請在發行集資料庫的發行者端執行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)。  
  
    -   如果結果集是空的，請建立記錄讀取器代理程式作業。 在發行者端，執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 針對 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] @job_name **@job_name** @password **@password**中啟用交易式發行集的訂閱更新。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 **@publisher_login** 以及 **@publisher_password**＞。 請繼續進行步驟 3。  
  
3.  在發行者端，執行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 指定的發行集名稱**@publication**，並針對**@repl_freq**參數，指定其值為`snapshot`的值或快照式發行集`continuous`的交易式發行集。 指定任何其他發行集選項。 這樣會定義此發行集。  
  
    > [!NOTE]  
    >  發行集名稱不能包含下列字元：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 為 **@publication** 指定步驟 2 中所使用的發行集名稱，以及針對 **@snapshot_job_name** @password **@password**中啟用交易式發行集的訂閱更新。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 **@publisher_login** @password **@publisher_password**中啟用交易式發行集的訂閱更新。 這麼做會為發行集建立快照集代理程式作業。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
5.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
6.  啟動快照集代理程式作業來產生此發行集的初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
#### <a name="to-create-a-merge-publication"></a>建立合併式發行集  
  
1.  在發行者端執行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)，以便使用合併式複寫來啟用目前資料庫的發行集。  
  
2.  在發行集資料庫的發行者端，執行 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 針對 **@publication** 指定發行集的名稱，並指定其他任何發行集選項。 這樣會定義此發行集。  
  
    > [!NOTE]  
    >  發行集名稱不能包含下列字元：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 為 **@publication** 指定步驟 3 中所使用的發行集名稱，以及快照集代理程式針對 **@snapshot_job_name** 以及 **@password**＞。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 **@publisher_login** @password **@publisher_password**中啟用交易式發行集的訂閱更新。 這麼做會為發行集建立快照集代理程式作業。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
4.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
5.  啟動快照集代理程式作業來產生此發行集的初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 此範例會建立交易式發行集。 指令碼變數是用來傳遞建立快照集代理程式作業和記錄讀取器代理程式作業所需的 Windows 認證。  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranpub)]  
  
 此範例會建立合併式發行集。 指令碼變數是用來傳遞建立快照集代理程式作業所需的 Windows 認證。  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergepub)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式建立發行集。 用來建立發行集的 RMO 類別，將取決於所建立的發行集類型而定。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>建立快照式或交易式發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別以建立連線至發行者。  
  
2.  為發行集資料庫建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體、將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 執行個體，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果<xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>傳回`false`，確認此資料庫確實存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 屬性為 `false`，請將它設定為 `true`。  
  
4.  如果是交易式發行集，請檢查 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> 屬性的值。 如果此屬性為`true`，記錄讀取器代理程式作業已存在這個資料庫。 如果此屬性為`false`，執行下列動作：  
  
    -   設定<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A>並<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A>或<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A>的欄位<xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A>提供的認證[!INCLUDE[msCoName](../../../includes/msconame-md.md)]執行記錄讀取器代理程式的 Windows 帳戶。  
  
        > [!NOTE]  
        >  設定<xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A>的成員所建立的發行集時不需`sysadmin`固定的伺服器角色。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](../security/replication-agent-security-model.md)。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「發行者」時，設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> ) 欄位。  
  
    -   呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> 方法來為資料庫建立記錄讀取器代理程式作業。  
  
5.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體，並為此物件設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設定為步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>設為發行的資料庫名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 的發行集名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationType> 或 <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> 的 <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位，以提供執行快照集代理程式所使用之 Windows 帳戶的認證。 當快照集代理程式要連接本機散發者及進行任何遠端連接 (使用 Windows 驗證) 時，也會使用此帳戶。  
  
        > [!NOTE]  
        >  設定<xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>的成員所建立的發行集時不需`sysadmin`固定的伺服器角色。 在這種情況下，代理程式會模擬「SQL Server Agent」帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](../security/replication-agent-security-model.md)。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到發行者時，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (或 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> ) 欄位。  
  
    -   (選擇性) 使用包含的邏輯 OR 運算子 (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`)，並使用排除的邏輯 OR 運算子 (Visual C# 中的 `^` 和 Visual Basic 中的 `Xor`)，為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 屬性設定 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 值。  
  
    -   (選擇性) 當散發者為非 SQL Server 散發者時，將 <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> 設定為散發者的名稱。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有屬性的值 (包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連線，然後再呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法來為發行集建立快照集代理程式作業。  
  
#### <a name="to-create-a-merge-publication"></a>建立合併式發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  為發行集資料庫建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體、將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 執行個體，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果<xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>傳回`false`，確認此資料庫確實存在。  
  
3.  如果<xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A>屬性是`false`，將它設定為`true`，並呼叫<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體，並為此物件設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設定為步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>設為發行的資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>設定為發行集名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 欄位，可提供執行快照集代理程式所使用之 Windows 帳戶的認證。 當快照集代理程式要連接本機散發者及進行任何遠端連接 (使用 Windows 驗證) 時，也會使用此帳戶。  
  
        > [!NOTE]  
        >  設定<xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>的成員所建立的發行集時不需`sysadmin`固定的伺服器角色。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](../security/replication-agent-security-model.md)。  
  
    -   (選擇性) 使用包含的邏輯 OR 運算子 (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`)，並使用排除的邏輯 OR 運算子 (Visual C# 中的 `^` 和 Visual Basic 中的 `Xor`)，為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 屬性設定 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 值。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有屬性的值 (包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連線，然後再呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法來為發行集建立快照集代理程式作業。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會針對交易式發行啟用 AdventureWorks 資料庫、定義記錄讀取器代理程式作業，並建立 AdvWorksProductTran 發行集。 必須為此發行集定義發行項。 建立記錄讀取器代理程式作業和快照集代理程式作業所需的 Windows 帳戶認證是在執行階段所傳遞。 若要了解如何使用 RMO 來定義快照發行項和交易式發行項，請參閱＜ [Define an Article](define-an-article.md)＞。  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 此範例會針對合併發行啟用 AdventureWorks 資料庫，並建立 AdvWorksSalesOrdersMerge 發行集。 仍然必須為此發行集定義發行項。 建立快照集代理程式作業所需的 Windows 帳戶認證是在執行階段所傳遞。 若要了解如何使用 RMO 來定義合併發行項，請參閱＜ [Define an Article](define-an-article.md)＞。  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## <a name="see-also"></a>另請參閱  
 [以指令碼變數使用 sqlcmd](../../scripting/sqlcmd-use-with-scripting-variables.md)   
 [發行資料和資料庫物件](publish-data-and-database-objects.md)   
 [Replication Management Objects Concepts](../concepts/replication-management-objects-concepts.md)   
 [Define an Article](define-an-article.md)   
 [檢視及修改發行集屬性](view-and-modify-publication-properties.md)   
 [[設定散發]](../configure-distribution.md)   
 [保護散發者](../security/secure-the-distributor.md)   
 [保護發行者](../security/secure-the-publisher.md)  
  
  
