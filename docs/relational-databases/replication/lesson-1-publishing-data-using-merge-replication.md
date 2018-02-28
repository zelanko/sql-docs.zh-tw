---
title: "第 1 課：使用合併式複寫發行資料 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b30cc7798d28ce9b13f9448f583891170f7309fd
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="lesson-1-publishing-data-using-merge-replication"></a>第 1 課：使用合併式複寫發行資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，建立合併式發行集，以發行 **範例資料庫中**Employee **、**SalesOrderHeader **和** SalesOrderDetail [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表的子集。 這些資料表是以參數化資料列篩選器加以篩選，讓每一個訂閱包含唯一的資料分割。 此外，您也會將合併代理程式所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入加入至發行集存取清單 (PAL)。 本教學課程要求您，先完成上一個教學課程 [準備伺服器進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
### <a name="to-create-a-publication-and-define-articles"></a>建立發行集並定義發行項  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 [複寫] 資料夾，然後以滑鼠右鍵按一下 [本機發行集]，再按一下 [新增發行集]。  
  
    [發行集設定精靈] 隨即啟動。  
  
3.  在 [發行集資料庫] 頁面上，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後按一下 [下一步]。  
  
4.  在 [發行集類型] 頁面上，選取 [合併式發行集]，然後按一下 [下一步]。  
  
5.  在 [訂閱者類型] 頁面上，確定只選取 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (含) 以後版本，然後按一下 [下一步]。  
  
6.  在 [發行項] 頁面上，展開 [資料表] 節點，選取 [SalesOrderHeader] 和 [SalesOrderDetail]，然後展開 [Employee]，選取 [EmployeeID] 或 [LoginID]，再按一下 [下一步]。  
  
    > [!TIP]  
    > 系統會自動選取其他必要的資料行。 選取任何一個自動選取的資料行，並檢視 [發行的物件] 清單下方有關為何需要資料行的說明。  
  
7.  在 [篩選資料表的資料列] 頁面上，按一下 [加入]，然後按一下 [加入篩選]。  
  
8.  在 [加入篩選] 對話方塊中，選取 [請選取要篩選的資料表] 中的 [Employee (HumanResources)]，按一下 [LoginID] 資料行，按一下向右箭號，將資料行加入篩選查詢的 WHERE 子句，並依照下列方式修改 WHERE 子句：  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. 按一下 [這個資料表中的一個資料列只會提供給一個訂閱]，然後按一下 [確定]。  
  
10. 在 [篩選資料表的資料列] 頁面上，依序按一下 [Employee (Human Resources)]、[加入] 和 [加入聯結以擴充選取的篩選]。  
  
11. 在 [加入聯結] 對話方塊中，選取 [聯結的資料表] 之下的 [Sales.SalesOrderHeader]，按一下 [手動寫入聯結陳述式]，如下完成聯結陳述式：  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. 在 [指定聯結選項] 中，選取 [唯一索引鍵]，然後按一下 [確定]。  
  
13. 在 [篩選資料表的資料列] 頁面上，依序按一下 [SalesOrderHeader]、[加入] 和 [加入聯結以擴充選取的篩選]。  
  
14. 在 [加入聯結] 對話方塊中，選取 [聯結的資料表] 之下的 [Sales.SalesOrderDetail]。  
  
15. 按一下 [手動寫入聯結陳述式]。  
  
16. 在 [已篩選的資料表資料行] 中，選取 [BusinessEntityID]，然後按一下箭號按鈕將資料行名稱複製到聯結陳述式。  
  
17. 在 [聯結陳述式] 方塊中，完成聯結陳述式，如下所示：  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. 在 [指定聯結選項] 中，選取 [唯一索引鍵]，然後按一下 [確定]。  
  
19. 在 [篩選資料表的資料列] 頁面上，依序按一下 [SalesOrderHeader (Sales)]、[加入] 和 [加入聯結以擴充選取的篩選]。  
  
20. 在 [加入聯結] 對話方塊中，選取 [聯結的資料表] 之下的 [Sales.SalesOrderDetail]，按一下 [確定]，然後按一下 [下一步]。  
  
21. 選取 [立即建立快照集]，清除 [排程快照集代理程式在下列時間執行]，然後按一下 [下一步]。  
  
22. 在 [代理程式安全性] 頁面上，按一下 [安全性設定]，在 [處理帳戶] 方塊中鍵入 \<電腦名稱>**\repl_snapshot**，提供此帳戶的密碼，然後按一下 [確定]。 按一下 **[完成]**。  
  
23. 在 [完成精靈] 頁面的 [發行集名稱] 方塊中輸入 **AdvWorksSalesOrdersMerge**，然後按一下 [完成]。  
  
24. 建立發行集以後，按一下 [關閉]。  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>檢視快照集產生的狀態  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksSalesOrdersMerge]，然後按一下 [檢視快照集代理程式的狀態]。  
  
3.  發行集之快照集代理程式作業的目前狀態隨即顯示。 確認快照集作業已成功，再繼續進行下一課。  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>將合併代理程式登入加入 PAL  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksSalesOrdersMerge]，然後按一下 [屬性]。  
  
    [發行集屬性] 對話方塊隨即顯示。  
  
3.  選取 [發行集存取清單] 頁面，然後按一下 [新增]。  
  
4.  在 [新增發行集存取] 對話方塊中，選取 <電腦名稱>**\repl_merge** ，然後按一下 [確定]。 按一下 [確定] 。  
  
## <a name="next-steps"></a>Next Steps  
您已順利建立合併式發行集。 下一步，您將訂閱此發行集。 請參閱 [第 2 課：建立合併式發行集的訂閱](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)。  
  
## <a name="see-also"></a>另請參閱  
[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)  
[參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
[定義發行項](../../relational-databases/replication/publish/define-an-article.md)  
  
  
  
