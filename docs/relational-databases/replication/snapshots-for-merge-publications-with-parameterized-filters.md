---
title: "含參數化篩選之合併式發行集的快照集 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 246e2e5db5c3e64973c165be8b03e03b7c8226a5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>含參數化篩選之合併式發行集的快照集
  在合併發行集內使用參數化資料列篩選器時，覆寫會以兩段式的快照集來初始化每一個訂閱。 首先建立包含複寫所需之所有物件以及已發行物件之結構描述的結構描述快照集，但不含資料。 然後使用包含結構描述快照集中物件與結構描述以及訂閱之資料分割所屬資料的快照集，來初始化每個訂閱。 如果有多個訂閱收到給定的資料分割 (即收到相同的結構描述和資料)，該資料分割的快照集只會建立一次，多個訂閱均從同一快照集初始化。 如需參數化資料列篩選器的詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 您可以使用下列三種方法之一為含參數化篩選的發行集建立快照集：  
  
-   為每個資料分割預先產生快照集。 您可以使用此選項控制快照集的產生時間。  
  
     您也可以選擇在排程時間重新整理快照集。 訂閱至已建立快照集之資料分割的新「訂閱者」，將收到最新的快照集。  
  
-   允許訂閱者在首次執行同步處理時，要求快照集產生和應用程式。 使用此選項可讓新「訂閱者」執行同步處理，而無需管理員介入 (必須在「發行者」端執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，才允許產生快照集)。  
  
    > [!NOTE]  
    >  如果發行集內的一或多個發行項的篩選產生對每個訂閱而言是唯一的非重疊資料分割，則只要合併代理程式一執行，就會清除中繼資料。 這表示分割快照集會更快過期。 使用這個選項時，您應該考慮允許訂閱者初始化快照集的產生與傳遞。 如需有關篩選選項的詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
-   使用「快照集代理程式」為每個「訂閱者」手動產生快照集。 然後，「訂閱者」必須為「合併代理程式」提供快照集位置，才能擷取和套用正確的快照集。  
  
    > [!NOTE]  
    >  此選項支援回溯相容性，不允許 FTP 快照集共用。  
  
 最靈活的方法是將預先產生的快照集選項和「訂閱者」要求的快照集選項組合使用：快照集會預先產生，並在排程時間重新整理 (通常在離峰時段)，但如果建立了需要新資料分割的訂閱，則「訂閱者」可以產生自己的快照集。  
  
 請考慮使用 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]，此產品具有行動工作能力，可將庫存傳遞至個別商店。 每個業務員都會收到其登入帳戶的訂閱 (擷取業務員服務之商店的資料)。 管理員選擇預先產生快照集，並在每個週日重新整理這些快照集。 偶而，會有新使用者新增到系統中，並且需要無可用快照集之資料分割中的資料。 管理員也可以選擇允許「訂閱者」初始化的快照集，以避免由於快照集不可用而造成「訂閱者」無法訂閱發行集的情況。 當新的「訂閱者」首次進行連接時，會為指定的資料分割建立快照集，並套用到「訂閱者」(必須在「發行者」端執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，才允許產生快照集)。  
  
 若要為含參數化篩選的發行集建立快照集，請參閱＜ [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)＞。  
  
## <a name="security-settings-for-the-snapshot-agent"></a>快照集代理程式的安全性設定  
 「快照集代理程式」會為每個資料分割建立快照集。 對於預先產生的快照集和「訂閱者」所需的快照集，代理程式會在建立發行集的快照集代理程式作業 (此作業由「新增發行集精靈」或 **sp_addpublication_snapshot**建立) 時指定的認證下執行並進行連接。 若要變更認證，請使用 **sp_changedynamicsnapshot_job**。 如需詳細資訊，請參閱 [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
