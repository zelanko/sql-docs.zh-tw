---
title: "使用標示的交易以一致的方式復原相關資料庫 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 937eb729c5252b09a82576805102d3cdcbceeb21
ms.lasthandoff: 04/11/2017

---
# <a name="use-marked-transactions-to-recover-related-databases-consistently"></a>使用標示的交易以一致的方式復原相關資料庫
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題只與使用完整或大量記錄復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。  
  
 當您對兩個以上的資料庫 (「相關資料庫」**) 進行相關的更新時，您可以使用交易標示將它們復原到邏輯上一致的時間點。 不過，這種復原會遺失任何在復原點標示之後所認可的交易。 只有當您要測試相關資料庫，或是願意遺失最近認可的交易時，才適合標示交易。  
  
 例行性標示每個相關資料庫中的相關交易會在資料庫中建立一系列通用的復原點。 交易標示將記錄於交易記錄，並且包含在記錄備份中。 如果發生損毀，即可將每個資料庫還原到相同的交易標示，進而復原至一致的時間點。  
  
> [!NOTE]  
>  不同的資料庫上的記錄備份可以各自建立，互不影響，而且也不必同時進行。  
  
 在下列狀況中復原相關資料庫時，您必須先在每個相關資料庫中標示過交易：  
  
-   一或多個交易記錄檔被毀。 您必須將一組資料庫還原到最後一次記錄備份時的一致狀態。  
  
-   您必須將整個資料庫集合還原到某個較早時間點的共同一致狀態。  
  
> [!IMPORTANT]  
>  您只能將相關資料庫復原到已標示的交易，而不能復原到特定的時間點。  
  
 如需有關如何建立標示交易的詳細資訊，請參閱本主題稍後的「建立標示的交易」。  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>使用標示的交易的一般狀況  
 使用標示的交易的一般狀況包括下列步驟：  
  
1.  建立每個相關資料庫的完整或差異資料庫備份。  
  
2.  在所有資料庫中標示交易區塊。  
  
3.  備份所有資料庫的交易記錄。  
  
4.  使用 WITH NORECOVERY 還原資料庫備份。  
  
5.  使用 WITH STOPATMARK 還原記錄。  
  
## <a name="considerations-for-using-marked-transactions"></a>使用標示的交易的考量  
 將具名標示插入交易記錄之前，請考慮以下幾點：  
  
-   因為交易標示須耗用記錄空間，所以除非它們在資料庫復原策略中扮演重要的角色，否則不應使用交易標示。  
  
-   標示的交易認可之後，會在 [msdb](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) 的 **logmarkhistory**資料表中插入一個資料列。  
  
-   如果標示交易跨越同一資料庫伺服器或不同伺服器上的多個資料庫，則標示會記錄在所有受影響的資料庫之記錄中。  
  
## <a name="creating-the-marked-transactions"></a>建立標示的交易  
 若要建立標示的交易，請使用 [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) 陳述式和 WITH MARK [描述**] 子句。 選擇性的「描述」**是標示的文字說明。 標示名稱對於交易而言是必要的。 標示名稱可以重複使用。 交易記錄中會記錄標示名稱、描述、資料庫、使用者、日期時間資訊與記錄序號 (LSN)。 日期時間資訊要連同標示名稱一起使用，才能唯一識別標示。  
  
 **若要在一組資料庫中建立標示的交易：**  
  
1.  在 BEGIN TRAN 陳述式中指定交易名稱，並使用 WITH MARK 子句  
  
     您可以在現有的交易中使用巢狀陳述式 BEGIN TRAN *new_mark_name* WITH MARK。 即使交易已經有交易名稱， *new_mark_name* 的值仍是交易的標示名稱。  
  
    > [!NOTE]  
    >  如果您發出第二個巢狀的 BEGIN TRAN...WITH MARK，則會略過該陳述式，但會出現警告訊息。  
  
2.  針對集合中的所有資料庫執行更新。  
  
     只有在執行 BEGIN TRAN...WITH MARK 陳述式的伺服器執行個體上，特定交易的標示才會插入交易記錄中。 交易標示會置於該伺服器執行個體上每個由標示的交易所更新之資料庫的交易記錄中。 如果資料庫位於不同的伺服器執行個體，則必須在每個伺服器執行個體上建立完全相同的標示。  
  
### <a name="examples"></a>範例  
 下列範例會將交易記錄還原到名為 `ListPriceUpdate`的標示交易中之標示。  
  
```tsql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>強制將標示散佈到其他伺服器  
 散佈交易時，交易標示名稱並不會自動散發到另一個伺服器。 若要強制將標示散佈到其他伺服器，必須撰寫一個包含 BEGIN TRAN *name* WITH MARK 陳述式的預存程序。 然後必須在遠端伺服器上原始伺服器的交易範圍內執行這個預存程序。  
  
 例如，假設有一個資料分割資料庫存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的多個執行個體上。 每一個執行個體上都有一個名為 `coyote`的資料庫。 首先，在每個資料庫中建立預存程序，例如 `sp_SetMark`。  
  
```tsql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 接下來，建立包含交易的預存程序 `sp_MarkAll` ，它會在每一個資料庫中放入標示。 `sp_MarkAll` 可以從任何執行個體來執行。  
  
```tsql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>兩階段認可  
 認可分散式交易分為兩階段進行：準備和認可。 認可標示的交易時，若任何記錄檔中都沒有值得懷疑的交易，就會將標示交易中每個資料庫的認可記錄放在記錄中。 這時候，可以保證不會有任何交易會在一個記錄中出現為已認可，而在另一個記錄中是未認可。  
  
 以下步驟會在認可標示的交易過程中完成這一點：  
  
1.  標示交易的準備階段會拖延所有新的準備和認可。  
  
2.  只有已完成準備的交易認可才能繼續。  
  
3.  接著標示交易等候所有完成準備的交易逐步完成 (有逾時限制)。  
  
4.  標示的交易完成準備並已認可。  
  
5.  移除新準備與認可的拖延。  
  
 跨越多個資料庫的標示交易所產生的拖延可能降低伺服器的交易處理效能。  
  
 我們建議您不要執行並行的標示的交易。 分散式標示交易的認可能因為另一個分散式標示交易同時間認可而產生死結，這是罕見但有可能發生的情況。 如果發生這種狀況，會選擇標示交易作為死結犧牲者，並將它回復。 發生這種錯誤時，應用程式可以重試標示的交易。 當多個標示的交易同時嘗試認可時，發生死結的可能性就比較高。  
  
## <a name="recovering-to-a-marked-transaction"></a>復原到標示的交易  
 如需如何將包含標示之交易的資料庫復原成特定標示或該標示之前的相關資訊，請參閱 [復原包含標記之異動的相關資料庫](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [復原包含標記之異動的相關資料庫](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
