---
title: 為交易式發行集啟用使用備份的初始化（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f5e22614c8c4f5250db3966e747b686091512774
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010716"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>為交易式發行集啟用使用備份的初始化 (SQL Server Management Studio)
  若要從備份初始化交易式發行集的訂閱，請啟用發行集以允許從備份進行初始化，然後在建立訂閱時指定備份資訊：  
  
-   在 [**發行集屬性 \<Publication> -** ] 對話方塊的 [**訂閱選項**] 頁面上啟用發行集。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)＞。  
  
-   使用預存程序 [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 指定備份資訊。 如需 **sp_addsubscription** 所需參數的詳細資訊，請參閱[從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](initialize-a-transactional-subscription-from-a-backup.md)。  
  
### <a name="to-enable-initialization-with-a-backup"></a>若要啟用使用備份的初始化  
  
1.  在 [**發行集 \<Publication> 屬性-** ] 對話方塊的 [**訂閱選項**] 頁面上，針對 [**允許從備份檔案初始化**] 選項選取 [ **True** ] 值。  
  
## <a name="see-also"></a>另請參閱  
 [不使用快照集初始化交易式訂閱](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
