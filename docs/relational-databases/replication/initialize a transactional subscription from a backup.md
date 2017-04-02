---
title: "從備份初始化交易式訂閱 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "手動訂閱初始化 [SQL Server 複寫]"
  - "訂閱 [SQL Server 複寫], 初始化"
  - "初始化訂閱 [SQL Server 複寫], 不使用快照集"
  - "異動複寫, 備份與還原"
  - "備份 [SQL Server 複寫], 異動複寫"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 從備份初始化交易式訂閱 (複寫 Transact-SQL 程式設計)
  雖然通常會使用快照集初始化交易式發行集的訂閱，但是可以使用複寫預存程序從備份初始化訂閱。 如需詳細資訊，請參閱 [初始化交易式訂閱不使用快照集](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
### 從備份初始化交易式訂閱者  
  
1.  對於現有的發行集，請確定發行集支援能夠從備份初始化執行 [sp_helppublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 記下的值 **allow_initialize_from_backup** 結果集中。  
  
    -   如果值為 **1**, ，發行集支援此功能。  
  
    -   如果值為 **0**, ，執行 [sp_changepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定的值為 **allow_initialize_from_backup** 的 **@property** 且值為 **true** 的 **@value**。  
  
2.  對於新的發行集執行 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 在發行集資料庫上的 「 發行者 」。 指定的值為 **true** 的 **allow_initialize_from_backup**。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
    > [!WARNING]  
    >  若要避免遺漏訂閱者資料時使用 **sp_addpublication** 與 `@allow_initialize_from_backup = N'true'`, ，一律使用 `@immediate_sync = N'true'`。  
  
3.  建立發行集資料庫使用的備份 [備份 & #40。TRANSACT-SQL & #41;](../../t-sql/statements/backup-transact-sql.md) 陳述式。  
  
4.  在 「 訂閱者 」 使用備份還原 [還原 & #40。TRANSACT-SQL & #41;](../Topic/RESTORE%20\(Transact-SQL\).md) 陳述式。  
  
5.  在發行集資料庫的發行者，執行預存程序 [sp_addsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定下列參數：  
  
    -   **@sync_type** -值 **的備份初始化**。  
  
    -   **@backupdevicetype** -備份裝置類型︰ **邏輯** （預設）、 **磁碟**, ，或 **磁帶**。  
  
    -   **@backupdevicename** -用於還原邏輯或實體備份裝置。  
  
         邏輯裝置中，指定當指定的備份裝置名稱 **sp_addumpdevice** 用來建立裝置。  
  
         如果是實體裝置，請指定完整路徑和檔案名稱，例如 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` 或 `TAPE = '\\.\TAPE0'`。  
  
    -   （選擇性） **@password** -建立備份組時所提供的密碼。  
  
    -   （選擇性） **@mediapassword** -當格式化媒體集時所提供的密碼。  
  
    -   （選擇性） **@fileidhint** -要還原之備份組的識別碼。 例如，指定 **1** 表示備份媒體上設定的第一個備份和 **2** 表示第二個備份組。  
  
    -   （選擇性的磁帶裝置） **@unload** -指定的值為 **1** （預設值） 應該卸載磁帶從磁碟機完成還原之後和 **0** 如果它不能卸載。  
  
6.  （選擇性）對於提取訂閱，請執行 [sp_addpullsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) 和 [sp_addpullsubscription_agent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 訂閱資料庫的訂閱者端。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
7.  (選擇性) 啟動散發代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
## 另請參閱  
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  