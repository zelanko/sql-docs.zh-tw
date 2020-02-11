---
title: 使用 PowerShell 將多個資料庫備份至 Azure Blob 儲存體服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 701928a722e14cf3eb5c1e678a1dd764597f46ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783091"
---
# <a name="use-powershell-to-backup-multiple-databases-to-azure-blob-storage-service"></a>使用 PowerShell 將多個資料庫備份到 Azure Blob 儲存體服務
  本主題提供範例指令碼，可讓您使用 PowerShell Cmdlet，自動執行 Azure Blob 儲存體服務的備份作業。  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>備份與還原之 PowerShell 指令程式的概觀  
 
  `Backup-SqlDatabase` 和 `Restore-SqlDatabase` 是進行備份和還原作業所能使用的兩個主要指令程式。 此外，自動操作 Azure Blob 儲存體備份作業可能還需要其他 Cmdlet，例如 **SqlCredential** Cmdlet。以下是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供可用於備份及還原之 PowerShell Cmdlet 的清單︰  
  
 Backup-SqlDatabase  
 此指令程式可用於建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。  
  
 Restore-SqlDatabase  
 可用於還原資料庫。  
  
 New-SqlCredential  
 此 Cmdlet 可用於建立 SQL Server 備份至 Azure 儲存體時所使用的 SQL 認證。 如需有關認證及其在 SQL Server 備份和還原中之用法的詳細資訊，請參閱[使用 Azure Blob 儲存體服務 SQL Server 備份和還原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 Get-SqlCredential  
 此指令程式可用於擷取認證物件及其屬性。  
  
 Remove-SqlCredential  
 刪除 SQL 認證物件  
  
 Set-SqlCredential  
 此指令程式可用於變更或設定 SQL 認證物件的屬性。  
  
> [!TIP]  
>  Credential Cmdlet 是用於備份及還原至 Azure Blob 儲存體的情節。  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>多個資料庫的 PowerShell，多個執行個體的備份作業  
 下列各節包含多種作業的指令碼，例如建立多個 SQL Server 執行個體的 SQL 認證、備份 SQL Server 執行個體中的所有使用者資料庫等等。 您可以根據環境的需求，利用這些指令碼自動化或排程備份作業。 此處所提供的指令碼僅為範例，您可以針對您的環境的需要而修改或擴充。  
  
 以下是範例指令碼的注意事項︰  
  
1.  **導覽 SQL Server PowerShell 路徑：** Windows PowerShell 會執行 Cmdlet，以流覽代表 PowerShell 提供者所支援之物件階層的路徑結構。 在您導覽至路徑中的節點時，可以使用其他 Cmdlet 來執行目前物件的基本作業。  
  
2.  
  `Get-ChildItem` 指令程式︰`Get-ChildItem` 傳回的資訊內容，視在 SQL Server PowerShell 路徑中的位置而定。 例如，如果位置在電腦層級，此指令程式會傳回所有安裝在電腦上的 SQL Server Database Engine 執行個體。 又例如，如果位置在物件層級 (例如資料庫)，此指令程式會傳回資料庫物件的清單。  
  `Get-ChildItem` 指令程式預設不會傳回任何系統物件。  使用 -Force 參數即可看到系統物件。  
  
     如需詳細資訊，請參閱 [Navigate SQL Server PowerShell Paths](../../powershell/navigate-sql-server-powershell-paths.md)。  
  
3.  雖然您可以利用變更變數值，嘗試個別變更每一個程式碼範例，但您還是必須針對 Azure Blob 儲存體服務之備份及還原作業，建立其必要條件：Azure Blob 儲存體帳戶與 SQL 認證。  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>建立所有 SQL Server 執行個體的 SQL 認證  
 下列兩個範例指令碼都會為電腦上所有的 SQL Server 執行個體上建立 SQL 認證 "mybackupToURL"。 第一個範例比較簡單而且會建立認證，但不會設陷例外狀況。  例如，如果電腦上的某一個執行個體目前已有同名的認證，此指令碼將會失敗。 第二個範例會設陷錯誤，並允許指令碼繼續執行。  
  
```powershell
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
# get the list of instances  
$instances = Get-ChildItem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString  
```  
  
```powershell
import-module sqlps  
  
# set the parameter values
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
# get the list of instances  
$instances = Get-ChildItem  
#loop through instances and create a SQL credential, output any errors  
ForEach ($instance In $instances)  
{  
    Try  
{  
     New-SqlCredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop
}  
Catch [Exception]  
    {
            Write-Host "instance - $($instance.name): "$_.Exception.Message
    }
 }
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>移除所有 SQL Server 執行個體的 SQL 認證  
 此指令碼可用於移除電腦上所安裝之所有 SQL Server 執行個體的特定認證。 如果指定執行個體的認證物件不存在，將會顯示錯誤訊息，而指令碼將會繼續執行，直到檢查過所有執行個體為止。  
  
```powershell
import-module sqlps  
  
cd SQLServer:\SQL\COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-ChildItem  
  
ForEach ($instance In $instances)  
   {
    Try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-SqlCredential -Path $path -ea stop   
         }  
         Catch [Exception]  
         {  
            Write-Host $_.Exception.Message
        }
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>所有資料庫的完整資料庫備份 (包括系統資料庫)  
 下列指令碼會為電腦上的所有資料庫建立備份。 這包括使用者資料庫和 **msdb** 系統資料庫。 此指令碼會篩選 **tempdb** 和 **model** 系統資料庫。  
  
```powershell
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-ChildItem
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 ForEach ($instance In $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = Get-ChildItem -Force -path $path | Where-Object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>所有使用者資料庫的完整資料庫備份  
 下列指令碼可用於備份電腦上所有 SQL Server 執行個體的所有使用者資料庫。  
  
```powershell
import-module sqlps
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-ChildItem
# loop through each instances and backup up all the user databases  
 ForEach ($instance In $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
    $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>所有 SQL Server 執行個體上之 Master 和 MSDB 資料庫 (系統資料庫) 的完整資料庫備份  
 下列指令碼可用於備份電腦上安裝之所有 SQL Server 執行個體的 **master** 和 **msdb** 資料庫。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
$instances = Get-ChildItem
ForEach ($instance In $instances)  
 {  
      ForEach ($s In $sysdbs)  
     {  
        Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}
 } 
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>SQL Server 執行個體上之所有使用者資料庫的完整資料庫備份  
 下列指令碼可用於只備份具名 SQL Server 執行個體上的使用者資料庫。 只要變更 $srvPath 參數值，電腦上的預設執行個體即可使用相同的指令碼。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>僅限 SQL Server 執行個體上之系統資料庫 (Master 和 MSDB) 的完整資料庫備份  
 完整的指令碼可用來備份具名 SQL Server 執行個體的 **master** 和 **msdb** 資料庫。 只要變更 $srvPath 參數值，電腦上的預設執行個體即可使用相同的指令碼。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
ForEach ($s In $sysDbs)
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}
```  
  
## <a name="see-also"></a>另請參閱
 [使用 Azure Blob 儲存體服務 SQL Server 備份和還原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) [SQL SERVER 備份至 URL 的最佳作法和疑難排解](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
