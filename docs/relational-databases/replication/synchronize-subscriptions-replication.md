---
title: "同步處理訂閱 (複寫) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dbd10248c5a6c358e6e8e6c64b0db355fc4ed66d
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="synchronize-subscriptions-replication"></a>同步處理訂閱 (複寫)
  複寫代理程式會同步處理訂閱。 散發代理程式會同步處理交易式和快照式發行集的訂閱，而合併代理程式會同步處理合併式發行集的訂閱。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、複寫預存程序和 Replication Management Objects (RMO)，以同步處理訂閱及控制同步處理行為。 下列主題描述如何同步處理訂閱及指定同步處理選項。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [為交易式發行集啟用使用備份的初始化 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [手動初始化訂閱](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [在套用快照集的前後執行指令碼 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [在同步處理期間執行指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [偵錯商務邏輯處理常式 &#40;複寫程式設計&#41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [為合併發行項實作自訂衝突解析程式](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>另請參閱  
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)  
  
  

