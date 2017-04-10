---
title: "MSSQL_ENG021797 | Microsoft Docs"
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
  - "MSSQL_ENG021797 錯誤"
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021797
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21797|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|'%s' 必須是有效的 Windows 登入，其格式為：'MACHINE\Login' 或 'DOMAIN\Login'。 請參閱 '%s' 的文件集。|  
  
## 說明  
 如果指定的值的下列複寫預存程序便會引發這個錯誤 **@job_login** 參數是 null 或無效。 如果的成員，可能會發生此錯誤 **db_owner** 固定的資料庫角色會執行指令碼從舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 安全性模型在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中已變更，同時必須更新這些指令碼。  
  
-   [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 成員可以執行這些預存程序 **sysadmin** 上適當的伺服器或成員的固定的伺服器角色 **db_owner** 固定的資料庫角色中適當的資料庫。 每個預存程序均會建立一個代理程式作業，並允許您指定代理程式執行所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 中的使用者 **sysadmin** 角色、 建立代理程式作業會以隱含方式即使未指定 Windows 帳戶 （如果指定的帳戶，則它必須是有效），代理程式的內容下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 適當的伺服器上的代理程式服務帳戶。 雖然不需要此帳戶，但安全性最佳做法是為代理程式指定不同的帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 使用者動作  
 請確認指定有效的 Windows 帳戶的 **@job_login** 的每個程序的參數。 若您有上一版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫指令碼，請更新這些指令碼以納入 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所需的預存程序和參數。 如需詳細資訊，請參閱 [升級複寫指令碼 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  