---
title: 將 SQL Server 資料庫還原至某個時間點 (完整復原模式) | Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- STOPAT clause [RESTORE LOG statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
ms.assetid: 3a5daefd-08a8-4565-b54f-28ad01a47d32
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f4a4a91c4703bd4634f471e3d6bc0b9b4baf2305
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908884"
---
# <a name="restore-a-sql-server-database-to-a-point-in-time-full-recovery-model"></a>將 SQL Server 資料庫還原至某個時間點 (完整復原模式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中將資料庫還原至時間點。 本主題僅與使用完整或大量記錄復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫相關。  
  
> [!IMPORTANT]  
>  在大量記錄復原模式下，如果記錄備份包含大量記錄的變更，則時間點復原不可能復原至該備份內的時間點。 資料庫必須復原至交易記錄備份的結尾。  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要將 SQL Server 資料庫還原到某個時間點，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   您可以使用 STANDBY 尋找未知時間點。  
  
-   指定還原順序中較早的時間點  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **將資料庫還原至某個時間點**  
  
1.  在 [物件總管] 中，連接至適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體，並展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** 。 視資料庫而定，選取使用者資料庫，或者展開 [系統資料庫]  ，再選取系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，依序指向 [工作]  及 [還原]  ，然後按一下 [資料庫]  。  
  
4.  在 **[一般]** 頁面上，使用 **[來源]** 區段指定要還原之備份組的來源和位置。 選取下列其中一個選項：  
  
    -   **Database**  
  
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    > [!NOTE]  
    >  如果備份是根據不同的伺服器建立的，目的地伺服器就沒有指定之資料庫的備份記錄資訊。 在此情況下，請選取 **[裝置]** ，以便手動指定要還原的檔案或裝置。  
  
    -   **裝置**  
  
         按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 在 **[備份媒體類型]** 方塊中，選取列出的其中一種裝置類型。 若要選取 **[備份媒體]** 方塊中的一個或多個裝置，請按一下 **[加入]** 。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
         在 **[來源：裝置：資料庫]** 清單方塊中，選取應該還原的資料庫名稱。  
  
         **注意** ：這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。  
  
5.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。  
  
6.  按一下 **[時間表]** ，存取 **[備份時間表]** 對話方塊。  
  
7.  在 **[還原至]** 區段中，按一下 **[特定的日期與時間]** 。  
  
8.  使用 **[日期]** 及 **[時間]** 方塊或滑動軸，指定應該停止還原的特定日期與時間。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  您可以使用 [時間表間隔]  方塊變更時間表上顯示的時間量。  
  
9. 當您指定了特定的時間點之後，Database Recovery Advisor 便會在 **[要還原的備份組]** 方格的 **[還原]** 資料行中確定只選取要還原到該時間點所需的備份。 這些選取的備份為您的時間點還原構成了建議的還原計畫。 您應該只使用選取的備份來進行時間點還原作業。  
  
     如需 [要還原的備份組]  方格中各資料行的相關資訊，請參閱[還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)。 如需資料庫復原建議程式的相關資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
10. 在 **[選項]** 頁面的 **[還原選項]** 面板中，您可以選取下列任何選項 (如果情況適用)：  
  
    -   **覆寫現有的資料庫 (WITH REPLACE)**  
  
    -   **保留複寫設定 (WITH KEEP_REPLICATION)**  
  
    -   **限制對還原資料庫的存取 (WITH RESTRICTED_USER)**  
  
     如需這些選項的詳細資訊，請參閱[還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)。  
  
11. 針對 **[還原狀態]** 方塊，選取選項。 此方塊決定資料庫在還原作業之後的狀態。  
  
    -   **RESTORE WITH RECOVERY** 是預設行為，透過回復未認可的交易，讓資料庫保持備妥可用。 無法還原其他交易記錄。 若您要立即還原所有必要的備份，請選取這個選項。  
  
    -   **RESTORE WITH NORECOVERY** ，讓資料庫保持不運作，且不回復未認可的交易。 可以還原其他交易記錄。 資料庫在復原之前都無法使用。  
  
    -   **RESTORE WITH STANDBY** ，讓資料庫處於唯讀模式。 它會復原未認可的交易，但會將復原動作儲存在待命資料庫檔案中，以還原復原影響。  
  
     如需這些選項的描述，請參閱[還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)。  
  
12. 如果選取的時間點需要 [還原前先進行結尾記錄備份]  ，則會予以選取。 您不需要修改這個設定，但是即使不需要，還是可以選擇備份記錄結尾。  
  
13. 若資料庫有使用中的連接，還原作業可能會失敗。 核取 **[關閉現有的連接選項]** ，確定已關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與資料庫之間的所有使用中連接。 這個核取方塊會在執行還原作業之前將資料庫設定為單一使用者模式，並在完成後將資料庫設定為多使用者模式。  
  
14. 如果想要系統在每個還原作業之間提示您，請選取 **[還原每個備份之前先提示]** 。 除非資料庫夠大，而且您想要監視還原作業的狀態，否則這通常不需要。  

##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **開始之前**  
  
 指定的時間一律是從記錄備份中還原。 在還原順序的每個 RESTORE LOG 陳述式中，您必須在相同的 STOPAT 子句中指定目標時間或交易。 您必須先還原其端點早於目標還原時間的完整資料庫備份，當做時間點還原的必要條件。 該完整資料庫備份可以晚於最近的完整資料庫備份，只要您之後還原每個後續的記錄備份即可，最多並包括含有目標時間點的記錄備份。  
  
 若要協助您識別要還原哪個資料庫備份，可以選擇性地在 RESTORE DATABASE 陳述式中指定 WITH STOPAT 子句，以便在資料庫備份太接近指定的目標時間時引發錯誤。 此時，系統一定會還原完整的資料備份，即使它包含目標時間也一樣。  
  
 **基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法**  
  
 RESTORE LOG *database_name* FROM <backup_device> WITH STOPAT **=** _time_ **,** RECOVERY...  
  
 復原點是在由 **時間** 指定的 *datetime*值當時或之前所發生的最新交易認可。  
  
 若只要還原特定時間點之前進行的修改，請為您要還原的每個備份指定 WITH STOPAT **=** _time_。 這樣可確保您不會還原到超過目標時間。  
  
 **將資料庫還原至某個時間點**  
  
> [!NOTE]  
>  如需這個程序的範例，請參閱本節稍後的 [範例 &#40;Transact-SQL&#41;](#TsqlExample)。  
  
1.  連接至想要在其上還原資料庫的伺服器執行個體。  
  
2.  使用 NORECOVERY 選項執行 RESTORE DATABASE 陳述式。  
  
    > [!NOTE]  
    >  如果部分還原順序排除任何 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) 檔案群組，則不支援時間點還原。 您可以強制還原順序，以繼續進行。 但是，絕對無法還原 RESTORE 陳述式中省略的 FILESTREAM 檔案群組。 若要強制時間點還原，請指定 CONTINUE_AFTER_ERROR 選項，連同 STOPAT、STOPATMARK 或 STOPBEFOREMARK 選項，而且您也必須在後續的 RESTORE LOG 陳述式中指定這些項目。 如果您指定 CONTINUE_AFTER_ERROR，則部分還原順序會成功，而 FILESTREAM 檔案群組則會變成無法復原。  
  
3.  還原上一次的差異資料庫備份 (如有)，但不復原資料庫 (RESTORE DATABASE *database_name* FROM *backup_device* WITH NORECOVERY)。  
  
4.  依建立的相同順序，套用每個交易記錄備份，並指定想要停止還原記錄的時間 (RESTORE DATABASE *database_name* FROM <backup_device> WITH STOPAT **=** _time_ **,** RECOVERY)。  
  
    > [!NOTE]  
    >  RECOVERY 及 STOPAT 選項。 如果交易記錄備份中不含所要求的時間 (例如指定的時間超出交易記錄的結束時間)，則會產生警告訊息，且此資料庫會維持未復原狀態。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 下列範例會將資料庫還原至 `12:00 AM``April 15, 2020` 時的狀態，並顯示含有多個記錄備份的還原作業。 在備份裝置 `AdventureWorksBackups`上，要還原的完整資料庫備份是裝置上的第三個備份組 (`FILE = 3`)，第一個記錄備份是第四個備份組 (`FILE = 4`)，而第二個記錄備份是第五個備份組 (`FILE = 5`)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫使用簡單復原模式。 若要允許記錄備份，在執行完整資料庫備份之前，已使用 `ALTER DATABASE AdventureWorks SET RECOVERY FULL`將資料庫設定為使用完整復原模式。  
  
```  
RESTORE DATABASE AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks WITH RECOVERY;   
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [復原到記錄序號 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ToPointInTime%2A> (SMO)  
  
## <a name="see-also"></a>另請參閱  
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
  
