---
title: 第 3 課：驗證訂閱及測量延遲 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6968331bc7699334f61997ec6a16e521c158078a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721054"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>第 3 課：驗證訂閱及測量延遲
  在這一課，您將使用追蹤 Token，以確認變更正複寫至訂閱者，並決定延遲 (亦即在「發行者」端所做變更顯示在「訂閱者」上所花費的時間)。 您必須先完成上一課 [第 2 課：建立交易式發行集的訂閱](lesson-2-creating-a-subscription-to-the-transactional-publication.md)，才能進行這一課。  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>插入追蹤 Token 並檢視 Token 上的資訊  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「發行者」，展開伺服器節點，再以滑鼠右鍵按一下 [複寫]**** 資料夾，然後按一下 [啟動複寫監視器]****。  
  
     複寫監視器隨即啟動。  
  
2.  在左窗格中展開「發行者」群組，展開「發行者」執行個體，然後按一下 **AdvWorksProductTrans** 發行集。  
  
3.  按一下 **[追蹤 Token]** 索引標籤。  
  
4.  按一下 **[插入追蹤]**。  
  
5.  在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 值為 [**暫**止] 表示 token 尚未到達指定的點。  
  
## <a name="next-steps"></a>後續步驟  
 在這一課，您已順利使用追蹤 Token，驗證資料變更正從「發行者」複寫至「訂閱者」。 您也可以在「發行者」端插入、更新或刪除 **Product** 資料表中的資料，並在複寫之後，在「訂閱者」端查詢 **Product** 資料表，檢視這些變更。  
  
 如此即已完成＜在連續連接的伺服器之間複寫資料＞教學課程。 如需使用合併式複寫的類似教學課程，請參閱 [教學課程：利用行動用戶端複寫資料](tutorial-replicating-data-with-mobile-clients.md)。  
  
## <a name="see-also"></a>另請參閱  
 [針對異動複寫測量延遲及驗證連線](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
