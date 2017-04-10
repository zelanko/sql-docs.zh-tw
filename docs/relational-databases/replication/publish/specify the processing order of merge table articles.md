---
title: "指定合併資料表發行項的處理順序 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
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
  - "發行項 [SQL Server 複寫], 處理順序"
  - "合併式複寫 [SQL Server 複寫], 發行項處理順序"
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 指定合併資料表發行項的處理順序 (複寫 Transact-SQL 程式設計)
  合併式複寫可讓您指定在同步處理期間，合併代理程式處理發行項的順序。 當您使用複寫預存程序建立發行項時，可以透過程式設計方式對每一個發行項指派順序。 發行項會依照從最低值到最高值的順序來處理。 如果兩個發行項有相同的值，就會同時處理它們。 如需詳細資訊，請參閱 [指定處理順序合併發行項的](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。  
  
### 為新的合併發行項指定處理順序  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定整數值，表示發行項的處理順序 **@processing_order**。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  當建立排序的發行項時，您應該在發行項順序值之間留一些間距。 這樣可讓您在將來更容易設定新的值。 例如，如果您有三個發行項，您必須指定固定的處理順序，設定的值 **@processing_order** 至 10、 20 和 30，而非 1、 2 和 3，分別。  
  
### 變更合併發行項的處理順序  
  
1.  若要判斷發行項的處理順序，請執行 [sp_helpmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 並記下的值 **processing_order** 結果集中。  
  
2.  在發行集資料庫的發行者，執行 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **processing_order** 的 **@property** 和整數值，表示處理順序 **@value**。  
  
## 另請參閱  
 [指定合併發行項的處理順序](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  