---
title: 從備份初始化交易式訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f3d81664c8b48d3ae03c9d80ade394fa657de87
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="initialize-a-transactional-subscription-from-a-backup"></a>從備份初始化交易式訂閱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  雖然通常會使用快照集初始化交易式發行集的訂閱，但是可以使用複寫預存程序從備份初始化訂閱。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>從備份初始化交易式訂閱者  
  
1.  如果是現有的發行集，請在發行集資料庫的發行者端執行 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)，以確定此發行集可支援從備份初始化的功能。 請記下結果集中 **allow_initialize_from_backup** 的值。  
  
    -   如果此值是 **1**，表示發行集支援此功能。  
  
    -   如果這個值是 **0**，請在發行集資料庫的發行者端執行 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 針對 **allow_initialize_from_backup** 指定 **@property** 的值，並針對 **@value** 指定 **@value**。  
  
2.  如果是新的發行集，請在發行集資料庫的發行者端執行 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 針對 **allow_initialize_from_backup** 指定 **true**的值。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
    > [!WARNING]  
    >  為了避免遺漏訂閱者資料，當您使用 **sp_addpublication** 搭配 `@allow_initialize_from_backup = N'true'`時，請一律使用 `@immediate_sync = N'true'`。  
  
3.  使用 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) 陳述式建立發行集資料庫的備份。  
  
4.  使用 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式還原訂閱者上的備份。  
  
5.  在發行集資料庫的發行者端，執行預存程序 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定下列參數：  
  
    -   **@sync_type** - **initialize with backup**。  
  
    -   **@backupdevicetype** - 備份裝置的類型： **logical** (預設值)、 **disk**或 **tape**。  
  
    -   **@backupdevicename** - 要用於還原的邏輯或實體備份裝置。  
  
         如果是邏輯裝置，請指定使用 **sp_addumpdevice** 來建立裝置時所指定的備份裝置名稱。  
  
         如果是實體裝置，請指定完整路徑和檔案名稱，例如 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` 或 `TAPE = '\\.\TAPE0'`。  
  
    -   (選擇性) **@password** - 當建立備份組時所提供的密碼。  
  
    -   (選擇性) **@mediapassword** - 當格式化媒體集時所提供的密碼。  
  
    -   (選擇性) **@fileidhint** - 要還原之備份組的識別碼。 例如，指定 **1** 表示備份媒體上的第一個備份組，指定 **2** 則表示第二個備份組。  
  
    -   (適用於磁帶裝置的選擇項) **@unload** - 如果在完成還原之後應該從磁碟機卸載磁帶，請指定 **1** (預設值) 的值；如果不應該將它卸載，請指定 **0** 的值。  
  
6.  (選擇性) 針對提取訂閱，在訂閱資料庫的訂閱者端執行 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) 和 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
7.  (選擇性) 啟動散發代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
