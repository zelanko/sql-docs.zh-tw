---
title: SQL Server 備份至 URL | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c654dc9117a8de55a3e90898487a6b9baa1d6c0d
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797995"
---
# <a name="sql-server-backup-to-url"></a>SQL Server 備份至 URL
  本主題將介紹使用 Azure Blob 儲存體服務作為備份目的地所需的概念、需求和元件。 使用磁碟或磁帶時，備份和還原功能相同或類似，只有些許的差異。 這些差異在於許多顯而易見的例外狀況，本主題中將內含某些程式碼範例。  
  
## <a name="requirements-components-and-concepts"></a>需求、元件和概念  
 **本節內容：**  
  
-   [安全性](#security)  
  
-   [重要元件和概念簡介](#intorkeyconcepts)  
  
-   [Azure Blob 儲存體服務](#Blob)  
  
-   [SQL Server 元件](#sqlserver)  
  
-   [限制](#limitations)  
  
-   [支援 Backup/Restore 陳述式](#Support)  
  
-   [在 SQL Server Management Studio 中使用備份工作](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [使用 [維護計畫精靈] 將 SQL Server 備份至 URL](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [使用 SQL Server Management Studio 從 Azure 儲存體還原](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> 安全性  
 以下是備份至 Azure Blob 儲存體服務或從中還原時的安全性考慮和需求。  
  
-   建立 Azure Blob 儲存體服務的容器時，建議您將存取權設定為 [**私**用]。 將存取權設定為 [私用] 可限制只有能夠提供必要資訊向 Azure 帳戶驗證的使用者或帳戶，才有存取權。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要將 Azure 帳戶名稱和存取金鑰驗證儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證中。 此資訊會在執行備份或還原作業時，用來向 Azure 帳戶進行驗證。  
  
-   用來發出 BACKUP 或 RESTORE 命令的使用者帳戶應該位於擁有 **改變任何認證** 權限的 **db_backup 運算子** 資料庫角色中。  
  
###  <a name="intorkeyconcepts"></a> 重要元件和概念簡介  
 下列兩節將介紹 Azure Blob 儲存體服務，以及備份至 Azure Blob 儲存體服務或從中還原時所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。 請務必瞭解這些元件，以及它們之間的互動，以執行 Azure Blob 儲存體服務的備份或還原。  
  
 建立 Azure 帳戶是此程式的第一個步驟。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用**Azure 儲存體帳戶名稱**及其**存取金鑰**值來驗證和讀取 blob，並將其寫入儲存體服務。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證會儲存這項驗證資訊，並且在備份或還原作業期間使用。 如需建立儲存體帳戶和執行簡單還原的完整逐步解說，請參閱[使用 Azure 儲存體服務進行 SQL Server 備份和還原的教學](https://go.microsoft.com/fwlink/?LinkId=271615)課程。  
  
 ![將儲存體帳戶對應至 sql 認證](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "將儲存體帳戶對應至 sql 認證")  
  
###  <a name="Blob"></a>Azure Blob 儲存體服務  
 **儲存體帳戶：** 儲存體帳戶是所有儲存體服務的起點。 若要存取 Azure Blob 儲存體服務，請先建立 Azure 儲存體帳戶。 必須要有**儲存體帳戶名稱**及其**存取金鑰**屬性，才能向 Azure Blob 儲存體服務及其元件進行驗證。  
  
 **容器：** 容器提供一組 Blob 的群組，而且可以儲存不限數目的 Blob。 若要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份寫入 Azure Blob 服務，您至少必須建立根容器。  
  
 **Blob：** 任何類型和大小的檔案。 有兩種類型的 blob 可儲存在 Azure Blob 儲存體服務中：區塊和分頁 blob。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份會使用分頁 Blob 做為 Blob 類型。 您可以使用下列 URL 格式來定址 blob： HTTPs://\<儲存體帳戶 >. net/\<容器 >/\<blob >  
  
 ![Azure Blob 儲存體](../../database-engine/media/backuptocloud-blobarchitecture.gif "Azure Blob 儲存體")  
  
 如需有關 Azure Blob 儲存體服務的詳細資訊，請參閱[如何使用 Azure Blob 儲存體服務](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 如需有關分頁 Blob 的詳細資訊，請參閱＜ [了解區塊和分頁 Blob](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)＞。  
  
###  <a name="sqlserver"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Components  
 **URL：** URL 會指定唯一備份檔案的統一資源識別項 (URI)。 此 URL 是用來提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份檔案的位置和名稱。 在此執行中，唯一有效的 URL 是指向 Azure 儲存體帳戶中分頁 Blob 的 URL。 此 URL 必須指向實際的 Blob，而非只有容器。 如果 Blob 不存在，就會建立 Blob。 如果指定了現有的 Blob，除非指定了 "WITH FORMAT" 選項，否則 BACKUP 會失敗。  
  
> [!WARNING]  
>  如果您選擇將備份檔案複製並上傳至 Azure Blob 儲存體服務，請使用分頁 Blob 作為儲存體選項。 不支援從區塊 Blob 還原。 從區塊 Blob 類型進行 RESTORE 會失敗，並出現錯誤。  
  
 以下是 URL 值範例： HTTP [s]：//ACCOUNTNAME.Blob.core.windows.net/\<CONTAINER >/\<FILENAME .bak >。 HTTPS 不是必要項目，但是建議使用。  
  
 **認證：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證是用來儲存連線到 SQL Server 外部資源所需之驗證資訊的物件。  在這裡，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份和還原程式會使用認證來向 Azure Blob 儲存體服務進行驗證。 認證會儲存儲存體帳戶的名稱以及儲存體帳戶的 **存取金鑰** 值。 一旦建立認證之後，您必須在發出 BACKUP/RESTORE 陳述式時，在 WITH CREDENTIAL 選項中指定認證。 如需有關如何查看、複製或重新產生儲存體帳戶**存取金鑰**的詳細資訊，請參閱[儲存體帳戶存取金鑰](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)。  
  
 如需有關如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證的逐步指示，請參閱本主題稍後的＜ [建立認證](#credential) ＞範例。  
  
 如需有關認證的一般資訊，請參閱＜ [認證](../security/authentication-access/credentials-database-engine.md)＞。  
  
 如需有關使用認證之其他範例的詳細資訊，請參閱 [建立 SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
###  <a name="limitations"></a> 限制  
  
-   不支援備份至進階儲存體。  
  
-   支援的備份大小上限為 1 TB。  
  
-   您可以使用 TSQL、SMO 或 PowerShell 指令程式發出 Backup 或 Restore 陳述式。 目前未啟用使用 SQL Server Management Studio 備份或還原嚮導，從 Azure Blob 儲存體服務進行備份或還原。  
  
-   不支援建立邏輯裝置名稱。 因此，不支援使用 sp_dumpdevice 或透過 SQL Server Management Studio 加入 URL 做為備份裝置。  
  
-   不支援附加至現有的備份 Blob。 現有 Blob 的備份只能使用 WITH FORMAT 選項來覆寫。  
  
-   不支援在單一備份作業中，備份至多個 Blob。 例如，下列程式碼會傳回錯誤：  
  
    ```sql
    BACKUP DATABASE AdventureWorks2012
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_1.bak'
       URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_2.bak'
          WITH CREDENTIAL = 'mycredential'
         ,STATS = 5;  
    GO
    ```  
  
-   不支援使用 `BACKUP` 來指定區塊大小。  
  
-   不支援指定 `MAXTRANSFERSIZE`。  
  
-   不支援指定備份組選項 - `RETAINDAYS` 和 `EXPIREDATE`。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的備份裝置名稱大小上限為 259 個字元。 BACKUP TO URL 會用 36 個字元的必要項目指定 URL - 'https://.blob.core.windows.net//.bak '，而保留 223 個字元供帳戶、容器和 Blob 名稱共用。  
  
###  <a name="Support"></a> 支援 Backup/Restore 陳述式  
  
|||||  
|-|-|-|-|  
|Backup/Restore 陳述式|支援|例外狀況|註解|  
|BACKUP|&#x2713;|不支援 BLOCKSIZE 和 MAXTRANSFERSIZE。|需要指定 WITH CREDENTIAL|  
|RESTORE|&#x2713;||需要指定 WITH CREDENTIAL|  
|RESTORE FILELISTONLY|&#x2713;||需要指定 WITH CREDENTIAL|  
|RESTORE HEADERONLY|&#x2713;||需要指定 WITH CREDENTIAL|  
|RESTORE LABELONLY|&#x2713;||需要指定 WITH CREDENTIAL|  
|RESTORE VERIFYONLY|&#x2713;||需要指定 WITH CREDENTIAL|  
|RESTORE REWINDONLY|&#x2713;|||  
  
 如需 Backup 陳述式的語法和一般資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
 如需 Restore 陳述式的語法和一般資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)。  
  
### <a name="support-for-backup-arguments"></a>支援 Backup 引數  
  
|||||  
|-|-|-|-|  
|引數|支援|例外狀況|註解|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
||  
|TO (URL)|&#x2713;|與 DISK 和 TAPE 不同，URL 不支援指定或建立邏輯名稱。|這個引數是用來指定備份檔案的 URL 路徑。|  
|MIRROR TO|&#x2713;|||  
|**WITH 選項：**||||  
|CREDENTIAL|&#x2713;||只有在使用 BACKUP TO URL 選項備份至 Azure Blob 儲存體服務時，才支援 WITH CREDENTIAL。|  
|DIFFERENTIAL|&#x2713;|||  
|COPY_ONLY|&#x2713;|||  
|COMPRESSION&#124;NO_COMPRESSION|&#x2713;|||  
|DESCRIPTION|&#x2713;|||  
|名稱|&#x2713;|||  
|EXPIREDATE &#124; RETAINDAYS|&#x2713;|||  
|NOINIT &#124; INIT|&#x2713;||如果使用這個選項，則會被忽略。<br /><br /> 您無法附加至 Blob。 若要覆寫備份，請使用 FORMAT 引數。|  
|NOSKIP &#124; SKIP|&#x2713;|||  
|NOFORMAT &#124; FORMAT|&#x2713;||如果使用這個選項，則會被忽略。<br /><br /> 除非指定了 WITH FORMAT，否則帶入現有 Blob 的備份會失敗。 指定 WITH FORMAT 時，系統會覆寫現有的 Blob。|  
|MEDIADESCRIPTION|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|NO_CHECKSUM &#124; CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|STATS|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|NORECOVERY &#124; STANDBY|&#x2713;|||  
|NO_TRUNCATE|&#x2713;|||  
  
 如需 Backup 引數的詳細資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
### <a name="support-for-restore-arguments"></a>支援 Restore 引數  
  
|||||  
|-|-|-|-|  
|引數|支援|例外狀況|註解|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
|FROM (URL)|&#x2713;||FROM URL 引數是用來指定備份檔案的 URL 路徑。|  
|**WITH Options:**||||  
|CREDENTIAL|&#x2713;||只有在使用 [從 URL 還原] 選項從 Azure Blob 儲存體服務還原時，才支援 WITH CREDENTIAL。|  
|PARTIAL|&#x2713;|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|&#x2713;|||  
|LOADHISTORY|&#x2713;|||  
|MOVE|&#x2713;|||  
|REPLACE|&#x2713;|||  
|RESTART|&#x2713;|||  
|RESTRICTED_USER|&#x2713;|||  
|FILE|&#x2713;|||  
|PASSWORD|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|MEDIAPASSWORD|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|CHECKSUM &#124; NO_CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|FILESTREAM|&#x2713;|||  
|STATS|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|KEEP_REPLICATION|&#x2713;|||  
|KEEP_CDC|&#x2713;|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|&#x2713;|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|&#x2713;|||  
  
 如需 Restore 引數的詳細資訊，請參閱 [RESTORE 引數 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)。  
  
##  <a name="BackupTaskSSMS"></a>在 SQL Server Management Studio 中使用備份工作  
 SQL Server Management Studio 中的備份工作已增強為包含 URL 做為其中一個目的地選項，以及備份至 Azure 儲存體（例如 SQL 認證）所需的其他支持對象。  
  
 下列步驟說明對備份資料庫工作所做的變更，以允許備份至 Azure 儲存體。：  
  
1.  啟動 SQL Server Management Studio 並連接至 SQL Server 執行個體。  選取您要備份的資料庫，並在 [工作]**上按一下**滑鼠右鍵，然後選取 [**備份 ...** ]。這會開啟 [備份資料庫] 對話方塊。  
  
2.  在 [一般] 頁面上，[ **URL** ] 選項是用來建立 Azure 儲存體的備份。 當您選取此選項時，會在此頁面上看到其他啟用的選項：  
  
    1.  **檔案名稱：** 備份檔案的名稱。  
  
    2.  **SQL 認證：** 您可以指定現有的 SQL Server 認證，或按一下 [SQL 認證] 方塊旁的 [**建立**] 來建立新的認證。  
  
        > [!IMPORTANT]  
        >  在您按一下 **[建立]** 時開啟的對話方塊需要管理憑證或訂閱的發行設定檔。 SQL Server 目前支援發行設定檔 2.0 版。 若要下載發行設定檔的支援版本，請參閱＜ [下載發行設定檔 2.0](https://go.microsoft.com/fwlink/?LinkId=396421)＞。  
        >   
        >  如果您無法存取管理憑證或發行設定檔，可以使用 Transact-SQL 或 SQL Server Management Studio 來指定儲存體帳戶名稱和存取金鑰資訊，藉以建立 SQL 認證。 請參閱[建立認證](#credential)一節中的範例程式碼，以使用 transact-sql 來建立認證。 或者，使用 SQL Server Management Studio，在資料庫引擎執行個體中，以滑鼠右鍵按一下 **[安全性]** 、選取 **[新增]** ，然後選取 **[認證]** 。 針對 **[識別]** 指定儲存體帳戶名稱，並且在 **[密碼]** 欄位中指定存取金鑰。  
  
    3.  **Azure 儲存體容器：** 用來儲存備份檔案的 Azure 儲存體容器名稱。  
  
    4.  **URL 前置詞：** 這會使用先前步驟中所述的欄位中所指定的資訊，自動建立。 如果您手動編輯此值，請確定其與您先前提供的其他資訊相符。 例如，如果您修改了儲存體 URL，請確定 SQL 認證已設定為對相同的儲存體帳戶進行驗證。  
  
 當您選取 URL 做為目的地時， **[媒體選項]** 頁面中的某些選項會停用。  下列主題包含有關備份資料庫對話方塊的詳細資訊：  
  
 [備份資料庫 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [備份資料庫 &#40;媒體選項頁面&#41;](back-up-database-media-options-page.md)  
  
 [備份資料庫 &#40;備份選項頁面&#41;](back-up-database-backup-options-page.md)  
  
 [建立認證 - 向 Azure 儲存體驗證](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> 使用 [維護計畫精靈] 將 SQL Server 備份至 URL  
 與先前所述的備份工作類似，SQL Server Management Studio 中的維護計畫 Wizard 已增強為包含**URL**做為其中一個目的地選項，以及備份至 Azure 儲存體（例如 SQL）所需的其他支持對象。證書. 如需詳細資訊，請參閱＜ **Using Maintenance Plan Wizard** ＞中的＜ [定義備份工作](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure)＞一節。  
  
##  <a name="RestoreSSMS"></a>使用 SQL Server Management Studio 從 Azure 儲存體還原  
 如果您要還原資料庫，會內含 **[URL]** 做為還原裝置的來源。 下列步驟說明還原工作中的變更，以允許從 Azure 儲存體進行還原：  
  
1.  當您在 SQL Server Management Studio 的還原工作之 [一般] 頁面中選取 [裝置] 時，會連結到內含 **URL** 作為備份媒體類型的 [選取備份裝置] 對話方塊。  
  
2.  當您選取 **[URL]** 並按一下 **[新增]** 時，會開啟 **[連接到 Azure 儲存體]** 對話。 指定要向 Azure 儲存體驗證的 SQL 認證資訊。  
  
3.  SQL Server 接著會使用您提供的 SQL 認證資訊連接到 Azure 儲存體，並開啟 [**在 Azure 中尋找備份檔案**] 對話方塊。 位於儲存體中的備份檔案，會顯示在此頁面上。 選取您要用以還原的檔案，並按一下 **[確定]** 。 如此會讓您回到 **[選取備份裝置]** 對話，而按一下此對話中的 **[確定]** ，會帶您回到您可完成還原的主要 **[還原]** 對話。  如需詳細資訊，請參閱下列主題：  
  
     [還原資料庫 &#40;一般頁面&#41;](restore-database-general-page.md)  
  
     [還原資料庫 &#40;檔案頁面&#41;](restore-database-files-page.md)  
  
     [還原資料庫 &#40;選項頁面&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> 程式碼範例  
 本節包含下列範例。  
  
-   [建立認證](#credential)  
  
-   [備份完整資料庫](#complete)  
  
-   [備份資料庫和記錄](#databaselog)  
  
-   [建立主要檔案群組的完整檔案備份](#filebackup)  
  
-   [建立主要檔案群組的差異檔案備份](#differential)  
  
-   [還原資料庫和移動檔案](#restoredbwithmove)  
  
-   [使用 STOPAT 還原至時間點](#PITR)  
  
###  <a name="credential"></a> 建立認證  
 下列範例會建立儲存 Azure 儲存體驗證資訊的認證。  

   ```sql
   IF NOT EXISTS  
   (SELECT * FROM sys.credentials   
   WHERE credential_identity = 'mycredential')  
   CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
   ,SECRET = '<storage access key>' ;  
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
   string secret = "<storage access key>";  
  
   // Create a Credential  
   string credentialName = "mycredential";  
   Credential credential = new Credential(server, credentialName);  
   credential.Create(identity, secret);  
   ```  
  
   ```powershell
   # create variables  
   $storageAccount = "mystorageaccount"  
   $storageKey = "<storage access key>"  
   $secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
   $credentialName = "mycredential"  
  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # Create a credential  
   New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString
   ```  
  
###  <a name="complete"></a>備份完整資料庫  
 下列範例會將 AdventureWorks2012 資料庫備份至 Azure Blob 儲存體服務。
  
   ```sql
   BACKUP DATABASE AdventureWorks2012   
   TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
         WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
   GO
   ```  
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url  
   string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup to Url  
   Backup backup = new Backup();  
   backup.CredentialName = credentialName;  
   backup.Database = dbName;  
   backup.CompressionOption = BackupCompressionOptions.On;  
   backup.Devices.AddDevice(url, DeviceType.Url);  
   backup.SqlBackup(server);  
   ```
  
   ```powershell
   # create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"   
   # for default instance, the $srvpath varilable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # navigate to SQL Server Instance  
   CD $srvPath   
   $backupFile = $backupUrlContainer + "AdventureWorks2012" +  ".bak"  
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On
   ```  
  
###  <a name="databaselog"></a>備份資料庫和記錄檔  
 下列範例會備份 AdventureWorks2012 範例資料庫，依預設採用簡單復原模式。 為了支援記錄備份，AdventureWorks2012 資料庫會修改成使用完整復原模式。 然後，此範例會建立 Azure Blob 的完整資料庫備份，並且在更新活動一段時間之後，備份記錄。 這個範例會建立含有日期時間戳記的備份檔案名稱。  
  
   ```sql
   -- To permit log backups, before the full database backup, modify the database   
   -- to use the full recovery model.  
   USE master;  
   GO  
   ALTER DATABASE AdventureWorks2012  
      SET RECOVERY FULL;  
   GO  
  
   -- Back up the full AdventureWorks2012 database.  
          -- First create a file name for the backup file with DateTime stamp  
  
   DECLARE @Full_Filename AS VARCHAR (300);  
   SET @Full_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Full_'+   
   REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.bak';   
   --Back up Adventureworks2012 database  
  
   BACKUP DATABASE AdventureWorks2012  
   TO URL =  @Full_Filename  
   WITH CREDENTIAL = 'mycredential';  
   ,COMPRESSION  
   GO  
   -- Back up the AdventureWorks2012 log.  
   DECLARE @Log_Filename AS VARCHAR (300);  
   SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
   REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
   BACKUP LOG AdventureWorks2012  
    TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,COMPRESSION;  
   GO  
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url for data backup  
   string urlDataBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Data-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup Database to Url  
   Backup backupData = new Backup();  
   backupData.CredentialName = credentialName;  
   backupData.Database = dbName;  
   backup.CompressionOption = BackupCompressionOptions.On;  
   backupData.Devices.AddDevice(urlDataBackup, DeviceType.Url);  
   backupData.SqlBackup(server);  
  
   // Generate Unique Url for data backup  
   string urlLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Log-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup Database Log to Url  
   Backup backupLog = new Backup();  
   backupLog.CredentialName = credentialName;  
   backupLog.Database = dbName;  
   backup.CompressionOption = BackupCompressionOptions.On;  
   backupLog.Devices.AddDevice(urlLogBackup, DeviceType.Url);  
   backupLog.Action = BackupActionType.Log;  
   backupLog.SqlBackup(server);  
   ```  

   ```powershell
   #create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # navigate to theSQL Server Instance
   CD $srvPath   
   #Create a unique file name for the full database backup  
   $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
   #Backup Database to URL
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Database    
  
   #Create a unique file name for log backup  
  
   $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
   #Backup Log to URL
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Log
   ```  
  
###  <a name="filebackup"></a>建立主要檔案群組的完整檔案備份  
 下列範例會建立主要檔案群組的完整檔案備份。
  
   ```sql
   --Back up the files in Primary:  
   BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
   GO  
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url  
   string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bck",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup to Url  
   Backup backup = new Backup();  
   backup.CredentialName = credentialName;  
   backup.Database = dbName;  
   backup.Action = BackupActionType.Files;  
   backup.DatabaseFileGroups.Add("PRIMARY");  
   backup.CompressionOption = BackupCompressionOptions.On;  
   backup.Devices.AddDevice(url, DeviceType.Url);  
   backup.SqlBackup(server);
   ```
  
   ```powershell
   #create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # navigate to the SQL Server Instance  
  
   CD $srvPath   
   #Create a unique file name for the file backup  
   $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bck"  
  
   #Backup Primary File Group to URL  
  
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary
   ```  
  
###  <a name="differential"></a>建立主要檔案群組的差異檔案備份  
 下列範例會建立主要檔案群組的差異檔案備份。  
  
   ```sql
   --Back up the files in Primary:  
   BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012filesdiff.bck'  
       WITH   
          CREDENTIAL = 'mycredential'  
          ,COMPRESSION  
      ,DIFFERENTIAL;  
   GO
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url  
   string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup to Url  
   Backup backup = new Backup();  
   backup.CredentialName = credentialName;  
   backup.Database = dbName;  
   backup.Action = BackupActionType.Files;  
   backup.DatabaseFileGroups.Add("PRIMARY");  
   backup.Incremental = true;  
   backup.CompressionOption = BackupCompressionOptions.On;  
   backup.Devices.AddDevice(url, DeviceType.Url);  
   backup.SqlBackup(server); 
   ```

   ```powershell
   #create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # navigate to SQL Server Instance
   CD $srvPath   
  
   #create a unique file name for the full backup  
   $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
   #Create a differential backup of the primary filegroup
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary -Incremental
   ```  
  
###  <a name="restoredbwithmove"></a>還原資料庫和移動檔案  
 若要還原完整資料庫備份並將還原的資料庫移至 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data 目錄，請使用下列步驟。
  
   ```sql
   -- Backup the tail of the log first
   DECLARE @Log_Filename AS VARCHAR (300);  
   SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
   REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
   BACKUP LOG AdventureWorks2012  
    TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,NORECOVERY;  
   GO  
  
   RESTORE DATABASE AdventureWorks2012 FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'  
   WITH CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,MOVE 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,STATS = 5
   ```
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url  
   string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup to Url  
   Backup backup = new Backup();  
   backup.CredentialName = credentialName;  
   backup.Database = dbName;  
   backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
   backup.SqlBackup(server);  
  
   // Generate Unique Url for tail log backup  
   string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup Tail Log to Url  
   Backup backupTailLog = new Backup();  
   backupTailLog.CredentialName = credentialName;  
   backupTailLog.Database = dbName;  
   backupTailLog.Action = BackupActionType.Log;  
   backupTailLog.NoRecovery = true;  
   backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
   backupTailLog.SqlBackup(server);  
  
   // Restore a database and move files  
   string newDataFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
   string newLogFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
   Restore restore = new Restore();  
   restore.CredentialName = credentialName;  
   restore.Database = dbName;  
   restore.ReplaceDatabase = true;  
   restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
   restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
   restore.RelocateFiles.Add(new RelocateFile(dbName+ "_Log", newLogFilePath));  
   restore.SqlRestore(server);
   ```  

   ```powershell
   #create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTNACENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # navigate to SQL Server Instance
   CD $srvPath   
  
   #create a unique file name for the full backup  
   $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
   # Full database backup to URL  
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On      
  
   #Create a unique file name for the tail log backup  
   $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
   #Backup tail log to URL
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery    
  
   # Restore Database and move files
   $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
   $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
   Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath)
   ```  
  
###  <a name="PITR"></a> 使用 STOPAT 還原至時間點  
 下列範例會將資料庫還原至某個時間點的狀態，並且顯示還原作業。  
  
   ```sql
   RESTORE DATABASE AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
   WITH   
     CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,Move 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,NORECOVERY  
    --,REPLACE  
    ,STATS = 5;  
   GO   
  
   RESTORE LOG AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.trn'   
   WITH CREDENTIAL = 'mycredential'  
    ,RECOVERY   
    ,STOPAT = 'Oct 23, 2012 5:00 PM'   
   GO  
   ```  
  
   ```csharp
   // Connect to default sql server instance on local machine  
   Server server = new Server(".");  
   string identity = "mystorageaccount";  
  
   string credentialName = "mycredential";  
   string dbName = "AdventureWorks2012";  
   string blobContainerName = "mycontainer";  
  
   // Generate Unique Url  
   string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup to Url  
   Backup backup = new Backup();  
   backup.CredentialName = credentialName;  
   backup.Database = dbName;  
   backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
   backup.SqlBackup(server);  
  
   // Generate Unique Url for Tail Log backup  
   string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
   // Backup Tail Log to Url  
   Backup backupTailLog = new Backup();  
   backupTailLog.CredentialName = credentialName;  
   backupTailLog.Database = dbName;  
   backupTailLog.Action = BackupActionType.Log;  
   backupTailLog.NoRecovery = true;  
   backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
   backupTailLog.SqlBackup(server);  
  
   // Restore a database and move files  
   string newDataFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
   string newLogFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
   Restore restore = new Restore();  
   restore.CredentialName = credentialName;  
   restore.Database = dbName;  
   restore.ReplaceDatabase = true;  
   restore.NoRecovery = true;  
   restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
   restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
   restore.RelocateFiles.Add(new RelocateFile(dbName + "_Log", newLogFilePath));  
   restore.SqlRestore(server);  
      
   // Restore transaction Log with stop at   
   Restore restoreLog = new Restore();  
   restoreLog.CredentialName = credentialName;  
   restoreLog.Database = dbName;  
   restoreLog.Action = RestoreActionType.Log;  
   restoreLog.Devices.AddDevice(urlBackupData, DeviceType.Url);  
   restoreLog.ToPointInTime = DateTime.Now.ToString();   
   restoreLog.SqlRestore(server);
   ```
  
   ```powershell
   #create variables  
   $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
   $credentialName = "mycredential"  
   $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
   # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
   # Navigate to SQL Server Instance Directory
   CD $srvPath   
  
   #create a unique file name for the full backup  
   $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
   # Full database backup to URL  
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On     
  
   #Create a unique file name for the tail log backup  
   $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
   #Backup tail log to URL
   Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery     
  
   # Restore Database and move files
   $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
   $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
   Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath) -NoRecovery    
  
   # Restore Transaction log with Stop At:  
   Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backuplogFile  -ToPointInTime (Get-Date).ToString()
   ```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 備份至 URL 的最佳作法和疑難排解](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [教學課程：SQL Server 備份及還原至 Azure Blob 儲存體服務](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
