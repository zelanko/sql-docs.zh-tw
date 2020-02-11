---
title: 第 2 課：建立交易式發行集的訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721082"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>第 2 課：建立交易式發行集的訂閱
  在這一課，您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立訂閱。 您必須先完成上一課 [第 1 課：使用異動複寫發行資料](lesson-1-publishing-data-using-transactional-replication.md)，才能進行這一課。  
  
### <a name="to-create-the-subscription"></a>建立訂閱  
  
1.  連接到中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的發行者，展開伺服器節點，然後展開 [複寫]**資料夾。**  
  
2.  在 **[本機發行集]** 資料夾中，以滑鼠右鍵按一下 **[AdvWorksProductTrans]** 發行集，然後按一下 **[新增訂閱]**。  
  
     「新增訂閱精靈」隨即啟動。  
  
3.  在 [發行集] 頁面上，選取 **[AdvWorksProductTrans]**，然後按一下 **[下一步]**。  
  
4.  在 [散發代理程式位置] 頁面上，選取 **[在散發者端執行所有代理程式]**，然後按一下 **[下一步]**。  
  
5.  在 [訂閱者] 頁面上，如果未顯示訂閱者執行個體的名稱，請按一下 **[加入訂閱者]**，再按 **[加入 SQL Server 訂閱者]**，在 **[連接到伺服器]** 對話方塊中輸入訂閱者執行個體名稱，然後按一下 **[連接]**。  
  
6.  在 [訂閱者] 頁面上，選取訂閱者伺服器的實例名稱，然後選取**** ** \< ** [訂閱資料庫] 下的 [新增資料庫>]。  
  
7.  在 **[新增資料庫]** 對話方塊的 **[資料庫名稱]** 方塊中，輸入 **ProductReplica** ，然後按一下 **[確定]**，再按 **[下一步]**。  
  
8.  在 [**散發代理程式安全性**] 對話方塊中，按一下省略號（**...**）按鈕，在 [**處理帳戶**] 方塊中輸入\< _Machine_Name>_ **\ repl_distribution** ，輸入此帳戶的密碼，按一下 **[確定]**，然後按 **[下一步**]。  
  
9. 按一下 **[完成]** 接受其餘頁面上的預設值，並完成精靈。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在訂閱者端設定資料庫權限  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「訂閱者」，依序展開 [資料庫]****、[ProductReplica]**** 和 [安全性]****，以滑鼠右鍵按一下 [使用者]****，然後選取 [新增使用者]****。  
  
2.  在 **[一般]** 頁面的 **[使用者類型]** 清單中，選取 **[Windows 使用者]**。  
  
3.  選取 [**使用者名稱**] 方塊，然後按一下省略號（...）按鈕，在 [**輸入物件名稱來選取**] 方塊類型 <Machine_Name>**\ Repl_distribution**，按一下 [**檢查名稱**]，然後按一下 **[確定]**。  
  
4.  在 [成員資格]**** 頁面的 [資料庫角色成員資格]**** 區域中，選取 [db_owner]****，然後按一下 [確定]**** 建立使用者。  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>檢視訂閱的同步處理狀態  
  
1.  連接到中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的發行者，展開伺服器節點，然後展開 [複寫]**資料夾。**  
  
2.  在 **[本機訂閱]** 資料夾中，展開 **[AdvWorksProductTrans]** 發行集，以滑鼠右鍵按一下 **ProductReplica** 資料庫中的訂閱，然後按一下 **[檢視同步處理狀態]**。  
  
     訂閱的目前訂閱狀態隨即顯示。  
  
3.  如果 **[AdvWorksProductTrans]** 之下看不到訂閱，請按 F5 重新整理清單。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利建立交易式發行集的訂閱。 由於此訂閱的散發代理程式會持續執行，因此，訂閱會在建立時初始化。 下一步，您將使用追蹤 Token，確認變更正複寫至「訂閱者」並決定延遲。 請參閱＜ [Lesson 3: Validating the Subscription and Measuring Latency](lesson-3-validating-the-subscription-and-measuring-latency.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
