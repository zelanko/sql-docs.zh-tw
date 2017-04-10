---
title: "指定合併訂閱類型和衝突解決優先權 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合併式複寫衝突解決 [SQL Server 複寫], 合併訂閱解析程式"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 指定合併訂閱類型和衝突解決優先權 (SQL Server Management Studio)
  在「新增訂閱精靈」的 **[訂閱類型]** 頁面中指定合併訂閱類型和衝突解決優先權。 如需使用此精靈的詳細資訊，請參閱＜ [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) ＞和＜ [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)＞。  
  
 無法修改訂閱類型之後，建立訂閱，但優先權可以修改伺服器訂閱類型，在 **訂閱屬性-\< 發行者>: \< u>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
### 若要指定合併訂閱類型與衝突解決優先權  
  
1.  在「新增訂閱精靈」的 **[訂閱類型]** 頁面上，為 **[訂閱類型]** 選項選取 **[用戶端]** 或 **[伺服器]** 。  
  
2.  如果您選取的訂閱類型 **Server**, ，也輸入的值 (0.00 到 99.99) **衝突解決優先權** 選項。  
  
### 若要修改衝突解決優先權  
  
1.  在 **訂閱屬性-\< 發行者>: \< u>** 在發行者上，輸入的值 (0.00 到 99.99) **優先順序** 選項。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  