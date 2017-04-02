---
title: "為交易式發行集啟用使用備份的初始化 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "手動訂閱初始化 [SQL Server 複寫]"
  - "訂閱 [SQL Server 複寫], 初始化"
  - "初始化訂閱 [SQL Server 複寫], 不使用快照集"
  - "異動複寫, 備份與還原"
  - "備份 [SQL Server 複寫], 異動複寫"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 為交易式發行集啟用使用備份的初始化 (SQL Server Management Studio)
  若要從備份初始化交易式發行集的訂閱，請啟用發行集以允許從備份進行初始化，然後在建立訂閱時指定備份資訊：  
  
-   啟用發行集上 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
-   使用預存程序指定備份資訊 [sp_addsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 如需有關所需的參數 **sp_addsubscription**, ，請參閱 [初始化交易式訂閱，從備份 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)。  
  
### 若要啟用使用備份的初始化  
  
1.  在 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取值 **True** 的 **允許從備份檔案初始化** 選項。  
  
## 另請參閱  
 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  