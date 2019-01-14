---
title: 檢視資料衝突，交易式發行集 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e046351ca3dc7977691fc98e24453ccbf8e6af53
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123778"
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>檢視交易式發行集的資料衝突 (SQL Server Management Studio)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 複寫衝突檢視器可讓您檢視點對點異動複寫和具有佇列更新訂閱之異動複寫的衝突。 如需如何偵測和解決衝突的資訊，請參閱[點對點複寫中的衝突偵測](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)和[設定佇列更新衝突解決選項 &#40;SQL Server Management Studio&#41;](publish/create-an-updatable-subscription-to-a-transactional-publication.md)。  
  
 衝突資料的可用性會取決於複寫的類型和衝突保留期限而定：  
  
-   如果是點對點複寫，則在預設情況下，當散發代理程式偵測到衝突時，就會發生失敗。 衝突錯誤會記錄到錯誤記錄檔中，但是不會將任何衝突資料記錄到衝突資料表中；因此，此資料表無法供人檢視。 如果允許散發代理程式繼續進行，會將衝突記錄在本機中偵測到衝突的每一個節點上。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。  
  
-   如果是佇列更新訂閱，則會針對每一個衝突提供資料。 複寫衝突檢視器可以在衝突保留期限指定的時間內使用衝突資料 (預設為 14 天)。 若要設定衝突保留期限，您可以執行以下其中一項作業：  
  
    -   為 @conflict_retention [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 的 參數指定保留值。  
  
    -   指定的值為 `'conflict_retention'` for @property 參數，並保留值 @value 參數[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。  
  
### <a name="to-view-conflicts"></a>若要檢視衝突  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的適當伺服器，然後展開伺服器節點：  
  
    -   如果是點對點複寫，這會是發生衝突的節點。  
  
    -   如果是佇列更新訂閱，這會是發行者。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要檢視衝突的發行集，然後按一下 **[檢視衝突]**。  
  
4.  在 **[選取衝突資料表]** 對話方塊中，選取要檢視衝突的資料庫、發行集和資料表。  
  
5.  在複寫衝突檢視器中，您可以：  
  
    -   使用上方格右側按鈕篩選資料列。  
  
    -   在上方格內選取資料列，以便於下方格的該資料列顯示資訊。  
  
    -   在上方格中選取一個或多個資料列，然後按一下 **[移除]**，會從衝突中繼資料表中移除資料列。  
  
    -   按一下屬性按鈕 ([...]) 以檢視更多有關於衝突的資料行資訊。  
  
    -   選取 **[記錄此衝突的詳細資料]** 即可將衝突資料記錄到檔案中。 若要指定檔案的位置，請指向 **[檢視]** 功能表，然後按一下 **[選項]**。 輸入值，或按一下瀏覽按鈕 (**[...]**)，然後導覽至適當的檔案。 按一下 **[確定]** 關閉 **[選項]** 對話方塊。  
  
6.  關閉複寫衝突檢視器。  
  
## <a name="see-also"></a>另請參閱  
 [點對點異動複寫](transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
