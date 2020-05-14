---
title: 還原頁面 (SQL Server) | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 在 SQL Server 中還原頁面。 還原損毀的頁面，而無需還原整個資料庫。
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8a7c149fbc59691519c1a85afe1ff64cc6da579a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823673"
---
# <a name="restore-pages-sql-server"></a>還原頁面 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在  中還原頁面。 分頁還原的目標是還原一個或多個受損頁面而毋需還原整個資料庫。 一般而言，選定要還原的頁面會標示為「有疑問」，因為存取該頁面時發生問題。 有疑問的頁面是在 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 資料庫的 **suspect_pages** 資料表中識別。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [頁面還原何時有用？](#WhenUseful)  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目還原頁面：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="when-is-a-page-restore-useful"></a><a name="WhenUseful"></a> 頁面還原何時有用？  
 頁面還原主要是用來修復隔離的損毀頁面。 還原和復原少數個別頁面可能比檔案還原更快，可以減少還原作業期間離線的資料量。 不過，如果不只是要還原一個檔案中的幾個頁面，則還原整個檔案，通常更有效率。 例如，如果在裝置上有很多頁面指出有暫止的裝置失敗，請考慮還原檔案，可能要還原至另一個位置，然後修復該裝置。  
  
 此外，並非所有頁面錯誤都需要還原。 快取資料 (如次要索引) 可能會發生問題，只要重新計算資料就可解決這個問題。 例如，如果資料庫管理員卸除並重建次要索引，則儘管已修正損毀資料，也不會在 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 資料表中指明為已修正。  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   頁面還原適用於使用完整或大量記錄復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 分頁還原只支援讀取/寫入檔案群組。  
  
-   只能還原資料庫頁面。 您無法使用分頁還原來還原下列項目：  
  
    -   交易記錄  
  
    -   配置頁面：全域配置對應 (Global Allocation Map，GAM) 頁面、共用全域配置對應 (Shared Global Allocation Map，SGAM) 頁面，以及頁面可用空間 (Page Free Space，PFS) 頁面。  
  
    -   所有資料檔案的頁面 0 (檔案啟動頁面)  
  
    -   頁面 1:9 (資料庫啟動頁面)  
  
    -   全文檢索目錄  
  
-   對於使用大量記錄復原模式的資料庫，分頁還原具有下列其他條件：  
  
    -   對於大量記錄資料而言，在檔案群組或分頁資料離線時進行備份會有問題，因為離線的資料並未記錄在記錄中。 任何離線頁面都可以阻止備份記錄。 在此情況下，請考慮使用 DBCC REPAIR，因為這可能會讓資料損失比還原最近備份還少。  
  
    -   除非指定 WITH CONTINUE_AFTER_ERROR，否則大量記錄資料庫的記錄備份遇到損壞的分頁時會失敗。  
  
    -   一般來說，分頁還原不適合用於大量記錄復原。  
  
         執行分頁還原的最佳作法是將資料庫設定為完整復原模式，並嘗試記錄備份。 如果記錄備份有效，您就可以進行分頁還原。 如果記錄備份失敗，您會失去自從前次記錄備份之後的工作，或必須試著執行 DBCC，且必須搭配 REPAIR_ALLOW_DATA_LOSS 選項來執行。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   頁面還原案例：  
  
     離線分頁還原  
     所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都支援在資料庫離線時還原頁面。 在離線頁面還原中，還原受損的頁面時資料庫是離線狀態。 在還原順序結束後，資料庫會恢復上線。  
  
     線上頁面還原  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 支援線上頁面還原，但是當資料庫目前離線時，該版本會使用離線還原。 在大部分情況下，損毀的頁面可以在資料庫保持上線時還原，包括正進行還原頁面的檔案群組在內。 即使有一個或多個次要檔案群組離線，只要主要檔案群組還在線上，通常就會在線上執行頁面還原。 但是，偶爾損毀的頁面可能需要進行離線還原。 例如，一些重要頁面損毀可能會讓資料庫無法啟動。  
  
    > [!WARNING]  
    >  若受損的頁面正在儲存重要資料庫中繼資料，則在嘗試線上頁面還原時，中繼資料的必要更新可能會失敗。 在此情況下，您可以執行離線頁面還原，但是您必須先建立 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) (使用 RESTORE WITH NORECOVERY 來備份交易記錄)。  
  
-   線上分頁還原會利用改良的頁面層級錯誤報告 (包括頁面總和檢查碼) 和追蹤。 因總和檢查碼或寫入損壞偵測為損毀的頁面 (「損毀頁面」  ) 可由頁面還原作業加以還原。 只有明確指定的頁面才會還原。 每一個指定的頁面都是由指定之資料備份中該頁面的複本所取代。  
  
     當您還原後續的記錄備份時，這些備份只會套用到至少包含一個正在復原之頁面的資料庫檔案。 必須套用未中斷的記錄備份鏈結至最後一個完整或差異還原，將包含該頁面的檔案群組向前帶到目前的記錄檔。 在檔案還原中，向前復原集會以單一記錄重做行程向前進行。 頁面還原若要成功，還原的頁面必須復原到與資料庫一致的狀態。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開始， 就會支援頁面還原。  
  
#### <a name="to-restore-pages"></a>若要還原頁面  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]連接到適當的  執行個體，然後在 [物件總管] 中，按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** 。 視資料庫而定，選取使用者資料庫，或者展開 [系統資料庫]  ，再選取系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]  ，再指向 [還原]  ，然後按一下 [頁面]  ，這樣會開啟 [還原頁面]  對話方塊。  
  
     **Restore**  
     此區段與 [還原資料庫 (一般頁面)](../../relational-databases/backup-restore/restore-database-general-page.md) 上的 **[還原至]** 執行相同功能。  
  
     **Database**  
     指定要還原的資料庫。 您可以輸入新的資料庫，或者從下拉式清單中選取現有的資料庫。  清單包含伺服器上的所有資料庫，但不含系統資料庫 **master**和 tempdb。  
  
    > [!WARNING]  
    >  若要還原受密碼保護的備份，必須使用 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式。  
  
     **結尾記錄備份**  
     在 [備份裝置]  中輸入或選取檔案名稱，在這個檔案中將會儲存資料庫的結尾記錄備份。  
  
     **備份組**  
     此區段顯示參與還原的備份組。  
  
    |頁首|值|  
    |------------|------------|  
    |**名稱**|備份組的名稱。|  
    |**元件**|備份的元件：[資料庫]  、[檔案]  或 [\<空白>]  (適用於交易記錄)。|  
    |**型別**|執行的備份類型：[完整]  、[差異]  或 [交易記錄]  。|  
    |**Server**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行備份作業的  執行個體名稱。|  
    |**Database**|備份作業中所含的資料庫名稱。|  
    |**位置**|備份組在磁碟區中的位置。|  
    |**第一個 LSN**|在備份組中第一個交易的記錄序號 (LSN)。 針對檔案備份為空白。|  
    |**最後一個 LSN**|在備份組中最後一個交易的記錄序號 (LSN)。 針對檔案備份為空白。|  
    |**檢查點 LSN**|建立備份時最近檢查點的記錄序號 (LSN)。|  
    |**完整 LSN**|最新完整資料庫備份的記錄序號 (LSN)。|  
    |**開始日期**|備份作業開始時的日期和時間，會出現在用戶端的地區設定中。|  
    |**完成日期**|備份作業完成時的日期和時間，會出現在用戶端的地區設定中。|  
    |**大小**|備份組的大小 (以位元組為單位)。|  
    |**使用者名稱**|執行備份作業的使用者名稱。|  
    |**到期**|備份組過期的日期和時間。|  
  
      按一下 [驗證] 來檢查執行頁面還原作業所需之備份檔案的完整性。  
  
4.   若要識別損毀頁面，在 **[資料庫]** 方塊中已選取正確的資料庫時，按一下 [檢查資料庫頁面]。 這是長時間執行的作業。  
  
    > [!WARNING]  
    >  若要還原未損毀的特定頁面，請按一下 [加入]  ，然後輸入要還原之頁面的 [檔案識別碼]  和 [頁面識別碼]  。  
  
5.  頁面方格會用來識別要還原的頁面。 一開始是從 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 系統資料表填入這個方格。  若要從方格中加入或移除頁面，請按一下 **[加入]** 或 [移除]。 如需詳細資訊，請參閱 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)，在  中還原頁面。  
  
6.  **[備份組]** 方格會列出預設還原計畫中的備份組。  您可以選擇按一下 [確認]，確認備份可讀取而且備份組是完整的，而不需加以還原。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
     **頁面**  
  
7.   若要還原頁面方格中所列的頁面，請按一下 [確定]。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 若要在 RESTORE DATABASE 陳述式中指定頁面，您需要包含該頁面之檔案的檔案識別碼和頁面的頁面識別碼。 所需語法如下：  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 如需 PAGE 選項之參數的詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。 如需 RESTORE DATABASE 語法的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
#### <a name="to-restore-pages"></a>若要還原頁面  
  
1.  取得要還原之已損壞頁面的頁面識別碼。 總和檢查碼或分次寫入錯誤會傳回頁面識別碼，提供指定頁面所需的資訊。 若要查閱已損壞頁面的頁面識別碼，請使用下列來源：  
  
    |頁面識別碼來源|主題|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)|  
    |錯誤記錄檔|[檢視 SQL Server 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)|  
    |事件追蹤|[監視及回應事件](../../ssms/agent/monitor-and-respond-to-events.md)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|  
    |WMI 提供者|[伺服器事件的 WMI 提供者概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  使用包含該頁面之完整資料庫、檔案或檔案群組備份，開始進行分頁還原。 在 RESTORE DATABASE 陳述式中，使用 PAGE 子句來列出要還原之所有分頁的頁面識別碼。  
  
3.  套用最新差異  
  
4.  套用後續的記錄備份。  
  
5.  為包含還原頁面之最後一個 LSN 的資料庫建立新的記錄備份，亦即上次進行離線分頁還原的時點。 最後一個 LSN (設定為順序中的第一個還原的一部分) 是重做目標 LSN。 針對包含頁面的檔案進行線上向前復原可在重做目標 LSN 停止。 若要了解檔案目前的重做目標 LSN，請參閱 **sys.master_files** 的 **redo_target_lsn** 資料行。 如需詳細資訊，請參閱 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)。  
  
6.  還原新的記錄備份。 套用此新的記錄備份後，就可完成分頁還原，頁面現在可以使用。  
  
    > [!NOTE]  
    >  這個順序與檔案還原順序類似。 事實上，分頁還原和檔案還原都可以做為相同順序的一部分來執行。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 下列範例會以 `B` 還原檔案 `NORECOVERY`的四個損毀頁面。 接著，兩個記錄備份會套用 `NORECOVERY`，後面接著以 `RECOVERY`還原的結尾記錄備份。 這個範例會執行線上還原。 在範例中，檔案 `B` 的檔案識別碼是 `1`，而損毀頁面的頁面識別碼是 `57`、 `202`、 `916`和 `1016`。  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
