---
title: 第 3 課：同步處理合併式發行集的訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8e382a5c39d67d4c38052bc2b52e0018d1233b3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207398"
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>第 3 課：同步處理合併式發行集的訂閱
  在這一課，您將啟動合併代理程式，以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來初始化訂閱。 此外，您會使用此程序與發行者進行同步處理。 您必須先完成上一課 [第 2 課：建立合併式發行集的訂閱](lesson-2-creating-a-subscription-to-the-merge-publication.md)，才能進行這一課。  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>啟動同步處理並初始化訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「訂閱者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 **[本機訂閱]** 資料夾中，以滑鼠右鍵按一下 **SalesOrdersReplica** 資料庫中的訂閱，然後按一下 **[檢視同步處理的狀態]**。  
  
3.  按一下 **[啟動]** ，以初始化訂閱。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利執行合併代理程式，以啟動同步處理並初始化訂閱。 您也可以在「發行者」或「訂閱者」端插入、更新或刪除 **SalesOrderHeader** 或 **SalesOrderDetail** 資料表中的資料，並且在可以使用網路連接來同步處理「發行者」或「訂閱者」之間的資料時，重複此程序，然後在其他伺服器上查詢 **SalesOrderHeader** 或 **SalesOrderDetail** 資料表，以檢視複寫的變更。  
  
 如此即完成「利用行動用戶端複寫資料」教學課程。 如需使用異動複寫的類似教學課程，請參閱＜ [Tutorial: Replicating Data Between Continuously Connected Servers](tutorial-replicating-data-between-continuously-connected-servers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [同步處理資料](synchronize-data.md)   
 [同步處理提取訂閱](synchronize-a-pull-subscription.md)  
  
  
