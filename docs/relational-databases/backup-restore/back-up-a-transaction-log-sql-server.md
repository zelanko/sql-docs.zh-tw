---
title: 備份交易記錄 | Microsoft Docs
description: 本文描述如何使用 SQL Server Management Studio、Transact-SQL 或 PowerShell 以在 SQL Server 中備份交易記錄。
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction log backups [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- backing up transaction logs [SQL Server], SQL Server Management Studio
ms.assetid: 3426b5eb-6327-4c7f-88aa-37030be69fbf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1e01e01544a0417210a8f2e3a40bb10398875c37
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719968"
---
# <a name="back-up-a-transaction-log"></a>備份交易記錄
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中備份交易記錄。  

## <a name="before-you-begin"></a>開始之前
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
在明確或[隱含](../../t-sql/statements/set-implicit-transactions-transact-sql.md)的交易中，並不允許使用 `BACKUP` 陳述式。 明確交易是明確定義交易的啟動與結束的一種交易。

### <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
- 如果資料庫使用完整復原模式或大量記錄[復原模式](recovery-models-sql-server.md)，您必須定期備份交易記錄，使其足以保護您的資料，並避免[交易記錄填滿](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)。 這會截斷記錄並支援將資料庫還原到特定時間點。 
  
- 根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
### <a name="permissions"></a><a name="Permissions"></a> 權限

需要的 `BACKUP DATABASE` 和 `BACKUP LOG` 權限預設為授與給 **系統管理員**固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。 請檢查權限是否正確，再開始進行。
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，在嘗試存取[實體資源](backup-devices-sql-server.md)之前，備份裝置實體檔案的權限問題可能不太明顯。 同樣地，請檢查權限，再開始進行。

## <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio

1. 連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
1. 展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
1. 以滑鼠右鍵按一下資料庫，指向 **[工作]** ，然後按一下 **[備份]** 。 會出現 **[備份資料庫]** 對話方塊。  
 
1. 在 **[資料庫]** 清單方塊中確認資料庫名稱。 您可以選擇性從清單中選取不同的資料庫。  
  
1. 確認復原模式是否為 **[FULL]** 或 **[BULK_LOGGED]** 。  
  
1. 在 **[備份類型]** 清單方塊中，選取 **[交易記錄]** 。  
  
1. 或選取 [只複製備份]  來建立只複製備份。 [只複製備份]  是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份，請參閱[只複製備份&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  
  
    > [!NOTE]
    > 選取 **[差異]** 選項時，您無法建立「只複製」備份。  
  
1. 接受 **[名稱]** 文字方塊中建議的預設備份組名稱，或者輸入不同的備份組名稱。  
  
1. (選擇性) 在 [描述]  文字方塊中輸入備份組的描述。  
  
1. 指定備份組會在何時過期：  
  
    - 若要讓備份組在特定的天數後過期，請按一下 [之後]  \(預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 **[伺服器屬性]** 對話方塊 ( **[資料庫設定]** 頁面) 的 **[預設備份媒體保留 (以天為單位)]** 選項中設定。 若要存取此對話方塊，請以滑鼠右鍵按一下 [物件總管] 中的伺服器名稱並選取 [屬性]，然後選取 **[資料庫設定]** 頁面。  
  
    - 若要讓備份組在特定日期過期，請按一下 **[於]** ，然後輸入備份組將過期的日期。  
  
1. 按一下 **[磁碟]** 、 **[URL]** 或 **[磁帶]** ，以選擇備份目的地的類型。 若要選取包含單一媒體集的磁碟或磁帶機 (最多 64 個) 的路徑，請按一下 **[加入]** 。 選取的路徑會在 **[備份至]** 清單方塊中顯示。  
  
     若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視備份目的地的內容，請選取目的地，然後按一下 **[內容]** 。  
  
1. 若要檢視或選取進階選項，請按一下 **[選取頁面]** 窗格中的 **[選項]** 。  
  
1. 按下列項目之一，以選取 **[覆寫媒體]** 選項：  
  
    - **備份至現有的媒體集**  
  
         針對這個選項，按一下 [附加至現有的備份組]  或 [覆寫所有現有的備份組]  ，請參閱[媒體集、媒體家族和備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         - (選擇性) 選取 [檢查媒體集名稱及備份組是否逾期]  ，以讓備份作業確認媒體集及備份組逾期的日期和時間。  
  
         - (選擇性) 在 [媒體集名稱]  文字方塊中輸入名稱。 如果未指定名稱，就會建立一個空白名稱的媒體集。 如果您指定媒體集名稱，就會檢查媒體 (磁帶或磁碟)，以查看實際名稱是否與您在此處輸入的名稱相符。  
  
         如果您讓媒體名稱保持空白，並核取方塊以針對媒體進行檢查，成功也會使媒體上的媒體名稱保持空白。  
  
    - **備份至新的媒體集，並清除所有現有的備份組**  
  
         針對這個選項，在 [新媒體集名稱]  文字方塊中輸入名稱，然後選擇性在 [新媒體集描述]  文字方塊中描述媒體集；請參閱[媒體集、媒體家族和備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
1. (選擇性) 在 **[可靠性]** 區段中選取：  
  
    - **[完成後驗證備份]** 。  
  
    - [寫入媒體之前執行總和檢查碼]  和 (選擇性) [發生總和檢查碼錯誤時繼續]  。
    
       如需總和檢查碼的相關資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
1. 在 **[交易記錄]** 區段中：  
  
    - 對於例行的記錄備份，請保留預設選項 **[移除非使用中的項目以截斷交易記錄]** 。  
  
    - 若要備份記錄的結尾 (亦即，使用中記錄)，請檢查 [備份記錄檔的結尾，並讓資料庫保持在還原狀態]  。  
  
         結尾記錄備份是在發生失敗後進行的，會備份記錄的結尾，以防止遺失工作資料。 在以下兩種情況時應備份使用中的記錄 (結尾記錄備份)：發生失敗後開始還原資料庫之前，或是容錯移轉到次要資料庫時。 選取此選項相當於在 Transact-SQL 的 BACKUP LOG 陳述式中，指定 NORECOVERY 選項。
         
         如需結尾記錄備份的詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
1. 如果是備份至磁帶機 (在 [一般]  頁面的 [目的地]  區段中指定)，[備份後卸載磁帶]  選項會啟用供選擇。 按一下這個選項會啟動 **[卸載之前倒轉磁帶]** 選項。  
  
1. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 和更新的版本支援 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 依預設，備份壓縮與否取決於 **備份壓縮預設** 伺服器組態選項的值。 不過，不論目前的伺服器層級預設值為何，您都可以透過核取 [壓縮備份]  壓縮備份，而且可以透過核取 [不要壓縮備份]  防止壓縮。  
  
     如需檢視現有備份壓縮設定，請參閱[檢視或設定備份壓縮預設伺服器設定選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。
  
     若要加密備份檔案，請核取 **[加密備份]** 核取方塊。 選取要用於加密備份檔案的加密演算法，並提供憑證或非對稱金鑰。 可用於加密的演算法包括：  
  
   - AES 128  
  
   - AES 192  
  
   - AES 256  
  
   - 三重 DES  

## <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
  
執行 BACKUP LOG 陳述式以備份交易記錄，並指定下列項目：  
  
- 所要備份的交易記錄所屬資料庫的名稱。  
  
- 寫入交易記錄備份的備份裝置。  
  
> [!IMPORTANT]
> 這個範例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫，而該資料庫則是使用簡單復原模式。 為了允許記錄備份，在執行完整資料庫備份之前，此資料庫已設定為使用完整復原模式。
>
> 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
 這個範例會在先前所建立的具名備份裝置 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 上建立 `MyAdvWorks_FullRM_log1`資料庫的交易記錄備份。  
  
```sql  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1;  
GO  
```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell

設定並使用 [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)。 使用 **Backup-SqlDatabase** Cmdlet，並指定 **Log** 作為 **-BackupAction** 參數的值。  
  
下列範例會在伺服器執行個體 `<myDatabase>` 的預設備份位置，建立 `Computer\Instance`資料庫的記錄備份。  
  
```powershell
Backup-SqlDatabase -ServerInstance Computer\Instance -Database <myDatabase> -BackupAction Log  
```
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks  
  
- [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
- [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
- [寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>另請參閱

 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
