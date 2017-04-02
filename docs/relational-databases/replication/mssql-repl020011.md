---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL020011 錯誤"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20011|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|該處理無法執行 '%1' (在 '%2')。|  
  
## 說明  
 此錯誤可能會引發許多情況下處理，例如當 「 記錄讀取器代理程式執行的交易式複寫期間 **sp_replcmds** (程序無法執行 'sp_replcmds' 上 \< 伺服器名稱>) 或 **sp_repldone** (該處理無法執行 'sp_repldone' 上 \< 伺服器名稱>)。  
  
## 使用者動作  
 如果只是從備份還原的資料庫中，會引發這個錯誤，請確定您已經依照備份和還原文件，包括執行中所述的步驟 **sp_replrestart** 的話。 如需詳細資訊，請參閱 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此錯誤為內部處理錯誤，如果它在還原以外的情況下出現，通常表示必須移除並重新設定複寫。 如果您無法移除複寫，請連絡客戶支援部門尋求幫助。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  