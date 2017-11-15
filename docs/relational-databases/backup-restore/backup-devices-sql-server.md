---
title: "備份裝置 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
caps.latest.revision: "93"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2decbc706e1bbc8ee6bb1057684ae0e643f129c3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="backup-devices-sql-server"></a>備份裝置 (SQL Server)
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫上進行備份作業期間，備份的資料 (「備份」) 會寫入至實體備份裝置。 當媒體集的第一個備份寫入此實體備份裝置時，此裝置就會初始化。 單一媒體集是由一組一個或多個備份裝置上的備份所組成。  
   
##  <a name="TermsAndDefinitions"></a> 詞彙和定義  
 備份磁碟  
 包含一個或多個備份檔案的硬碟或其他磁碟儲存媒體。 備份檔案是一般作業系統檔案。  
  
 媒體集  
 按順序排列的備份媒體、磁帶或磁碟檔案集合，而且它會使用備份裝置的固定類型和編號。 如需媒體集的詳細資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
 實體備份裝置  
 磁帶機或作業系統所提供的磁碟檔案。 備份可以寫入 1 到 64 部備份裝置。 如果備份需要多部備份裝置，這些裝置都必須對應至單一裝置類型 (磁碟或磁帶)。  
  
 除了磁碟或磁帶之外，SQL Server 備份也可以寫入 Windows Azure Blob 儲存體服務。  
 
  
##  <a name="DiskBackups"></a> 使用磁碟備份裝置  
  
 如果備份作業將備份附加至媒體集時，磁碟檔案填滿，備份作業就會失敗。 由於備份檔案的大小上限是由磁碟裝置上的可用磁碟空間決定，所以備份磁碟裝置的適當大小要根據您的備份大小而定。  
  
 磁碟備份裝置可以是簡單的磁碟裝置，例如 ATA 磁碟機。 或者，您也可以使用可熱抽換的 (Hot-swappable) 磁碟機，以便您將磁碟機上寫滿的磁碟直接了當地更換成空的磁碟。 備份磁碟可以是伺服器上的本機磁碟，也可以是屬於共用網路資源的遠端磁碟。 如需有關如何使用遠端磁碟的詳細資訊，請參閱本主題後面的＜ [備份至網路共用上的檔案](#NetworkShare)＞。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具在處理磁碟備份裝置時相當有彈性，因為它們會自動在磁碟檔案上產生具有時間戳記的名稱。  
  
> **重要！** 我們建議備份磁碟應該與資料庫資料和記錄磁碟使用不同的磁碟。 為了確保您可以在資料或記錄磁碟故障時存取備份，這樣做有其必要。 
>
>如果資料庫檔案和備份檔案位於相同的裝置上，而且該裝置發生錯誤，將無法使用資料庫和備份。 此外，將資料庫和備份檔案放在不同裝置上會將資料庫的生產使用和寫入備份的 I/O 效能最佳化。
  
##  <a name="BackupFileUsingPhysicalName"></a> 使用實體名稱來指定備份檔案 (Transact-SQL)  
 使用實體裝置名稱來指定備份檔案的基本 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 語法為：  
  
 BACKUP DATABASE *database_name*  
  
 TO DISK **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* }  
  
 例如：  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 若要在 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中指定實體磁碟裝置，基本語法為：  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM DISK **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* }  
  
 例如，  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
  
##  <a name="BackupFileDiskPath"></a> 指定磁碟備份檔案路徑 
 指定備份檔案時，您應該輸入完整路徑及檔案名稱。 當您要備份至檔案時，如果僅指定檔案名稱或相對路徑，便會將備份檔案放在預設的備份目錄中。 預設的備份目錄為 C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup，其中 *n* 是伺服器執行個體的編號。 因此，對預設的伺服器執行個體而言，其預設備份目錄為：C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup。  
  
 若要避免模稜兩可的情形 (特別是在指令碼中)，建議您在每個 DISK 子句中明確指定備份目錄的路徑。 不過，當您使用「查詢編輯器」時，這就不是那麼重要。 在這種情況下，如果您確定備份檔案是在預設的備份目錄中，即可省略 DISK 子句中的路徑。 例如，下列 `BACKUP` 陳述式會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫備份到預設備份目錄。  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = ’AdventureWorks2012.bak’;  
GO  
```  
  
> **注意** ：預設位置為儲存在 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer** 下的 **BackupDirectory**登錄機碼。  
  
   
###  <a name="NetworkShare"></a> 備份至網路共用檔案  
 為了讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取遠端磁碟檔案， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須具有網路共用的存取權。 這包括具有讓備份作業寫入網路共用以及讓還原作業從中讀取所需的權限。 網路磁碟機和權限的可用性會根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務執行的內容而定：  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在網域使用者帳戶下執行時，若要備份至網路磁碟機，共用磁碟機就必須對應成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在執行之工作階段中的網路磁碟機。 如果是從命令列啟動 Sqlservr.exe， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便看得到您登入工作階段中已對應的所有網路磁碟機。  
  
-   不過，如果 Sqlservr.exe 是以服務方式執行，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在另一個與登入工作階段無關的工作階段中執行。 服務執行的工作階段可擁有自己的對應磁碟機 (只是它通常沒有)。  
  
-   您可以使用電腦帳戶代替網域使用者來與網路服務帳戶連接。 若要允許從特定電腦備份至共用磁碟機，請將存取權授與電腦帳戶。 只要正在寫入備份的 Sqlservr.exe 處理序具有存取權，傳送 BACKUP 命令的使用者是否具有存取權便無關了。  
  
    > **重要！** 透過網路備份資料可能會受到網路問題的影響。因此，我們建議您在使用遠端磁碟時，於備份作業完成後進行驗證。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
## <a name="specify-a-universal-naming-convention-unc-name"></a>指定通用命名慣例 (UNC) 名稱  
 若要在備份或還原命令中指定網路共用，請使用備份裝置檔案的完整通用命名慣例 (UNC) 名稱。 UNC 名稱的格式為 **\\\\**<系統名稱>**\\**<共用名稱>**\\**<路徑>**\\**<檔案名稱>。  
  
 例如：  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
 
##  <a name="TapeDevices"></a> 使用磁帶裝置  
  
> **注意** ：未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中將會移除磁帶備份裝置的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
   
 磁帶機必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 作業系統所支援的，才能將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 資料備份到磁帶中。 此外，對指定的磁帶機而言，我們建議您僅使用磁帶機製造商所建議的磁帶。 如需有關如何安裝磁帶機的詳細資訊，請參閱 Windows 作業系統的文件。  
  
 使用磁帶機時，備份作業可能會填滿一捲磁帶，然後繼續寫入另一捲磁帶。 每個磁帶都含有媒體標頭。 第一個使用的媒體稱為 *「初始磁帶」*。 後續的磁帶都稱為 *接續磁帶* ，每捲磁帶都有一個媒體序號，後面的磁帶編號比前面的高。 例如，與四個磁帶裝置相關聯的媒體集，內含至少四捲初始磁帶；而如果一捲磁帶裝不下整個資料庫，則還會有四捲接續磁帶。 附加備份組的時候，您必須掛載整組媒體中的最後一捲磁帶。 若未掛載最後一捲磁帶， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 往前掃描到掛載磁帶的結尾時，便會要求您更換磁帶。 此時，請掛載最後一捲磁帶。  
  
 使用磁帶備份裝置就像使用磁碟裝置一樣，但有以下例外情況：  
  
-   磁帶裝置必須在實體上連接至執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦。 不支援備份至遠端磁帶裝置。  
  
-   如果在備份作業進行時磁帶備份裝置填滿，但還必須寫入更多資料的話， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提示換新磁帶，並於載入新磁帶後繼續進行備份作業。  
  
##  <a name="BackupTapeUsingPhysicalName"></a> 使用實體名稱來指定備份磁帶 (Transact-SQL)  
 使用磁帶機之實體裝置名稱來指定備份磁帶的基本 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 語法為：  
  
 BACKUP { DATABASE | LOG } *database_name*  
  
 TO TAPE **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* }  
  
 例如：  
  
```  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 若要在 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中指定實體磁帶裝置，基本語法為：  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM TAPE **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* }  
  
###  <a name="TapeOptions"></a> 磁帶專用的 BACKUP 和 RESTORE 選項 (Transact-SQL)  
 為了方便磁帶管理作業，BACKUP 陳述式提供了下列磁帶專用的選項：  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     您可以控制在備份或還原作業之後，備份磁帶是否會自動從磁帶機卸載。 UNLOAD/NOUNLOAD 是工作階段設定，在工作階段的存留期間會一直保持不變，直到指定其他設定來進行重設為止。  
  
-   { **REWIND** | NOREWIND }  
  
     您可以控制在備份或還原作業之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將磁帶保持在開啟狀態，還是會在磁帶填滿之後，釋出並倒轉磁帶。 預設行為是倒轉磁帶 (REWIND)。  
  
> **注意**：如需 BACKUP 語法和引數的詳細資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。 如需 RESTORE 語法和引數的詳細資訊，請分別參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 和 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
###  <a name="OpenTapes"></a> 管理開啟的磁帶  
 若要檢視開啟的磁帶裝置清單以及掛載要求的狀態，請查詢 [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 動態管理檢視。 這個檢視顯示所有開啟的磁帶。 這包括正在等待下一個 BACKUP 或 RESTORE 作業而暫時閒置的使用中磁帶。  
  
 如果磁帶不慎保持在開啟狀態，釋放磁帶最快速的方式為使用下列命令：RESTORE REWINDONLY FROM TAPE **=***backup_device_name*。 如需詳細資訊，請參閱 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)。  
  
  
## <a name="using-the-windows-azure-blob-storage-service"></a>使用 Windows Azure Blob 儲存體服務  
 SQL Server 備份可以寫入 Windows Azure Blob 儲存體服務。  如需如何針對備份使用 Windows Azure Blob 儲存體服務的詳細資訊，請參閱 [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
##  <a name="LogicalBackupDevice"></a> 使用邏輯備份裝置  
 *「邏輯備份裝置」* (Logical backup device) 是選擇性的使用者自訂名稱，而且它會指向特定的實體備份裝置 (磁碟檔案或磁帶機)。 邏輯備份裝置可讓您在參考對應的實體備份裝置時，使用間接取值。  
  
 定義邏輯備份裝置會需要將邏輯名稱指派給實體裝置。 例如，您可以將邏輯裝置 AdventureWorksBackups 定義為指向 Z:\SQLServerBackups\AdventureWorks2012.bak 檔案或 \\\\.\tape0 磁帶機。 備份和還原命令便可以將 AdventureWorksBackups 指定為備份裝置，而不需設定 DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' 或 TAPE = '\\\\.\tape0'。  
  
 邏輯裝置名稱在伺服器執行個體上所有邏輯備份裝置中都必須是唯一的。 若要檢視現有的邏輯裝置名稱，請查詢 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) 目錄檢視。 這個檢視會顯示每個邏輯備份裝置的名稱，並且描述對應實體備份裝置的類型及實體檔案名稱或路徑。  
  
 定義邏輯備份裝置之後，您就可以在 BACKUP 或 RESTORE 命令中指定邏輯備份裝置來替代裝置的實體名稱。 例如，下列陳述式會將 `AdventureWorks2012` 資料庫備份到 `AdventureWorksBackups` 邏輯備份裝置。  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> **注意** ：在指定的 BACKUP 或 RESTORE 陳述式中，邏輯備份裝置名稱和對應的實體備份裝置名稱是可互換的。  
  
 使用邏輯備份裝置的其中一項優點是，它比冗長的路徑名稱更容易使用。 如果您打算將一系列備份寫入相同的路徑名稱或磁帶裝置，使用邏輯備份裝置會很有用。 邏輯備份裝置對於識別磁帶備份裝置特別有用。  
  
 您可以撰寫備份指令碼來使用特定的邏輯備份裝置。 這樣您就可以不更新指令碼而切換到新的實體備份裝置。 切換時會涉及下列程序：  
  
1.  卸除原始邏輯備份裝置。  
  
2.  定義使用原始邏輯裝置名稱，但對應至不同實體備份裝置的新邏輯備份裝置。 邏輯備份裝置對於識別磁帶備份裝置特別有用。  
  
  
##  <a name="MirroredMediaSets"></a> 鏡像備份媒體集  
 備份媒體集的鏡像功能可減少備份裝置功能異常時的影響。 這些功能異常會特別嚴重，因為備份是避免資料遺失的最後一道防線。 隨著資料庫大小的成長，備份裝置或媒體故障而導致備份無法還原的可能性也越大。 鏡像備份媒體可透過提供實體備份裝置的備援性，藉以提升備份的可靠性。 如需詳細資訊，請參閱 [鏡像備份媒體集 &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)。  
  
> **注意** ：只有 [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] 和更新版本才支援鏡像備份媒體集。  
  
  
##  <a name="Archiving"></a> 封存 SQL Server 備份  
 建議您使用檔案系統備份公用程式來封存磁碟備份，並將封存保存在異地。 使用磁碟的優點是，您可以使用網路將封存的備份寫入異地磁碟。 Windows Azure Blob 儲存體服務可做為異地封存選項。  您可以上傳磁碟備份，或是直接將備份寫入 Windows Azure Blob 儲存體服務中。  
  
 另一種常見的封存方法是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份寫入本機備份磁碟、將備份封存至磁帶，然後將磁帶存放在異地。  

  
##  <a name="RelatedTasks"></a> 相關工作  
 **指定磁碟裝置 (SQL Server Management Studio)**  
  
-   [指定磁碟或磁帶作為備份目的地 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **指定磁帶裝置 (SQL Server Management Studio)**  
  
-   [指定磁碟或磁帶作為備份目的地 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **定義邏輯備份裝置**  
  
-   [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
-   [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **使用邏輯備份裝置**  
  
-   [指定磁碟或磁帶作為備份目的地 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [從裝置還原備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **檢視有關備份裝置的資訊**  
  
-   [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **若要刪除邏輯備份裝置**  
  
-   [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)  
  
-   [刪除備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 Backup Device 物件](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)   
 [鏡像備份媒體集 &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
