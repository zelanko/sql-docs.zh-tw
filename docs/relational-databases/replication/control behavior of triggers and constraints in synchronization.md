---
title: "在同步處理期間控制觸發程序和條件約束的行為 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "識別 [SQL Server 複寫]"
  - "條件約束 [SQL Server], 複寫"
  - "觸發程序 [SQL Server], 複寫"
  - "觸發程序 [SQL Server 複寫]"
  - "條件約束 [SQL Server 複寫]"
  - "NOT FOR REPLICATION 選項"
  - "NFR 選項"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在同步處理期間控制觸發程序和條件約束的行為 (複寫 Transact-SQL 程式設計)
  同步處理期間，複寫代理程式執行 [插入 & #40。TRANSACT-SQL & #41;](../../t-sql/statements/insert-transact-sql.md), ，[更新 & #40。TRANSACT-SQL & #41;](../../t-sql/queries/update-transact-sql.md), ，和 [刪除 & #40。TRANSACT-SQL & #41;](../../t-sql/statements/delete-transact-sql.md) 複寫的資料表，可能會造成資料操作語言 (DML) 觸發程序來執行這些資料表的陳述式。 在某些情況下，您可能需要在同步處理期間避免這些觸發程序的引發或避免條件約束的強制使用。 這個行為取決於觸發程序或條件約束的建立方式而定。  
  
### 在同步處理期間避免觸發程序的執行  
  
1.  在建立新的觸發程序時，指定 NOT FOR REPLICATION 選項的 [建立觸發程序 & #40。TRANSACT-SQL & #41;](../../t-sql/statements/create-trigger-transact-sql.md)。  
  
2.  現有的觸發程序，指定 NOT FOR REPLICATION 選項的 [ALTER TRIGGER & #40。TRANSACT-SQL & #41;](../../t-sql/statements/alter-trigger-transact-sql.md)。  
  
### 在同步處理期間避免條件約束的強制使用  
  
1.  在建立新的 CHECK 或 FOREIGN KEY 條件約束時，指定 CHECK NOT FOR REPLICATION 選項的條件約束定義中 [CREATE TABLE & #40。TRANSACT-SQL & #41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## 另請參閱  
 [建立資料表 #40; 資料庫引擎 & #41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  