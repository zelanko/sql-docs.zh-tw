---
title: 建立完整資料庫備份 (SQL Server) | Microsoft 文件
ms.custom: sqlfreshmay19
ms.date: 05/29/2019
ms.prod: sql
ms.prod_service: backup-restore
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
ms.openlocfilehash: 8888784d2adccddeb5b3f509b39803405d102efd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076057"
---
# <a name="create-a-full-database-backup-sql-server"></a>建立完整資料庫備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立完整資料庫備份。  
  

如需將 SQL Server 備份至 Azure Blob 儲存體服務的資訊，請參閱[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)和 [SQL Server 備份至 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。  
  
##  <a name="Restrictions"></a> 限制事項  
  
-   在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。    
-   在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，無法還原較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本所建立的備份。   
-   如需備份概念和工作的概觀及深入探討，請參閱[備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) 之後再繼續。  
  
## <a name="Recommendations"></a> 建議  
  
-   資料庫的大小增加時，完整資料庫備份就需要更多的時間才能完成，同時也需要更多的儲存空間。 若為大型資料庫，請考慮透過一系列的[差異資料庫備份](../../relational-databases/backup-restore/differential-backups-sql-server.md)補充完整資料庫備份。 如需詳細資訊，請參閱 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。    
-   使用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 系統預存程序來估計完整資料庫備份的大小。    
-   根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份，這些成功訊息將會快速累積，因而產生龐大的錯誤記錄檔！ 這會讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些備份記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
##  <a name="Security"></a> 安全性  
 資料庫備份上的 TRUSTWORTHY 是設為 OFF。 如需如何將 TRUSTWORTHY 設成 ON 的資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始， **PASSWORD** 和 **MEDIAPASSWORD** 選項無法再用於建立備份。 您仍然可以還原以密碼建立的備份。  
  
##  <a name="Permissions"></a> 權限  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶 **必須** 具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您按一下 [指令碼]  按鈕，再選取指令碼目的地，即可產生對應的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 指令碼。  
  
### <a name="back-up-a-database"></a>備份資料庫  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在物件總管  中按一下伺服器名稱展開伺服器樹狀目錄。    
1.  展開 [資料庫]  ，並選取使用者資料庫或展開 [系統資料庫]  ，然後選取系統資料庫。    
1.  以滑鼠右鍵按一下資料庫，指向 **[工作]** ，然後按一下 **[備份]** 。 會出現 **[備份資料庫]** 對話方塊。  
1. 從下拉式清單中選取**資料庫**。 
1. 在 [備份類型]  下拉式清單中，選取 [完整]  。 
1. 在 [備份元件]  下方，選取 [資料庫]  。 
1. 在 [目的地]  區段中，使用 [備份至]  下拉式清單選取備份目的地。 按一下 [新增]  ，以新增其他備份物件和/或目的地。 若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視現有備份目的地的內容，請選取目的地，然後按一下 [內容]  。
1. (選擇性) 檢閱 [媒體選項]  和 [備份選項]  頁面下方的其他可用設定。 如需各種備份選項的詳細資訊，請參閱[一般頁面](back-up-database-general-page.md)、[媒體選項頁面](back-up-database-media-options-page.md)及[備份選項頁面](back-up-database-backup-options-page.md)。 



### <a name="additional-information"></a>其他資訊
- 您可以在建立完整資料庫備份之後，建立差異資料庫備份。如需詳細資訊，請參閱[建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)。  
- 您可以選擇性地選取 [只複製備份]  核取方塊來建立僅限複製備份。 「只複製備份」  是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  僅限複製備份不適用於 [差異]  備份類型。  
- 如果您要備份至 URL，則可能會在 [媒體選項]  頁面上停用 [覆寫媒體]  選項。 


## <a name="ssms-examples"></a>SSMS 範例  

針對後續範例，使用下列 Transact-SQL 程式碼建立測試資料庫：

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```

### <a name="a-full-back-up-to-disk-to-default-location"></a>A. 完整備份至預設位置的磁碟
在此範例中，`SQLTestDB` 資料庫將會備份至預設備份位置上的磁碟。  絕不會備份 `SQLTestDB`。
1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
2.  展開 [資料庫]  ，以滑鼠右鍵按一下 `SQLTestDB`，指向 [工作]  ，然後按一下 [備份...]  。
3.  選取 [確定]  。

![進行 SQL 備份](media/quickstart-backup-restore-database/backup-db-ssms.png) 
 

### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.完整備份至非預設位置的磁碟**
在此範例中，`SQLTestDB` 資料庫將會備份至 `F:\MSSQL\BAK` 上的磁碟。  先前已備份 `SQLTestDB`。
1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
2.  展開 [資料庫]  ，以滑鼠右鍵按一下 `Sales`，指向 [工作]  ，然後按一下 [備份...]  。
3.  在 [一般]  頁面之 [目的地]  區段的 [備份至]  下拉式清單中，選取 [磁碟]  。
4.  選取 [移除]  ，直到移除所有現有的備份檔案為止。
5.  選取 [新增]  ，[選取備份目的地]  對話方塊將隨即開啟。
6.  在 [檔案名稱]  文字方塊中，輸入 `F:\MSSQL\BAK\Sales_20160801.bak`。
7.  選取 [確定]  。
8.  選取 [確定]  。

![變更 DB 位置](media/create-a-full-database-backup-sql-server/change-db-location.png)

### <a name="c--create-an-encrypted-backup"></a>**C.建立加密的備份**
在此範例中，`SQLTestDB` 資料庫將會使用加密備份至預設備份位置。  

1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
1. 開啟 [新增查詢]  視窗，然後執行下列命令，以便在您的 `SQLTestDB` 資料庫內建立[**資料庫主要金鑰**](../../relational-databases/security/encryption/create-a-database-master-key.md)和[**憑證**](../../t-sql/statements/create-certificate-transact-sql.md)。 

    ```sql
    USE [SQLTestDB]
        
    -- Create the database master key
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    
    
    -- Create the certificate
    CREATE CERTIFICATE MyCertificate   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    EXPIRY_DATE = '20201031';  
    GO  
    ```

1.  在 [物件總管]  中，展開 [資料庫]  、以滑鼠右鍵按一下 `SQLTestDB`、指向 [工作]  ，然後按一下 [備份]  。
1.  在 [媒體選項]  頁面的 [覆寫媒體]  區段中，選取 [備份至新的媒體集，並清除所有現有的備份組]  。
1.  在 [備份選項]  頁面的 [加密]  區段中，選取 [加密備份]  核取方塊。
1.  從 [演算法] 下拉式清單中，選取 [AES 256]  。
1.  從 [憑證或非對稱金鑰]  下拉式清單中，選取 `MyCertificate`。
1.  選取 [確定]  。

![加密的備份](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.備份到 Azure Blob 儲存體服務**


下列範例會將 `Sales` 資料庫完整備份至 Microsoft Azure Blob 儲存體服務。  儲存體帳戶名稱為 `mystorageaccount`。  容器名稱為 `myfirstcontainer`。  為求簡潔，前四個步驟只會在此列出一次，所有範例將從**步驟 5** 開始進行。

1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
2.  展開 [資料庫]  ，以滑鼠右鍵按一下 `Sales`，指向 [工作]  ，然後按一下 [備份...]  。
3.  在 [一般]  頁面之 [目的地]  區段的 [備份至:]  下拉式清單中，選取 [URL]  。
4.  按一下 [加入]  ，[選取備份目的地]  對話方塊隨即開啟。

#### <a name="striped-backup-to-url-and-a-sql-server-credential-already-exists"></a>等量備份至 URL 且 SQL Server 認證已經存在

已建立具有讀取、寫入和列出權限的預存存取原則。  使用與此預存存取原則相關聯的共用存取簽章建立了 SQL Server 認證 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。  

   5.   從 [Azure 儲存體容器:]  文字方塊中選取 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`
   6.  在 [備份檔案:]  文字方塊中，輸入 `Sales_stripe1of2_20160601.bak`。
   7.  按一下 [確定]  。
   8.  重複步驟 **4** 和 **5**。
   9.  在 [備份檔案:]  文字方塊中，輸入 `Sales_stripe2of2_20160601.bak`。
   10.  按一下 [確定]  。
   11.   按一下 [確定]  。

#### <a name="a-shared-access-signature-exists-and-a-sql-server-credential-does-not-exist"></a>共用存取簽章存在，但 SQL Server 認證不存在

  5.    在 [Azure 儲存體容器:]  文字方塊中，輸入 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`  
  6.    在 [共用存取原則:]  文字方塊中，輸入共用存取簽章。  
  7.    按一下 [確定]  。  
  8.    按一下 [確定]  。


#### <a name="a-shared-access-signature-does-not-exist"></a>共用存取簽章不存在

  5.    按一下 [新增容器]  按鈕，[連接至 Microsoft 訂用帳戶]  對話方塊隨即開啟。   
  6.    完成 [連接至 Microsoft 訂用帳戶]  對話方塊，然後按一下 [確定]  回到 [選取備份目的地]  對話方塊。  如需其他資訊，請參閱[連接到 Microsoft Azure 訂用帳戶](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)。  
  7.    在 [選取備份目的地]  對話方塊中，按一下 [確定]  。  
  8.    按一下 [確定]  。

  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>建立完整資料庫備份  
  
1.  執行 BACKUP DATABASE 陳述式以建立完整資料庫備份，請指定：  
  
    -   欲備份的資料庫名稱。   
    -   寫入完整資料庫備份的備份裝置。    
     完整資料庫備份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法如下：  
  
     BACKUP DATABASE *database*  
       TO *backup_device* [ **,** ...*n* ]    
     [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
    |選項|[描述]|  
    |------------|-----------------|  
    |*database*|為要備份的資料庫。|  
    |*backup_device* [ **,** ...*n* ]|指定一份清單，列出備份作業可使用的 1 到 64 個備份裝置。 您可以指定實體備份裝置，或者指定對應的邏輯備份裝置 (若已經定義)。 若要指定實體備份裝置，請使用 DISK 或 TAPE 選項：<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|  
    |WITH *with_options* [ **,** ...*o* ]|或者，也可以指定一個或多個其他選項 *o*。 如需有關選項基本概念的詳細資訊，請參閱步驟 2。|  
  
2.  選擇性地指定一或多個 WITH 選項。 這裡描述的是一些基本的 WITH 選項。 如需所有 WITH 選項的資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。  

基本備份組 WITH 選項：

- **{ COMPRESSION | NO_COMPRESSION }** ：只有在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 及更新的版本中，才會指定是否要在此備份上執行 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md) ，以覆寫伺服器層級的預設值。 
- **ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)** ：只有在 SQL Server 2014 或更新的版本中，才能指定要使用的加密演算法以及憑證或非對稱金鑰來維護加密的安全。
- **DESCRIPTION** **=** { **'** _text_ **'**  |  **@** _text\_variable_ }：指定描述備份組的自由形式文字。 這個字串最多可有 255 個字元。  
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** ：指定備份組的名稱。 名稱最多可有 128 個字元。 如果未指定 NAME，它就是空白。 
  
 
根據預設，BACKUP 會將備份附加到現有的媒體集，以保留現有的備份組。 若要明確指定這項，請使用 NOINIT 選項。 如需附加至現有備份組的資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  

另外，若要格式化備份媒體，請使用 FORMAT 選項：  

FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]  
當您第一次使用媒體或是想要覆寫所有現有的資料時，請使用 FORMAT 子句。 選擇性地為新的媒體指派媒體名稱和描述。  

> [!IMPORTANT]  
>  當您使用 BACKUP 陳述式的 FORMAT 子句時要非常小心，因為它會破壞備份媒體先前所儲存的任何備份。  
  
##  <a name="TsqlExample"></a> Transact-SQL 範例  
針對後續範例，使用下列 Transact-SQL 程式碼建立測試資料庫：

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
  
#### <a name="a-back-up-to-a-disk-device"></a>**A.備份到磁碟裝置**  
 下列範例使用 `SQLTestDB` 建立新的媒體集，以將整個 `FORMAT` 資料庫備份至磁碟。  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
TO DISK = 'Z:\SQLServerBackups\SQLTestDB.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B.備份到磁帶裝置**  
 下列範例會將完整的 `SQLTestDB` 資料庫備份到磁帶上，並將備份附加到先前的備份中。  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C.備份到邏輯磁帶裝置**  
 下列範例會為磁帶機建立邏輯備份裝置。 這個範例接著會將完整的 SQLTestDB 資料庫備份至該裝置。  
  
```sql  
-- Create a logical backup device,   
-- SQLTestDB_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'SQLTestDB_Bak_Tape', '\\.\tape0'; USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO SQLTestDB_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'SQLTestDB_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
使用 **Backup-SqlDatabase** Cmdlet。 為明確指出這是完整的資料庫備份，請以預設值 **Database**  指定 **-BackupAction**參數。 此參數在完整資料庫備份下是選擇性的。  

## <a name="powershell-examples"></a>PowerShell 範例

### <a name="a--full-local-backup"></a>A.  完整本機備份 
下列範例會在伺服器執行個體 `MyDB` 的預設備份位置，建立 `Computer\Instance`資料庫的完整資料庫備份。 這個範例指定了選擇性的 **-BackupAction Database**。  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
### <a name="b--full-backup-to-microsoft-azure"></a>B.  完整備份至 Microsoft Azure 
下列範例會將 `MyServer` 執行個體上的資料庫 `Sales`，完整備份至 Microsoft Azure Blob 儲存體服務。  已建立具有讀取、寫入和列出權限的預存存取原則。  使用與此預存存取原則相關聯的共用存取簽章建立了 SQL Server 認證 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。  此 PowerShell 命令會使用 **BackupFile** 參數指定備份檔案的位置 (URL) 和名稱。

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" -Database $database -BackupFile $BackupFile;
```
 
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [備份資料庫 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
-   [在簡單復原模式下還原資料庫備份 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
-   [將資料庫還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
-   [使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
- [SQL Server 備份與還原作業的疑難排解](https://support.microsoft.com/kb/224071)
- [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)
- [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)
- [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
- [備份資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)
- [備份資料庫 &#40;備份選項頁面&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)
- [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)
- [完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
