---
title: 第 1 課：使用異動複寫發行資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d75a44c44442917f61b52c7aa0f2e770dcdf5d83
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590562"
---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>第 1 課：使用異動複寫發行資料
  在這一課，您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立交易式發行集，以發行 **範例資料庫中** Product [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表的篩選子集。 此外，您也會將散發代理程式所使用的 SQL Server 登入加入至發行集存取清單 (PAL)。 開始進行此教學課程之前，必須先完成上一個教學課程 [準備伺服器進行複寫](tutorial-preparing-the-server-for-replication.md)。  
  
### <a name="to-create-a-publication-and-define-articles"></a>建立發行集並定義發行項  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 [複寫] 資料夾，然後以滑鼠右鍵按一下 [本機發行集] 資料夾，再按一下 [新增發行集]。  
  
     [發行集設定精靈] 隨即啟動。  
  
3.  在 [發行集資料庫] 頁面上，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後按一下 [下一步]。  
  
4.  在 [發行集類型] 頁面上，選取 [交易式發行集]，然後按一下 [下一步]。  
  
5.  在 [發行項] 頁面上，展開 [Tables] 節點，選取 [Product] 核取方塊，然後展開 [Product]，再清除 [ListPrice] 和 [StandardCost] 核取方塊。 按 [下一步] 。  
  
6.  在 [篩選資料表的資料列] 頁面上，按一下 [新增]。  
  
7.  在 [新增篩選] 對話方塊中，按一下 [SafetyStockLevel] 資料行，再按一下向右鍵，將資料行新增至篩選查詢的篩選陳述式 WHERE 子句中，並依照下列方式修改 WHERE 子句：  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  按一下 [確定]，然後按一下 [下一步]。  
  
9. 選取 [立即建立快照集，並保留快照集為可使用狀態，以初始化訂閱] 核取方塊，然後按一下 [下一步]。  
  
10. 在 [代理程式安全性] 頁面上，清除 [使用快照集代理程式的安全性設定] 核取方塊。  
  
11. 按一下快照集代理程式的 [安全性設定]，在 [處理帳戶] 方塊中輸入 \<_電腦名稱>_**\repl_snapshot**，提供此帳戶的密碼，然後按一下 [確定]。  
  
12. 重複執行先前的步驟，將 repl_logreader 設定為記錄讀取器代理程式的處理帳戶，然後按一下 [完成]。  
  
13. 在 [完成精靈] 頁面的 [發行集名稱] 方塊中輸入 [AdvWorksProductTrans]，然後按一下 [完成]。  
  
14. 建立發行集之後，按一下 [關閉] 以完成精靈。  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>檢視快照集產生的狀態  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後按一下 [檢視快照集代理程式狀態]。  
  
3.  發行集之快照集代理程式作業的目前狀態隨即顯示。 確認快照集作業已成功，再繼續進行下一課。  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>將散發代理程式登入加入 PAL  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後按一下 [屬性]。  
  
     [發行集屬性] 對話方塊隨即顯示。  
  
3.  選取 [發行集存取清單] 頁面，然後按一下 [新增]。  
  
4.  在 [新增發行集存取] 對話方塊中，選取 [<電腦名稱>\repl_distribution]，然後按一下 [確定]。 按一下 [確定] 。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利建立交易式發行集。 下一步，您將訂閱此發行集。 請參閱[第 2 課：建立交易式發行集的訂閱](lesson-2-creating-a-subscription-to-the-transactional-publication.md)。  
  
## <a name="see-also"></a>另請參閱  
 [篩選發行的資料](publish/filter-published-data.md)   
 [Define an Article](publish/define-an-article.md)   
 [建立並套用快照集](create-and-apply-the-snapshot.md)  
  
  
