---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018752 錯誤"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|18752|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|一次只有一個記錄讀取器代理程式或記錄檔相關程序 (sp_repldone, sp_replcmds, and sp_replshowcmds) 可連接到資料庫。 若您已執行記錄檔相關程序，請卸除執行程序的連接，或者利用該連接執行 sp_replflush 之後，再啟動記錄讀取器代理程式或執行其他記錄檔相關程序。|  
  
## 說明  
 多個目前連線正在嘗試執行下列任一項︰ **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds**。 預存程序 [sp_repldone & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) 和 [sp_replcmds & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 預存程序用於記錄讀取器代理程式找出並更新中已發行的資料庫複寫的交易的相關資訊。 預存程序 [sp_replshowcmds & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) 用於特定類型的交易式複寫的問題進行疑難排解。  
  
 此錯誤在下列情況下產生：  
  
-   如果已發行資料庫的「記錄讀取器代理程式」正在執行，而第二個「記錄讀取器代理程式」嘗試針對相同的資料庫執行，則錯誤就會在第二個代理程式中產生，並且出現在代理程式記錄中。  
  
     若出現多個代理程式的情況，則可能其中一個代理程式是被遺棄處理的結果。  
  
-   如果已發行的資料庫記錄讀取器代理程式已啟動，且使用者執行 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** 針對相同的資料庫執行預存程序所在的應用程式中引發的錯誤 (例如 **sqlcmd**)。  
  
-   如果沒有記錄讀取器代理程式正在執行已發行資料庫，且使用者執行 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** ，之後也未關閉記錄讀取器代理程式會嘗試連接至資料庫時引發的程序執行，所以的連線錯誤。  
  
## 使用者動作  
 下列步驟可以幫助您對此問題進行疑難排解。 如果任一步驟允許「記錄讀取器代理程式」在沒有錯誤的情況下啟動，則無需完成剩餘步驟。  
  
-   檢查「記錄讀取器代理程式」的記錄，以便尋找可能導致此錯誤的其他任何錯誤。 複寫監視器中檢視代理程式狀態和錯誤詳細資料的相關資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
-   檢查輸出中的 [sp_who & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 針對特定處理序識別碼 (Spid) 連線到已發行的資料庫。 關閉可能已執行的任何連線 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds**。  
  
-   重新啟動「記錄讀取器代理程式」。 如需詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
-   在「散發者」上重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務 (使其在叢集中離線或上線)。 如果無法執行排程的工作可能會 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** 從其他任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，請重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這些執行個體的代理程式。 如需詳細資訊，請參閱 [啟動、 停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)。  
  
-   執行 [sp_replflush & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 在 「 發行者 」 上發行集資料庫，然後重新啟動記錄讀取器代理程式。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  