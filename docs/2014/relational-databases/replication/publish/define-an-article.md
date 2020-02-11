---
title: 定義發行項 | Microsoft 文件
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], defining
- sp_addmergearticle
- adding articles
- sp_addarticle
- articles [SQL Server replication], adding
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65512a212290db4cc9a470402e2ae75175c23cb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73882311"
---
# <a name="define-an-article"></a>定義發行項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義發行項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列專案定義發行項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   發行項名稱不能包含下列任何字元：% , * , [ , ] , | , : , " , ? 、'、\、/、 \< >。 如果資料庫中的物件包含這些字元的任何一個，而且您要複寫它們，則必須指定一個不同於物件名稱的發行項名稱。  
  
##  <a name="Security"></a> Security  
 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」建立發行集並定義發行項。 建立發行集之後，您可以在 [發行集屬性 - **發行集>]\<** 對話方塊中，檢視及修改發行集屬性。 如需從 Oracle 資料庫建立發行集的詳細資訊，請參閱[從 Oracle 資料庫建立發行集](create-a-publication-from-an-oracle-database.md)。  
  
#### <a name="to-create-a-publication-and-define-articles"></a>建立發行集並定義發行項  
  
1.  連接到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
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
 在建立發行集之後，可以使用複寫預存程序來以程式設計的方式建立發行項。 要使用哪些預存程序來建立發行項，將取決於定義此發行項的發行集類型而定。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-define-an-article-for-a-snapshot-or-transactional-publication"></a>為快照式或交易式發行集定義發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 指定** \@發行項**所屬的發行集名稱、發行** \@項的名稱、針對** ** \@source_object**發行的資料庫物件，以及任何其他選擇性參數。 使用** \@source_owner**來指定物件的架構擁有權（如果不是**dbo**）。 如果發行項不是以記錄為基礎的資料表發行項，請指定** \@類型**的發行項類型。如需詳細資訊，請參閱[ 指定發行項類型 &#40;複寫 transact-sql 程式設計&#41;](specify-article-types-replication-transact-sql-programming.md)。  
  
2.  若要以水平方式篩選資料表中的資料列或是檢視發行項，請使用 [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) 來定義篩選子句。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
3.  若要以垂直方式篩選資料表中的資料行或是檢視發行項，請使用 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
4.  如果發行項已經過篩選，請執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) 。  
  
5.  如果發行集有現有的訂閱，而且 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) 在 **immediate_sync** 資料行中傳回 **0** 的值，您就必須呼叫 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) ，將此發行項加入到每一個現有的訂閱中。  
  
6.  如果發行集有現有的提取訂閱，請在發行者上執行 [sp_refreshsubscriptions](/sql/relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql) ，針對只包含新發行項的現有提取訂閱建立新的快照集。  
  
    > [!NOTE]  
    >  如果是未使用快照集初始化的訂閱，您就不需要執行 [sp_refreshsubscriptions](/sql/relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql) ，因為這個程序是由 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)所執行。  
  
#### <a name="to-define-an-article-for-a-merge-publication"></a>為合併式發行集定義發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 針對** \@發行**集指定發行集的名稱、發行項的** \@** 發行項名稱，以及要為** \@source_object**發佈的物件。 若要以水準方式篩選資料表資料列，請指定** \@subset_filterclause**的值。 如需相關資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) 以及 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。 如果發行項不是資料表發行項，請指定** \@類型**的發行項類型。 如需詳細資訊，請參閱[指定發行項類型 &#40;複寫 Transact-SQL 程式設計&#41;](specify-article-types-replication-transact-sql-programming.md)。  
  
2.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) ，以定義兩個發行項之間的聯結篩選。 如需詳細資訊，請參閱 [定義和修改合併發行項之間的聯結篩選](define-and-modify-a-join-filter-between-merge-articles.md)。  
  
3.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) ，以篩選資料表資料行。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例是根據交易式發行集的 `Product` 資料表來定義發行項，其中會以水平和垂直方式篩選發行項。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 此範例會定義合併式發行集的發行項，其中的 `SalesOrderHeader` 發行項是根據 **SalesPersonID**進行靜態篩選，而 `SalesOrderDetail` 發行項則是根據 `SalesOrderHeader`進行聯結篩選。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式定義發行項。 用於定義發行項的 RMO 類別，將取決於定義發行項的發行集類型而定。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 下列範例會將具有資料列篩選和資料行篩選的發行項加入交易式發行集中。  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 下列範例會將三個發行項加入合併式發行集中。 這些發行項具有資料行篩選，而且會使用兩個聯結篩選將參數化資料列篩選器列傳播至其他發行項。  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](create-a-publication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [在現有發行集中加入和卸載發行項](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [篩選發行的資料](filter-published-data.md)   
 [發行資料和資料庫物件](publish-data-and-database-objects.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
