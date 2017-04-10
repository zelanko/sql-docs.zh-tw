---
title: "為異動複寫啟用協調備份 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
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
  - "異動複寫, 備份與還原"
  - "sp_replicationdboption"
  - "與備份同步 [SQL Server 複寫]"
  - "協調備份 [SQL Server 複寫]"
  - "備份 [SQL Server 複寫], 異動複寫"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 為異動複寫啟用協調備份 (複寫 Transact-SQL 程式設計)
  在啟用異動複寫的資料庫時，可以指定所有的交易必須先備份，才能傳遞到散發資料庫。 也可以在散發資料庫上啟用協調備份，如此在傳播到「散發者」的交易進行備份之前，發行集資料庫的交易記錄都不會遭到截斷。 如需詳細資訊，請參閱 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
### 若要為使用異動複寫所發行的資料庫啟用協調備份  
  
1.  在 「 發行者 」 使用 [DATABASEPROPERTYEX & #40。TRANSACT-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函數傳回 **IsSyncWithBackup** 發行集資料庫的屬性。 如果此函數會傳回 **1**, 協調備份已發行資料庫已啟用。  
  
2.  如果在步驟 1 中的函式傳回 **0**, ，執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定的值為 **與備份同步** 的 **@optname**, ，和 **true** 的 **@value**。  
  
    > [!NOTE]  
    >  如果您變更 **與備份同步** 選項 **false**, ，發行集資料庫的截斷點將會更新間隔或之後記錄讀取器代理程式執行時，如果記錄讀取器代理程式會持續執行。 最大間隔由控制 **– MessageInterval** 代理程式參數 （預設值是 30 秒）。  
  
### 若要啟用散發資料庫的協調備份  
  
1.  在散發者 」 使用 [DATABASEPROPERTYEX & #40。TRANSACT-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函數傳回 **IsSyncWithBackup** 散發資料庫的屬性。 如果此函數會傳回 **1**, 協調備份散發資料庫已啟用。  
  
2.  如果在步驟 1 中的函式傳回 **0**, ，執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 在散發資料庫的散發者端。 指定的值為 **與備份同步** 的 **@optname** 和 **true** 的 **@value**。  
  
### 若要停用協調備份  
  
1.  在發行集資料庫的發行者或散發資料庫的散發者端，執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 指定的值為 **與備份同步** 的 **@optname** 和 **false** 的 **@value**。  
  
  