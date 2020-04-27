---
title: 從備份初始化交易式訂閱（複寫 Transact-sql 程式設計） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e7fb32de254729c4173fab260e5797db5f2cc2f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67793298"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>從備份初始化交易式訂閱 (複寫 Transact-SQL 程式設計)
  雖然通常會使用快照集初始化交易式發行集的訂閱，但是可以使用複寫預存程序從備份初始化訂閱。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>從備份初始化交易式訂閱者  
  
1.  如果是現有的發行集，請在發行集資料庫的發行者端執行 [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)，以確定此發行集可支援從備份初始化的功能。 請記下結果集中 **allow_initialize_from_backup** 的值。  
  
    -   如果此值是 **1**，表示發行集支援此功能。  
  
    -   如果這個值是 **0**，請在發行集資料庫的發行者端執行 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 針對 [ ** \@屬性**] 指定 [ **allow_initialize_from_backup** ] 的值， `true`並** \@** 針對 [值] 指定值。  
  
2.  如果是新的發行集，請在發行集資料庫的發行者端執行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 `true`針對 [ **allow_initialize_from_backup**] 指定的值。 如需詳細資訊，請參閱[建立發行集](publish/create-a-publication.md)。  
  
    > [!WARNING]  
    >  為了避免遺漏訂閱者資料，當您使用 **sp_addpublication** 搭配 `@allow_initialize_from_backup = N'true'`時，請一律使用 `@immediate_sync = N'true'`。  
  
3.  使用 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) 陳述式建立發行集資料庫的備份。  
  
4.  使用 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式還原訂閱者上的備份。  
  
5.  在發行集資料庫的發行者端，執行預存程序 [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定下列參數：  
  
    -   sync_type- **initialize with backup**的值。 ** \@ **  
  
    -   backupdevicetype-備份裝置的類型： [**邏輯**（預設）]、[**磁片**] 或 [**磁帶**]。 ** \@ **  
  
    -   backupdevicename-要用於還原的邏輯或實體備份裝置。 ** \@ **  
  
         如果是邏輯裝置，請指定使用 **sp_addumpdevice** 來建立裝置時所指定的備份裝置名稱。  
  
         如果是實體裝置，請指定完整路徑和檔案名稱，例如 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` 或 `TAPE = '\\.\TAPE0'`。  
  
    -   選擇性密碼-建立備份組時所提供的密碼。 ** \@ **  
  
    -   選擇性mediapassword-格式化媒體集時所提供的密碼。 ** \@ **  
  
    -   選擇性fileidhint-要還原之備份組的識別碼。 ** \@ ** 例如，指定 **1** 表示備份媒體上的第一個備份組，指定 **2** 則表示第二個備份組。  
  
    -   （適用于磁帶裝置的選用）unload-如果在還原完成後應該從磁片磁碟機卸載磁帶，請指定**1** （預設值）的值; 如果不應該卸載，請指定**0** 。 ** \@ **  
  
6.  (選擇性) 針對提取訂閱，在訂閱資料庫的訂閱者端執行 [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) 和 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 如需詳細資訊，請參閱 [建立提取訂閱](create-a-pull-subscription.md)。  
  
7.  (選擇性) 啟動散發代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用備份與還原複製資料庫](../databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 資料庫的備份與還原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
