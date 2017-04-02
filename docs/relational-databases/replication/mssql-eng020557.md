---
title: "MSSQL_ENG020557 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020557 錯誤"
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# MSSQL_ENG020557
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20557|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|代理程式關閉。 如需詳細資訊，請參閱 SQL Server Agent 作業記錄中的作業 '%s'。|  
  
## 說明  
 複寫代理程式已關閉，而未將原因寫入適當的記錄資料表，或者代理程式在處理序仍執行時關閉。  
  
## 使用者動作  
  
-   重新啟動代理程式，查看現在執行是否已無錯誤。 如需詳細資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
-   請檢查代理程式記錄和作業記錄是否同時發生其他錯誤。 如需有關如何檢視代理程式狀態以及複寫監視器中有關錯誤的詳細資訊，請參閱下列主題：  
  
    -   快照集代理程式、 記錄讀取器代理程式和佇列讀取器代理程式，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
    -   針對散發代理程式 」 和 「 合併代理程式，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
-   確認基本連線運作，由代理程式，並使用公用程式，例如連線至各電腦的電腦之間 **sqlcmd** 公用程式。 連接時，請使用代理程式建立連接的相同帳戶。 如需各代理程式帳戶所需的權限的詳細資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
-   如果在建立或套用快照集時發生錯誤，則請檢查快照集目錄中的檔案以找出錯誤。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和其他錯誤訊息。 如需有關如何設定複寫記錄的詳細資訊，請參閱 Microsoft 知識庫文件 [312292](http://support.microsoft.com/kb/312292)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  