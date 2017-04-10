---
title: "在套用快照集的前後執行指令碼 (SQL Server Management Studio) | Microsoft Docs"
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
  - "快照集 [SQL Server 複寫], 指令碼"
  - "指令碼 [SQL Server 複寫], 快照集"
  - "快照式複寫 [SQL Server], 指令碼"
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在套用快照集的前後執行指令碼 (SQL Server Management Studio)
  指定選擇性的指令碼執行之前或之後在套用快照集 **快照** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
> [!NOTE]  
>  並未提供這些選項如果 **快照集格式** 選項設定為 **字元**。  
  
### 若要在套用快照集的前後執行指令碼  
  
1.  在 **快照** 頁面 **發行集屬性-\< 發行集>** ] 對話方塊中︰  
  
    -   若要指定指令碼執行在套用快照集之前，請按一下 [ **瀏覽** 指令碼中，瀏覽或輸入的路徑中的指令碼 **之前套用快照集，執行此指令碼** 文字方塊。  
  
        > [!NOTE]  
        >  「散發代理程式」或「合併代理程式」必須具有指定目錄的讀取權限。 如果使用提取訂閱，您必須指定共用的目錄做為通用的命名慣例 (UNC) 路徑，例如 \\\computername\scripts\myscript.sql。  
  
    -   若要指定在套用快照集之後執行的指令碼，請按一下 [ **瀏覽** 指令碼中，瀏覽或輸入的 UNC 路徑中的指令碼 **之後套用快照集，執行這個指令碼** 文字方塊。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另請參閱  
 [設定快照集屬性和 #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [在套用快照集之前及之後執行指令碼](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  