---
title: 備份與還原合併式複寫的策略 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a91d050e489aa782ab10490d294a7fba8c806fe4
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131908"
---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>備份與還原合併式複寫的策略
  對於合併式複寫，請定期備份下列資料庫：  
  
-   發行者端的發行集資料庫   
-   散發者端的散發資料庫    
-   每個訂閱者端的訂閱資料庫    
-   發行者、散發者及所有訂閱者端的 **master** 與 **msdb** 系統資料庫。 這些資料庫應與其他每個及相關的複寫資料庫同時備份。 例如，在您備份發行集資料庫的同時，在發行者端備份 **master** 與 **msdb** 資料庫。 還原發行集資料庫時，請確定 **master** 與 **msdb** 資料庫的複寫組態與設定和發行集資料庫一致。  
  
 如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果您沒有執行記錄備份，每當與複寫相關的設定有所變更，就應該執行備份。 如需相關資訊，請參閱 [需要更新之備份的常見動作](common-actions-requiring-an-updated-backup.md)。  
  
 選擇下面詳述的方法之一，以備份與還原發行集資料庫，然後遵循為散發資料庫與訂閱資料庫列出的建議。  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>備份與還原發行集資料庫  
 還原合併式發行集資料庫有兩種方法。 從備份還原發行集資料庫之後，應執行下列之一：  
  
-   同步處理發行集資料庫與訂閱資料庫。  
  
-   將所有的訂閱重新初始化至發行集資料庫的發行集。  
  
 使用以上方法之一確定在執行還原之後，「發行者」與所有「訂閱者」均保持同步。  
  
> [!NOTE]  
>  如果任何資料表都包含識別欄位，則必須確定在還原後指派的識別範圍正確。 如需詳細資訊，請參閱[複寫識別資料欄](../publish/replicate-identity-columns.md)。  
  
### <a name="synchronizing-the-publication-database"></a>同步處理發行集資料庫  
 將訂閱資料庫與發行集資料庫同步處理，可讓您從一或多個訂閱資料庫中上傳之前在發行集資料庫中所作、但在還原的備份中未顯示的變更。 可以上傳的資料視發行集的篩選方式而定：  
  
-   如果發行集未篩選，您可以透過與最新的「訂閱者」進行同步處理，使發行集資料庫處於最新狀態。  
  
-   如果發行集已篩選，則可能無法使發行集資料庫處於最新狀態。 請考慮已分割，每個訂用帳戶接收只會針對單一區域的客戶資料的資料表：北美東部、 美國南部、 和西部。 如果每個資料分割至少有一個「訂閱者」，則與每個資料分割的「訂閱者」進行同步處理就可使發行集資料庫處於最新狀態。 不過，如果在「西區」資料分割中的資料未複寫到任何「訂閱者」(舉例來說)，則「發行者」端的此資料將無法處於最新狀態。  
  
> [!IMPORTANT]  
>  同步處理發行集資料庫與訂閱資料庫，可能會導致發行的資料表還原到的時間點比從備份處還原的其他未發行的資料表的時間點要新。  
  
 如果同步處理的「訂閱者」執行的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本早於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，則訂閱不可是匿名的，而必須是客訂閱或主訂閱 (在之前的版本中稱為本機訂閱與全域訂閱)。  
  
 若要同步處理訂閱，請參閱＜ [Synchronize a Push Subscription](../synchronize-a-push-subscription.md) ＞和＜ [Synchronize a Pull Subscription](../synchronize-a-pull-subscription.md)＞。  
  
### <a name="reinitializing-all-subscriptions"></a>重新初始化所有訂閱  
 重新初始化所有訂閱可確保所有「訂閱者」的狀態均與還原的發行集資料庫保持一致。 若要將整個拓撲返回到給定發行集資料庫備份表示的之前狀態，則應使用此方法。 例如，如果您要將發行集資料庫還原到更早的時間點，即作為一種從錯誤執行的批次作業復原的機制，則您可能要重新初始化所有訂閱。  
  
 如果選擇此選項，應在復原發行集資料庫之後，立即產生新的快照集以傳遞給重新初始化的「訂閱者」。  
  
 若要重新初始化訂閱，請參閱＜ [重新初始化訂閱](../reinitialize-a-subscription.md)＞。  
  
 若要建立並套用快照集，請參閱＜ [建立和套用初始快照集](../create-and-apply-the-initial-snapshot.md) ＞和＜ [使用參數化篩選建立合併式發行集的快照集](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)＞。  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>備份與還原散發資料庫  
 對於合併式複寫，散發資料庫應定期備份，並且只要使用的備份不晚於使用「散發者」之所有發行集的最短保留期限，無需任何特殊考量即可還原。 例如，如果有三個保留期間分別為 10、20 及 30 天的發行集，則用來還原資料庫的備份不應晚於 10 天。 散發資料庫在合併式複寫中擁有有限的角色：它不儲存變更追蹤中使用的任何資料，也不提供要轉送到訂閱資料庫之合併式複寫變更的暫時儲存 (與它在異動複寫中一樣)。  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>備份與還原訂閱資料庫  
 為確保成功復原訂閱資料庫，在備份訂閱資料庫之前應將「訂閱者」應與「發行者」同步；它們在訂閱資料庫還原之後還應再同步一次：  
  
-   在訂閱資料庫備份之前與「發行者」進行同步處理，有助於確保在「訂閱者」從備份中還原時，訂閱仍處於發行集保留期限內。 例如，假設發行集保留期限為 10 天。 上次同步是在 8 天前，且現在已執行備份。 如果在 4 天後還原備份，則上次同步處理發生在 12 天前，已超出保留期限。 在此情況下，您必須重新初始化「訂閱者」。 如果「訂閱者」在備份前已同步處理，則訂閱資料庫應處於保留期限內。  
  
     備份不得晚於「訂閱者」訂閱的所有發行集中的最短保留期限。 例如，如果「訂閱者」分別訂閱了三個保留期限為 10、20 及 30 天的發行集，則用來還原資料庫的備份不應該晚於 10 天。  
  
-   在還原之後將訂閱資料庫與每個發行集同步處理，可確保「訂閱者」處於最新狀態 (具有「發行者」端的所有變更)。  
  
 若要設定發行集保留期限，請參閱[設定訂閱的逾期期限](../publish/set-the-expiration-period-for-subscriptions.md)。  
  
 若要同步處理訂閱，請參閱＜ [同步處理發送訂閱](../synchronize-a-push-subscription.md) ＞和＜ [同步處理提取訂閱](../synchronize-a-pull-subscription.md) ＞。  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>備份與還原重新發行資料庫  
 當資料庫從「發行者」來訂閱資料並轉而將相同的資料發行至其他訂閱資料庫時，該資料庫便是一個重新發行集資料庫。 還原重新發行的資料庫時，請遵循本主題中＜備份與還原發行集資料庫＞以及＜備份與還原訂閱資料庫＞兩節所描述的指導方針。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](back-up-and-restore-replicated-databases.md)  
  
  
