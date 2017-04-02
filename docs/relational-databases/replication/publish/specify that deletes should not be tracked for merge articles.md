---
title: "指定不應該為合併發行項追蹤刪除 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "條件式刪除追蹤 [SQL Server 複寫]"
  - "合併式複寫 [SQL Server 複寫], 條件式刪除追蹤"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 指定不應該為合併發行項追蹤刪除 (複寫 Transact-SQL 程式設計)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 依預設，合併式複寫會同步處理發行者與散發者之間的 DELETE 命令。 合併式複寫可讓您保留訂閱資料庫中的資料列，即時已從發行集中刪除資料列 (反之亦然)。 您可透過程式設計方式指定在建立新的發行項時要忽略 DELETE 命令，或是可以在稍後使用複寫預存程序來啟用這項功能。  
  
> [!IMPORTANT]  
>  啟用這項功能將會導致非聚合的情況，這表示訂閱者上的資料將不會正確反映發行者上的資料。 您必須實作自己的機制，以手動移除刪除的資料列。  
  
### 指定新的合併發行項要忽略刪除  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定的值為 **false** 的 **@delete_tracking**。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集的值 **delete_tracking** 必須是兩個發行項相同。  
  
### 指定現有的合併發行項要忽略刪除  
  
1.  若要判斷發行項是否已啟用錯誤補償，執行 [sp_helpmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 並記下的值 **delete_tracking** 結果集中。 如果這個值是 **0**，就表示已經忽略刪除。  
  
2.  如果步驟 1 中的值為 **1**, ，執行 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定的值為 **delete_tracking** 的 **@property**, ，而值為 **false** 的 **@value**。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集的值 **delete_tracking** 必須是兩個發行項相同。  
  
## 另請參閱  
 [使用條件式刪除追蹤最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  