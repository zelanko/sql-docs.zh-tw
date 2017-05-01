---
title: "指定合併發行項的互動式衝突解決方法 | Microsoft Docs"
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
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d488371a34cefb0ecf73824e362137243c115926
ms.lasthandoff: 04/11/2017

---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>指定合併發行項的互動式衝突解決方法
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中針對合併發行項指定互動式衝突解決方法。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replication provides an Interactive Resolver, which allows you to resolve conflicts manually during on-demand synchronization in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager. 在啟用互動式解決方案之後，在同步處理期間會使用「互動解決器」以互動方式解決衝突。 互動解決器可以從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱[使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要指定合併發行項的互動式衝突解決方法，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   如果是在 Windows Synchronization Manager 之外執行同步處理 (如 SQL Server Management Studio 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會使用針對發行項指定的預設衝突解決方式來自動解決衝突。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>若要啟用發行項的互動式衝突解決方案  
  
1.  在 [新增發行集精靈] 的 [發行項] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊中，選取一個資料表。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 [發行項屬性 - \<發行項>] 或 [發行項屬性 - \<發行項類型>] 頁面上，按一下 [解析程式] 索引標籤。  
  
4.  選取 **[允許訂閱者在依要求同步期間，以互動方式解決衝突]**。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 儲存並關閉對話方塊。  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>若要指定訂閱應使用互動式衝突解決方案  
  
1.  在 [訂閱屬性 - \<訂閱者>: \<訂閱資料庫>] 對話方塊方塊中，將 [以互動方式解決衝突] 選項的值指定為 **True**。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以透過程式設計方式指定在建立合併式發行集的提取訂閱時，訂閱者將使用此圖形化介面來解決發行項衝突。 只有支援此選項之發行項中的衝突才會顯示在互動式解決器中。  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>建立使用互動式解決器的合併式提取訂閱  
  
1.  在發行集資料庫的發行者上執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)，指定 **@publication**中針對合併發行項指定互動式衝突解決方法。 請記下結果集中每一個發行項的 **allow_interactive_resolver** 值 (互動式解決器將針對它來使用)。  
  
    -   如果這個值是 **1**，將會使用互動式解決器。  
  
    -   如果這個值是 **0**，您必須先針對每一個發行項啟用互動式解決器。 若要這樣做，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，指定 **@publication**、 **@article**，並針對 **allow_interactive_resolver** 指定 **@property**的值及針對 **true** 指定 **@value**中針對合併發行項指定互動式衝突解決方法。  
  
2.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
3.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)並指定下列參數：  
  
    -   **@publisher**、 **@publisher_db** (發行的資料庫) 和 **@publication**中針對合併發行項指定互動式衝突解決方法。  
  
    -   為 **true** 指定 **@enabled_for_syncmgr**中針對合併發行項指定互動式衝突解決方法。  
  
    -   為 **true** 指定 **@use_interactive_resolver**中針對合併發行項指定互動式衝突解決方法。  
  
    -   合併代理程式所需的安全性帳戶資訊。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
4.  在發行集資料庫的發行者上，執行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>定義支援互動式解決器的發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 針對 **@publication**指定發行項所屬的發行集名稱、針對 **@article**指定發行項名稱、針對 **@source_object**的值及針對 **true** 指定 **@allow_interactive_resolver**中針對合併發行項指定互動式衝突解決方法。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
