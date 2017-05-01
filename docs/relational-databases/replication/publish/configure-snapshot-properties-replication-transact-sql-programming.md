---
title: "設定快照集屬性 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 696e717afbf46a23987d1cd611e5b57d5c935c4e
ms.lasthandoff: 04/11/2017

---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>設定快照集屬性 (複寫 Transact-SQL 程式設計)
  可以使用複寫預存程序來以程式設計的方式定義及修改快照集屬性，使用的預存程序將取決於發行集的類型而定。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>在建立快照式或交易式發行集時，設定快照集屬性  
  
1.  在發行者上，執行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 針對 **@publication**指定發行集名稱、針對 **@repl_freq** 指定 **snapshot** 或 **@repl_freq**的值，並指定下列其中一個或多個快照集相關的參數：  
  
    -   **@alt_snapshot_folder** - 如果從該位置 (而不是從快照集預設資料夾) 存取這個發行集的快照集，則指定路徑。  
  
    -   **@compress_snapshot** - 如果替代快照集資料夾中的快照集檔案壓縮成 **CAB 檔案格式，則指定** true [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的值。  
  
    -   **@pre_snapshot_script** - 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **@post_snapshot_script** - 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **@snapshot_in_defaultfolder** - 如果替代快照集資料夾中的快照集檔案壓縮成 **false** 的值。  
  
     如需有關建立發行集的詳細資訊，請參閱＜ [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)＞。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>在建立合併式發行集時，設定快照集屬性  
  
1.  在發行者端，執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 針對 **@publication**指定發行集名稱、針對 **@repl_freq** 指定 **snapshot** 或 **@repl_freq**的值，並指定下列其中一個或多個快照集相關的參數：  
  
    -   **@alt_snapshot_folder** - 如果從該位置 (而不是從快照集預設資料夾) 存取這個發行集的快照集，則指定路徑。  
  
    -   **@compress_snapshot** - 如果替代快照集資料夾中的快照集檔案壓縮成 **CAB 檔案格式，則指定** 的值。  
  
    -   **@pre_snapshot_script** - 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **@post_snapshot_script** - 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **@snapshot_in_defaultfolder** - 如果替代快照集資料夾中的快照集檔案壓縮成 **false** 的值。  
  
2.  如需有關建立發行集的詳細資訊，請參閱＜ [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)＞。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>修改現有快照式或交易式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者上，執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 針對 **@force_invalidate_snapshot** 或 **@force_invalidate_snapshot** 的值，並針對 **@property**指定下列其中一個值：  
  
    -   **alt_snapshot_folder** - 也針對 **@value**。  
  
    -   **compress_snapshot** - 也針對 **CAB 檔案格式，則指定** 指定 **false** 或 **@value** 的值，以指示替代快照集資料夾中的快照集檔案是否壓縮成 CAB 檔案格式。  
  
    -   **pre_snapshot_script** - 也針對 **@value** 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **post_snapshot_script** - 也針對 **@value** 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **snapshot_in_defaultfolder** - 也指定 **true** 或 **false** 的值，以指示快照集是否可在非預設位置中使用。  
  
2.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)。 指定 **@publication** 及所變更之一個或多個排程或安全性認證參數。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
3.  從命令提示字元執行 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 或是啟動快照集代理程式作業來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>修改現有合併式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 針對 **@force_invalidate_snapshot** 或 **@force_invalidate_snapshot** 的值，並針對 **@property**指定下列其中一個值：  
  
    -   **alt_snapshot_folder** - 也針對 **@value**。  
  
    -   **compress_snapshot** - 也針對 **CAB 檔案格式，則指定** 指定 **false** 或 **@value** 的值，以指示替代快照集資料夾中的快照集檔案是否壓縮成 CAB 檔案格式。  
  
    -   **pre_snapshot_script** - 也針對 **@value** 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **post_snapshot_script** - 也針對 **@value** 指定在套用初始快照集之前的初始化期間，將於訂閱者上執行之 **.sql** 檔案的檔案名稱和完整路徑。  
  
    -   **snapshot_in_defaultfolder** - 也指定 **true** 或 **false** 的值，以指示快照集是否可在非預設位置中使用。  
  
2.  從命令提示字元執行 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 或是啟動快照集代理程式作業來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
## <a name="example"></a>範例  
 這個範例會建立使用替代快照集資料夾和壓縮快照集的發行集。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [壓縮的快照集](../../../relational-databases/replication/compressed-snapshots.md)   
 [在套用快照集之前及之後執行指令碼](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [透過 FTP 傳送快照集](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
