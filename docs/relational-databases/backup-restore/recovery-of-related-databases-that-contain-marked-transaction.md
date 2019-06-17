---
title: 復原包含標記之異動的相關資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a548fe7327c6e3c8ac4febca3db442490c983058
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025432"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>復原包含標記之異動的相關資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  這個主題僅與包含標示的交易，且使用完整模式或大量記錄復原模式的資料庫有關。  
  
 如需還原至特定復原點之需求的相關資訊，請參閱 [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援將具名標示插入交易記錄，以允許復原至特定的標示。 記錄標示是針對交易而設，並且只有在其相關的交易認可時才會插入。 如此一來，標示可以結合特定工作，您也就可以復原至包含或排除此工作的某一點。  
  
 將具名標示插入交易記錄之前，請考慮以下幾點：  
  
-   因為交易標示須耗用記錄空間，所以除非它們在資料庫復原策略中扮演重要的角色，否則不應使用交易標示。  
  
-   標示的交易認可之後，會在 [msdb](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) 的 **logmarkhistory**資料表中插入一個資料列。  
  
-   如果標示交易跨越同一資料庫伺服器或不同伺服器上的多個資料庫，則標示會記錄在所有受影響的資料庫之記錄中。 如需詳細資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>將具名標示插入交易記錄檔中的 Transact-SQL 語法  
 若要將標示插入交易記錄，請使用 [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) 陳述式和 WITH MARK [*description*] 子句。 標示和交易的名稱相同。 選擇性的 *description* 是標示的文字描述，而不是標示名稱。 例如，在下列 `BEGIN TRANSACTION` 陳述式中建立的交易及標示名稱為 `Tx1`：  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 交易記錄檔中會記錄標示名稱 (交易名稱)、描述、資料庫、使用者、 **datetime** 資訊與記錄序號 (LSN)。 **datetime** 資訊是與標示名稱一起使用，才能唯一識別標示。  
  
 如需如何將標示插入跨越多個資料庫之交易的相關資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>復原標示的 Transact-SQL 語法  
 針對標示的交易使用 [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式時，您可以使用下列其中一個子句，以在標示上或標示當前停止：  
  
-   使用 WITH STOPATMARK = **'** _<mark_name>_ **'** 子句，以指定標示的交易為復原點。  
  
     STOPATMARK 可向前復原標示，並將已標示的交易納入向前復原。  
  
-   使用 WITH STOPBEFOREMARK = **'** _<mark_name>_ **'** 子句，以指定標示之前的記錄為復原點。  
  
     STOPBEFOREMARK 可向前復原標示，並從向前復原中排除已標示的交易。  
  
 STOPATMARK 與 STOPBEFOREMARK 選項都支援選擇性的 AFTER *datetime* 子句。 使用 *datetime* 時，標示名稱不必是唯一的。  
  
 如果省略 AFTER *datetime* ，向前復原會停在具有指定名稱的第一個標示。 如果指定 AFTER *datetime* ，向前復原會在 *datetime*時或之後，停止於具有指定名稱的第一個標示。  
  
> [!NOTE]  
>  如同所有的時間點還原作業，當資料庫進行大量記錄的作業時，不允許其復原至標示。  
  
 **若要還原標示的交易**  
  
 [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
### <a name="preparing-the-log-backups"></a>準備記錄備份  
 就此範例而言，這些相關資料庫的適當備份策略如下：  
  
1.  兩個資料庫均使用完整復原模式。  
  
2.  建立每一個資料庫的完整備份。  
  
     可循序或同時備份這些資料庫。  
  
3.  在備份交易記錄之前，先標示要在所有資料庫中執行的交易。 如需如何建立標示的異動的相關資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
4.  備份每個資料庫的交易記錄。  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>將資料庫復原至標示的交易  
 **若要還原備份**  
  
1.  盡可能建立未受損資料庫的 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 。  
  
2.  還原每個資料庫的最新完整資料庫備份。  
  
3.  識別所有交易記錄備份中可用的最新標示交易。 此資訊是儲存在每一個伺服器上 **msdb** 資料庫的 **logmarkhistory** 資料表中。  
  
4.  識別所有包含此標示之相關資料庫的記錄備份。  
  
5.  還原每個記錄檔備份，停在標示的交易。  
  
6.  復原每個資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [規劃和執行還原順序 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
