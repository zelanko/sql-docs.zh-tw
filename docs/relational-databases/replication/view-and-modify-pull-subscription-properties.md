---
title: "檢視及修改提取訂閱屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "修改訂閱"
  - "檢視複寫屬性"
  - "修改複寫屬性, 提取訂閱"
  - "提取訂閱 [SQL Server 複寫], 修改"
  - "訂閱 [SQL Server 複寫], 提取"
  - "提取訂閱 [SQL Server 複寫], 屬性"
  - "修改訂閱, SQL Server Management Studio"
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 檢視及修改提取訂閱屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中檢視及修改提取訂閱屬性。  
  
 **本主題內容**  
  
-   **若要檢視及修改提取訂閱屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 檢視從 「 發行者 」 或 「 訂閱者 」 中的提取訂閱屬性 **訂閱屬性-\< 發行者>: \< u>** 對話方塊中，可從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 「訂閱者」可看見更多屬性，而屬性可於「訂閱者」端修改。 您也可以從 **[所有訂閱]** 索引標籤上的「發行者」檢視屬性，該索引標籤位於「複寫監視器」中。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
#### 從 Management Studio 中的發行者檢視提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  依序展開適當的發行集，訂閱中，按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  檢視屬性，然後按一下 **[確定]**。  
  
#### 從 Management Studio 中的訂閱者檢視和修改提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  訂閱中，按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
#### 從複寫監視器中的發行者檢視提取訂閱屬性  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  訂閱中，按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  檢視屬性，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改提取訂閱及存取其屬性。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### 檢視快照式或交易式發行集之提取訂閱的屬性  
  
1.  在 「 訂閱者 」 執行 [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 這樣會傳回儲存於訂閱者上之系統資料表內的訂閱相關資訊。  
  
2.  在 「 訂閱者 」 執行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，和下列其中一個值 **@publication_type**:  
  
    -   **0** -訂閱屬於交易式發行集。  
  
    -   **1** -訂閱屬於快照式發行集。  
  
3.  在 「 發行者 」 執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。  
  
4.  在 「 發行者 」 執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，並指定 **@subscriber**。 這樣會顯示與訂閱者有關的資訊。  
  
#### 變更快照式或交易式發行集之提取訂閱的屬性  
  
1.  在 「 訂閱者 」 執行 [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，並指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，值的其中一個 **0** （交易式） 或 **1** （快照） 的 **@publication_type**, 、 訂閱屬性變更為 **@property**, ，和新的值，如 **@value**。  
  
2.  （選擇性）在訂閱資料庫上的 「 訂閱者 」 執行 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md)。 指定的散發代理程式作業識別碼 **@jobid**, ，以及下列的資料轉換服務 (DTS) 封裝屬性︰  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     這樣會變更訂閱的 DTS 封裝屬性。  
  
    > [!NOTE]  
    >  工作識別碼，可取得執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。  
  
#### 檢視合併式發行集之提取訂閱的屬性  
  
1.  在 「 訂閱者 」 執行 [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。  
  
2.  在 「 訂閱者 」 執行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，和值 2， **@publication_type**。  
  
3.  在 「 發行者 」 執行 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) 以顯示訂閱資訊。 若要傳回特定訂閱的資訊，您必須指定 **@publication**, ，**@subscriber**, ，而值為 **提取** 的 **@subscription_type**。  
  
4.  在 「 發行者 」 執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，並指定 **@subscriber**。 這樣會顯示與訂閱者有關的資訊。  
  
#### 變更合併式發行集之提取訂閱的屬性  
  
1.  在 「 訂閱者 」 執行 [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)。 指定 **@publication**, ，**@publisher**, ，**@publisher_db**, 、 訂閱屬性變更為 **@property**, ，和新的值，如 **@value**。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於檢視或修改提取訂閱屬性的 RMO 類別，將取決於該提取訂閱所訂閱的發行集類型而定。  
  
#### 檢視或修改快照式或交易式發行集之提取訂閱的屬性  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 屬性，可以設定，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （選擇性）若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
#### 檢視或修改合併式發行集之提取訂閱的屬性  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 屬性，可以設定，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （選擇性）若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
## 另請參閱  
 [檢視資訊以及訂閱 & #40; 執行工作複寫監視器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  