---
title: "在同步處理期間執行指令碼 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "同步處理 [SQL Server 複寫], 指令碼"
  - "指令碼 [SQL Server 複寫], 同步處理和"
  - "sp_addscriptexec"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 在同步處理期間執行指令碼 (複寫 Transact-SQL 程式設計)
  複寫可支援視需要針對交易式與合併式發行集的訂閱者執行指令碼。 這項功能會將指令碼複製到複寫工作目錄，然後使用 **sqlcmd** 套用訂閱者的指令碼。 依預設，如果針對交易式發行集的訂閱套用指令碼時發生失敗，則散發代理程式將會停止。 您可以使用複寫預存程序以程式設計的方式指定要執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
### 針對快照式、交易式或合併式發行集的所有訂閱者指定要執行的指令碼  
  
1.  撰寫及測試將會視需要執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
2.  將指令碼檔案儲存到可由發行集之快照集代理程式存取的位置。  
  
3.  在發行集資料庫的發行者，執行 [sp_addscriptexec & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md)。 指定 **@publication**, ，具有完整的 UNC 路徑，如步驟 2 中建立的指令碼檔案名稱 **@scriptfile**, ，和下列其中一個值 **@skiperror**:  
  
    -   **0** -代理程式將會停止執行指令碼，如果發生錯誤。  
  
    -   **1** -代理程式將會記錄錯誤並繼續執行指令碼發生錯誤時。  
  
4.  當下一次執行代理程式來同步處理訂閱時，指定的指令碼將會在每一個訂閱者上執行。  
  
## 另請參閱  
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)  
  
  