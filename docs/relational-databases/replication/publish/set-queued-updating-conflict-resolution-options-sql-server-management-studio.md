---
title: "設定佇列更新衝突解決選項 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee3af1a65573f04bce7f414638b052fdd38c4777
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>設定佇列更新衝突解決選項 (SQL Server Management Studio)
  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，為支援佇列更新訂閱的發行集設定衝突解決選項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>若要設定佇列更新衝突解決選項  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，選取下列 [衝突解決原則] 選項的其中一個值︰  
  
    -   **[保留發行者變更]**  
  
    -   **[保留訂閱者變更]**  
  
    -   **[重新初始化訂閱]**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [啟用交易式發行集的更新訂閱](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
