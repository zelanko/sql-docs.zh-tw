---
title: 設定佇列更新衝突解決選項 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f05328a43c75158e9be6c13e4fc23b0cc9ab2799
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749001"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>設定佇列更新衝突解決選項 (SQL Server Management Studio)
  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，為支援佇列更新訂閱的發行集設定衝突解決選項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>若要設定佇列更新衝突解決選項  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，選取下列 [衝突解決原則] 選項的其中一個值︰  
  
    -   **[保留發行者變更]**  
  
    -   **[保留訂閱者變更]**  
  
    -   **[重新初始化訂閱]**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [啟用交易式發行集的更新訂閱](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
