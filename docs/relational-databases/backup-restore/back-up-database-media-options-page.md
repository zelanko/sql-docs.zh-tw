---
title: "備份資料庫 (媒體選項頁面) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql13.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7e1fd480768d75f33793f7260eb2652a25c1cc77
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="back-up-database-media-options-page"></a>備份資料庫 (媒體選項頁面)
  使用 [備份資料庫] 對話方塊的 [媒體選項] 頁面以簡式或修改資料庫媒體選項。  
  
 **若要使用 SQL Server Management Studio 建立備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  您可以定義資料庫維護計畫來建立資料庫備份。 如需詳細資訊，請參閱[維護計劃](../../relational-databases/maintenance-plans/maintenance-plans.md)和[使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您可以按下 [指令碼] 按鈕，然後選取指令碼的目的地，以產生相對應的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 指令碼。  
  
## <a name="options"></a>選項  
  
### <a name="overwrite-media"></a>覆寫媒體  
 [覆寫媒體] 面板的選項會控制備份寫入媒體的方式。 如果在 [備份資料庫] 對話方塊的 [一般] 頁面中選取 URL (Windows Azure 儲存體) 做為備份目的地，將會停用 [覆寫媒體] 區段下方的選項。 您可以覆寫備份，方法是使用 **BACKUP TO URL.WITH FORMAT** Transact-SQL 陳述式。 如需詳細資訊，請參閱 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。  
  
 只有 [Backup to a new media, and erase all existing backup sets (備份至新的媒體，並清除所有現有的備份組)] 選項支援加密選項。 如果您選取 [Back up to existing media (備份至現有媒體)] 區段下的選項，[備份選項] 頁面上的加密選項會停用。  
  
> [!NOTE]  
>  如需媒體集的一般資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)之執行個體的電腦上時，此選項才可以使用。  
  
 **備份至現有的媒體集**  
 將資料庫備份至現有的媒體集。 選取此選項按鈕來啟動三個選項。  
  
 選擇下列其中一個選項：  
  
 **附加至現有的備份組**  
 將備份組附加至現有的媒體集，會保留任何先前的備份。  
  
 **覆寫所有現有的備份組**  
 以目前的備份來取代現有媒體集上之任何先前的備份。  
  
 **檢查媒體集名稱及備份組是否逾期**  
 如果選擇性地備份到現有的媒體集，則備份作業必須確認媒體集的名稱以及備份組的到期日。  
  
 **媒體集名稱**  
 如果選擇性地選取了 [檢查媒體集名稱及備份組是否逾期]，請指定要用於此項備份作業的媒體集名稱。  
  
 **備份至新的媒體集，並清除所有現有的備份組**  
 使用新的媒體集，清除先前的備份組。  
  
 按一下此選項會啟動下列選項：  
  
 **新媒體集名稱**  
 選擇性地輸入媒體集的新名稱。  
  
 **新媒體集描述**  
 選擇性地輸入新媒體集具有意義的描述。 此項描述應該足夠詳實，才能精確地表示內容。  
  
### <a name="reliability"></a>可靠性  
 [交易記錄] 面板的選項控制備份作業的錯誤管理。  
  
 **完成後驗證備份**  
 確認備份組是完整的，且所有磁碟區都可以讀取。  
  
 **寫入媒體之前執行總和檢查碼**  
 寫入備份媒體之前確認總和檢查碼是否正確。 選取此選項相當於在 [!INCLUDE[tsql](../../includes/tsql-md.md)]的 BACKUP 陳述式中指定 CHECKSUM 選項。 選取此選項可能會增加工作負載，並減少備份作業的備份輸送量。 如需有關備份總和檢查碼的資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
 **發生錯誤時繼續**  
 即使發生一或多個錯誤，備份作業也會繼續執行。  
  
### <a name="transaction-log"></a>交易記錄  
 [交易記錄] 面板的選項控制交易記錄備份的行為。 只有在完整復原模式或大量記錄復原模式之下，這些選項才具有相關性。 只有在 [備份資料庫] 對話方塊的 [[一般](../../relational-databases/backup-restore/back-up-database-general-page.md)] 頁面中的 [備份類型] 欄位中，選取 [交易記錄] 後，才會啟動這些選項。****  
  
> [!NOTE]  
>  如需交易記錄備份的相關資訊，請參閱[交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
 **截斷交易記錄**  
 備份交易記錄並截斷，以釋放記錄空間。 資料庫仍維持在線上。 這是預設選項。  
  
 **備份記錄的結尾，並讓資料庫保持在還原狀態**  
 備份記錄的結尾，並讓資料庫保持在還原狀態。 此選項會建立「結尾記錄備份」，其會為尚未備份的記錄 (使用中的記錄) 進行備份，一般而言，是為還原資料庫做準備。** 資料庫完全還原之前，使用者無法使用資料庫。  
  
 選取此選項相當於在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 中指定 WITH NO_TRUNCATE, NORECOVERY。 如需詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
### <a name="tape-drive"></a>磁帶機  
 [磁帶機] 面板的選項控制備份作業的磁帶管理。 只有在 [備份資料庫] 對話方塊的 [[一般](../../relational-databases/backup-restore/back-up-database-general-page.md)] 頁面中的 [目的地] 面板中，選取 [磁帶] 後，才會啟動這些選項。****  
  
> [!NOTE]  
>  如需有關如何使用磁帶裝置的資訊，請參閱[備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)。  
  
 **備份後卸載磁帶**  
 備份完成之後再卸載磁帶。  
  
 **卸載之前倒轉磁帶**  
 卸載磁帶之前先將其釋放及倒轉。 只有在選取 [備份後卸除磁帶] 時才會啟用這個選項。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
