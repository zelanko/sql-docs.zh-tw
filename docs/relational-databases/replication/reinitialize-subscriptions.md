---
title: "重新初始化訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5f652ed0f32412e0286aedea209c6dfd031b30c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="reinitialize-subscriptions"></a>重新初始化訂閱
  重新初始化訂閱涉及將一個或多個發行項的新快照集套用至一個或多個「訂閱者」：交易式和快照式複寫允許重新初始化個別發行項；合併式複寫要求重新初始化所有發行項。 無法重新初始化點對點異動複寫拓撲中的節點。 如果您必須確定節點有資料的新副本，請在節點還原備份。 發生重新初始化的情況有兩種：  
  
-   您將訂閱明確標示為要重新初始化。  
  
-   您執行了要求重新初始化的動作，例如屬性變更。 如需要求重新初始化動作的詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 在這兩種情況下，「散發代理程式」或「合併代理程式」下次執行時，將為「訂閱者」套用最新的快照集。 對於快照式和異動複寫，發生重新初始化時，在「訂閱者」端已經作過但尚未與「發行者」同步處理的任何變更，均將被新快照集的應用程式覆寫。  
  
 對於合併式複寫，您可以選擇在套用快照集之前從「訂閱者」上傳所有資料變更。 「發行者」中任何暫止的結構描述變更都將在「訂閱者」端套用，然後，自上次同步處理之後在「訂閱者」端所作的任何更新都將在套用快照集之前傳播到「發行者」。 此行為由 **upload_first** 與 **automatic_reinitialization_policy** 屬性控制；如需詳細資訊，請參閱＜ [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md)＞。 如果使用 SQL Server Management Studio 或「複寫監視器」將訂閱標示為要重新初始化，則在 **[重新初始化訂閱]** 對話方塊中會提供您一個選項來首先上傳變更。  
  
> [!IMPORTANT]  
>  如果在合併式複寫中新增、卸除或變更參數化篩選，則無法在重新初始化期間將「訂閱者」端暫止的變更上傳至「發行者」。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
 如果在建立訂閱時，已指定不會將初始快照集套用至「訂閱者」，然後將該訂閱標示為要重新初始化，則不會套用快照集。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
 **若要重新初始化訂閱**  
  
 若要重新初始化訂閱中的所有發行項，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、預存程序或 Replication Management Objects (RMO)。 若要重新初始化快照式和交易式發行集中的個別發行項，則必須使用預存程序。 如需相關資訊，請參閱 [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
 [初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)   
 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
