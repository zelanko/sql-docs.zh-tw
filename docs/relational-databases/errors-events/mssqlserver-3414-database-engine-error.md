---
description: MSSQLSERVER_3414
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a7a7d69c27ed422763c5c697f003ba9fb4c82286
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618094"
---
# <a name="mssqlserver_3414"></a>MSSQLSERVER_3414
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3414|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REC_GIVEUP|  
|訊息文字|復原時發生錯誤，導致資料庫 '%.*ls' (資料庫識別碼 %d) 無法重新啟動。 請診斷並修正復原錯誤，或者從已知完好的備份還原。 如果不能更正或預期錯誤，請連絡技術支援部門。|  
  
## <a name="explanation"></a>說明  
已復原指定的資料庫，但是因為復原期間發生錯誤而無法啟動。 這個錯誤已經將資料庫置於 SUSPECT 狀態。 主要檔案群組以及可能還有其他檔案群組都有疑問，而且可能已損毀。 資料庫在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間無法復原，因此無法使用。 需要使用者動作來解決問題。 當在 SQL Server Management Studio (資料庫標旁的圖示) 中，以及查看 sys.databases.state_desc 資料行時，都會看到 SUSPECT 狀態。 如果嘗試在此狀態下使用資料庫，則會發生下列錯誤：

```
Msg 926, Level 14, State 1, Line 1 
Database 'mydb' cannot be opened. It has been marked SUSPECT by recovery. See the SQL Server errorlog for more information
```
  
請注意，當這個錯誤發生於 **tempdb** 時，將會關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  

## <a name="cause"></a>原因
當嘗試啟動伺服器執行個體或復原資料庫時，存在於系統上的暫時性狀況會引發這個錯誤。 每當您嘗試啟動資料庫時所發生的永久性失敗也會造成這個錯誤。 復原失敗原因通常會在錯誤記錄檔或事件記錄檔內錯誤 3414 之前的錯誤中找到。 記錄檔中的先前錯誤會包含相同 spid<n> 值。 例如，下列復原失敗是因為嘗試讀取記錄區塊時，發生總和檢查碼錯誤。 請注意，*spid15s* 出現在每一行中：

```
2020-03-31 17:33:13.00 spid15s     Error: 824, Severity: 24, State: 4.  
2020-03-31 17:33:13.00 spid15s     SQL Server detected a logical consistency-based I/O error: (bad checksum). It occurred during a read of page (0:-1) in database ID 13 at offset 0x0000000000b800 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb_log.LDF'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2020-03-31 17:33:13.16 spid15s     Error: 3414, Severity: 21, State: 1.  
2020-03-31 17:33:13.16 spid15s     An error occurred during recovery, preventing the database 'mydb' (database ID 13) from restarting. Diagnose the recovery errors and fix them, or restore from a known good backup. If errors are not corrected or expected, contact Technical Support
```


導致資料庫復原失敗的錯誤有很多種。 雖然您必須根據個別案例來評估每個錯誤，但資料庫復原失敗其解決方式通常與下方使用者動作區段中所描述的相同。

## <a name="user-action"></a>使用者動作  
 
如需此 3414 錯誤發生原因的詳細資訊，請檢查 Windows 事件記錄檔或錯誤記錄檔，以尋找指出特定失敗的先前錯誤。 適當的使用者動作取決於 Windows 事件記錄檔中的資訊指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤是由暫時性狀況或永久性失敗所造成。 錯誤訊息的描述為「請診斷並修正復原錯誤，或從已知完好的備份進行還原」。 因此，您可嘗試修正所遇到的錯誤，讓復原得以完成 (請參閱[可修正錯誤與延遲交易](#correctable-errors-and-deferred-transactions))。

如果無法修正錯誤，則解決此問題的最佳優先選項，就是從完好的備份進行還原。 不過，如果無法從備份復原，仍有另外兩個選項，但不保證能夠完整復原資料，其為搭配 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 使用緊急修復，或嘗試盡可能地將資料複製到另一個資料庫。 

 1. 從上次已知完好的資料庫備份進行還原
 1. 使用 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 所提供的緊急修復方法
 1. 嘗試盡可能地將資料複製到另一個資料庫。

第一種方法是從良好資料庫備份進行還原，這是讓資料庫進入已知一致狀態的最佳選擇。  

第二優先的選擇 (如果沒有可用的備份)，是將資料庫與網路連線並讓其可供存取。 不過，您必須了解，因為復原失敗，所以無法保證交易一致性。 沒有任何方法可知道哪些交易應該向後復原或向前復原，但由於復原失敗而不允許動作。 若要繼續進行緊急修復步驟，請參閱 DBCC CHECKDB 文件的[解決緊急模式中的資料庫錯誤](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode)一節中所述。 

如果緊急修復無法提供幫助，而您想要嘗試將某些資料搶救至另一個資料庫，則可透過 ALTER DATABASE <dbname> SET EMERGENCY 命令，將資料庫設定為緊急模式，藉此取得資料庫存取權。 然後，您即可嘗試從資料表複製資料。

### <a name="correctable-errors-and-deferred-transactions"></a>可修正錯誤與延遲交易
並非在資料庫復原期間遇到的所有錯誤都會導致復原失敗與 SUSPECT 資料庫：

第一次開啟資料庫和/或交易記錄檔時所發生的錯誤，就會在復原之前發生。 這類錯誤的範例包括 [17204](mssqlserver-17204-database-engine-error.md) 和 [17207](mssqlserver-17207-database-engine-error.md)。 在修正這些錯誤之後，就能允許進行復原 (但若發生其他復原錯誤，則不保證可完成)。 類似於 17204 和 17207 的錯誤不會導致 SUSPECT 資料庫。 事實上，當這些問題發生時，資料庫的狀態會呈現 RECOVERY_PENDING。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使發生頁面層級錯誤，也可讓復原完成，且仍會維持交易一致性。 這個流程減少了會導致 SUSPECT 資料庫的案例數量。 這個概念稱為[延遲交易](../backup-restore/deferred-transactions-sql-server.md)。

如果復原期間發生的錯誤表示資料庫頁面發生問題 (例如，總和檢查碼錯誤或訊息 824)，則可能會在存在待決錯誤的情況下允許復原完成。 在未認可交易的情況下，頁面上的錯誤可能會導致[延遲交易](../backup-restore/deferred-transactions-sql-server.md)，讓復原得以完成。  

下列錯誤記錄檔項目顯示在復原期間發生的訊息 [824](mssqlserver-824-database-engine-error.md) 錯誤範例，其中已允許使用延遲交易來完成復原。 請注意，此案例中並未發生錯誤 3414，而已完成資料庫復原的訊息如下：

```2010-03-31 19:17:18.45 spid7s      Error: 824, Severity: 24, State: 2.   
2010-03-31 19:17:18.45 spid7s      SQL Server detected a logical consistency-based I/O error: incorrect checksum (expected: 0xb2c87a0a; actual: 0xb6c0a5e2). It occurred during a read of page (1:153) in database ID 13 at offset 0x00000000132000 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2010-03-31 19:17:18.45 spid7s      Error: 3314, Severity: 21, State: 1.   
2010-03-31 19:17:18.45 spid7s      During undoing of a logged operation in database 'mydb', an error occurred at log record ID (25:100:19). Typically, the specific failure is logged previously as an error in the Windows Event Log service. Restore the database or file from a backup, or repair the database.
2010-03-31 19:17:18.45 spid7s      Errors occurred during recovery while rolling back a transaction. The transaction was deferred. Restore the bad page or file, and re-run recovery.   
2010-03-31 19:17:18.45 spid7s      Recovery completed for database mydb (database ID 13) in 2 second(s) (analysis 204 ms, redo 25 ms, undo 1832 ms.) This is an informational message only. No user action is required.   
```

如果要向前復原已認可的交易，可將頁面標示為無法存取 (未來針對該頁面的任何存取嘗試都會導致訊息 829)，且復原得以完成。 在此情況下，必須藉由從備份還原頁面，或使用具有修復功能的 DBCC CHECKDB 將頁面解除配置，以修正錯誤。


  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[完整資料庫還原 &#40;簡單復原模式&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[延遲交易](../backup-restore/deferred-transactions-sql-server.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)

  
