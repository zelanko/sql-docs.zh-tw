---
title: "為交易式發行集啟用使用備份的初始化 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6840a9eddbdf15b75a19d7b04615cffc44a0d3e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>為交易式發行集啟用使用備份的初始化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 若要從備份初始化交易式發行集的訂閱，請啟用發行集以允許從備份進行初始化，然後在建立訂閱時指定備份資訊：  
  
-   在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面上啟用發行集。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
-   使用預存程序 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 指定備份資訊。 如需 **sp_addsubscription** 所需參數的詳細資訊，請參閱[從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)。  
  
### <a name="to-enable-initialization-with-a-backup"></a>若要啟用使用備份的初始化  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面上，將 [允許從備份檔案初始化] 選項選取為值 [True]。  
  
## <a name="see-also"></a>另請參閱  
 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
