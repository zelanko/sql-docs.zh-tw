---
title: 設定快照集屬性 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63021331"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>設定快照集屬性 (複寫 Transact-SQL 程式設計)
  可以使用複寫預存程序來以程式設計的方式定義及修改快照集屬性，使用的預存程序將取決於發行集的類型而定。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>在建立快照式或交易式發行集時，設定快照集屬性  
  
1.  在發行者上，執行 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 針對**@publication**指定發行集名稱、針對指定**快照**集或**連續**的值**@repl_freq**，並針對下列其中一個或多個快照集相關的參數：  
  
    -   **@alt_snapshot_folder**-如果從該位置（而不是快照集預設資料夾）存取這個發行集的快照集，則指定路徑。  
  
    -   **@compress_snapshot**-如果替代快照集**** 資料夾中的快照集檔案壓縮成[!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB 檔案格式，則指定 true 的值。  
  
    -   **@pre_snapshot_script**-指定在套用初始快照集之前的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **@post_snapshot_script**-指定在套用初始快照集之後的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **@snapshot_in_defaultfolder**-如果快照集只能在非預設位置中使用，請指定**false**的值。  
  
     如需有關建立發行集的詳細資訊，請參閱＜ [Create a Publication](create-a-publication.md)＞。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>在建立合併式發行集時，設定快照集屬性  
  
1.  在發行者端，執行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 針對**@publication**指定發行集名稱、針對指定**快照**集或**連續**的值**@repl_freq**，並針對下列其中一個或多個快照集相關的參數：  
  
    -   **@alt_snapshot_folder**-如果從該位置（而不是快照集預設資料夾）存取這個發行集的快照集，則指定路徑。  
  
    -   **@compress_snapshot**-如果替代快照集資料夾中的快照集檔案壓縮成 CAB 檔案格式，則指定**true**的值。  
  
    -   **@pre_snapshot_script**-指定在套用初始快照集之前的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **@post_snapshot_script**-指定在套用初始快照集之後的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **@snapshot_in_defaultfolder**-如果快照集只能在非預設位置中使用，請指定**false**的值。  
  
2.  如需有關建立發行集的詳細資訊，請參閱＜ [Create a Publication](create-a-publication.md)＞。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>修改現有快照式或交易式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者上，執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 針對**@force_invalidate_snapshot**指定**@property** **1**的值，並針對下列其中一個值：  
  
    -   **alt_snapshot_folder** -也指定的替代快照集資料夾的新路徑**@value**。  
  
    -   **compress_snapshot** -也針對**@value**指定**true**或**false**的值，以指示替代快照集資料夾中的快照集檔案是否壓縮成 CAB 檔案格式。  
  
    -   **pre_snapshot_script** -也針對**@value**指定在套用初始快照集之前的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **post_snapshot_script** -也針對**@value**指定在套用初始快照集之後的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **snapshot_in_defaultfolder** - 也指定 **true** 或 **false** 的值，以指示快照集是否可在非預設位置中使用。  
  
2.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)。 指定**@publication**和一或多個要變更的排程或安全性認證參數。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
3.  從命令提示字元執行 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 或是啟動快照集代理程式作業來產生新的快照集。 如需詳細資訊，請參閱 [建立和套用初始快照集](../create-and-apply-the-initial-snapshot.md)。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>修改現有合併式發行集的快照集屬性  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 針對**@force_invalidate_snapshot**指定**@property** **1**的值，並針對下列其中一個值：  
  
    -   **alt_snapshot_folder** -也指定的替代快照集資料夾的新路徑**@value**。  
  
    -   **compress_snapshot** -也針對**@value**指定**true**或**false**的值，以指示替代快照集資料夾中的快照集檔案是否壓縮成 CAB 檔案格式。  
  
    -   **pre_snapshot_script** -也針對**@value**指定在套用初始快照集之前的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **post_snapshot_script** -也針對**@value**指定在套用初始快照集之後的初始化期間，將于訂閱者上執行之 **.sql**檔案的檔案名和完整路徑。  
  
    -   **snapshot_in_defaultfolder** - 也指定 **true** 或 **false** 的值，以指示快照集是否可在非預設位置中使用。  
  
2.  從命令提示字元執行 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 或是啟動快照集代理程式作業來產生新的快照集。 如需詳細資訊，請參閱 [建立和套用初始快照集](../create-and-apply-the-initial-snapshot.md)。  
  
## <a name="example"></a>範例  
 這個範例會建立使用替代快照集資料夾和壓縮快照集的發行集。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../alternate-snapshot-folder-locations.md)   
 [壓縮的快照集](../compressed-snapshots.md)   
 [在套用快照集之前及之後執行指令碼](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [透過 FTP 傳送快照集](../transfer-snapshots-through-ftp.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)  
  
  
