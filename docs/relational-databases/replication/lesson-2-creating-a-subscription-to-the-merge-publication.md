---
title: "第 2 課：建立合併式發行集的訂閱 | Microsoft Docs"
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
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 423ad3b42e75c70e6826e04a298c5eac4e590291
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>第 2 課：建立合併式發行集的訂閱
在這一課，您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立訂閱。 接著，您將在訂閱資料庫上設定權限，並手動為新訂閱產生已篩選資料快照集。 您必須先完成上一課 [第 1 課：使用合併式複寫發行資料](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)，才能進行這一課。  
  
### <a name="to-create-the-subscription"></a>建立訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「訂閱者」，依序展開伺服器節點和 [複寫] 資料夾，以滑鼠右鍵按一下 [本機訂閱] 資料夾，然後按一下 [新增訂閱]。  
  
    「新增訂閱精靈」隨即啟動。  
  
2.  在 [發行集] 頁面上，按一下 [發行者] 清單中的 [尋找 SQL Server 發行者]。  
  
3.  在 [連接到伺服器] 對話方塊的 [伺服器名稱] 方塊中，輸入「發行者」執行個體的名稱，然後按一下 [連接]。  
  
4.  按一下 [AdvWorksSalesOrdersMerge]，然後按一下 [下一步]。  
  
5.  在 [合併代理程式位置] 頁面上，按一下 [在訂閱者端執行每一個代理程式]，然後按一下 [下一步]。  
  
6.  在 [訂閱者] 頁面上，選取「訂閱者」伺服器的執行個體名稱，然後在 [訂閱資料庫] 之下，從清單選取 [<New Database>]。  
  
7.  在 [新增資料庫] 對話方塊的 [資料庫名稱] 方塊中，輸入 **SalesOrdersReplica**，然後按一下 [確定]，再按一下 [下一步]。  
  
8.  在 [合併代理程式安全性] 頁面上，按一下省略符號 (**…**) 按鈕，在 [處理帳戶] 方塊中輸入 \<*電腦名稱>***\repl_merge**，提供此帳戶的密碼，並依序按一下 [確定]、[下一步]，然後再按一次 [下一步]。  
  
9. 在 [初始化訂閱] 頁面上，從 [初始化時機] 清單中選取 [第一次同步處理時]，按一下 [下一步]，然後再按一次 [下一步]。  
  
10. 在 [HOST_NAME 值] 頁面的 [HOST_NAME 值] 方塊中，輸入 **adventure-works\pamela0**，然後按一下 [完成]。  
  
11. 再按一次 [完成]，建立訂閱之後，按一下 [關閉]。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在訂閱者端設定資料庫權限  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「訂閱者」，依序展開 [資料庫]、[SalesOrdersReplica] 和 [安全性]，以滑鼠右鍵按一下 [使用者]，然後選取 [新增使用者]。  
  
2.  在 [一般] 頁面的 [使用者名稱] 方塊中，輸入 \<*電腦名稱>***\repl_merge**，按一下省略符號 (**…**) 按鈕，再按一下 [瀏覽]，選取 \<*電腦名稱>***\repl_merge**，依序按一下 [確定] 和 [檢查名稱]，然後按一下 [確定]。  
  
3.  在 [資料庫角色成員資格] 中，選取 [db_owner]，然後按一下 [確定] 建立使用者。  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>為訂閱建立已篩選資料快照集  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksSalesOrdersMerge] 發行集，然後按一下 [屬性]。  
  
    [發行集屬性] 對話方塊隨即顯示。  
  
3.  選取 [資料分割] 頁面，然後按一下 [加入]。  
  
4.  在 [加入資料分割] 對話方塊的 [HOST_NAME 值] 方塊中，輸入 **adventure-works\pamela0**，然後按一下 [確定]。  
  
5.  選取新加入的資料分割，按一下 [立即產生選取的快照集]，然後按一下 [確定]。  
  
## <a name="next-steps"></a>後續步驟  
您已順利建立合併式發行集的訂閱，並為新訂閱的資料分割產生已篩選快照集，因此在訂閱初始化時，即可使用此快照集。 下一步，您將授與權限給訂閱資料庫上的合併代理程式，並執行合併代理程式以啟動同步處理並初始化訂閱。 請參閱 [第 3 課：同步處理合併式發行集的訂閱](../../relational-databases/replication/lesson-3-synchronizing-the-subscription-to-the-merge-publication.md)。  
  
## <a name="see-also"></a>另請參閱  
[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
[建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)  
[含參數化篩選之合併式發行集的快照集](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  

