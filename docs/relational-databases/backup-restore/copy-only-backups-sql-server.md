---
title: 只複製備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 03/30/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6ddbd4e3f18083290e024d1c333e51ded6e57ef1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="copy-only-backups-sql-server"></a>只複製備份 (SQL Server)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  「只複製備份」是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 通常，進行備份會變更資料庫，而且會影響往後其他備份的還原方式。 不過，偶爾為了特殊目的在不影響資料庫整體備份及還原程序的情況下進行備份，相當有用。 只複製備份即是供此目的之用。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
 只複製備份的類型如下所示：  
  
-   只複製完整備份 (所有復原模式)  
  
     只複製備份不能當做差異基底或差異備份，因此不會影響差異基底。  
  
     還原只複製完整備份與還原任何其他完整備份相同。  
  
-   只複製記錄備份 (僅完整復原模式和大量記錄復原模式)  
  
     只複製記錄備份會保留現有的記錄封存點，因此不會影響一般記錄備份的順序。 只複製記錄備份通常是沒有必要的。 您反倒可以建立新的例行記錄備份 (使用 WITH NORECOVERY)，且一併使用此備份與還原順序所需之任何先前的記錄備份。 但是，只複製記錄備份有時相當利於進行線上還原。 如需這類範例，請參閱[範例：線上還原讀寫檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)。  
  
     交易記錄永遠不會在只複製備份之後截斷。  
  
 只複製備份會記錄在 **backupset** 資料表的 [is_copy_only](../../relational-databases/system-tables/backupset-transact-sql.md) 資料行中。  
  
## <a name="to-create-a-copy-only-backup"></a>若要建立只複製備份  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 PowerShell 建立只複製備份。  

### <a name="examples"></a>範例  
###  <a name="SSMSProcedure"></a> A.  使用 SQL Server Management Studio  
在此範例中，`Sales` 資料庫的只複製備份將會備份至預設備份位置的磁碟。

1.  在物件總管中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。

2.  展開 [資料庫]，以滑鼠右鍵按一下 `Sales`，指向 [工作]，然後按一下 [備份...]。

3.  在 [一般] 頁面的 [來源] 區段中，核取 [只複製備份] 核取方塊。

4.  按一下 [確定] 。

  
###  <a name="TsqlProcedure"></a>B.  使用 Transact-SQL  
此範例使用 COPY_ONLY 參數來建立 `Sales` 資料庫的只複製備份。  此外，也會擷取交易記錄的只複製備份。

```sql
BACKUP DATABASE Sales
TO DISK = 'E:\BAK\Sales_Copy.bak'
WITH COPY_ONLY;

BACKUP LOG Sales
TO DISK = 'E:\BAK\Sales_LogCopy.trn'
WITH COPY_ONLY;
```
  
> [!NOTE]  
> 指定 DIFFERENTIAL 選項時，COPY_ONLY 沒有任何作用。  

  
###  <a name="PowerShellProcedure"></a>C.  使用 PowerShell  
此範例使用 -CopyOnly 參數來建立 `Sales` 資料庫的只複製備份。  
```powershell
Backup-SqlDatabase -ServerInstance 'SalesServer' -Database 'Sales' -BackupFile 'E:\BAK\Sales_Copy.bak' -CopyOnly
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要建立完整備份或記錄備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **檢視只複製備份**  
  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[Backup-SqlDatabase](https://technet.microsoft.com/library/mt683378.aspx)

  
