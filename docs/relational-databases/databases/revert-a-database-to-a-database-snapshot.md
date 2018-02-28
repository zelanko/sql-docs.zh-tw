---
title: "將資料庫還原成資料庫快照集 | Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a93fde67cfb08245607153afbddaffd1aca6669
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="revert-a-database-to-a-database-snapshot"></a>將資料庫還原成資料庫快照集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
如果線上資料庫中的資料已經損毀，在某些情況下，將資料庫還原成發生損毀之前的資料庫快照集可能是從備份還原資料庫的正確替代方式。 例如，還原資料庫可用於反轉最近發生的嚴重使用者錯誤，例如誤將資料表卸除。 不過，在快照集之後進行的所有變更都將遺失。  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **To Revert a Database to a Database Snapshot, using:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 在下列狀況下，不支援還原：  
  
-   資料庫目前只能有一個資料庫快照集，就是您打算要還原的目標快照集。  
  
-   任何唯讀或壓縮的檔案群組存在資料庫中。  
  
-   建立快照集時原本處於線上狀態的所有檔案，現在都變成離線狀態。  
  
 在還原資料庫之前，請仔細考慮以下限制：  
  
-   還原不適用於媒體復原。 執行個體時提供 SQL Server 登入。 資料庫快照集是不完整的資料庫檔案複本，因此如果資料庫或資料庫快照集已損毀，很可能無法從快照集還原。 此外，即使可以還原，但是在損毀的情況下還原也不太可能會更正問題。 因此，建立定期備份和測試還原計畫是保護資料庫的基本措施。 如需詳細資訊，請參閱 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
    > [!NOTE]  
    >  如果您必須能夠將來源資料庫還原到您建立資料庫快照集當時的時間點，請使用完整復原模式並實作可讓您執行此作業的備份原則。  
  
-   還原的資料庫會覆寫原始的來源資料庫，因此自從建立快照集以來對資料庫進行的任何更新都將遺失。  
  
-   還原作業也會覆寫舊的記錄檔並重建記錄檔。 所以，您無法將還原的資料庫向前復原至發生使用者錯誤的時間點。 因此，我們建議您先備份記錄檔，然後再還原資料庫。  
  
    > [!NOTE]  
    >  雖然您不能藉由還原原始記錄檔來向前復原資料庫，但原始記錄檔中的資訊對於重建失去的資料還是非常有用。  
  
-   還原會中斷記錄備份鏈結。 因此，您必須先進行完整資料庫備份或檔案備份，然後才能進行已還原資料庫的記錄備份。 我們建議您進行完整資料庫備份。  
  
-   在還原作業期間，將無法使用快照集和來源資料庫。 來源資料庫和快照都會標示為「還原中」。 如果還原作業期間發生錯誤，當資料庫重新啟動時，還原作業會嘗試完成還原。  
  
-   已還原之資料庫的中繼資料，將與建立快照時的中繼資料相同。  
  
-   還原會卸除所有全文檢索目錄。  
  
###  <a name="Prerequisites"></a> 必要條件  
 請確定來源資料庫和資料庫快照集符合下列必要條件：  
  
-   確認資料庫尚未損毀。  
  
    > [!NOTE]  
    >  如果資料庫已損毀，您就必須從備份還原資料庫。 如需詳細資訊，請參閱[完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) 或[完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)。  
  
-   識別在發生錯誤之前建立的最近快照集。 如需詳細資訊，請參閱 [檢視資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
-   卸除目前存在資料庫上的任何其他快照集。 如需詳細資訊，請參閱 [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 任何擁有來源資料庫之 RESTORE DATABASE 權限的使用者都可以將它還原成建立資料庫快照集時的狀態。  
  
##  <a name="TsqlProcedure"></a> 如何將資料庫還原成資料庫快照集 (使用 Transact-SQL)  
 **若要將資料庫還原成資料庫快照集**  
  
> [!NOTE]  
>  如需此程序的範例，請參閱本節稍後的 [範例 (Transact-SQL)](#TsqlExample)。  
  
1.  識別您要將資料庫還原成哪一個資料庫快照集。 您可以檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中之資料庫的快照集 (請參閱 [檢視資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md))。 此外，您可以從 **sys.databases &#40;Transact-SQL&#41;** 目錄檢視的 [sys.databases &amp;#40;Transact-SQL&amp;#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 資料行中，識別某個檢視的來源資料庫。  
  
2.  卸除任何其他資料庫快照集。  
  
     如需卸除快照集的相關資訊，請參閱 [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md). 如果資料庫使用完整復原模式，您應該在還原之前備份記錄。 如需詳細資訊，請參閱[備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md) 或[資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)。  
  
3.  執行還原作業。  
  
     還原作業需要來源資料庫上的 RESTORE DATABASE 權限。 若要還原資料庫，請使用下列 Transact-SQL 陳述式：  
  
     RESTORE DATABASE *database_name* FROM DATABASE_SNAPSHOT **=***database_snapshot_name*  
  
     其中 *database_name* 是來源資料庫，而 *database_snapshot_name* 是要用來還原資料庫的快照集名稱。 請注意，在此陳述式中，您必須指定快照名稱，而非備份裝置。  
  
     如需詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
    > [!NOTE]  
    >  在還原作業期間，將無法使用快照和來源資料庫。 來源資料庫和快照集都會標示為「還原中」。 如果還原作業期間發生錯誤，它會在資料庫重新啟動時嘗試完成還原。  
  
4.  如果建立資料庫快照集之後，資料庫擁有者有變更過，您可以更新所還原資料庫的資料庫擁有者。  
  
    > [!NOTE]  
    >  還原的資料庫會保留資料庫快照集的權限和組態 (例如，資料庫擁有者和復原模式)。  
  
5.  啟動資料庫。  
  
6.  您可以選擇性地備份還原的資料庫，特別是當它使用完整 (或大量記錄) 復原模式時。 若要備份資料庫，請參閱[建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 本節包含將資料庫還原成資料庫快照集的下列範例：  
  
-   A. [還原 AdventureWorks 資料庫上的快照集](#Reverting_AW)  
  
-   B. [還原 Sales 資料庫上的快照集](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. 還原 AdventureWorks 資料庫上的快照集  
 此範例假設 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上目前只有一個快照集。 如需建立還原資料庫之快照集的範例，請參閱 [建立資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. 還原 Sales 資料庫上的快照集  
 此範例假設 **Sales** 資料庫中目前有兩個快照集： **sales_snapshot0600** 和 **sales_snapshot1200**。 此範例會刪除較舊的快照集，並將資料庫還原到較新的快照集。  
  
 如需建立範例資料庫與此範例使用之快照的程式碼，請參閱：  
  
-   對於 **Sales** 資料庫與 **sales_snapshot0600** 快照集，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) 中的＜使用檔案群組建立資料庫＞和＜建立資料庫快照集＞。  
  
-   對於 **sales_snapshot1200** 快照集，請參閱 [建立資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [檢視資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [資料庫鏡像和資料庫快照集 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
