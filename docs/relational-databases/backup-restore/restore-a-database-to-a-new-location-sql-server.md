---
title: 將資料庫還原到新位置 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4e3c7cfdc24c55dde67e8abe5473b934fc6ac5f4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "72989556"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>將資料庫還原到新位置 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 SQL Server Management Studio (SSMS) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中將 [!INCLUDE[tsql](../../includes/tsql-md.md)]資料庫還原至新位置，並選擇性地重新命名資料庫。 您可以將資料庫移至新目錄路徑，或是在相同的伺服器執行個體或不同的伺服器執行個體上建立資料庫的複本。  
    
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前！  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   負責還原完整資料庫備份的系統管理員，必須是目前唯一正在使用即將還原之資料庫的人員。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   在完整或大量記錄復原模式下，您必須先備份使用中交易記錄，才能還原資料庫。 如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  

-   若要還原加密資料庫， **您必須能夠存取用來加密資料庫的憑證或非對稱金鑰！** 如果沒有憑證或非對稱金鑰，您就無法還原資料庫。 只要您需要備份，就必須保留用來加密資料庫加密金鑰的憑證！ 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   如需移動資料庫的其他考量，請參閱 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)。  
  
-   如果您將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本的資料庫還原成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，資料庫會自動升級。 通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據  **upgrade_option** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為匯入 (**upgrade_option** = 2) 或重建 (**upgrade_option** = 0)，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 若要變更 **upgrade_option** 伺服器屬性的設定，請使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 基於安全性的理由，建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，則 RESTORE 權限預設為 **系統管理員** 和 **dbcreator** 固定伺服器角色的成員，以及資料庫的擁有者 (**dbo**)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
  
## <a name="restore-a-database-to-a-new-location-optionally-rename-the-database-using-ssms"></a>將資料庫還原至新位置，並選擇性地使用 SSMS 重新命名資料庫 

  
1.  連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體，然後在 [物件總管] 中，按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後按一下 [還原資料庫]。 **[還原資料庫]** 對話方塊隨即開啟。  
  
3.  在 **[一般]** 頁面上，使用 **[來源]** 區段指定要還原之備份組的來源和位置。 選取下列其中一個選項：  
  
    -   **Database**  
  
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    > **注意：** 如果備份是根據不同的伺服器所建立，目的地伺服器就沒有所指定資料庫的備份記錄資訊。 在此情況下，請選取 **[裝置]** ，以便手動指定要還原的檔案或裝置。  
  
    1.  **裝置**  
  
         按一下瀏覽 (**...**) 按鈕，開啟 [選取備份裝置] 對話方塊。 在 **[備份媒體類型]** 方塊中，選取列出的其中一種裝置類型。 若要選取 **[備份媒體]** 方塊中的一個或多個裝置，請按一下 **[加入]**。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
         在 **[來源: 裝置: 資料庫]** 清單方塊中，選取應該還原的資料庫名稱。  
  
         **注意** ：這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。  
  
4.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。  
  
5.  在 **[還原至]** 方塊中，保留 **[到上次建立的備份]** 預設值，或按一下 **[時間表]** 存取 **[備份時間表]** 對話方塊，手動選取停止復原動作的時間點。 如需有關指定特定時間點的詳細資訊，請參閱＜ [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md) ＞。  
  
6.  在 **[要還原的備份組]** 方格中，選取要還原的備份。 這個方格會顯示指定位置可用的備份。 依預設，會建議一個復原計畫。 若要覆寫建議的復原計畫，您可以變更方格中的選取項目。 取消選取先前的備份時，會自動取消選取相依於先前備份還原的備份。  
  
     如需 [要還原的備份組] 方格中各資料行的相關資訊，請參閱[還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)。  
  
7.  若要指定資料庫檔案的新位置，請選取 **[檔案]** 頁面，然後按一下 **[將所有檔案重新放置到資料夾]**。 提供 **[資料檔資料夾]** 及 **[記錄檔資料夾]** 的新位置。 如需這個方格的詳細資訊，請參閱[還原資料庫 &#40;檔案頁面&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)。  
  
8.  在 **[選項]** 頁面上，依需要調整選項。 如需這些選項的詳細資訊，請參閱[還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)。  

 ## <a name="restore-database-to-a-new-location-optionally-rename-the-database-using-t-sql"></a>將資料庫還原至新位置，並選擇性地使用 T-SQL 重新命名資料庫
 
 
1.  (選擇性) 在包含您想要還原之完整資料庫備份的備份組中，決定檔案的邏輯和實體名稱。 這個陳述式會傳回備份組內所自主資料庫和記錄檔清單。 基本語法如下：  
  
     RESTORE FILELISTONLY FROM <備份裝置> WITH FILE = *backup_set_file_number* 
  
     此處，*backup_set_file_number* 表示媒體集中的備份位置。 您可以使用 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 陳述式來取得備份組的位置。 如需詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md) 中的＜指定備份組＞。  
  
     這個陳述式也支援一些 WITH 選項。 如需詳細資訊，請參閱 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。  
  
2.  使用 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式來還原完整資料庫備份。 根據預設，資料和記錄檔會還原到其原始位置。 若要重新放置資料庫，請使用 MOVE 選項來重新放置每個資料庫檔案，避免與現有的檔案發生衝突。  

  將資料庫還原至新位置和新名稱的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法為：  
  ```sql
  RESTORE DATABASE *new_database_name*  
  
  FROM *backup_device* [ ,...*n* ]  
  
  [ WITH  
 
   {  
  
      [ **RECOVERY** | NORECOVERY ]  
  
      [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
      [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
  }  
  
  ;  
  ```
  > [!NOTE] 
  > 準備要在不同的磁碟上重新放置資料庫時，您應該確認有足夠的可用空間，並且識別與現有檔案發生衝突的任何可能性。 這項作業包括使用 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md) 陳述式，其中指定您打算在 RESTORE DATABASE 陳述式中使用的相同 MOVE 參數。  
  
  下表針對將資料庫還原到新位置的作業，描述這個 RESTORE 陳述式的引數。 如需這些引數的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  
  
  *new_database_name*  
  資料庫的新名稱。  
  
  > [!NOTE]
  > 如果您要將資料庫還原至不同的伺服器執行個體，可以使用原始資料庫名稱而非新名稱。  
  
  *backup_device* [ **,**...*n* ]  
  指定一份逗號分隔清單，其中列出要從中還原資料庫備份的 1 到 64 個備份裝置。 您可以指定實體備份裝置，也可以指定對應的邏輯備份裝置 (如果已定義的話)。 若要指定實體備份裝置，請使用 DISK 或 TAPE 選項：  
  
  { DISK | TAPE } **=**_physical_backup_device_name_  
  
  如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。  
  
  { **RECOVERY** | NORECOVERY }  
  如果資料庫使用完整復原模式，您可能必須在還原資料庫之後套用交易記錄備份。 在此情況下，請指定 NORECOVERY 選項。  
  
  否則，請使用 RECOVERY 選項 (預設值)。  
  
  FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
  識別要還原的備份組。 例如， *backup_set_file_number* 為 **1** ，表示備份媒體的第一個備份組； *backup_set_file_number* 為 **2** ，表示第二個備份組。 您可以使用 *RESTORE HEADERONLY* 陳述式來取得備份組的 [backup_set_file_number](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 。  
  
  沒有指定這個選項時，預設值是使用備份裝置上的第一個備份組。  
  
  如需詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md) 中的＜指定備份組＞。  
  
  MOVE **'**_logical_file_name_in_backup_**'** TO **'**_operating_system_file_name_**'** [ **,**...*n* ]  
  指定 *logical_file_name_in_backup* 所指定的資料或記錄檔要還原至 *operating_system_file_name*所指定的位置。 針對您想要從備份組還原到新位置的每一個邏輯檔案指定 MOVE 陳述式。  
  
  |選項|描述|  
  |------------|-----------------|  
  |*logical_file_name_in_backup*|指定備份組中資料或記錄檔的邏輯名稱。 備份組中資料或記錄檔的邏輯檔案名稱，會與當初建立備份組時資料庫中的邏輯名稱相符。<br /><br /> <br /><br /> 注意：若要取得備份組中的邏輯檔清單，請使用 [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。|  
  |*operating_system_file_name*|針對 *logical_file_name_in_backup*所指定的檔案指定新的位置。 檔案將還原至這個位置。<br /><br /> (選擇性) *operating_system_file_name* 會針對還原的檔案指定新的檔案名稱。 如果您要在相同的伺服器執行個體上建立現有資料庫的副本，這就是必要選項。|  
  |*n*|這是預留位置，表示您可以指定其他 MOVE 陳述式。|  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 此範例會透過還原 `MyAdvWorks` 範例資料庫的備份 (其中包括兩個檔案： [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] _Data 和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log)，建立名為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]的新資料庫。 這個資料庫會使用簡單復原模式。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫已經存在伺服器執行個體上，因此備份中的檔案都必須還原至新的位置。 RESTORE FILELISTONLY 陳述式是用來決定資料庫中所要還原的檔案數目及名稱。 此資料庫備份是備份裝置上的第一個備份組。  
  
> **注意：** 備份和還原交易記錄 (包括時間點還原) 的範例會使用從 `MyAdvWorks_FullRM` 建立的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫，就如同以下 `MyAdvWorks` 範例。 不過，您必須使用下列 `MyAdvWorks_FullRM` 陳述式，將產生的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料庫變更為使用完整復原模式：ALTER DATABASE <database_name> SET RECOVERY FULL。  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 如需如何建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之完整資料庫備份的範例，請參閱 [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  
