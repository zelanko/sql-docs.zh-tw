---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "MSSQL_ENG021798 錯誤"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21798|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|必須先透過 '%s' 新增 '%s' 代理程式工作，方可繼續。 請參閱 '%s' 的文件集。|  
  
## 說明  
 若要建立發行集，您必須是屬於 **sysadmin** 上 「 發行者 」 或成員的固定的伺服器角色 **db_owner** 發行集資料庫中的固定的資料庫角色。 如果您的成員 **db_owner** 如果角色，此錯誤會產生︰  
  
-   您會從 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 執行指令碼。 安全性模型在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中已變更，同時必須更新這些指令碼。  
  
-   預存程序 **sp_addpublication** 執行之前，先執行 [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 適用於所有交易式發行集。  
  
-   預存程序 **sp_addpublication** 執行之前，先執行 [sp_addqreader_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)。 這適用於已啟用佇列更新訂閱的交易式發行集 (值為 TRUE **@allow_queued_tran** 參數 **sp_addpublication**)。  
  
 預存程序 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 每個建立的代理程式作業，並可讓您指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶執行代理程式。 中的使用者 **sysadmin** 角色，代理程式作業以隱含方式，才會建立 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 不會執行; 代理程式的內容下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在散發者代理程式服務帳戶。 雖然 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 並不需要使用者在 **sysadmin** 角色，它是安全性最佳做法，代理程式指定不同的帳戶。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 使用者動作  
 確保您以正確的順序執行程序。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。 若您有舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫指令碼，請更新這些指令碼以納入 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本所需的預存程序和參數。 如需詳細資訊，請參閱 [升級複寫指令碼 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  