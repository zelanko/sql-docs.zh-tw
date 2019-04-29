---
title: 只複製備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cba784ed6e81152e91b8320ac5e441187c07df9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922129"
---
# <a name="copy-only-backups-sql-server"></a>只複製備份 (SQL Server)
  「只複製備份」是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 通常，進行備份會變更資料庫，而且會影響往後其他備份的還原方式。 不過，偶爾為了特殊目的在不影響資料庫整體備份及還原程序的情況下進行備份，相當有用。 只複製備份即是供此目的之用。  
  
 只複製備份的類型如下所示：  
  
-   只複製完整備份 (所有復原模式)  
  
     只複製備份不能當做差異基底或差異備份，因此不會影響差異基底。  
  
     還原只複製完整備份與還原任何其他完整備份相同。  
  
-   只複製記錄備份 (僅完整復原模式和大量記錄復原模式)  
  
     只複製記錄備份會保留現有的記錄封存點，因此不會影響一般記錄備份的順序。 只複製記錄備份通常是沒有必要的。 您反倒可以建立新的例行記錄備份 (使用 WITH NORECOVERY)，且一併使用此備份與還原順序所需之任何先前的記錄備份。 但是，只複製記錄備份有時相當利於進行線上還原。 如需這類範例，請參閱[範例：線上還原讀取/寫入檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)。  
  
     交易記錄永遠不會在只複製備份之後截斷。  
  
 只複製備份會記錄在 **backupset** 資料表的 [is_copy_only](/sql/relational-databases/system-tables/backupset-transact-sql) 資料行中。  
  
## <a name="to-create-a-copy-only-backup"></a>若要建立只複製備份  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]或 PowerShell 建立只複製備份。  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
1.  在 [備份資料庫] 對話方塊的 [一般] 頁面上，選取 [只複製備份] 選項。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 基本的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語法如下：  
  
-   用於只複製完整備份：  
  
     BACKUP DATABASE *database_name* TO \<backup_device>*>* ...WITH COPY_ONLY...  
  
    > [!NOTE]  
    >  指定 DIFFERENTIAL 選項時，COPY_ONLY 沒有任何作用。  
  
-   用於只複製記錄備份：  
  
     BACKUP LOG *database_name* TO *\<* backup_device>*>* ...WITH COPY_ONLY...  
  
###  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
1.  使用 `Backup-SqlDatabase` 指令程式搭配 `-CopyOnly` 參數。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要建立完整備份或記錄備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
 **檢視只複製備份**  
  
-   [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../powershell/sql-server-powershell-provider.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復原模式 &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [使用備份與還原複製資料庫](../databases/copy-databases-with-backup-and-restore.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
