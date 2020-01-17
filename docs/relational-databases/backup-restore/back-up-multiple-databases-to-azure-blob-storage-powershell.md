---
title: 備份多個資料庫：Azure Blob 儲存體
titleSuffix: PowerShell
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3e89a3dc9cff58b5ab610f0454217cc3b658dc4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247462"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>將多個資料庫備份至 Azure Blob 儲存體服務 - Powershell

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題提供範例指令碼，可讓您使用 PowerShell Cmdlet，自動執行 Azure Blob 儲存體服務的備份作業。  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>備份與還原之 PowerShell 指令程式的概觀

**Backup-SqlDatabase** 和 **Restore-SqlDatabase** 是可用於備份和復原作業的兩個主要 Cmdlet。

此外，您也可能需要其他 Cmdlet，才能將備份自動化至 Windows Azure Blob 儲存體，例如 **SqlCredential** Cmdlet 的集合。

如需所有可用 Cmdlet 的清單，請參閱 [SqlServer Cmdlet](/powershell/module/sqlserver)。
  
> [!TIP]  
> **SqlCredential** Cmdlet 是用於備份及還原至 Azure Blob 儲存體的情節。 如需認證及其用法的詳細資訊，請參閱[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>多個資料庫的 PowerShell，多個執行個體的備份作業

下列各節包含多種作業的指令碼，例如建立多個 SQL Server 執行個體的 SQL 認證、備份 SQL Server 執行個體中的所有使用者資料庫等等。 您可以根據環境的需求，利用這些指令碼自動化或排程備份作業。 此處所提供的指令碼僅為範例，您可以針對您的環境的需要而修改或擴充。  
  
以下是範例指令碼的注意事項︰  
  
- SQL Server PowerShell 會實作 Cmdlet 以巡覽路徑結構，而路徑結構代表 PowerShell 提供者所支援物件的階層。 在您導覽至路徑中的節點時，可以使用其他 Cmdlet 來執行目前物件的基本作業。

  如需詳細資訊，請參閱 [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md)。

- **Get-ChildItem** Cmdlet：**Get-ChildItem** 傳回的資訊內容，視在 SQL Server PowerShell 路徑中的位置而定。 例如，如果位置在電腦層級，此指令程式會傳回所有安裝在電腦上的 SQL Server Database Engine 執行個體。 或者，如果位置在物件層級 (例如資料庫)，則其會傳回資料庫物件的清單。 **Get-ChildItem** Cmdlet 預設不會傳回任何系統物件。 使用 `–Force` 參數來查看系統物件。

- Azure 儲存體帳戶和 SQL 認證都是 Azure Blob 儲存體服務所有備份和還原作業所需的必要條件。
  
### <a name="create-a-sql-credential-on-all-instances-of-sql-server"></a>建立所有 SQL Server 執行個體的 SQL 認證

下列指令碼可用來建立電腦上所有 SQL Server 執行個體的一般 SQL 認證。 如果電腦上的某一個執行個體目前已有同名的認證，此指令碼會顯示錯誤並繼續。  
  
```powershell
# load the sqlps module
import-module sqlps  
  
# set parameters
$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$storageKey = "<myStorageAccessKey>"  
$secureString = ConvertTo-SecureString $storageKey -AsPlainText -Force  
$credentialName = "myCredential-$(Get-Random)"

Write-Host "Generate credential: " $credentialName
  
#cd to sql server and get instances  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and create a SQL credential, output any errors
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials"
        New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString -Path $path -ea Stop | Out-Null
        Write-Host "...generated credential $($path)\$($credentialName)."  }
    catch { Write-Host $_.Exception.Message } }
```

> [!NOTE]
> `-ea Stop | Out-Null` 陳述式用於使用者定義的例外狀況輸出。 如果您偏好預設的 PowerShell 錯誤訊息，則可以移除此陳述式。 

### <a name="remove-a-sql-credential-from-all-instances-of-sql-server"></a>移除所有 SQL Server 執行個體的 SQL 認證

下列指令碼可用來移除電腦上所安裝所有 SQL Server 執行個體的特定認證。 如果特定執行個體的認證不存在，則系統會顯示錯誤訊息，並繼續執行指令碼，直到檢查過所有執行個體為止。  
  
```powershell
import-module sqlps

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$credentialName = "<myCredential>"

Write-Host "Delete credential: " $credentialName

cd $sqlPath
$instances = Get-ChildItem

#loop through instances and delete a SQL credential
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials\$($credentialName)"
        Remove-SqlCredential -Path $path -ea Stop | Out-Null
        Write-Host "...deleted credential $($path)."  }
    catch { Write-Host $_.Exception.Message } }
```  
  
### <a name="full-backup-for-all-databases"></a>針對所有資料庫進行完整備份

下列指令碼會為電腦上的所有資料庫建立備份。 這包括使用者資料庫和 **msdb** 系統資料庫。 此指令碼會篩選 **tempdb** 和 **model** 系統資料庫。  
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $backupUrlContainer
  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and backup all databases (excluding tempdb and model)
foreach ($instance in $instances)  {
    $path = "$($sqlPath)\$($instance.DisplayName)\databases"
    $databases = Get-ChildItem -Force -Path $path | Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}

    foreach ($database in $databases) {
        try {
            $databasePath = "$($path)\$($database.Name)"
            Write-Host "...starting backup: " $databasePath
            Backup-SqlDatabase -Database $database.Name -Path $path -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
            Write-Host "...backup complete."  }
        catch { Write-Host $_.Exception.Message } } }
```  
  
### <a name="full-backup-for-system-databases-only-on-a-specific-instance-of-sql-server"></a>僅針對特定 SQL Server 執行個體的系統資料庫進行完整備份

完整的指令碼可用來備份具名 SQL Server 執行個體的 **master** 和 **msdb** 資料庫。 您可以變更執行個體參數值，以將相同的指令碼用於任何執行個體。 SQL Server 的預設執行個體名為 `DEFAULT`。
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$instanceName = "DEFAULT"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $instanceName " to " $backupUrlContainer
  
cd "$($sqlPath)\$($instanceName)"

#loop through instance and backup specific databases
$databases = "master", "msdb"  
foreach ($database in $databases) {
    try {
        Write-Host "...starting backup: " $database
        Backup-SqlDatabase -Database $database -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
        Write-Host "...backup complete." }
    catch { Write-Host $_.Exception.Message } }
```  
  
## <a name="see-also"></a>另請參閱

[使用 Azure Blob 儲存體服務的 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

[SQL Server 備份至 URL 的最佳做法和疑難排解](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)
