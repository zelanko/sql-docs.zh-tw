---
title: 備份檔案與檔案群組 | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cf87d09eed5b955c1773c46270f25cb0a2d57eaa
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71708689"
---
# <a name="back-up-files-and-filegroups"></a>備份檔案與檔案群組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中備份檔案與檔案群組。 當完整的資料庫備份因資料庫大小和效能需求而變得不可行時，您可以建立檔案備份來代替。 *「檔案備份」* (File Backup) 包含一或多個檔案 (或檔案群組) 中的所有資料。
  
如需詳細資訊，請參閱 [完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 和 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
- 在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。  
  
- 在簡單復原模式下，必須將所有的讀取/寫入檔案備份在一起。 這有助於確保資料庫還原到一致的時間點。 不要個別指定每一個讀取/寫入檔案或檔案群組，請改用 READ_WRITE_FILEGROUPS 選項。 這個選項會備份資料庫中的所有讀取/寫入檔案群組。 藉由指定 READ_WRITE_FILEGROUPS 所建立的備份即稱為「部分備份」  ，請參閱[部分備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)。  
  
如需基本備份概念的詳細資訊，請參閱 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議
  
根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  

###  <a name="permissions"></a><a name="Permissions"></a> 權限

`BACKUP DATABASE` 和 `BACKUP LOG` 權限預設為 **系統管理員**固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。

## <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio   
  
1. 連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
1. 展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
1. 以滑鼠右鍵按一下資料庫，指向 **[工作]** ，然後按一下 **[備份]** 。 會出現 **[備份資料庫]** 對話方塊。  
  
1. 在 **[資料庫]** 清單中，確認資料庫名稱。 您可以選擇性從清單中選取不同的資料庫。  
  
1. 在 **[備份類型]** 清單中，選取 **[完整]** 或 **[差異]** 。  
  
1. 若是 **[備份元件]** 選項，請按一下 **[檔案與檔案群組]** 。  
  
1. 在 **[選取檔案與檔案群組]** 對話方塊中，選取您要備份的檔案及檔案群組。 您可以選取一或多個個別檔案，或選取檔案群組的方塊，以便自動選取該檔案群組中的所有檔案。  
  
1. 接受 **[名稱]** 文字方塊中建議的預設備份組名稱，或者輸入不同的備份組名稱。  
  
1. (選擇性) 在 [描述]  文字方塊中輸入備份組的描述。  
  
1. 指定備份組會在何時過期：  
  
    - 若要讓備份組在特定的天數後過期，請按一下 [之後]  (預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 **[伺服器屬性]** 對話方塊 ( **[資料庫設定]** 頁面) 的 **[預設備份媒體保留 (以天為單位)]** 選項中設定。 若要存取此選項，請以滑鼠右鍵按一下物件總管中的伺服器名稱，然後選取 [資料庫設定]  頁面。  
  
    - 若要讓備份組在特定日期過期，請按一下 **[於]** ，然後輸入備份組將過期的日期。  
  
1. 按一下 **[磁碟]** 或 **[磁帶]** ，以選擇備份目的地的類型。 若要選取包含單一媒體集的磁碟或磁帶機 (最多 64 個) 的路徑，請按一下 **[加入]** 。 選取的路徑會在 **[備份至]** 清單中顯示。  
  
    > [!NOTE]
    > 若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視備份目的地的內容，請選取目的地，然後按一下 **[內容]** 。  
  
1. 若要檢視或選取進階選項，請按一下 **[選取頁面]** 窗格中的 **[選項]** 。  
  
1. 按下列項目之一，以選取 **[覆寫媒體]** 選項：  
  
    - **備份至現有的媒體集**  
  
         針對這個選項，按一下 **[附加至現有的備份組]** 或 **[覆寫所有現有的備份組]** 。 
         
         如需備份至現有媒體集的相關資訊，請參閱[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         - (選擇性) 選取 [檢查媒體集名稱及備份組是否逾期]  ，以讓備份作業確認媒體集及備份組逾期的日期和時間。  
  
         - (選擇性) 在 [媒體集名稱]  文字方塊中輸入名稱。 如果未指定名稱，就會建立一個空白名稱的媒體集。 如果您指定媒體集名稱，就會檢查媒體 (磁帶或磁碟)，以查看實際名稱是否與您在此處輸入的名稱相符。  
  
         如果您讓媒體名稱保持空白，並核取方塊以針對媒體進行檢查，成功也會使媒體上的媒體名稱保持空白。  
  
    - **備份至新的媒體集，並清除所有現有的備份組**  
  
         針對這個選項，在 **[新媒體集名稱]** 文字方塊中輸入名稱，然後選擇性在 **[新媒體集描述]** 文字方塊中描述媒體集。
         
         如需建立新媒體集的詳細資訊，請參閱[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
1. (選擇性) 在 [可靠性]  區段中，核取：  
  
    - **[完成後驗證備份]** 。  
  
    - [寫入媒體之前執行總和檢查碼]  和 (選擇性) [發生總和檢查碼錯誤時繼續]  。
    
         如需總和檢查碼的詳細資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
1. 如果是備份至磁帶機 (在 [一般]  頁面的 [目的地]  區段中指定)，[備份後卸載磁帶]  選項會啟用供選擇。 按一下這個選項會啟用 **[卸載之前倒轉磁帶]** 選項。  
  
    > [!NOTE]
    > 除非您備份的是交易記錄檔 (依 [一般]  頁面的 [備份類型]  區段中的指定)，否則 [交易記錄檔]  區段中的選項為非使用中。  
  
1. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 及更新版本支援 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 依預設，備份壓縮與否取決於 **備份壓縮預設** 伺服器組態選項的值。 不過，不論目前的伺服器層級預設值為何，您都可以透過核取 [壓縮備份]  壓縮備份，而且可以透過核取 [不要壓縮備份]  防止壓縮。  
  
     如需檢視現有備份壓縮預設值，請參閱[檢視或設定備份壓縮預設伺服器設定選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  

## <a name="using-transact-sql"></a>使用 TRANSACT-SQL
  
若要建立檔案或檔案群組備份，請使用 [BACKUP DATABASE <file_or_filegroup>](../../t-sql/statements/backup-transact-sql.md) 陳述式。 這個陳述式至少必須指定下列各項：  
  
  - 資料庫名稱。  
  
  - 分別為每個檔案或檔案群組指定 FILE 或 FILEGROUP 子句。  
  
  - 完整備份所要寫入的備份裝置。  
  
檔案備份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法為：  
  
  BACKUP DATABASE *database*  
  
  { FILE _=_ *logical_file_name* | FILEGROUP _=_ *logical_filegroup_name* } [ **,** ...*f* ]  
  
  TO *backup_device* [ **,** ...*n* ]  
  
  [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
|選項|描述|  
|------------|-----------------|  
|*database*|這是要備份交易記錄、部分資料庫或完整資料庫的來源資料庫。|  
|FILE _=_ *logical_file_name*|指定要包含在檔案備份中檔案的邏輯名稱。|  
|FILEGROUP _=_ *logical_filegroup_name*|指定要包含在檔案備份中的檔案群組的邏輯名稱。 在簡單復原模式之下，只允許唯讀檔案群組使用檔案群組備份。|  
|[ **,** ...*f* ]|這是一個預留位置，表示可以指定多個檔案和檔案群組。 檔案或檔案群組的數目沒有限制。|  
|*backup_device* [ **,** ...*n* ]|指定一份清單，列出備份作業可使用的 1 到 64 個備份裝置。 您可以指定實體備份裝置，或者指定對應的邏輯備份裝置 (若已經定義)。 若要指定實體備份裝置，請使用 DISK 或 TAPE 選項：<br /><br /> { DISK &#124; TAPE } _=_ *physical_backup_device_name*<br /><br /> 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|  
|WITH *with_options* [ **,** ...*o* ]|另外，也可以指定一個或多個其他選項，如 DIFFERENTIAL。 差異檔案備份需要以完整檔案備份作為基底。 <br /><br />如需詳細資訊，請參閱[建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)。|  
  
在完整復原模式下，您還必須備份交易記錄。 若要使用一組完整的完整檔案備份來還原資料庫，您還必須有足夠的記錄備份，才能從第一個檔案備份開始涵蓋所有的檔案備份。

如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  
  
###  <a name="examples"></a><a name="TsqlExample"></a> 範例
下列範例會備份 `Sales` 資料庫次要檔案群組的一或多個檔案。 這個資料庫使用完整復原模式，而且包含下列次要檔案群組：  
  
- 名為 `SalesGroup1` 的檔案群組，其中含有檔案 `SGrp1Fi1` 和 `SGrp1Fi2`。  
  
- 名為 `SalesGroup2` 的檔案群組，其中含有檔案 `SGrp2Fi1` 和 `SGrp2Fi2`。  
  
#### <a name="a-create-a-file-backup-of-two-files"></a>A. 建立兩個檔案的檔案備份  
下列範例會建立只有 `SGrp1Fi2` 檔案群組之 `SalesGroup1` 檔案及 `SGrp2Fi2` 檔案群組之 `SalesGroup2` 檔案的差異檔案備份。  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-create-a-full-file-backup-of-the-secondary-filegroups"></a>B. 建立次要檔案群組的完整檔案備份  
下列範例會為兩個次要檔案群組中的每個檔案建立完整檔案備份。  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-create-a-differential-file-backup-of-the-secondary-filegroups"></a>C. 建立次要檔案群組的差異檔案備份  
下列範例會為兩個次要檔案群組中的每個檔案建立差異檔案備份。  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
## <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell

設定並使用 [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)。
  
使用 **Backup-SqlDatabase** Cmdlet，並指定 **-BackupAction** 參數值的 **Files** 。 另外再指定下列其中一個參數：  
  
- 若要備份特定檔案，請指定 _-DatabaseFile_*String* 參數，其中 *String* 是要備份的一個或多個資料庫檔案。  
  
- 若要備份指定檔案群組中的所有檔案，請指定 _-DatabaseFileGroup_*String* 參數，其中 *String* 是要備份的一個或多個資料庫檔案群組。  
  
以下範例會為 `<myDatabase>` 資料庫內的次要檔案群組 'FileGroup1' 和 'FileGroup2' 建立其中每個檔案的完整檔案備份。 備份是建立在伺服器執行個體 `Computer\Instance`的預設備份位置。  

```powershell
Backup-SqlDatabase -ServerInstance Computer\Instance -Database <myDatabase> -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2" 
```
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [備份資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [備份資料庫 &#40;備份選項頁面&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
