---
title: "設定交易式發行集的散發保留週期 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "交易保留週期 [SQL Server 複寫]"
  - "保留週期 [SQL Server 複寫]"
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 設定交易式發行集的散發保留週期 (SQL Server Management Studio)
  指定的最小散發保留期限和最大散發保留期限 **散發資料庫屬性-\< DistributionDatabase>** 對話方塊。 這是可從 **一般** 頁面 **散發者屬性-\< 散發者>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱 [檢視和修改 「 散發者 」 和 「 發行者 」 屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### 若要指定散發保留期限  
  
1.  在 **一般** 頁面 **散發者屬性-\< 散發者>** 對話方塊方塊中，按一下 [內容] 按鈕 (**...**) 散發資料庫。  
  
2.  若要指定最小散發保留期限，請輸入中的值 **至少** 方塊; 若要指定最大散發保留期限，請輸入中的值 **，但不是能超過** 方塊。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另請參閱  
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  