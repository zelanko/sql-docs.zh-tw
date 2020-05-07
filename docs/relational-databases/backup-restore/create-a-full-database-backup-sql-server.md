---
title: 建立完整資料庫備份 | Microsoft Docs
description: 本文說明如何使用 SQL Server Management Studio、Transact-SQL 或 PowerShell，在 SQL Server 中建立完整資料庫備份。
ms.custom: sqlfreshmay19
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: backup-restore
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
ms.reviewer: carlrab
ms.openlocfilehash: f49ba7c3f8d1ad352821e9f33e554209e88bbf37
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82179279"
---
# <a name="create-a-full-database-backup"></a>建立完整資料庫備份

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立完整資料庫備份。

如需將 SQL Server 備份至 Azure Blob 儲存體服務的資訊，請參閱[使用 Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)和 [SQL Server 備份至 URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項

- 在明確或隱含的交易中不允許使用 `BACKUP` 陳述式。
- 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，無法還原較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本所建立的備份。

如需備份概念和工作的概觀及深入探討，請參閱[備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) 之後再繼續。

## <a name="recommendations"></a><a name="Recommendations"></a> 建議

- 資料庫的大小增加時，完整資料庫備份就需要更多的時間才能完成，同時也需要更多的儲存空間。 若為大型資料庫，請考慮透過一系列的[差異資料庫備份](../../relational-databases/backup-restore/differential-backups-sql-server.md)來補充完整資料庫備份。
- 使用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 系統預存程序來估計完整資料庫備份的大小。
- 根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份，這些成功訊息將會快速累積，因而產生龐大的錯誤記錄檔！ 這會讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些備份記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。

## <a name="security"></a><a name="Security"></a> Security

資料庫備份上的 **TRUSTWORTHY** 是設為 OFF。 如需如何將 **TRUSTWORTHY** 設為 ON，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。

從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始， **PASSWORD** 和 **MEDIAPASSWORD** 選項無法再用於建立備份。 您仍然可以還原以密碼建立的備份。

## <a name="permissions"></a><a name="Permissions"></a> 權限

`BACKUP DATABASE` 和 `BACKUP LOG` 權限預設為 **系統管理員**固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。

 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務必須能夠讀取和寫入裝置，這表示執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務之帳戶必須具備寫入備份裝置的權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 其結果為當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio

> [!NOTE]
> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您可以按一下 [指令碼]  按鈕，然後選取指令碼目的地來產生對應的 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 指令碼。

1. 連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，請在 [物件總管]  中展開伺服器樹狀目錄。

1. 展開 [資料庫]  ，並選取使用者資料庫或展開 [系統資料庫]  ，然後選取系統資料庫。

1. 以滑鼠右鍵按一下您希望備份的資料庫，指向 [工作]  ，然後按一下 [備份...]  。

1. 在 [備份資料庫]  對話方塊中，您選取的資料庫會顯示在下拉式清單內 (您可以變更為伺服器上任何其他的資料庫)。

1. 在 [備份類型]  下拉式清單中，選取需要的備份類型 (預設為 [完整]  )。

   > [!IMPORTANT]
   > 您必須執行至少一次完整的資料庫備份，才可以執行差異或交易記錄備份。
   
1. 在 [備份元件]  下方，選取 [資料庫]  。

1. 在 [目的地]  區段中，檢閱備份檔案的預設位置 (位於 ../mssql/data 資料夾)。

   若要備份到不同裝置，請使用 [備份至]  下拉式清單來變更選取項目。 若要將備份組分割成多個檔案以增加備份速度，請按一下 [新增]  來新增其他備份物件和/或目的地。
 
   若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視現有備份目的地的內容，請選取目的地，然後按一下 [內容]  。

1. (選擇性) 檢閱 [媒體選項]  和 [備份選項]  頁面下方的其他可用設定。

   如需各種備份選項的詳細資訊，請參閱[一般頁面](back-up-database-general-page.md)、[媒體選項頁面](back-up-database-media-options-page.md)及[備份選項頁面](back-up-database-backup-options-page.md)。

1. 按一下 [確定]  來起始備份。

1. 備份成功完成後，請按一下 [確定]  來關閉 Microsoft SQL Server Management Studio 對話方塊。

### <a name="additional-information"></a>其他資訊

- 在建立完整的資料庫備份後，您可以建立[差異資料庫備份](create-a-differential-database-backup-sql-server.md)或[交易記錄備份](back-up-a-transaction-log-sql-server.md)。

- (選擇性) 您可以選取 [只複製備份]  核取方塊來建立僅限複製備份。 「只複製備份」  是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)。 僅限複製備份不適用於 [差異]  備份類型。

- 如果您要備份至 URL，則會在 [媒體選項]  頁面上停用 [覆寫媒體]  選項。

### <a name="examples"></a>範例

針對後續範例，使用下列 Transact-SQL 程式碼建立測試資料庫：

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest
   (
      ID INT NOT NULL PRIMARY KEY,
      c1 VARCHAR(100) NOT NULL,
      dt1 DATETIME NOT NULL DEFAULT getdate()
   );
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

#### <a name="a-full-back-up-to-disk-to-default-location"></a>A. 完整備份至預設位置的磁碟

在此範例中，`SQLTestDB` 資料庫將會備份至預設備份位置上的磁碟。

1. 連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，請在 [物件總管]  中展開伺服器樹狀目錄。

1. 展開 [資料庫]  ，以滑鼠右鍵按一下 `SQLTestDB`，指向 [工作]  ，然後按一下 [備份...]  。

1. 按一下 [確定]  。

1. 備份成功完成後，請按一下 [確定]  來關閉 Microsoft SQL Server Management Studio 對話方塊。

![進行 SQL 備份](media/quickstart-backup-restore-database/backup-db-ssms.png)

#### <a name="b-full-back-up-to-disk-to-non-default-location"></a>B. 完整備份至非預設位置的磁碟

在此範例中，`SQLTestDB` 資料庫會備份到磁碟上您選擇的位置。

1. 連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，請在 [物件總管]  中展開伺服器樹狀目錄。

1. 展開 [資料庫]  ，以滑鼠右鍵按一下 `SQLTestDB`，指向 [工作]  ，然後按一下 [備份...]  。

1. 在 [一般]  頁面之 [目的地]  區段的 [備份至]  下拉式清單中，選取 [磁碟]  。

1. 選取 [移除]  ，直到移除所有現有的備份檔案為止。

1. 選取 [新增]  ，[選取備份目的地]  對話方塊將隨即開啟。

1. 在 [檔案名稱]  文字方塊中輸入有效的路徑和檔案名稱，然後使用 **.bak** 作為副檔名來簡化此檔案的分類。

1. 按一下 [確定]  ，然後按一下 [確定]  來起始備份。

1. 備份成功完成後，請按一下 [確定]  來關閉 Microsoft SQL Server Management Studio 對話方塊。

![變更 DB 位置](media/create-a-full-database-backup-sql-server/change-db-location.png)

#### <a name="c-create-an-encrypted-backup"></a>C. 建立加密備份

在此範例中，`SQLTestDB` 資料庫將會使用加密備份至預設備份位置。

1. 連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，請在 [物件總管]  中展開伺服器樹狀目錄。

1. 依序展開 [資料庫]  及 [系統資料庫]  、以滑鼠右鍵按一下 `master`，然後按一下 [新查詢]  來開啟查詢視窗並連線到您的 `SQLTestDB` 資料庫。

1. 執行下列命令以在 `master` 資料庫中建立[**資料庫主要金鑰**](../../relational-databases/security/encryption/create-a-database-master-key.md)及[**憑證**](../../t-sql/statements/create-certificate-transact-sql.md)。  

   ```sql
   -- Create the master key
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   -- If the master key already exists, open it in the same session that you create the certificate (see next step)
   OPEN MASTER KEY DECRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe'

   -- Create the certificate encrypted by the master key
   CREATE CERTIFICATE MyCertificate
   WITH SUBJECT = 'Backup Cert', EXPIRY_DATE = '20201031';  
   ```

1. 在 [物件總管]  的 [資料庫]  節點中，以滑鼠右鍵按一下 `SQLTestDB`、指向 [工作]  ，然後按一下 [備份...]  。

1. 在 [媒體選項]  頁面的 [覆寫媒體]  區段中，選取 [備份至新的媒體集，並清除所有現有的備份組]  。

1. 在 [備份選項]  頁面的 [加密]  區段中，選取 [加密備份]  核取方塊。

1. 從 [演算法] 下拉式清單中，選取 [AES 256]  。

1. 從 [憑證或非對稱金鑰]  下拉式清單中，選取 `MyCertificate`。

1. 選取 [確定]  。

![加密的備份](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

#### <a name="d-back-up-to-the-azure-blob-storage-service"></a>D. 備份至 Azure Blob 儲存體服務

以下範例會執行 `SQLTestDB` 的完整資料庫備份到 Azure Blob 儲存體服務。 此範例假設您已擁有具備 Blob 容器的儲存體帳戶。 此範例會為您建立共用存取簽章；此範例會在已有現有共用存取簽章的容器上失敗。

若您在儲存體帳戶中尚未擁有 Azure Blob 容器，請先建立一個再繼續。 如需詳細資訊，請參閱[建立一般用途儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal)及[建立容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container)。

1. 連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，請在 [物件總管]  中展開伺服器樹狀目錄。

1. 展開 [資料庫]  ，以滑鼠右鍵按一下 `SQLTestDB`，指向 [工作]  ，然後按一下 [備份...]  。

1. 在 [一般]  頁面之 [目的地]  區段的 [備份至:]  下拉式清單中，選取 [URL]  。

1. 按一下 [加入]  ，[選取備份目的地]  對話方塊隨即開啟。

1. 若您先前已向 SQL Server Management Studio 註冊您希望使用的 Azure 儲存體容器，請選取它。 否則，請按一下 [新增容器]  來註冊新的容器。

1. 在 [連線到 Microsoft 訂用帳戶]  對話方塊中，登入您的帳戶。

1. 在 [選取儲存體帳戶]  下拉式文字方塊中，選取您的儲存體帳戶。

1. 在 [選取 Blob 容器]  下拉式文字方塊中，選取您的 Blob 容器。

1. 在 [共用存取原則逾期]  下拉式行事曆方塊中，選取您在此範例中所建立共用存取原則的到期日。

1. 按一下 [建立認證]  來在 SQL Server Management Studio 中產生共用存取簽章和認證。

1. 按一下 [確定]  來關閉 [連線到 Microsoft 訂用帳戶]  對話方塊。

1. 在 [備份檔案]  文字方塊中，修改備份檔案的名稱 (選擇性)。

1. 按一下 [確定]  來關閉 [選取備份目的地]  對話方塊。

1. 按一下 [確定]  來起始備份。

1. 備份成功完成後，請按一下 [確定]  來關閉 Microsoft SQL Server Management Studio 對話方塊。

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL

執行 `BACKUP DATABASE` 陳述式以建立完整資料庫備份，請指定：

- 欲備份的資料庫名稱。
- 寫入完整資料庫備份的備份裝置。

完整資料庫備份的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法如下：

 BACKUP DATABASE *database* TO *backup_device* [ **,** ...*n* ] [ WITH *with_options* [ **,** ...*o* ] ] ;

|選項|描述|
|------------|-----------------|
|*database*|為要備份的資料庫。|
|*backup_device* [ **,** ...*n* ]|指定一份清單，列出備份作業可使用的 1 到 64 個備份裝置。 您可以指定實體備份裝置，或者指定對應的邏輯備份裝置 (若已經定義)。 若要指定實體備份裝置，請使用 DISK 或 TAPE 選項：<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|
|WITH *with_options* [ **,** ...*o* ]|或者，也可以指定一個或多個其他選項 *o*。 如需有關選項基本概念的詳細資訊，請參閱步驟 2。|
|||

選擇性地指定一或多個 **WITH** 選項。 這裡描述的是一些基本 **WITH** 選項。 如需所有 **WITH** 選項的資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。

基本備份組 **WITH** 選項：

- **{ COMPRESSION | NO_COMPRESSION }** ：只有在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 及更新的版本中，才會指定是否要在此備份上執行 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md) ，以覆寫伺服器層級的預設值。
- **ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)** ：只有在 SQL Server 2014 或更新的版本中，才能指定要使用的加密演算法以及憑證或非對稱金鑰來維護加密的安全。
- **DESCRIPTION** **=** { **'** _text_ **'**  |  **@** _text\_variable_ }：指定描述備份組的自由形式文字。 這個字串最多可有 255 個字元。
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** ：指定備份組的名稱。 名稱最多可有 128 個字元。 如果未指定 NAME，它就是空白。

根據預設，`BACKUP` 會將備份附加到現有的媒體集，以保留現有的備份組。 若要明確指定此項目，請使用 `NOINIT` 選項。 如需附加至現有備份組的資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。

另外，若要格式化備份媒體，請使用 **FORMAT** 選項：

 FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]

 當您第一次使用媒體或是想要覆寫所有現有的資料時，請使用 **FORMAT** 子句。 選擇性地為新的媒體指派媒體名稱和描述。

 > [!IMPORTANT]
 > 當您使用 `BACKUP` 陳述式的 **FORMAT** 子句時要非常小心，因為它會破壞備份媒體先前所儲存的任何備份。

### <a name="examples"></a><a name="TsqlExample"></a> 範例

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
   dt1 DATETIME NOT NULL DEFAULT GETDATE()
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

#### <a name="a-back-up-to-a-disk-device"></a>A. 備份到磁碟裝置

下列範例使用 `SQLTestDB` 建立新的媒體集，以將整個 `FORMAT` 資料庫備份至磁碟。

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
TO DISK = 'c:\tmp\SQLTestDB.bak'
   WITH FORMAT,
      MEDIANAME = 'SQLServerBackups',
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="b-back-up-to-a-tape-device"></a>B. 備份到磁帶裝置

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

#### <a name="c-back-up-to-a-logical-tape-device"></a>C. 備份到邏輯磁帶裝置

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

## <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell

使用 **Backup-SqlDatabase** Cmdlet。 為明確指出這是完整的資料庫備份，請以預設值 **Database** 指定 **-BackupAction** 參數。 此參數在完整資料庫備份下是選擇性的。

> [!NOTE]
> 這些範例需要 SqlServer 模組。 若要判斷是否已安裝，請執行 `Get-Module -Name SqlServer`。 若要安裝此模組，請在 PowerShell 的系統管理員工作階段中執行 `Install-Module -Name SqlServer`。
>
> 如需詳細資訊，請參閱 [SQL Server PowerShell Provider](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。

> [!IMPORTANT]
> 若您正在從 SQL Server Management Studio 開啟 PowerShell 視窗來連線到安裝的 SQL Server，您可以省略此範例的認證部分，因為會自動使用您在 SSMS 中認證來建立 PowerShell 與您 SQL Server 執行個體間的連線。

### <a name="examples"></a>範例

#### <a name="a-full-backup-local"></a>A. 完整備份 (本機)

下列範例會在伺服器執行個體 `<myDatabase>` 的預設備份位置，建立 `Computer\Instance`資料庫的完整資料庫備份。 這個範例指定了選擇性的 **-BackupAction Database**。

如需完整的語法和其他範例，請參閱 [Backup-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/backup-sqldatabase)。

```powershell
$credential = Get-Credential

Backup-SqlDatabase -ServerInstance Computer[\Instance] -Database <myDatabase> -BackupAction Database -Credential $credential
```

#### <a name="b-full-backup-to-azure"></a>B. 完整備份到 Azure

下列範例會將資料庫 `<myDatabase>` 上的 `<myServer>` 執行個體完整備份至 Azure Blob 儲存體服務。 已建立具有讀取、寫入和列出權限的預存存取原則。 使用與此預存存取原則相關聯的共用存取簽章建立了 SQL Server 認證 `https://<myStorageAccount>.blob.core.windows.net/<myContainer>`。 此 PowerShell 命令會使用 **BackupFile** 參數指定備份檔案的位置 (URL) 和名稱。

```powershell
$credential = Get-Credential
$container = 'https://<myStorageAccount>blob.core.windows.net/<myContainer>'
$fileName = '<myDatabase>.bak'
$server = '<myServer>'
$database = '<myDatabase>
$backupFile = $container + '/' + $fileName

Backup-SqlDatabase -ServerInstance $server -Database $database -BackupFile $backupFile -Credential $credential
```

## <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks

- [備份資料庫 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
- [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
- [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [在簡單復原模式下還原資料庫備份 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
- [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
- [將資料庫還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
- [使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)

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
