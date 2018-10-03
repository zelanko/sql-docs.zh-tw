---
title: 建立完整資料庫備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e1daefbc5625aaf034a9be9218a59daf5286cc1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094020"
---
# <a name="create-a-full-database-backup-sql-server"></a>建立完整資料庫備份 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立完整資料庫備份。  
  
> [!NOTE]  
>  如需有關 SQL Server 備份至 Windows Azure Blob 儲存服務的詳細資訊，請參閱＜ [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要建立完整資料庫備份，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。  
  
-   在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，無法還原較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本所建立的備份。  
  
-   如需詳細資訊，請參閱 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)。  
  
###  <a name="Recommendations"></a> 建議  
  
-   資料庫的大小增加時，完整資料庫備份就需要更多的時間才能完成，同時也需要更多的儲存空間。 因此，若為大型資料庫，您可能會想透過一系列的 *「差異資料庫備份」*(Differential database backups) 補充完整資料庫備份。 如需詳細資訊，請參閱 [差異備份 &#40;SQL Server&#41;](differential-backups-sql-server.md)。  
  
-   您可以使用 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 系統預存程序來估計完整資料庫備份的大小。  
  
-   根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)。  
  
###  <a name="Security"></a> 安全性  
 資料庫備份上的 TRUSTWORTHY 是設為 OFF。 如需如何將 TRUSTWORTHY 設成 ON 的資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 開頭[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]`PASSWORD`和`MEDIAPASSWORD`選項已遭到停用建立備份。 您仍然可以還原以密碼建立的備份。  
  
####  <a name="Permissions"></a> 權限  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您按一下 [指令碼] 按鈕，再選取指令碼目的地，即可產生對應的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 指令碼。  
  
#### <a name="to-back-up-a-database"></a>備份資料庫  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]**，根據資料庫選取使用者資料庫或展開 **[系統資料庫]** ，然後選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]，然後按一下 [備份]。 會出現 **[備份資料庫]** 對話方塊。  
  
4.  在 `Database`清單方塊中，確認資料庫名稱。 您可以選擇性從清單中選取不同的資料庫。  
  
5.  您可以針對任何復原模式 (**完整**、**大量記錄**或**簡單**) 執行資料庫備份。  
  
6.  請在 **[備份類型]** 清單方塊中，選取 **[完整]**。  
  
     請注意，您可在建立完整資料庫備份之後，建立差異資料庫備份。如需詳細資訊，請參閱[建立差異資料庫備份 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)。  
  
7.  或者，您也可以選取 [只複製備份] 來建立只複製備份。 「只複製備份」是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](copy-only-backups-sql-server.md)。  
  
    > [!NOTE]  
    >  選取 **[差異]** 選項時，您無法建立「只複製」備份。  
  
8.  針對**備份元件**，按一下  `Database`。  
  
9. 接受 **[名稱]** 文字方塊中建議的預設備份組名稱，或者輸入不同的備份組名稱。  
  
10. (選擇性) 在 **[描述]** 文字方塊中輸入備份組的描述。  
  
11. 按一下 **[磁碟]**、 **[磁帶]** 或 **[URL]** 來選擇備份目的地的類型。 若要選取包含單一媒體集的磁碟或磁帶機 (最多 64 個) 的路徑，請按一下 **[加入]**。 選取的路徑會在 **[備份至]** 清單方塊中顯示。  
  
     若要移除備份目的地，請選取目的地，然後按一下 **[移除]**。 若要檢視備份目的地的內容，請選取目的地，然後按一下 **[內容]**。  
  
12. 若要檢視或選取媒體選項，請按一下 **[選取頁面]** 窗格中的 **[媒體選項]** 。  
  
13. 按下列項目之一，以選取 **[覆寫媒體]** 選項：  
  
    -   **備份至現有的媒體集**  
  
         針對這個選項，按一下 **[附加至現有的備份組]** 或 **[覆寫所有現有的備份組]**。 如需詳細資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         另外，也可以選取 **[檢查媒體集名稱及備份組是否逾期]** ，以讓備份作業確認媒體集及備份組逾期的日期和時間。  
  
         另外，也可以在 **[媒體集名稱]** 文字方塊中輸入名稱。 如果未指定名稱，就會建立一個空白名稱的媒體集。 如果您指定媒體集名稱，就會檢查媒體 (磁帶或磁碟)，以查看實際名稱是否與您在此處輸入的名稱相符。  
  
        > [!IMPORTANT]  
        >  如果在 **[一般]** 頁面中選取 **[URL]** 做為備份目的地，則會停用這個選項。 如需詳細資訊，請參閱[備份資料庫 &#40;媒體選項頁面&#41;](back-up-database-media-options-page.md)  
        >   
        >  如果您打算使用加密，請不要選取這個選項。 如果您選取這個選項， **[備份選項]** 頁面中的加密選項將會停用。 當附加至現有的備份組時，不支援加密。  
  
    -   **備份至新的媒體集，並清除所有現有的備份組**  
  
         針對這個選項，在 **[新媒體集名稱]** 文字方塊中輸入名稱，然後選擇性在 **[新媒體集描述]** 文字方塊中描述媒體集。  
  
        > [!IMPORTANT]  
        >  如果在 **[一般]** 頁面中選取 **[URL]** ，則會停用這個選項。 當備份至 Windows Azure 儲存體時，不支援這些動作。  
  
14. 在 **[可靠性]** 區段中，選擇性核取：  
  
    -   **[完成後驗證備份]**。  
  
    -   **[寫入媒體之前執行總和檢查碼]** 及/或 **[發生總和檢查碼錯誤時繼續]**。 如需總和檢查碼的資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
15. 如果您要備份至磁帶機 (如同 [一般] 頁面的 [目的地] 區段中所指定)，即可使用 [備份後卸載磁帶] 選項。 按一下這個選項會啟動 **[卸載之前倒轉磁帶]** 選項。  
  
    > [!NOTE]  
    >  除非您要備份交易記錄 (如同 [一般] 頁面的 [備份類型] 區段中所指定)，否則 [交易記錄] 區段中的選項無法使用。  
  
16. 若要檢視或選取備份選項，請按一下 **[選取頁面]** 窗格中的 **[備份選項]** 。  
  
17. 指定備份組逾期的時間，和不需明確略過逾期資料的驗證即可覆寫的時間：  
  
    -   若要讓備份組在特定的天數後過期，請按一下 [之後] \(預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 [伺服器屬性] 對話方塊 ([資料庫設定] 頁面) 的 [預設備份媒體保留 (以天為單位)] 選項中設定。 若要存取，請以滑鼠右鍵按一下物件總管中的伺服器名稱並選取 [屬性]，然後選取 [資料庫設定] 頁面。  
  
    -   若要讓備份組在特定日期過期，請按一下 **[於]**，然後輸入備份組將過期的日期。  
  
         如需備份到期日的詳細資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 和更新的版本支援 [備份壓縮](backup-compression-sql-server.md)。 依預設，備份壓縮與否取決於 **備份壓縮預設** 伺服器組態選項的值。 不過，不論目前的伺服器層級預設值為何，您都可以透過核取 [壓縮備份] 壓縮備份，而且可以透過核取 [不要壓縮備份] 防止壓縮。  
  
     **若要檢視或變更目前的 backup compression default**  
  
    -   [檢視或設定 backup compression default 伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. 指定是否要對備份使用加密。 選取要加密步驟所要使用的加密演算法，並提供現有憑證或非對稱金鑰清單中的憑證或非對稱金鑰。 SQL Server 2014 或更新版本支援加密。 如需加密選項的詳細資訊，請參閱[備份資料庫 &#40;備份選項頁面&#41;](back-up-database-backup-options-page.md)。  
  
> [!NOTE]  
>  或者，您可以使用「維護計畫精靈」來建立資料庫備份。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-full-database-backup"></a>建立完整資料庫備份  
  
1.  執行 BACKUP DATABASE 陳述式以建立完整資料庫備份，請指定：  
  
    -   欲備份的資料庫名稱。  
  
    -   寫入完整資料庫備份的備份裝置。  
  
     完整資料庫備份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法如下：  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *with_options* [ **,**...*o* ] ] ;  
  
    |選項|[描述]|  
    |------------|-----------------|  
    |*database*|為要備份的資料庫。|  
    |*backup_device* [ **,**...*n* ]|指定一份清單，列出備份作業可使用的 1 到 64 個備份裝置。 您可以指定實體備份裝置，或者指定對應的邏輯備份裝置 (若已經定義)。 若要指定實體備份裝置，請使用 DISK 或 TAPE 選項：<br /><br /> { DISK &#124; TAPE } **=***physical_backup_device_name*<br /><br /> 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|  
    |WITH *with_options* [ **,**...*o* ]|或者，也可以指定一個或多個其他選項 *o*。 如需有關選項基本概念的詳細資訊，請參閱步驟 2。|  
  
2.  選擇性地指定一或多個 WITH 選項。 這裡描述的是一些基本的 WITH 選項。 如需所有 WITH 選項的資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
    -   基本備份組 WITH 選項：  
  
         { COMPRESSION | NO_COMPRESSION }  
         只有在 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 及更新的版本中，才會指定是否要在此備份上執行 [備份壓縮](backup-compression-sql-server.md) ，以覆寫伺服器層級的預設值。  
  
         ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  
         只有在 SQL Server 2014 或更新的版本中，才能指定要使用的加密演算法以及憑證或非對稱金鑰來維護加密的安全。  
  
         描述**=** { **'*`text`*'** | **@ * * * text_variable* }  
         指定描述備份組的自由形式文字。 這個字串最多可有 255 個字元。  
  
         NAME **=** { *backup_set_name* | **@***backup_set_name_var* }  
         指定備份組的名稱。 名稱最多可有 128 個字元。 如果未指定 NAME，它就是空白。  
  
    -   基本備份組 WITH 選項：  
  
         根據預設，BACKUP 會將備份附加到現有的媒體集，以保留現有的備份組。 若要明確指定這項，請使用 NOINIT 選項。 如需附加至現有備份組的資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
         另外，若要格式化備份媒體，請使用 FORMAT 選項：  
  
         FORMAT [ **,** MEDIANAME**=** { *media_name* | **@***media_name_variable* } ] [ **,** MEDIADESCRIPTION **=** { *text* | **@***text_variable* } ]  
         當您第一次使用媒體或是想要覆寫所有現有的資料時，請使用 FORMAT 子句。 選擇性地為新的媒體指派媒體名稱和描述。  
  
        > [!IMPORTANT]  
        >  當您使用 BACKUP 陳述式的 FORMAT 子句時要非常小心，因為它會破壞備份媒體先前所儲存的任何備份。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. 備份到磁碟裝置  
 下列範例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 建立新的媒體集，以將整個 `FORMAT` 資料庫備份至磁碟。  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>B. 備份到磁帶裝置  
 下列範例會將完整的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫備份到磁帶上，並將備份附加到先前的備份中。  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. 備份到邏輯磁帶裝置  
 下列範例會為磁帶機建立邏輯備份裝置。 這個範例會將完整的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫備份至該裝置。  
  
```tsql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
1.  使用`Backup-SqlDatabase`cmdlet。 若要明確指出這是完整資料庫備份，指定 **-BackupAction**參數的預設值， `Database`。 此參數在完整資料庫備份下是選擇性的。  
  
     下列範例會在伺服器執行個體 `MyDB` 的預設備份位置，建立 `Computer\Instance`資料庫的完整資料庫備份。 這個範例指定了選擇性的 `-BackupAction Database`。  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [備份資料庫 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [還原資料庫備份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [在簡單復原模式下還原資料庫備份 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [將資料庫還原到新位置 &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [使用維護計畫精靈](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [備份資料庫 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [備份資料庫 &#40;備份選項頁面&#41;](back-up-database-backup-options-page.md)   
 [差異備份 &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [完整資料庫備份 &#40;SQL Server&#41;](full-database-backups-sql-server.md)  
  
  
