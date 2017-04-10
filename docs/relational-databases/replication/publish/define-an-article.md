---
title: "定義發行項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "發行項 [SQL Server 複寫], 定義"
  - "sp_addmergearticle"
  - "加入發行項"
  - "sp_addarticle"
  - "發行項 [SQL Server 複寫], 加入"
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 定義發行項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中定義發行項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要定義發行項，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   發行項名稱不能包含下列任何字元：% , * , [ , ] , | , : , " , ? 、'、\、/、\<、>。 如果資料庫中的物件包含這些字元的任何一個，而且您要複寫它們，則必須指定一個不同於物件名稱的發行項名稱。  
  
##  <a name="Security"></a> 安全性  
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
 在建立發行集之後，可以使用複寫預存程序來以程式設計的方式建立發行項。 要使用哪些預存程序來建立發行項，將取決於定義此發行項的發行集類型而定。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 為快照式或交易式發行集定義發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, ，及其他選用的參數。 使用 **@source_owner** 如果未指定結構描述物件的擁有權， **dbo**。 如果發行項不是記錄檔為基礎的資料表發行項，指定的發行項類型 **@type**; 如需詳細資訊，請參閱 [指定發行項類型 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md)。  
  
2.  若要水平篩選的資料表資料列，或是檢視發行項，請使用 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 來定義篩選子句。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  若要以垂直方式篩選資料表的資料行，或是檢視發行項，請使用 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
4.  執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 如果篩選發行項。  
  
5.  如果發行集有現有的訂閱和 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 傳回值的 **0** 中 **immediate_sync** 資料行中，您必須呼叫 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 加入至每個現有的訂閱的發行項。  
  
6.  如果發行集現有的提取訂閱，請執行 [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) 在 「 發行者 」 來建立新的快照集現有的提取訂閱，其中包含新的文章。  
  
    > [!NOTE]  
    >  不會使用快照集初始化的訂閱，您不需要執行 [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) ，來執行此程序 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
#### 為合併式發行集定義發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定的發行集名稱 **@publication**, ，發行項名稱的名稱 **@article**, ，發行的物件和 **@source_object**。 若要水平篩選資料表的資料列，指定的值 **@subset_filterclause**。 如需相關資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) 以及 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。 如果此發行項不是資料表發行項，請為 **@type**指定發行項類型。 如需詳細資訊，請參閱 [指定發行項類型 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md)。  
  
2.  （選擇性）在發行集資料庫的發行者，執行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 來定義兩個發行項之間的聯結篩選。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
3.  （選擇性）在發行集資料庫的發行者，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 篩選資料表資料行。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例是根據交易式發行集的 `Product` 資料表來定義發行項，其中會以水平和垂直方式篩選發行項。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 此範例會定義合併式發行集的發行項，其中的 `SalesOrderHeader` 發行項是根據 **SalesPersonID**進行靜態篩選，而 `SalesOrderDetail` 發行項則是根據 `SalesOrderHeader`進行聯結篩選。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式定義發行項。 用於定義發行項的 RMO 類別，將取決於定義發行項的發行集類型而定。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 下列範例會將具有資料列篩選和資料行篩選的發行項加入交易式發行集中。  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 下列範例會將三個發行項加入合併式發行集中。 這些發行項具有資料行篩選，而且會使用兩個聯結篩選將參數化資料列篩選器列傳播至其他發行項。  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## 另請參閱  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [在現有發行集中加入和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  