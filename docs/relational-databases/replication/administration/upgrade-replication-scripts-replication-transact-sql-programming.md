---
title: "升級複寫指令碼 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
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
  - "指令碼 [SQL Server 複寫], 升級"
  - "升級 SQL Server, 複寫的資料庫"
  - "升級複寫的應用程式"
  - "複寫 [SQL Server], 指令碼處理"
  - "複寫 [SQL Server], 升級"
  - "升級複寫的資料庫"
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 升級複寫指令碼 (複寫 Transact-SQL 程式設計)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼檔案可以用於以程式設計的方式設定複寫拓撲。 如需詳細資訊，請參閱 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)。  
  
> [!IMPORTANT]  
>  雖然並不一定要升級由 **sysadmin** 角色的成員所執行的指令碼，但建議您依照本主題所述修改現有的指令碼。 請根據主題＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞的「代理程式所需的權限」一節所述，為每個複寫代理程式指定具有最小權限的帳戶。  
  
 這些安全性改進會影響現有指令碼中的下列預存程序，讓您可以明確地指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶，並在這些帳戶下執行複寫代理程式工作，對權限可以有更多的控制：  
  
-   **sp_addpublication_snapshot**:  
  
     您現在應該提供 「 Windows 認證 **@job_login** 和 **@job_password** 執行時 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 若要建立快照集代理程式執行 「 散發者 」 的作業。  
  
-   **sp_addpushsubscription_agent**:  
  
     您現在應該執行 [sp_addpushsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) 若要明確地加入作業，並提供 「 Windows 認證 (**@job_login** 和 **@job_password**) 在散發者端執行散發代理程式作業。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addmergepushsubscription_agent**:  
  
     您現在應該執行 [sp_addmergepushsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) 若要明確地加入作業，並提供 「 Windows 認證 (**@job_login** 和 **@job_password**) 在散發者執行合併代理程式作業。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addpullsubscription_agent**:  
  
     您現在應該提供 「 Windows 認證 **@job_login** 和 **@job_password** 執行時 [sp_addpullsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 若要建立 「 散發代理程式執行在訂閱者 」 的作業。  
  
-   **sp_addmergepullsubscription_agent**:  
  
     您現在應該提供 「 Windows 認證 **@job_login** 和 **@job_password** 執行時 [sp_addmergepullsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 若要建立 「 合併代理程式執行在訂閱者 」 的作業。  
  
-   **sp_addlogreader_agent**:  
  
     您現在應該執行 [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) 若要手動加入作業，並提供 「 記錄讀取器代理程式執行 「 散發者 」 的 Windows 認證。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立交易式發行集時自動完成。  
  
-   **sp_addqreader_agent**:  
  
     您現在應該執行 [sp_addqreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) 若要手動加入作業，並提供 「 散發者端的佇列讀取器代理程式執行的 Windows 認證。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立支援佇列更新的交易式發行集時自動完成。  
  
 中導入的安全性模型中 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ，複寫代理程式一律會進行連線的本機執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 Windows 驗證中提供的認證 **@job_name** 和 **@job_password**。 如需有關在執行複寫代理程式作業時所使用 Windows 帳戶之需求的資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果將認證儲存在指令碼檔案中，請確定該檔案本身受到安全保護。  
  
### 若要升級設定快照式或交易式發行集的指令碼  
  
1.  在現有的指令碼之前 [sp_addpublication & #40;TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ，執行 [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定 Windows 認證的 「 記錄讀取器代理程式執行 **@job_name** 和 **@job_password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 如此會建立發行集資料庫的「記錄讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有交易式發行集才需要這個步驟，快照式發行集不需要。  
  
2.  （選擇性）之前 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ，執行 [sp_addqreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) 在散發資料庫的散發者端。 指定 Windows 認證的佇列讀取器代理程式執行 **@job_name** 和 **@job_password**。 如此會為「散發者」建立「佇列讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有支援佇列更新訂閱者的交易式發行集才需要這個步驟。  
  
3.  （選擇性）更新執行 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 若要設定非預設的值針對實作新複寫功能的參數。  
  
4.  之後 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ，執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定 **@publication** 和 Windows 認證的快照集代理程式執行 **@job_name** 和 **@job_password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
5.  （選擇性）更新執行 [sp_addarticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 若要設定非預設的值針對實作新複寫功能的參數。  
  
### 若要升級將訂閱加入至快照式或交易式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「散發代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   提取訂閱，更新執行 [sp_addpullsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 提供在 「 訂閱者 」 的散發代理程式執行的 Windows 認證 **@job_name** 和 **@job_password**。 這是執行後 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
    -   對於發送訂閱，請執行 [sp_addpushsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) 在 「 發行者 」。 指定 **@subscriber**, ，**@subscriber_db**, ，**@publication**, ，散發代理程式執行 「 散發者 」 的 Windows 認證 **@job_name** 和 **@job_password**, ，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)。 這是執行後 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
### 若要升級設定合併式發行集的指令碼  
  
1.  （選擇性）在現有的指令碼，來更新執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 若要設定非預設的值針對實作新複寫功能的參數。  
  
2.  之後 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定 **@publication** 和 Windows 認證的快照集代理程式執行 **@job_name** 和 **@job_password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
3.  （選擇性）更新執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要設定非預設的值針對實作新複寫功能的參數。  
  
### 若要升級將訂閱加入至合併式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「合併代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   提取訂閱，更新執行 [sp_addmergepullsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 提供 Windows 認證到訂閱者端合併代理程式執行 **@job_name** 和 **@job_password**。 這是執行後 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
    -   對於發送訂閱，請執行 [sp_addmergepushsubscription_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) 在 「 發行者 」。 指定 **@subscriber**, ，**@subscriber_db**, ，**@publication**, ，Windows 認證的合併代理程式在散發者端執行 **@job_name** 和 **@job_password**, ，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)。 這是執行後 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Product 資料表建立交易式發行集。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Customers 資料表建立合併式發行集。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## 範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## 範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  提供在執行階段使用 Windows 認證 **sqlcmd** 指令碼變數。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## 另請參閱  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [升級複寫的資料庫](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  