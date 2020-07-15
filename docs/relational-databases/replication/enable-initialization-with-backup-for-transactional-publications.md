---
title: 啟用使用備份的初始化 (交易式)
description: 了解如何在 SQL Server 中針對交易式發行集啟用備份的初始化。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0416bc5ff174520ef5548ec6ad91eea647eafaf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653037"
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>為交易式發行集啟用使用備份的初始化
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  若要從備份初始化交易式發行集的訂閱，請啟用發行集以允許從備份進行初始化，然後在建立訂閱時指定備份資訊：  
  
-   在 [發行集屬性 - \<Publication>] 對話方塊的 [訂閱選項] 頁面上啟用發行集。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
-   使用預存程序 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 指定備份資訊。 如需 **sp_addsubscription** 所需參數的詳細資訊，請參閱[從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)。  
  
### <a name="to-enable-initialization-with-a-backup"></a>若要啟用使用備份的初始化  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [訂閱選項] 頁面上，將 [允許從備份檔案初始化] 選項選取為值 [True]。  
  
## <a name="see-also"></a>另請參閱  
 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
