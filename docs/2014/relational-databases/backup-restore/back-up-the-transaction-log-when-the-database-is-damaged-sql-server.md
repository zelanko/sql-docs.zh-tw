---
title: 資料庫損毀時備份交易記錄 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], damaged
- backing up [SQL Server]. damaged database
- transaction log backups [SQL Server], damaged databases
ms.assetid: 9b8873cc-df54-4336-ab9b-8f525132c2b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea712e6bc4e73119a4f07a7775f9f25e212f8534
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959558"
---
# <a name="back-up-the-transaction-log-when-the-database-is-damaged-sql-server"></a>資料庫損毀時備份交易記錄 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中於資料庫損毀時備份交易記錄。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，在資料庫損毀時備份交易記錄**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   如果是使用完整復原模式或大量記錄復原模式的資料庫，則在開始還原資料庫之前，您通常需要先備份記錄結尾。 在容錯移轉記錄傳送組態之前，您也應該先備份主要資料庫的記錄結尾。 在復原資料庫之前將結尾記錄備份還原為最終的記錄備份可在失敗之後避免工作遺失的狀況。 如需結尾記錄備份的詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](tail-log-backups-sql-server.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-back-up-the-tail-of-the-transaction-log"></a>若要備份交易記錄的結尾  
  
1.  連線至適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 **[工作]** ，然後按一下 **[備份]** 。 會出現 **[備份資料庫]** 對話方塊。  
  
4.  在 **[資料庫]** 清單方塊中確認資料庫名稱。 您可以選擇性從清單中選取不同的資料庫。  
  
5.  確認復原模式是否為 **[FULL]** 或 **[BULK_LOGGED]** 。  
  
6.  在 **[備份類型]** 清單方塊中，選取 **[交易記錄]** 。  
  
7.  保留 **[只複製備份]** 的未選取狀態。  
  
8.  在 **[備份組]** 區域，接受 **[名稱]** 文字方塊中建議的預設備份組名稱，或者輸入不同的備份組名稱。  
  
9. 在 [描述]  文字方塊中，輸入結尾記錄備份的描述。  
  
10. 指定備份組會在何時過期：  
  
    -   若要讓備份組在特定的天數後過期，請按一下 [之後]  \(預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 **[伺服器屬性]** 對話方塊 ( **[資料庫設定]** 頁面) 的 **[預設備份媒體保留 (以天為單位)]** 選項中設定。 若要存取此對話方塊，請以滑鼠右鍵按一下 [物件總管] 中的伺服器名稱並選取 [屬性]，然後選取 **[資料庫設定]** 頁面。  
  
    -   若要讓備份組在特定日期過期，請按一下 **[於]** ，然後輸入備份組將過期的日期。  
  
11. 按一下 **[磁碟]** 或 **[磁帶]** ，以選擇備份目的地的類型。 若要選取包含單一媒體集的磁碟或磁帶機 (最多 64 個) 的路徑，請按一下 **[加入]** 。 選取的路徑會在 **[備份至]** 清單方塊中顯示。  
  
     若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視備份目的地的內容，請選取目的地，然後按一下 **[內容]** 。  
  
12. 在 **[選項]** 頁面上，按一下下列其中一個項目，選取 **[覆寫媒體]** 選項：  
  
    -   **備份至現有的媒體集**  
  
         針對這個選項，按一下 **[附加至現有的備份組]** 或 **[覆寫所有現有的備份組]** 。  
  
         另外，也可以選取 **[檢查媒體集名稱及備份組是否逾期]** ，以讓備份作業確認媒體集及備份組逾期的日期和時間。  
  
         另外，也可以在 **[媒體集名稱]** 文字方塊中輸入名稱。 如果未指定名稱，就會建立一個空白名稱的媒體集。 如果您指定媒體集名稱，就會檢查媒體 (磁帶或磁碟)，以查看實際名稱是否與您在此處輸入的名稱相符。  
  
         如果您讓媒體名稱保持空白，並核取方塊以針對媒體進行檢查，成功也會使媒體上的媒體名稱保持空白。  
  
    -   **備份至新的媒體集，並清除所有現有的備份組**  
  
         針對這個選項，在 **[新媒體集名稱]** 文字方塊中輸入名稱，然後選擇性在 **[新媒體集描述]** 文字方塊中描述媒體集。  
  
     如需媒體集選項的詳細資訊，請參閱[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
13. (選擇性) 在 **[可靠性]** 區段中選取：  
  
    -   **[完成後驗證備份]** 。  
  
    -   **寫入媒體之前執行總和檢查碼**。  
  
    -   **發生總和檢查碼錯誤時繼續**  
  
     如需總和檢查碼的相關資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
14. 在 **[交易記錄]** 區段中，按一下 **[備份記錄的結尾，並讓資料庫保持在還原狀態]** 。  
  
     這相當於指定以下 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 陳述式：  
  
     `BACKUP LOG <database_name> TO <backup_device> WITH NORECOVERY`  
  
    > [!IMPORTANT]  
    >  在還原時，[還原資料庫] 對話方塊會將結尾記錄備份的類型顯示為 [交易記錄 (只複製)]  。  
  
15. 如果是備份至磁帶機 (在 [一般]  頁面的 [目的地]  區段中指定)，[備份後卸載磁帶]  選項會啟用供選擇。 按一下這個選項會啟動 **[卸載之前倒轉磁帶]** 選項。  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 和更新的版本支援 [備份壓縮](backup-compression-sql-server.md)。 依預設，備份壓縮與否取決於 **備份壓縮預設** 伺服器組態選項的值。 不過，不論目前的伺服器層級預設值為何，您都可以透過核取 [壓縮備份]  壓縮備份，而且可以透過核取 [不要壓縮備份]  防止壓縮。  
  
     **檢視目前的 backup compression default**  
  
    -   [檢視或設定 backup compression default 伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-backup-of-the-currently-active-transaction-log"></a>若要為目前使用中的交易記錄建立備份  
  
1.  執行 BACKUP LOG 陳述式，備份目前使用中的交易記錄，方法為指定：  
  
    -   欲備份之交易記錄所屬的資料庫名稱。  
  
    -   將寫入交易記錄備份的備份裝置。  
  
    -   NO_TRUNCATE 子句。  
  
         這個子句允許交易記錄作用中的部份也進行備份，即使資料庫無法存取，只要交易記錄可以存取而且沒有損毀即可。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
  
> [!NOTE]  
>  這個範例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，而這個資料庫使用簡單復原模式。 為了允許記錄備份，在執行完整資料庫備份之前，此資料庫已設定為使用完整復原模式。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
 在資料庫已損毀且無法存取時，只要交易記錄沒有損毀且可存取，這個範例就會備份目前使用中的交易記錄。  
  
```scr  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1  
   WITH NO_TRUNCATE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [備份資料庫 &#40;備份選項頁面&#41;](back-up-database-backup-options-page.md)   
 [備份資料庫 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [檔案還原 &#40;簡單復原模式&#41;](file-restores-simple-recovery-model.md)   
 [檔案還原 &#40;完整復原模式&#41;](file-restores-full-recovery-model.md)  
  
  
