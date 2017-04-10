---
title: "設定發行和散發 | Microsoft Docs"
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
  - "複寫 [SQL Server], 散發"
  - "散發組態 [SQL Server 複寫]"
  - "發行 [SQL Server 複寫], 設定"
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 設定發行和散發
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定發行和散發。  
  

##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
 如需詳細資訊，請參閱[安全的部署 &#40;Replication&#41;](../../relational-databases/replication/security/secure-deployment-replication.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」或「設定散發精靈」來設定散發。 設定「散發者」後，檢視並修改在 [散發者屬性 - \<散發者>] 對話方塊中的屬性。 如果您想設定「散發者」以便 **db_owner** 固定資料庫角色的成員可以建立發行集，或者因為您想設定非「發行者」的遠端「散發者」，則請使用「設定散發精靈」。  
  
#### 若要設定散發  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到將成為「散發者」的伺服器 (在許多情況下，「發行者」與「散發者」是同一個伺服器)，然後展開伺服器節點。  
  
2.  在以滑鼠右鍵按一下 [複寫] 資料夾，然後按一下 [設定散發]。  
  
3.  遵循「設定散發精靈」的指示執行下列項目：  
  
    -   選取「散發者」。 若要使用本機「散發者」，請選取 ['\<伺服器名稱>' 將扮演本身的散發者; SQL Server 將建立散發資料庫和記錄]。 若要使用遠端散發者，請選取 **[使用下列伺服器做為散發者]**，然後選取伺服器。 伺服器必須已設定為散發者，且必須先啟用發行者才能使用散發者。 如需詳細資訊，請參閱[在散發者端啟用遠端發行者 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md)。  
  
         如果您選取遠端「散發者」，則必須在 **[管理密碼]** 頁面上輸入密碼才能從「發行者」連接到「散發者」。 此密碼必須符合發行者於遠端散發者啟用時所指定的密碼。  
  
    -   指定根快照集資料夾 (針對本機「散發者」)。 快照集資料夾只是指定為共用的目錄；讀取並寫入此資料夾的代理程式必須具有足夠的權限才能對其進行存取。 使用此「散發者」的每個「發行者」在根資料夾下建立資料夾，每個發行集在要儲存快照集檔案的「發行者」資料夾下建立資料夾。 如需適當設定資料夾安全性的詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
    -   指定散發資料庫 (針對本機「散發者」)。 散發資料庫為異動複寫中所有類型的複寫與交易，儲存中繼資料和歷程資料。  
  
    -   選擇性地啟用其他「發行者」來使用「散發者」。 如果啟用其他「發行者」來使用「散發者」，則必須在 **[散發者密碼]** 頁面上輸入密碼才能從這些「發行者」連接到「散發者」。  
  
    -   選擇性地編寫組態設定的指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../relational-databases/replication/scripting-replication.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式設定複寫發行和散發。  
  
#### 使用本機散發者設定發行  
  
1.  請執行 [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) 來判斷伺服器是否已經設定為散發者。  
  
    -   如果結果集中 **installed** 的值是 **0**，請在 master 資料庫的散發者上執行 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)。  
  
    -   如果結果集中 **distribution db installed** 的值是 **0**，請在 master 資料庫的散發者上執行 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)。 針對 **@database**指定散發資料庫的名稱。 您可以選擇針對 **@max_distretention** 指定最大交易保留期限，並針對 **@history_retention** 指定記錄保留期限。 如果正在建立新的資料庫，請指定所要的資料庫屬性參數。  
  
2.  在散發者 (也是發行者) 上，執行 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)，針對 **@working_directory** 指定將當做預設快照集資料夾使用的 UNC 共用。  
  
3.  在發行者上，執行 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 針對 **@dbname**指定發行的資料庫、針對 **@optname**指定複寫的類型，並針對 **@value** 指定 **true**的值。  
  
#### 使用遠端散發者設定發行  
  
1.  請執行 [sp_get_distributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md) 來判斷伺服器是否已經設定為散發者。  
  
    -   如果結果集中 **installed** 的值是 **0**，請在 master 資料庫的散發者上執行 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)。 針對 **@password**指定增強式密碼。 **distributor_admin** 帳戶的這個密碼將會由發行者連接到散發者時使用。  
  
    -   如果結果集中 **distribution db installed** 的值是 **0**，請在 master 資料庫的散發者上執行 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)。 針對 **@database**指定散發資料庫的名稱。 您可以選擇針對 **@max_distretention** 指定最大交易保留期限，並針對 **@history_retention** 指定記錄保留期限。 如果正在建立新的資料庫，請指定所要的資料庫屬性參數。  
  
2.  在散發者上，執行 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)，針對 **@working_directory** 指定將當做預設快照集資料夾使用的 UNC 共用。 如果散發者會在與發行者連接時使用「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，則也必須針對 **@security_mode** 指定值 **0**，並針對 **@login** 和 **@password** 指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊。  
  
3.  在 master 資料庫的發行者上，執行 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)。 針對 **@password**指定步驟 1 中所使用的增強式密碼。 這個密碼將會由發行者連接到散發者時使用。  
  
4.  在發行者上，執行 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 針對 **@dbname**指定發行的資料庫、針對 **@optname**指定複寫的類型，並針對 **@value**指定 true 的值。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會示範如何以程式設計方式設定發行和散發。 在此範例中，會使用指令碼變數來提供設定為發行者和本機散發者的伺服器名稱。 您可以使用複寫預存程序來以程式設計的方式設定複寫發行和散發。  
  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/configure-publishing-and_1.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
#### 在單一伺服器上設定發行和散發  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與伺服器的連接。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別。 傳遞步驟 1 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。  
  
3.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 類別。  
  
4.  設定 <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 屬性為資料庫名稱並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中。  
  
5.  安裝散發者呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法。 傳遞 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 步驟 3 中的物件。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 類別。  
  
7.  設定下列屬性的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> -發行者的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> -步驟 5 中建立資料庫的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> -用來存取快照集檔案的共用。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> -連接到發行者時使用的安全性模式。 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 建議。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 方法。  
  
#### 使用遠端散發者設定發行和散發  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與遠端散發者伺服器的連接。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別。 傳遞步驟 1 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。  
  
3.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 類別。  
  
4.  設定 <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 屬性為資料庫名稱，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中。  
  
5.  安裝散發者呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法。 指定安全密碼 （由發行者連接到遠端散發者時） 和 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 步驟 3 中的物件。 如需詳細資訊，請參閱[保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
    > **重要！！** 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 類別。  
  
7.  設定下列屬性的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> -本機發行者伺服器的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> -步驟 5 中建立資料庫的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> -用來存取快照集檔案的共用。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> -連接到發行者時使用的安全性模式。 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 建議。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 方法。  
  
9. 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與本機發行者伺服器的連接。  
  
10. 建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別。 傳遞步驟 9 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。  
  
11. 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法。 傳遞遠端散發者的名稱以及步驟 5 中指定之遠端散發者的密碼。  
  
    > **重要！！**  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 Windows .NET Framework 提供的 [密碼編譯服務](http://go.microsoft.com/fwlink/?LinkId=34733) 。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式設定複寫發行和散發。  
  
 [!code-csharp[HowTo#rmo_AddDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## 另請參閱  
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [複寫系統預存程序概念](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects 概念。](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [設定 AlwaysOn 可用性群組的複寫 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
  