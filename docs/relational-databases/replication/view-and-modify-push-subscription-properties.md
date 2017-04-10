---
title: "檢視及修改發送訂閱屬性 | Microsoft Docs"
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
  - "viewing replication properties"
  - "push subscriptions [SQL Server replication], properties"
  - "subscriptions [SQL Server replication], push"
  - "push subscriptions [SQL Server replication], modifying"
  - "modifying replication properties, push subscriptions"
  - "修改訂閱, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 檢視及修改發送訂閱屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中檢視及修改發送訂閱屬性。  
  
 **本主題內容**  
  
-   **若要檢視及修改發送訂閱屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 從「發行者」在以下項目中檢視並修改發送訂閱屬性：  
  
-    **訂閱屬性-\< 發行者>: \< u>** 對話方塊中，可從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
-   **[所有訂閱]** 索引標籤，在「複寫監視器」中可用。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
#### 若要在 Management Studio 中檢視並修改發送訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  依序展開適當的發行集，訂閱中，按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
#### 若要在複寫監視器中檢視和修改發送訂閱屬性  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  訂閱中，按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改發送訂閱及存取其屬性。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### 檢視快照式或交易式發行集之發送訂閱的屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。 指定 **@publication**、 **@subscriber**，並針對 **@article** 指定 **all**的值。  
  
2.  在發行集資料庫的發行者，執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，並指定 **@subscriber**。  
  
#### 變更快照式或交易式發行集之發送訂閱的屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), ，並指定 **@subscriber** 和 「 訂閱者 」 屬性，變更任何參數。  
  
2.  在發行集資料庫的發行者，執行 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，**@destination_db**, ，值為 **所有** 的 **@article**, 、 訂閱屬性變更為 **@property**, ，和新的值，如 **@value**。 這樣會變更發送訂閱的安全性設定。  
  
3.  （選擇性）若要變更訂閱的資料轉換服務 (DTS) 封裝屬性，請執行 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) 訂閱資料庫的訂閱者端。 針對 **@jobid** 指定散發代理程式作業的識別碼以及下列 DTS 封裝屬性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     這樣會變更訂閱的 DTS 封裝屬性。  
  
    > [!NOTE]  
    >  工作識別碼，可取得執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。  
  
#### 檢視合併式發行集之發送訂閱的屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。  
  
2.  在 「 發行者 」 執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，並指定 **@subscriber**。  
  
#### 變更合併式發行集之發送訂閱的屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, 、 訂閱屬性變更為 **@property**, ，和新的值，如 **@value**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於檢視或修改發送訂閱屬性的 RMO 類別，將取決於該發送訂閱所訂閱的發行集類型而定。  
  
#### 檢視或修改快照式或交易式發行集之發送訂閱的屬性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性。  
  
4.  設定 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.TransSubscription> 屬性，可以設定，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （選擇性）若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入訂閱的屬性。  
  
#### 檢視或修改合併式發行集之發送訂閱的屬性  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性。  
  
4.  設定 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 屬性，可以設定，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （選擇性）若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入訂閱的屬性。  
  
## 另請參閱  
 [檢視資訊以及訂閱 & #40; 執行工作複寫監視器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  