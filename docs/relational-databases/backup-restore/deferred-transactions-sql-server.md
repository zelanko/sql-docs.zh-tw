---
title: 延遲交易 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- I/O [SQL Server], database recovery
- restoring pages [SQL Server]
- deferred transactions
- modifying transaction deferred state
ms.assetid: 6fc0f9b6-d3ea-4971-9f27-d0195d1ff718
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5db753c673c38a0f14340d06b21abebd59887c93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666126"
---
# <a name="deferred-transactions-sql-server"></a>延遲交易 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 中，如果在資料庫啟動期間，回復 (復原) 所需的資料已離線，就會延期損毀的交易。 「延遲交易」是在向前復原階段完成時尚未認可，而發生無法回復之錯誤的交易。 因為交易無法回復，所以會延期。  
  
> [!NOTE]  
>  只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 才會延期損毀的交易。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他版本中，損毀的交易會造成啟動失敗。  
  
 發生延遲交易通常是因為，在向前復原資料庫時發生 I/O 錯誤，使得系統無法讀取交易所需的頁面。 不過，檔案層級的錯誤也可能導致交易延遲。 當部分還原順序在需要進行交易回復時停止，且交易所需的資料已離線，就有可能發生交易延遲。  
  
 正在回復中且發生 I/O 錯誤的使用者交易，會導致整個資料庫離線。 當資料庫回到線上時，重做便會重新取得原先擁有的所有鎖定，並嘗試回復所有未認可的交易。 交易修改的所有資料仍會適當地鎖定，直到可以回復該交易為止。 當修復損毀且重新啟動資料庫時，或者在線上還原之後，當資料庫仍在線上並解決了延遲交易的問題時，無法回復的交易將會放棄鎖定。 在此之前，延遲交易可以保留鎖定，以防止整個資料庫上的特定作業。 例如，如果延遲交易包含 CREATE TABLE 指示，則在解決延遲交易的問題之前，沒有任何使用者可以建立資料表。  
  
 發生延遲交易的原因也可能是，分次還原將資料庫復原到了某個時間點，而資料庫就在此時尚有未還原且離線的檔案群組受到一或多個使用中交易影響。 因為無法回復交易，所以就將它延遲。  
  
 下表列出會導致資料庫執行復原的動作，以及如果發生 I/O 問題時的結果。  
  
|動作|解決方法 (如果發生 I/O 問題，或所需的資料離線)|  
|------------|-----------------------------------------------------------------------|  
|伺服器啟動|延遲交易|  
|Restore|延遲交易|  
|附加|附加動作失敗|  
|自動重新啟動|延遲交易|  
|建立資料庫或資料庫快照集|建立動作失敗|  
|重做資料庫鏡像|延遲交易|  
|檔案群組離線|延遲交易|  
  
## <a name="moving-a-transaction-out-of-the-deferred-state"></a>將交易移出 DEFERRED 狀態  
  
> [!IMPORTANT]  
>  延遲交易會讓交易記錄保持在使用中狀態。 在這些交易移出延遲狀態之前，將無法截斷含有任何延遲交易的虛擬記錄檔。 如需記錄截斷的詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
 若要將交易移出延遲狀態，資料庫必須正確地啟動，沒有任何 I/O 錯誤。 如果有延遲交易存在，您必須修正 I/O 錯誤的來源。 以下依一般嘗試的順序，列出可用的解決方法：  
  
-   重新啟動資料庫。 如果問題是暫時性的，資料庫啟動時應該就不再有延遲交易。  
  
-   如果是因為檔案群組離線而導致交易延遲，請將檔案群組連回線上。  
  
     若要讓離線的檔案群組恢復上線，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    RESTORE DATABASE database_name FILEGROUP=<filegroup_name>  
    ```  
  
-   還原資料庫。 進行線上還原後，任何延遲的交易都會解決。  
  
     在完整或大量記錄復原模式下，如果延遲交易只是由少數的損毀頁面所造成，線上分頁還原可能就可以解決錯誤 (在支援的情況下)。  
  
-   如果您不再需要用到某個因離線狀態引起延遲交易的檔案群組，請將離線檔案群組設定為無用 (不再使用)。 因檔案群組離線而延遲的交易會在檔案群組變成無用之後移出延遲狀態。  
  
    > [!IMPORTANT]  
    >  無用的檔案群組永遠都不能復原。  
  
     如需詳細資訊，請參閱 [移除無用的檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)。  
  
-   如果交易因錯誤的頁面而延遲，而且資料庫的完好備份不存在，請使用下列程序來修復資料庫：  
  
    -   首先執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，將資料庫置於緊急模式中：  
  
        ```  
        ALTER DATABASE <database_name> SET EMERGENCY  
        ```  
  
         如需緊急模式的詳細資訊，請參閱 [資料庫狀態](../../relational-databases/databases/database-states.md)。  
  
    -   接著，在下列其中一個 DBCC 陳述式內使用 DBCC REPAIR_ALLOW_DATA_LOSS 選項以修復資料庫： [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)、 [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)或 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。  
  
         當 DBCC 發現錯誤的頁面時，它會取消配置該頁面，並修復任何相關的錯誤。 此方式可以讓資料庫以實體上一致的狀態回到線上。 不過，很可能遺失其他資料，因此除非不得已，盡量不要使用這個方式。  
  
## <a name="see-also"></a>另請參閱  
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [移除無用的檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)   
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
