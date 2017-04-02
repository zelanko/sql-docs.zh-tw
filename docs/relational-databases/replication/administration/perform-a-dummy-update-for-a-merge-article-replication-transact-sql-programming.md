---
title: "執行合併發行項的虛擬更新 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "sp_mergedummyupdate"
  - "虛擬更新 [SQL Server 複寫]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 執行合併發行項的虛擬更新 (複寫 Transact-SQL 程式設計)
  合併式複寫會使用觸發程序做為複寫程序的一部分；對已發行資料表進行更新時，就會引發更新觸發程序。 在某些情況下，可以不引發觸發程序而更新資料，例如在 WRITETEXT 和 UPDATETEXT 作業期間。 在這些情況下，您需要加入虛擬 UPDATE 陳述式以明確地複寫變更。 您可以使用複寫預存程序加入虛擬 UPDATE 陳述式。  
  
### 若要加入虛擬 UPDATE 陳述式  
  
1.  在需要虛擬更新的已發行合併資料表中的資料列上執行作業 (例如，UPDATETEXT)。  
  
2.  在伺服器上 （「 發行者 」 或 「 訂閱者 」） 進行變更的資料庫上，執行 [sp_mergedummyupdate & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md)。 指定的資料表上所做的變更 **@source_object**, ，和已變更的資料列的唯一識別碼 **@rowguid**。  
  
3.  同步處理訂閱來複寫已變更的資料列。  
  
  