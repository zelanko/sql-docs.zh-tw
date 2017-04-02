---
title: "Database Mail 記錄與稽核 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "稽核 [SQL Server]"
  - "Database Mail [SQL Server], 稽核"
  - "記錄檔 [Database Mail]"
  - "稽核 [SQL Server], Database Mail"
  - "Database Mail [SQL Server], 記錄"
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# Database Mail 記錄與稽核
  Database Mail 記錄功能的設計目的是要提供方法來隔離並更正問題。 Database Mail 會將記錄資訊儲存至 **msdb** 資料庫。 Database Mail 電子郵件內容、電子郵件狀態和任何收到之訊息 (例如錯誤) 的相關資訊，是透過 Database Mail 進行記錄，而且可用於進行疑難排解和稽核。  
  
## Database Mail 記錄檔  
 **msdb** 資料庫中的資料表會記錄來自 [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)的資訊。 [Database Mail 檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) 會公開資料表以供疑難排解之用。 如果 Service Broker 無法啟動外部程式、外部程式發生網路問題或 Simple Mail Transport Protocol (SMTP) 伺服器拒絕電子郵件訊息，則 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) 檢視中會出現錯誤。 當外部程式無法登入 **msdb** 資料表時，該程式會將錯誤記錄到 Windows 應用程式事件記錄檔中。  
  
 **msdb** 資料庫中的內部資料表包含從 Database Mail 送出的電子郵件訊息與附加檔案，以及每封訊息的目前狀態。 Database Mail 會在每個訊息處理後更新這些資料表。  
  
## Database Mail 稽核工作  
  
|||  
|-|-|  
|**檢閱和管理 Database Mail 記錄檔**|**主題連結**|  
|檢查個別訊息的傳遞狀態|[檢查使用 Database Mail 傳送之電子郵件訊息的狀態](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|清除 Database Mail 訊息、附件和記錄項目|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|封存資料庫電子郵件訊息和記錄檔|[建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件記錄檔](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## 另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  