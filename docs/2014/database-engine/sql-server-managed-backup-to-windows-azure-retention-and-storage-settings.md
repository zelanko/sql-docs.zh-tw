---
title: SQL Server 受管理的備份至 Azure-保留和儲存設定 |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: c4aa26ea-5465-40cc-8b83-f50603cb9db1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a427c12d8296ffc7f3f2603c9f34c33d1fd94bc3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797834"
---
# <a name="sql-server-managed-backup-to-azure---retention-and-storage-settings"></a>SQL Server Managed Backup 到 Azure - 保留和儲存體設定
  本主題說明設定資料庫之 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 及設定執行個體之預設設定的基本步驟。 本主題也描述為執行個體暫停及繼續 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服務的必要步驟。  
  
 如需設定的完整逐步解說[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，請參閱[設定 SQL Server 受管理的備份至 Azure](../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)和[針對可用性群組設定 SQL Server 受控備份至 azure](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)。  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   請勿對目前正在使用維護計劃或記錄傳送的資料庫啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 如需有關互通性和與其他 SQL Server 功能共存的詳細資訊，請參閱[SQL Server 受控備份至 Azure：互通性與共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   SQL Server Agent 應在執行中。  
  
    > [!WARNING]  
    >  如果 SQL Server Agent 已停止一段時間然後重新啟動，您可能會看見備份活動增加 (視 SQL Agent 停止和啟動之間經過的時間長度而定)，而且可能會有記錄備份積存等待執行。 請考慮將 SQL Server Agent 設定為啟動時自動啟動。  
  
-   在設定之前，您應該先建立 Azure 儲存體帳戶，以及將驗證資訊儲存到儲存體帳戶的 SQL 認證[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 如需詳細資訊，請參閱 [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md#intorkeyconcepts) 主題中的 **Introduction to Key Components and Concepts** 一節，以及 [Lesson 2: Create a SQL Server Credential](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會建立必要的容器以儲存備份。 使用「電腦名稱稱-實例名稱」格式建立容器名稱。 AlwaysOn 可用性群組的容器會以可用性群組的 GUID 命名。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要執行啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的預存程式，您必須是具有**ALTER ANY CREDENTIAL**許可權的**db_backupoperator**資料庫角色中的`System Administrator`或成員，以及`EXECUTE` **sp_delete_backuphistory**和`smart_admin.sp_backup_master_switch`預存程式的許可權。  用於檢閱現有設定的預存程序及函式，通常需要具備預存程序的 `Execute` 權限及函式的 `Select`。  
  

  
###  <a name="considerations-for-enabling-ss_smartbackup-for-databases-and-instances"></a><a name="Considerations"></a>針對資料庫和[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]實例啟用的考慮  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可以為了個別資料庫而分別啟用，或者為了整個執行個體而啟用。 這些選擇取決於實例上資料庫的復原能力需求、管理多個資料庫和實例的需求，以及策略性地使用 Azure 儲存體。  
  
#### <a name="enabling-ss_smartbackup-at-the-database-level"></a>正在資料庫層級啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 如果資料庫有特定的備份需求與保留週期 (復原能力 SLA)，並且和執行個體上的其他資料庫不同，請在資料庫層級為此資料庫設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 資料庫層級設定會覆寫執行個體層級的組態設定。 但相同的執行個體可以並用這兩個選項。 下列清單列有在資料庫層級上啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的優點及注意事項。  
  
-   更為精細：分隔每個資料庫的組態設定。 可以針對不同的資料庫支援不同的保留週期。  
  
-   覆寫資料庫的執行個體層級設定。  
  
-   透過選取要備份的個別資料庫，可用來降低儲存成本。  
  
-   需要管理每個資料庫  
  
#### <a name="enabling-ss_smartbackup-at-the-instance-level-with-default-settings"></a>使用預設設定在執行個體層級啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 如果大部分執行個體上的資料庫都有相同的備份和保留原則需求，或者如果您想要新的資料庫執行個體在建立時自動備份，請使用此設定。 一些未套用原則的資料庫仍可個別加以設定。 在執行個體層級上啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 時，以下為優點和考量清單。  
  
-   在執行個體層級的自動化：常見的設定會自動套用於之後加入的新資料庫。  
  
-   新資料庫於執行個體上建立後，它們很快就會自動備份  
  
-   可以套用至具有相同保留週期需求的資料庫。  
  
-   即使已在執行個體層級啟用使用預設設定的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，您仍可設定需要不同保留週期的各個資料庫。 如果您不想[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]要使用 Azure 儲存體來進行備份，您也可以停用資料庫的。  
  
##  <a name="enable-and-configure-ss_smartbackup-for-a-database"></a><a name="DatabaseConfigure"></a>針對資料庫啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]和設定  
 系統預存程序 `smart_admin.sp_set_db_backup` 可用於為特定資料庫啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 第一次啟用資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 時，除了啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之外，還必須指定下列資訊︰  
  
-   資料庫的名稱。  
  
-   保留週期。  
  
-   用來向 Azure 儲存體帳戶進行驗證的 SQL 認證。  
  
-   請指定不要使用* \@encryption_algorithm* = **NO_ENCRYPTION**加密，或是指定支援的加密演算法。 如需加密的詳細資訊，請參閱＜ [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)＞。  
  
 只能透過 Transact-SQL 支援資料庫層級設定的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
 啟用資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 之後，此資訊會被保存。 如果要變更組態，只需要資料庫名稱和您要變更的設定；如果未指定其他參數， [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 將會保留其他參數現有的值。  
  
> [!IMPORTANT]  
>  在設定資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 前，它對現有的組態 (如果有的話) 也許會有幫助。 檢閱資料庫組態設定的步驟，於本節稍後說明。  
  
-   **使用 Transact-sql：**  
  
     如果您是第[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]一次啟用，所需的參數為： * \@database_name*、 * \@credential_name* * \@encryption_algorithm*， * \@enable_backup* * \@storage_url*參數是選擇性的。 如果您未提供@storage_url參數的值，則會使用 SQL 認證中的儲存體帳戶資訊來衍生值。 如有提供儲存體 URL，應只提供儲存體帳戶根目錄的 URL，而且必須符合所指定之 SQL 認證中的資訊。  
  
    1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
    2.  在標準列中，按一下 **[新增查詢]** 。  
  
    3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。 這個範例會[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]啟用資料庫 ' TestDB ' 的。 保留週期設為 30 天。 此範例會指定加密演算法和加密程式資訊來使用加密選項。  
  
    ```sql
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@enable_backup=1  
                    ,@retention_days =30   
                    ,@credential_name ='MyCredential'  
                    ,@encryption_algorithm ='AES_256'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
    GO
    ```  
  
    > [!IMPORTANT]  
    >  保留週期可設為 1 到 30 天之間的任何值。  
    >   
    >  如需有關建立憑證以進行加密的詳細資訊，請參閱＜ [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)＞中的「建立備份憑證」步驟。  
  
     如需此預存程式的詳細資訊，請參閱[smart_admin。 set_db_backup &#40;transact-sql&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)  
  
     若要檢閱資料庫的組態設定，請使用下列查詢：  
  
    ```sql
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('TestDB')  
    ```  
  
##  <a name="enable-and-configure-default-ss_smartbackup-settings-for-the-instance"></a><a name="InstanceConfigure"></a>啟用和設定實例[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的預設設定  
 您可以透過兩種方式[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在實例層級啟用和設定預設設定：使用系統預存程式`smart_admin.set_instance_backup`或**SQL Server Management Studio**。 這兩種方法說明如下：  
  
 **smart_admin. set_instance_backup：**。 藉由為* \@enable_backup*參數指定**1**的值，您就可以啟用備份並設定預設設定。 套用在執行個體層級之後，這些預設設定值會套用至加入此執行個體的所有新資料庫。  第一次啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 時，除了啟用執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 之外，還必須提供下列資訊︰  
  
-   保留週期。  
  
-   用來向 Azure 儲存體帳戶進行驗證的 SQL 認證。  
  
-   加密選項。 請指定不要使用* \@encryption_algorithm* = **NO_ENCRYPTION**加密，或是指定支援的加密演算法。 如需加密的詳細資訊，請參閱＜ [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)＞。  
  
 啟用之後，這些設定會保存。 如果要變更組態，只需要資料庫名稱和您要變更的設定。 如果未指定，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會保留現有的值。  
  
> [!IMPORTANT]  
>  在設定執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 前，它對檢查現有的組態 (如果有的話) 也許會有幫助。 檢閱資料庫組態設定的步驟，於本節稍後說明。  
  
 **SQL Server Management Studio** ：若要在 SQL Server Management Studio 中執行這項工作，請移至 [物件總管]，再展開 **[管理]** 節點，並以滑鼠右鍵按一下 **[Managed Backup]**。 選取 [設定]  。 這樣會開啟 **[Managed Backup]** 對話方塊。 使用此對話方塊可指定保留週期、SQL 認證、儲存體 URL 和加密設定。 如需此對話方塊的特定說明，請參閱[設定受管理的備份 &#40;SQL Server Management Studio&#41;](configure-managed-backup-sql-server-management-studio.md)。  
  
#### <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。  
  
```sql
Use msdb;  
Go  
   EXEC smart_admin.sp_set_instance_backup  
                @retention_days=30   
                ,@credential_name='sqlbackuptoURL'  
                ,@encryption_algorithm ='AES_128'  
                ,@encryptor_type= 'Certificate'  
                ,@encryptor_name='MyBackupCert'  
                ,@enable_backup=1;  
GO  
  
```  
  
> [!IMPORTANT]  
>  保留週期可設為 1 到 30 天之間的任何值。  
>   
>  如需有關建立憑證以進行加密的詳細資訊，請參閱＜ [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)＞中的「建立備份憑證」步驟。  
  
 若要檢視執行個體的預設組態設定，請使用下列查詢：  
  
```sql
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_instance_config ();
```  
  
#### <a name="using-powershell"></a>使用 PowerShell  
  
1.  啟動 PowerShell 執行個體  
  
2.  修改到符合您的設定後，執行下列指令碼。  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    $encryptionOption = New-SqlBackupEncryptionOption -EncryptionAlgorithm Aes128 -EncryptorType ServerCertificate -EncryptorName "MyBackupCert"  
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -BackupEnabled $True -BackupRetentionPeriodInDays 10 -EncryptionOption $encryptionOption  
    ```  
  
> [!IMPORTANT]  
>  當您進行預設設定後，建立新的資料庫時，可能需要花費 15 分鐘對資料庫進行預設設定。 這也適用於從 **Simple** 變更至 **Full** 或 **Bulk-Logged** 復原模式的資料庫。  
  
##  <a name="disable-ss_smartbackup-for-a-database"></a><a name="DatabaseDisable"></a>停[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用資料庫的  
 您可以使用 `sp_set_db_backup` 系統預存程序來停用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定。 Enableparameter 是用來啟用和停[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]用特定資料庫的設定，其中1會啟用，而0會停用設定。 * \@ *  
  
#### <a name="to-disable-ss_smartbackup-for-a-specific-database"></a>停用特定資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ：  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。  
  
```sql
Use msdb;  
Go  
EXEC smart_admin.sp_set_db_backup   
                @database_name='TestDB'   
                ,@enable_backup=0;  
GO
```  
  
##  <a name="disable-ss_smartbackup-for-all-the-databases-on-the-instance"></a><a name="DatabaseAllDisable"></a>針對[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]實例上的所有資料庫停用  
 從近期在執行個體上啟用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的所有資料庫中，若您要停用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 組態設定，可使用下列程序。  組態設定 (例如儲存體 URL、保留項目和 SQL 認證) 都會保留在中繼資料中，如果稍後啟用資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 即可使用。 如果您只是想暫停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服務，可使用主切換，本主題的以下章節會解釋。  
  
#### <a name="to-disable-ss_smartbackupfor-all-the-databases"></a>停用所有資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]：  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。 下列範例會指出是否已在執行個體層級設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，以及該執行個體上，所有已經啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的資料庫，並會執行系統預存程序 `sp_set_db_backup`，以停用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
```sql
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM
  
       smart_admin.fn_backup_db_config (NULL)  
       WHERE is_smart_backup_enabled = 1  
  
       --Select DBName from @DBNames 
       select @rowid = min(RowID) FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC smart_admin.sp_set_db_backup    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END
```  
  
 若要檢閱執行個體上所有資料庫的組態設定，請使用下列查詢：  
  
```sql
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_db_config (NULL);  
GO
```  
  
##  <a name="disable-default-ss_smartbackup-settings-for-the-instance"></a><a name="InstanceDisable"></a>停用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]實例的預設設定  
 執行個體層級的預設設定會套用到建立在該執行個體上的所有新資料庫。  如果您不再需要或要求預設設定，可以使用 **smart_admin.sp_set_instance_backup** 系統預存程序以停用此組態。 停用不會移除其他組態設定，像是儲存體 URL、保留設定或 SQL 認證名稱。 如果稍後啟用執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，將會使用這些設定。  
  
#### <a name="to-disable-ss_smartbackup-default-configuration-settings"></a>停用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 預設組態設定：  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。  
  
    ```sql
    Use msdb;  
    Go  
    EXEC smart_admin.sp_set_instance_backup  
                    @enable_backup=0;  
    GO
    ```  
  
#### <a name="using-powershell"></a>使用 PowerShell  
  
1.  啟動 PowerShell 執行個體  
  
2.  執行下列指令碼：  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Set-SqlSmartAdmin -BackupEnabled $False  
    ```  
  
##  <a name="pause-ss_smartbackup-at-the-instance-level"></a><a name="InstancePause"></a>在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]實例層級暫停  
 有些時候，您可能會需要暫停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服務一段時間。  `smart_admin.sp_backup_master_switch` 系統預存程序可讓您在執行個體層級停用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]服務。  使用同一個預存程序繼續執行 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 @state 參數可用來定義是否應該關閉或開啟 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
#### <a name="to-pause-ss_smartbackup-services-using-transact-sql"></a>使用 Transact-SQL 暫停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服務：  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`  
  
```sql
Use msdb;  
GO  
EXEC smart_admin.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-pause-ss_smartbackup-using-powershell"></a>使用 PowerShell 暫停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
  
1.  啟動 PowerShell 執行個體  
  
2.  修改到符合您的設定後，執行下列指令碼。  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $False  
    ```  
  
#### <a name="to-resume-ss_smartbackup-using-transact-sql"></a>使用 Transact-SQL 繼續進行 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下`Execute`。  
  
```sql
Use msdb;  
Go  
EXEC smart_admin. sp_backup_master_switch @new_state=1;  
GO
```  
  
#### <a name="to-resume-ss_smartbackup-using-powershell"></a>使用 PowerShell 繼續進行 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
  
1.  啟動 PowerShell 執行個體  
  
2.  修改到符合您的設定後，執行下列指令碼。  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $True  
    ```  
