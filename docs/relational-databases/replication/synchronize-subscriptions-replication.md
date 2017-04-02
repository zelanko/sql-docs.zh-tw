---
title: "同步處理訂閱 (複寫) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "同步處理 [SQL Server 複寫], 訂閱"
  - "訂閱 [SQL Server 複寫], 同步處理"
  - "複寫 [SQL Server 複寫], 同步處理"
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 同步處理訂閱 (複寫)
  複寫代理程式會同步處理訂閱。 散發代理程式會同步處理交易式和快照式發行集的訂閱，而合併代理程式會同步處理合併式發行集的訂閱。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、複寫預存程序和 Replication Management Objects (RMO)，以同步處理訂閱及控制同步處理行為。 下列主題描述如何同步處理訂閱及指定同步處理選項。  
  
## 本節內容  
  
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [啟用使用備份的初始化交易式發行集 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/enable initialization with backup for transactional publications.md)  
  
-   [初始化備份 & #40; 從交易式訂閱複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)  
  
-   [手動初始化訂閱](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [在套用快照集前後執行指令碼 （& s) #40。SQL Server Management Studio & #41;](../../relational-databases/replication/execute scripts before and after a snapshot is applied.md)  
  
-   [同步處理 & #40; 期間執行指令碼複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [檢視並解決資料衝突的合併式發行集與 #40。SQL Server Management Studio & #41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [檢視資料衝突，交易式發行集 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [同步處理訂閱，使用 Windows Synchronization Manager & #40。Windows Synchronization Manager & #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)  
  
-   [為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [偵錯商務邏輯處理常式 & #40。複寫程式設計 & #41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [同步處理 & #40; 期間控制觸發程序和條件約束的行為複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/control behavior of triggers and constraints in synchronization.md)  
  
-   [Implement a Custom Conflict Resolver for a Merge Article](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## 另請參閱  
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)  
  
  