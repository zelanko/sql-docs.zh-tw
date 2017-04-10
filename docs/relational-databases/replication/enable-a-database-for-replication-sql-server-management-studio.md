---
title: "為複寫啟用資料庫 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料庫 [SQL Server 複寫]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 為複寫啟用資料庫 (SQL Server Management Studio)
  複寫的成員時隱含啟用資料庫 **sysadmin** 固定的伺服器角色與新的發行集精靈 」 建立發行集。 成員 **sysadmin** 固定的伺服器角色也可以啟用資料庫進行複寫，這樣的成員 **db_owner** 固定的資料庫角色可以建立一或多個發行集，該資料庫中。 若要明確啟用資料庫，使用 **發行集資料庫** 頁面 **發行者屬性-\< 發行者>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱 [建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 若要為複寫啟用資料庫  
  
1.  在 **發行集資料庫** 頁面 **發行者屬性-\< 發行者>** 對話方塊中，選取 **交易式** 和/或 **合併** 針對每個您想要複寫的資料庫] 核取方塊。 選取 **交易式** 啟用快照集複寫的資料庫。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  