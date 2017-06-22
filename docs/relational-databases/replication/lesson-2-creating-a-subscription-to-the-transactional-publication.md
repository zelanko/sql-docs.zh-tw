---
title: "第 2 課：建立交易式發行集的訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2065387bdf7d23b372f70058c509855e0b0f0792
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>第 2 課：建立交易式發行集的訂閱
在這一課，您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立訂閱。 您必須先完成上一課 [第 1 課：使用異動複寫發行資料](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)，才能進行這一課。  
  
### <a name="to-create-the-subscription"></a>建立訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 **[本機發行集]** 資料夾中，以滑鼠右鍵按一下 **[AdvWorksProductTrans]** 發行集，然後按一下 **[新增訂閱]**。  
  
    「新增訂閱精靈」隨即啟動。  
  
3.  在 [發行集] 頁面上，選取 **[AdvWorksProductTrans]**，然後按一下 **[下一步]**。  
  
4.  在 [散發代理程式位置] 頁面上，選取 **[在散發者端執行所有代理程式]**，然後按一下 **[下一步]**。  
  
5.  在 [訂閱者] 頁面上，如果未顯示訂閱者執行個體的名稱，請按一下 **[加入訂閱者]**，再按 **[加入 SQL Server 訂閱者]**，在 **[連接到伺服器]** 對話方塊中輸入訂閱者執行個體名稱，然後按一下 **[連接]**。  
  
6.  在 [訂閱者] 頁面上，選取訂閱者伺服器的執行個體名稱，然後在 [訂閱資料庫] 之下選取 [<New Database>]。  
  
7.  在 **[新增資料庫]** 對話方塊的 **[資料庫名稱]** 方塊中，輸入 **ProductReplica** ，然後按一下 **[確定]**，再按 **[下一步]**。  
  
8.  在 [散發代理程式安全性] 對話方塊中，按一下省略符號 (**…**) 按鈕，在 [處理帳戶] 方塊中輸入 \<*電腦名稱>***\repl_distribution**，輸入此帳戶的密碼，按一下 [確定]，然後按一下 [下一步]。  
  
9. 按一下 **[完成]** 接受其餘頁面上的預設值，並完成精靈。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在訂閱者端設定資料庫權限  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「訂閱者」，依序展開 [資料庫]、[ProductReplica] 和 [安全性]，以滑鼠右鍵按一下 [使用者]，然後選取 [新增使用者]。  
  
2.  在 **[一般]** 頁面的 **[使用者類型]** 清單中，選取 **[Windows 使用者]**。  
  
3.  選取 [使用者名稱] 方塊並按一下省略符號 (…) 按鈕，在 [輸入要選取的物件名稱] 方塊中，輸入 <電腦名稱>**\repl_distribution**，按一下 [檢查名稱]，然後按一下 [確定]。  
  
4.  在 [成員資格] 頁面的 [資料庫角色成員資格] 區域中，選取 [db_owner]，然後按一下 [確定] 建立使用者。  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>檢視訂閱的同步處理狀態  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 **[本機訂閱]** 資料夾中，展開 **[AdvWorksProductTrans]** 發行集，以滑鼠右鍵按一下 **ProductReplica** 資料庫中的訂閱，然後按一下 **[檢視同步處理狀態]**。  
  
    訂閱的目前訂閱狀態隨即顯示。  
  
3.  如果 **[AdvWorksProductTrans]**之下看不到訂閱，請按 F5 重新整理清單。  
  
## <a name="next-steps"></a>後續步驟  
您已順利建立交易式發行集的訂閱。 由於此訂閱的散發代理程式會持續執行，因此，訂閱會在建立時初始化。 下一步，您將使用追蹤 Token，確認變更正複寫至「訂閱者」並決定延遲。 請參閱＜ [Lesson 3: Validating the Subscription and Measuring Latency](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md)＞。  
  
## <a name="see-also"></a>另請參閱  
[使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  

