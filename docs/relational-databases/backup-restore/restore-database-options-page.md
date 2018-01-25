---
title: "還原資料庫 (選項頁面) | Microsoft 文件"
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
f1_keywords: sql13.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
caps.latest.revision: "68"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0bdd383335126a36265bc917c1679dbd5ab0dc3e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="restore-database-options-page"></a>還原資料庫 (選項頁面)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用 [還原資料庫] 對話方塊的 [選項] 頁面，即可修改還原作業的行為和結果。  
  
 **若要使用 SQL Server Management Studio 還原資料庫備份**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]指定還原工作時，可以針對這個還原作業產生包含 RESTORE 陳述式的對應 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 若要產生指令碼，請按一下 [指令碼]，然後選取指令碼的目的地。 如需 RESTORE 語法的資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
## <a name="options"></a>選項。  
  
### <a name="restore-options"></a>還原選項  
 若要修改還原作業的行為方面，可以使用 [還原選項] 面板的選項。  
  
 **覆寫現有的資料庫 [WITH REPLACE]**  
 還原作業將會覆寫目前正在使用資料庫名稱 (在 [還原資料庫] 對話方塊之 [一般](../../relational-databases/backup-restore/restore-database-general-page.md) 頁面的 [還原至] 欄位中指定) 的任何資料庫檔案。 即使是將備份從不同的資料庫還原為現有的資料庫名稱，現有資料庫的檔案也會遭到覆寫。 選取此選項相當於使用 [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) 陳述式 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 的 REPLACE 選項。  
  
> [!CAUTION]  
>  請仔細考慮之後再使用這個選項。 如需詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
 **保留複寫設定 [WITH KEEP_REPLICATION]**  
 將發行資料庫還原至並非建立該資料庫的伺服器時，就會保留複寫設定。 只有在建立備份時複寫了資料庫，這個選項才會相關。  
  
 這個選項只能搭配 [回復未認可的交易，讓資料庫保持備妥可用] 選項 (本資料表稍後會描述) 使用，這相當於使用 RECOVERY 選項來還原備份。  
  
 選取此選項相當於使用 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中的 KEEP_REPLICATION 選項。  
  
 如需詳細資訊，請參閱 [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。  
  
 **限制對還原資料庫的存取 [WITH RESTRICTED_USER]**  
 僅有 **db_owner**、 **dbcreator**或 **系統管理員**的成員可以使用還原資料庫。  
  
 選取此選項相當於使用 RESTORE 陳述式的 RESTRICTED_USER 選項。  
  
### <a name="recovery-state"></a>復原狀態  
 若要在存放區作業之後判斷資料庫的狀態，則必須選取 [復原狀態] 面板的其中一個選項。  
  
 **RESTORE WITH RECOVERY**  
 透過還原 [[一般] 頁面](../../relational-databases/backup-restore/restore-database-general-page.md)之 [要還原的備份組] 方格中所核取的最後一個備份來復原資料庫。 這是預設的選項，而且相當於在 [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) 陳述式 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 中指定 WITH RECOVERY。  
  
> [!NOTE]  
>  在完整復原模式或大量記錄復原模式下時，只有在需要立即還原所有記錄檔時才選擇此選項。  
  
 **RESTORE WITH NORECOVERY**  
 讓資料庫保持在還原狀態。 這樣可讓您還原目前復原路徑中的其他備份。 若要復原資料庫，必須使用 RESTORE WITH RECOVERY 選項 (請參閱先前選項) 執行還原作業。  
  
 此選項相當於在 RESTORE 陳述式中指定 WITH NORECOVERY。  
  
 如果選取此選項，將無法使用 **[保留複寫設定]** 選項。  
  
 **RESTORE WITH STANDBY**  
 將資料庫保留為待命狀態，資料庫在此狀態下可提供有限的唯讀存取。 此選項相當於在 RESTORE 陳述式中指定 WITH STANDBY。  
  
 若要選擇此選項，則必須在 [待命資料庫檔案] 文字方塊中指定待命資料庫檔案。 待命資料庫檔案可以恢復復原效果。  
  
 **待命資料庫檔案**  
 指定待命資料庫檔案。 您可以瀏覽待命資料庫檔案，或者在文字方塊中直接輸入其路徑名稱。  
  
### <a name="tail-log-backup"></a>結尾記錄備份  
 可讓您指定在資料庫還原時一併執行結尾記錄備份。  
  
 **還原前建立結尾記錄備份**  
 核取此方塊，即可指定應該執行結尾記錄備份。  
  
> [!NOTE]  
>  如果您在 [[備份時間表]](../../relational-databases/backup-restore/backup-timeline.md) 對話方塊中選取的時間點需要結尾記錄備份，系統就會選取這個方塊，而且您無法進行編輯。  
  
 **備份檔案**  
 指定記錄結尾的備份檔案。 您可以瀏覽備份檔案，也可以直接在文字方塊中輸入其名稱。  
  
### <a name="server-connections"></a>伺服器連接  
 可讓您關閉現有的資料庫連接。  
  
 **關閉現有的連接**  
 若資料庫有使用中的連接，還原作業可能會失敗。 核取 **[關閉現有的連接選項]** ，確定已關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與資料庫之間的所有使用中連接。 這個核取方塊會在執行還原作業之前將資料庫設定為單一使用者模式，並在完成後將資料庫設定為多使用者模式。  
  
### <a name="prompt"></a>提示  
 **還原每個備份之前先提示**  
 指定在還原每個備份之後顯示 [繼續還原] 對話方塊，以便詢問是否還要繼續還原順序。 這個對話方塊會顯示下一個媒體集的名稱 (如果知道)，以及下一個備份組的名稱和描述。  
  
 這個選項可讓您在還原任何備份之後暫停還原順序。 您必須為不同的媒體集交換磁帶時，這個選項特別有用，例如當伺服器只有一個磁帶裝置時。 當您準備繼續時，請按一下 [確定]。  
  
 您可以按一下 [否] 中斷還原順序。 這會使資料庫處於還原狀態。 您可以依您的方便，稍後再繼續 [繼續還原] 對話方塊中描述的下一項備份，以繼續進行還原順序。 還原下一項備份的程序是依照該備份是否包含資料或交易記錄而定，如下所示：  
  
-   如果下一個備份是完整備份或差異備份，請再次使用 [還原資料庫] 工作。  
  
-   如果下一個備份是檔案備份，請使用 [還原檔案和檔案群組] 工作。 如需詳細資訊，請參閱[還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)。  
  
-   如果下一個備份是記錄檔備份，請使用 **[還原交易記錄檔]** 工作。 如需藉由還原交易記錄來繼續還原順序的資訊，請參閱 [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [從裝置還原備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
