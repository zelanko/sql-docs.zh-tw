---
title: "在散發資料庫中檢視複寫的命令和其他資訊 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
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
  - "sp_browsereplcmds"
  - "異動複寫, 監視"
  - "散發資料庫 [SQL Server 複寫], 檢視複寫指令"
  - "檢視複寫指令"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在散發資料庫中檢視複寫的命令和其他資訊 (複寫 Transact-SQL 程式設計)
  在使用異動複寫時，交易命令在傳播到所有「訂閱者」之前或在「訂閱者」端的「散發代理程式」 您可以使用複寫預存程序，以程式設計的方式檢視散發資料庫中的這些暫止命令。 如需詳細資訊，請參閱 [複寫預存程序 & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。  
  
### 若要在散發資料庫中檢視從所有交易式發行集所複寫的命令  
  
1.  在散發資料庫的散發者端，執行 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)。  
  
### 若要在散發資料庫中，檢視從使用異動複寫所發行之特定發行項或特定資料庫複寫的命令  
  
1.  （選擇性）在發行集資料庫的發行者，執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)。 指定 **@publication** 和 **@article**。 記下的值 **發行項識別碼** 結果集中。  
  
2.  在散發資料庫的散發者端，執行 [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)。 （選擇性）指定步驟 2 的發行項識別碼 **@article_id**。 （選擇性）指定發行集資料庫的識別碼 **@publisher_database_id**, ，其可從取得 **database_id** 中的資料行 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視。  
  
## 另請參閱  
 [Programmatically Monitor Replication](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  