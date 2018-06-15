---
title: 切換可更新之交易式訂閱的更新模式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4bf0695819d8f4a75a974a0235de092976281a51
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957383"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>切換可更新之交易式訂閱的更新模式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中切換可更新之交易訂閱的更新模式。 使用「新增訂閱精靈」指定可更新訂閱的模式。 如需使用此精靈時設定模式的資訊，請參閱[檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要切換可更新之交易式訂閱的更新模式，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您可以隨時從立即更新容錯移轉到到佇列更新。 不過在進行這項作業之後，在「訂閱者」和「發行者」連接，且「佇列讀取器代理程式」將佇列中所有暫止訊息套用至「發行者」之前，無法切換回立即更新。  
  
###  <a name="Recommendations"></a> 建議  
  
-   當交易式訂閱的更新訂閱支援從一種更新模式容錯移轉到另一種模式時，您可以透過程式設計的方式切換更新模式，以處理連接在短時間內變更的情況。 您可以使用複寫預存程序，以程式設計的方式並視需要而設定更新模式。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)中切換可更新之交易訂閱的更新模式。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  若要在建立訂閱後變更更新模式，則須在建立訂閱時將 **update_mode** 屬性設為 **failover** (允許從立即更新切換到佇列更新) 或 **queued failover** (允許從佇列更新切換到立即更新)。 這些屬性會自動在「新增訂閱精靈」中設定。  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>若要設定發送訂閱的更新模式  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要設定更新模式的訂閱，再按一下 **[設定更新方法]**。  
  
4.  在 [設定更新方法 - \<訂閱者>: \<訂閱資料庫>] 對話方塊中，選取 [立即更新] 或 [佇列更新]。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>若要設定提取訂閱的更新模式  
  
1.  在 [訂閱屬性 - \<發行者>: \<發行資料庫>] 對話方塊中，選取 [立即複寫變更] 的值或 [訂閱者更新方法] 選項的 [佇列變更]。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 如需存取 [訂閱屬性 - \<發行者>: \<發行集資料庫>] 對話方塊的詳細資訊，請參閱[檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>切換更新模式  
  
1.  針對提取訂閱執行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) ，或針對發送訂閱執行 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) ，確定訂閱支援容錯移轉。 如果結果集中 **update mode** 的值是 **3** 或 **4**，即支援容錯移轉。  
  
2.  在訂閱資料庫的「訂閱者」端執行 [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)。 指定 **@publisher**、 **@publisher_db**、 **@publication**和 **@failover_mode**的下列其中一個值：  
  
    -   **queued** - 當連接已暫時遺失時，容錯移轉到佇列更新。  
  
    -   **immediate** - 當連接已還原時，容錯移轉到立即更新。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
