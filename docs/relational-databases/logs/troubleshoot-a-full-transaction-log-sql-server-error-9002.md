---
title: "寫滿交易記錄疑難排解 (SQL Server 錯誤 9002) | Microsoft 文件"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5f0ea9dba2803d981b5e259105d1e699e08611f1
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2018
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>寫滿交易記錄疑難排解 (SQL Server 錯誤 9002)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題將討論對於寫滿交易記錄的可能回應，並建議將來可採用的避免方法。 
  
  當交易記錄寫滿時， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 就會發出 **9002 錯誤**。 此記錄可能會在資料庫處於線上或復原狀態時填滿。 如果此記錄是在資料庫處於線上狀態時填滿，資料庫會保持線上狀態，不過只能讀取而無法更新資料庫。 如果此記錄是在復原期間填滿，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將資料庫標示為 RESOURCE PENDING。 不論是哪一種情況，使用者都必須採取動作，以便提供足夠的記錄空間。  
  
## <a name="responding-to-a-full-transaction-log"></a>寫滿交易記錄的回應  
 寫滿交易記錄的適當回應會部分根據導致記錄填滿的條件而定。 
 
 若要探索指定情況下無法進行記錄截斷的原因，請使用 **sys.database** 目錄檢視的 **log_reuse_wait** 和 **log_reuse_wait_desc** 資料行。 如需詳細資訊，請參閱 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。 如需可能延遲記錄截斷之其他因素的描述，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
> **重要！！**  
>  如果發生 9002 錯誤時資料庫處於復原狀態，請在解決問題後，使用 [ALTER DATABASE *資料庫名稱* SET ONLINE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 來復原資料庫。  
  
 寫滿交易記錄的替代回應方式包括：  
  
-   備份記錄。  
  
-   釋出磁碟空間，使記錄可以自動成長。  
  
-   將記錄檔移動到空間足夠的磁碟機。  
  
-   增加記錄檔的大小。  
  
-   在不同的磁碟上加入記錄檔。  
  
-   完成或刪除長時間執行的交易。  
  
 這些替代方式將於下列各節中討論。 請選擇最適合您情況的回應。  
  
## <a name="back-up-the-log"></a>備份記錄  
 在完整復原模式或大量記錄復原模式下，如果最近尚未備份交易記錄，備份可能就是阻止記錄截斷的主因。 如果記錄從未備份過，您就 **必須建立兩個記錄備份** ，以便讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將記錄截斷至上次備份的時間點。 截斷記錄可針對新記錄檔的記錄釋出空間。 若要防止記錄檔再度被填滿，請經常備份記錄檔。  
  
 **若要建立交易記錄備份**  
  
> **重要**  
>  如果資料庫已損毀，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>釋出磁碟空間  
 您可以透過刪除或移動其他檔案，在包含資料庫交易記錄檔的磁碟機上釋出磁碟空間。 釋出的磁碟空間會讓復原系統自動加大記錄檔。  
  
### <a name="move-the-log-file-to-a-different-disk"></a>將記錄檔移至不同的磁碟  
 如果無法在目前包含記錄檔的磁碟機上，釋出足夠的磁碟空間，請考慮將檔案移動到有足夠空間的其他磁碟機。  
  
> **重要！！** 記錄檔絕不可放在壓縮檔案系統上。  
  
 **移動記錄檔**  
  
-   [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>增加記錄檔大小  
 如果記錄磁碟上還有可用空間，您就可以增加記錄檔的大小。 記錄檔大小的最大值是每個記錄檔 2 TB。  
  
 **增加檔案大小**  
  
 如果已停用自動成長、資料庫在線上，而且磁碟上有足夠的可用空間，請執行下列其中一項動作：  
  
-   手動增加檔案大小以產生單一成長遞增。  
  
-   使用 ALTER DATABASE 陳述式，設定 FILEGROWTH 選項的非零成長遞增，藉以開啟自動成長。  
  
> **注意** ：無論是哪一種情況，如果已達到目前的大小限制，都需增加 MAXSIZE 值。  
  
### <a name="add-a-log-file-on-a-different-disk"></a>在不同的磁碟上加入記錄檔  
 使用 ALTER DATABASE <database_name> ADD LOG FILE，在含有足夠空間的不同磁碟上加入資料庫的新記錄檔。  
  
 **加入記錄檔**  
  
-   [將資料或記錄檔加入資料庫](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>完成或刪除長時間執行的交易
### <a name="discovering-long-running-transactions"></a>探索長時間執行的交易
非常長時間執行的交易可能會造成交易記錄被填滿。 若要尋找長時間執行的交易，請使用下列其中一種方式：
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。**
這個動態管理檢視傳回有關資料庫層級之交易的資訊。 對於長時間執行的交易，較重要的資料行包括第一筆記錄檔記錄的時間 [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)、交易的目前狀態 [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)和交易記錄之開始記錄的 [記錄序號 (LSN)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)。**
此陳述式可讓您識別交易擁有者的使用者識別碼，如此就可以追蹤交易來源，以便更有條理地終止交易 (進行認可而非回復)。

### <a name="kill-a-transaction"></a>刪除交易
有時您必須結束處理序；您可能必須使用 [KILL](../../t-sql/language-elements/kill-transact-sql.md) 陳述式。 請小心使用此陳述式，尤其是執行您不想刪除的重要處理序時。 如需詳細資訊，請參閱 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)

## <a name="see-also"></a>另請參閱  
[知識庫支援文章 - SQL Server 中的交易記錄意外地擴充或滿溢](https://support.microsoft.com/en-us/kb/317375) [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [管理交易記錄檔的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
