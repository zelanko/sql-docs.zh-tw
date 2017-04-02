---
title: "指定合併發行項的互動式衝突解決方法 | Microsoft Docs"
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
  - "合併式複寫衝突解決 [SQL Server 複寫]，互動解析程式"
  - "互動式衝突解決 [SQL Server 複寫]"
  - "發行項 [SQL Server 複寫], 衝突解決"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 指定合併發行項的互動式衝突解決方法
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中針對合併發行項指定互動式衝突解決方法。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫提供互動式解決器，可讓您在視同步處理期間手動解決衝突 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager。 在啟用互動式解決方案之後，在同步處理期間會使用「互動解決器」以互動方式解決衝突。 互動解決器可以從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱 [同步處理訂用帳戶使用 Windows Synchronization Manager & #40。Windows Synchronization Manager & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要指定合併發行項的互動式衝突解決方法，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   如果是在 Windows Synchronization Manager 之外執行同步處理 (如 SQL Server Management Studio 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會使用針對發行項指定的預設衝突解決方式來自動解決衝突。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要啟用發行項的互動式衝突解決方案  
  
1.  在 **文章** 新增發行集精靈 」 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取的資料表。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 **發行項屬性-\< 發行項>** 或 **發行項屬性-\< l>** 頁面上，按一下 **解析程式** ] 索引標籤。  
  
4.  選取 **允許視需要同步期間以互動方式解決衝突的訂閱者**。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要指定訂閱應使用互動式衝突解決方案  
  
1.  在 **訂閱屬性-\< 訂閱者>: \< u>** 對話方塊方塊中，指定其值為 **True** 的 **以互動方式解決衝突** 選項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以透過程式設計方式指定在建立合併式發行集的提取訂閱時，訂閱者將使用此圖形化介面來解決發行項衝突。 只有支援此選項之發行項中的衝突才會顯示在互動式解決器中。  
  
#### 建立使用互動式解決器的合併式提取訂閱  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，並指定 **@publication**。 記下的值 **allow_interactive_resolver** 每個發行項中的結果集將會使用互動式解析程式。  
  
    -   如果這個值是 **1**，將會使用互動式解決器。  
  
    -   如果這個值是 **0**，您必須先針對每一個發行項啟用互動式解決器。 若要這樣做，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，並指定 **@publication**, ，**@article**, ，值為 **allow_interactive_resolver** 的 **@property**, ，而值為 **true** 的 **@value**。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
3.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), ，指定下列參數︰  
  
    -   **@publisher**, ，**@publisher_db** （已發行的資料庫），和 **@publication**。  
  
    -   值為 **true** 的 **@enabled_for_syncmgr**。  
  
    -   值為 **true** 的 **@use_interactive_resolver**。  
  
    -   合併代理程式所需的安全性帳戶資訊。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
4.  在發行集資料庫的發行者，執行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。  
  
#### 定義支援互動式解決器的發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, ，且值為 **true** 的 **@allow_interactive_resolver**。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 另請參閱  
 [檢視並解決資料衝突的合併式發行集與 #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [互動式衝突解決](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  