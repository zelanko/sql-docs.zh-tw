---
title: "還原差異資料庫備份 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full differential backups [SQL Server]
- restoring databases [SQL Server], full differential backups
- database backups [SQL Server], full differential backups
- database restores [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
ms.assetid: 0dd971a4-ee38-4dd3-9f30-ef77fc58dd11
caps.latest.revision: "46"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d5a965b04e6c09bfe067b3894cac0591fefd0247
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="restore-a-differential-database-backup-sql-server"></a>還原差異資料庫備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中還原差異資料庫備份。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **若要使用下列項目還原差異資料庫備份：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在明確或隱含的交易中，不允許使用 RESTORE。  
  
-   在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，無法還原較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本所建立的備份。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以從使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本所建立的資料庫備份還原使用者資料庫。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   在完整或大量記錄還原模式下，您必須先備份使用中的交易記錄檔 (也稱為記錄檔的結尾)，才能還原資料庫。 如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-restore-a-differential-database-backup"></a>還原差異資料庫備份  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 [資料庫]。 視資料庫而定，選取使用者資料庫，或者展開 [系統資料庫] ，再選取系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，依序指向 [工作] 及 [還原]，然後按一下 [資料庫]。  
  
4.  在 **[一般]** 頁面上，使用 **[來源]** 區段指定要還原之備份組的來源和位置。 選取下列其中一個選項：  
  
    -   **[資料庫備份]**  
  
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    > [!NOTE]  
    >  如果備份是根據不同的伺服器建立的，目的地伺服器就沒有指定之資料庫的備份記錄資訊。 在此情況下，請選取 **[裝置]** ，以便手動指定要還原的檔案或裝置。  
  
    -   **[裝置]**  
  
         按一下瀏覽 (**...**) 按鈕，開啟 [選取備份裝置] 對話方塊。 在 **[備份媒體類型]** 方塊中，選取列出的其中一種裝置類型。 若要選取 **[備份媒體]** 方塊中的一個或多個裝置，請按一下 **[加入]**。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
         在 **[來源: 裝置: 資料庫]** 清單方塊中，選取應該還原的資料庫名稱。  
  
         **注意** ：這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。  
  
5.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。  
  
    > [!NOTE]  
    >  若要在特定時間點停止還原，請按一下 **[時間表]** 存取 **[備份時間表]** 對話方塊。 如需在特定時間點停止資料庫還原的說明，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
6.  在 **[要還原的備份組]** 方格中，透過您想要還原的差異備份選取備份。  
  
     如需 [要還原的備份組] 方格中各資料行的相關資訊，請參閱[還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)。  
  
7.  在 **[選項]** 頁面的 **[還原選項]** 面板中，您可以選取下列任何選項 (如果情況適用)：  
  
    -   **覆寫現有的資料庫 (WITH REPLACE)**  
  
    -   **保留複寫設定 (WITH KEEP_REPLICATION)**  
  
    -   **還原每個備份之前先提示**  
  
    -   **限制對還原資料庫的存取 (WITH RESTRICTED_USER)**  
  
     如需這些選項的詳細資訊，請參閱[還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)。  
  
8.  針對 **[還原狀態]** 方塊，選取選項。 此方塊決定資料庫在還原作業之後的狀態。  
  
    -   **RESTORE WITH RECOVERY** 是預設行為，透過回復未認可的交易，讓資料庫保持備妥可用。 無法還原其他交易記錄。 若您要立即還原所有必要的備份，請選取這個選項。  
  
    -   **RESTORE WITH NORECOVERY** ，讓資料庫保持不運作，且不回復未認可的交易。 可以還原其他交易記錄。 資料庫在復原之前都無法使用。  
  
    -   **RESTORE WITH STANDBY** ，讓資料庫處於唯讀模式。 它會復原未認可的交易，但會將復原動作儲存在待命資料庫檔案中，以還原復原影響。  
  
     如需這些選項的描述，請參閱[還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)。  
  
9. 若資料庫有使用中的連接，還原作業會失敗。 核取 **[關閉現有的連接選項]** ，確定已關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與資料庫之間的所有使用中連接。  
  
10. 如果想要系統在每個還原作業之間提示您，請選取 **[還原每個備份之前先提示]** 。 除非資料庫夠大，而且您想要監視還原作業的狀態，否則這通常不需要。  
  
11. 或者，使用 **[檔案]** 頁面將資料庫還原到新位置。 如需移動資料庫的說明，請參閱[將資料庫還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-a-differential-database-backup"></a>還原差異資料庫備份  
  
1.  執行 RESTORE DATABASE 陳述式並指定 NORECOVERY 子句，以還原在差異資料庫備份之前的完整資料庫備份。 如需詳細資訊，請參閱＜ [如何：還原完整備份](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)＞。  
  
2.  執行 RESTORE DATABASE 陳述式以還原差異資料庫備份，請指定：  
  
    -   將套用差異資料庫備份的資料庫名稱。  
  
    -   將要還原差異資料庫備份的備份裝置。  
  
    -   如果在還原差異資料庫備份之後，您有交易記錄備份可以套用，則指定 NORECOVERY 子句。 否則，指定 RECOVERY 子句。  
  
3.  使用完整或大量記錄復原模式，還原差異資料庫備份可將資料庫還原到完成差異資料庫備份的時間點。 若要復原到失敗點，您必須套用上次建立差異資料庫備份後所建立的所有交易記錄備份。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
  
#### <a name="a-restoring-a-differential-database-backup"></a>A. 還原差異資料庫備份  
 這個範例還原 `MyAdvWorks` 資料庫與差異資料庫備份。  
  
```sql  
-- Assume the database is lost, and restore full database,   
-- specifying the original full database backup and NORECOVERY,   
-- which allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   RECOVERY;  
GO  
```  
  
#### <a name="b-restoring-a-database-differential-database-and-transaction-log-backup"></a>B. 還原資料庫、差異資料庫及交易記錄備份  
 這個範例還原 `MyAdvWorks` 資料庫、差異資料庫及其交易記錄備份。  
  
```sql  
-- Assume the database is lost at this point. Now restore the full   
-- database. Specify the original full database backup and NORECOVERY.  
-- NORECOVERY allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   NORECOVERY;  
GO  
-- Now restore each transaction log backup created after  
-- the differential database backup.  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log1  
   WITH NORECOVERY;  
GO  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log2  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [還原 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
