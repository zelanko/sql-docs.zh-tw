---
title: "設定快照集屬性 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
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
  - "快照集 [SQL Server 複寫], 屬性"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 設定快照集屬性 (複寫 Transact-SQL 程式設計)
  可以使用複寫預存程序來以程式設計的方式定義及修改快照集屬性，使用的預存程序將取決於發行集的類型而定。  
  
### 在建立快照式或交易式發行集時，設定快照集屬性  
  
1.  在 「 發行者 」 執行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定的發行集名稱 **@publication**, 的其中一個值 **快照** 或 **連續** 的 **@repl_freq**, ，和一或多個快照集相關的下列參數︰  
  
    -   **@alt_snapshot_folder** -如果此發行集的快照集從該位置，而不是，或除了預設快照集資料夾存取指定的路徑。  
  
    -   **@compress_snapshot** -指定的值為 **true** 如果壓縮替代快照集資料夾中的快照集檔案 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB 檔案格式。  
  
    -   **@pre_snapshot_script** -指定檔案名稱和完整路徑 **.sql** 之前會先執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **@post_snapshot_script** -指定檔案名稱和完整路徑 **.sql** 之後將執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **@snapshot_in_defaultfolder** -指定的值為 **false** 如果快照集功能只能在非預設位置中。  
  
     如需有關如何建立發行集的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 在建立合併式發行集時，設定快照集屬性  
  
1.  在 「 發行者 」 執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定的發行集名稱 **@publication**, 的其中一個值 **快照** 或 **連續** 的 **@repl_freq**, ，和一或多個快照集相關的下列參數︰  
  
    -   **@alt_snapshot_folder** -如果此發行集的快照集從該位置，而不是，或除了預設快照集資料夾存取指定的路徑。  
  
    -   **@compress_snapshot** -指定的值為 **true** 如果替代快照集資料夾中的快照集檔案壓縮成 CAB 檔案格式。  
  
    -   **@pre_snapshot_script** -指定檔案名稱和完整路徑 **.sql** 之前會先執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **@post_snapshot_script** -指定檔案名稱和完整路徑 **.sql** 之後將執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **@snapshot_in_defaultfolder** -指定的值為 **false** 如果快照集功能只能在非預設位置中。  
  
2.  如需有關如何建立發行集的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 修改現有快照式或交易式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和下列其中一個值 **@property**:  
  
    -   **alt_snapshot_folder** -也指定替代快照集資料夾的新路徑 **@value**。  
  
    -   **compress_snapshot** -也指定值的其中一個 **true** 或 **false** 的 **@value** 表示替代快照集資料夾中的快照集檔案是否壓縮 CAB 檔案格式。  
  
    -   **pre_snapshot_script** -也針對 **@value** 指定檔案名稱和完整路徑 **.sql** 之前會先執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **post_snapshot_script** -也針對 **@value** 指定檔案名稱和完整路徑 **.sql** 之後將執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **snapshot_in_defaultfolder** -也指定值的其中一個 **true** 或 **false** 表示快照集只在非預設位置是否可用。  
  
2.  （選擇性）在發行集資料庫的發行者，執行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)。 指定 **@publication** 和一或多個要變更排程或安全性認證參數。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
3.  執行 [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 從命令提示字元或開始產生新的快照集的快照集代理程式作業。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
### 修改現有合併式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和下列其中一個值 **@property**:  
  
    -   **alt_snapshot_folder** -也指定替代快照集資料夾的新路徑 **@value**。  
  
    -   **compress_snapshot** -也指定值的其中一個 **true** 或 **false** 的 **@value** 表示替代快照集資料夾中的快照集檔案是否壓縮 CAB 檔案格式。  
  
    -   **pre_snapshot_script** -也針對 **@value** 指定檔案名稱和完整路徑 **.sql** 之前會先執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **post_snapshot_script** -也針對 **@value** 指定檔案名稱和完整路徑 **.sql** 之後將執行 「 訂閱者 」 初始化期間套用初始快照集的檔案。  
  
    -   **snapshot_in_defaultfolder** -也指定值的其中一個 **true** 或 **false** 表示快照集只在非預設位置是否可用。  
  
2.  執行 [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 從命令提示字元或開始產生新的快照集的快照集代理程式作業。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
## 範例  
 這個範例會建立使用替代快照集資料夾和壓縮快照集的發行集。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## 另請參閱  
 [替代快照集資料夾位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [壓縮的快照集](../../../relational-databases/replication/compressed-snapshots.md)   
 [在套用快照集之前及之後執行指令碼](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [透過 FTP 傳送快照集](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  