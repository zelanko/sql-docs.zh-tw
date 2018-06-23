---
title: 刪除擁有使用中租用的備份 Blob 檔案 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f3c46becd5ae766627e96ad935900f063c4389bb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034583"
---
# <a name="deleting-backup-blob-files-with-active-leases"></a>刪除擁有使用中租用的備份 Blob 檔案
  備份至 Windows Azure 儲存體或從中還原時，SQL Server 會取得無限期租用，以便鎖定 Blob 的獨佔存取權。 當備份或還原程序順利完成時，就會釋放租用。 如果備份或還原失敗，備份程序會嘗試清除任何無效的 Blob。 不過，如果由於過長或持續性網路連線失敗而無法備份，備份程序可能無法存取 Blob，而該 Blob 可能仍然是被遺棄狀態。 這表示，在釋放租用之前，無法寫入或刪除 Blob。 此主題描述如何釋放租用及刪除 Blob。  
  
 如需租用類型的詳細資訊，請閱讀這篇 [文章](http://go.microsoft.com/fwlink/?LinkId=275664)。  
  
 如果備份作業失敗，可能會產生無效的備份檔案。  備份 Blob 檔案可能也擁有使用中租用，導致無法刪除或覆寫此檔案。  若要刪除或覆寫這類 Blob，應該先中斷租用。如果發生備份失敗，我們建議您清除租用並刪除 Blob。 您也可以選擇在儲存體管理工作中進行定期清除。  
  
 如果發生還原失敗，系統不會封鎖後續還原，因此使用中租用可能不會產生問題。 只有當您必須覆寫或刪除 Blob 時，才需要中斷租用。  
  
## <a name="managing-orphaned-blobs"></a>管理被遺棄的 Blob  
 下列步驟將說明如何在備份或還原活動失敗之後進行清除。 所有步驟都可以使用 PowerShell 指令碼來完成。 下一節將提供程式碼範例：  
  
1.  **識別擁有租用的 Blob：** 如果您有執行備份程序的指令碼或處理序，就可以在指令碼或處理序內部擷取失敗，並且使用該項資訊來清除 Blob。   您也可以使用 LeaseStats 和 LeastState 屬性來識別擁有其租用的 Blob。 識別出 Blob 之後，我們建議您檢閱清單、確認備份檔案的有效性，然後再刪除 Blob。  
  
2.  **中斷租用：** 授權要求可以中斷租用，而不需要提供租用識別碼。 如需詳細資訊，請參閱 [此處](http://go.microsoft.com/fwlink/?LinkID=275664) 。  
  
    > [!TIP]  
    >  SQL Server 會發出租用識別碼，以便在還原作業期間確立獨佔存取權。 還原租用識別碼為 BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2。  
  
3.  **刪除 Blob：** 若要刪除擁有使用中租用的 Blob，您必須先中斷租用。  
  
###  <a name="Code_Example"></a> PowerShell 指令碼範例  
 **\*\* 重要\* \*** 如果您正在執行 PowerShell 2.0，您可能必須載入 Microsoft WindowsAzure.Storage.dll 組件的問題。 我們建議您升級為 Powershell 3.0 以解決此問題。 您也可以針對 PowerShell 2.0 使用下列因應措施：  
  
-   使用下列內容來建立或修改 powershell.exe.config 檔案，以便在執行階段載入 .NET 2.0 和 .NET 4.0 組件：  
  
    ```  
    <?xml version="1.0"?>   
    <configuration>   
        <startup useLegacyV2RuntimeActivationPolicy="true">   
            <supportedRuntime version="v4.0.30319"/>   
            <supportedRuntime version="v2.0.50727"/>   
        </startup>   
    </configuration>  
  
    ```  
  
 下列範例將說明如何識別擁有使用中租用的 Blob，然後中斷租用。 此範例也會示範如何篩選釋放租用識別碼。  
  
 執行這個指令碼的秘訣  
  
> [!WARNING]  
>  如果在執行這個指令碼時正備份到 Windows Azure Blob 儲存體服務，備份可能會失敗，因為這個指令碼會中斷備份嘗試同時取得的租用。 建議在維護期間或預期不會執行任何備份時執行這個指令碼。  
  
1.  當您執行這個指令碼時，系統會提示您提供儲存體帳戶、儲存體金鑰、容器以及 Windows Azure 儲存體組件路徑和名稱參數的值。 儲存體的路徑是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄。 儲存體組件的檔案名稱是 Microsoft.WindowsAzure.Storage.dll。 下面是提示與輸入值的範例：  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  如果沒有任何鎖定租用的 Blob，您應該會看見下列訊息：  
  
     **沒有任何處於鎖定租用狀態的 Blob**  
  
     如果有鎖定租用的 Blob，您應該會看見下列訊息：  
  
     **中斷租用**  
  
     **\<Blob 的 URL> 的租用不是還原租用：只有當您的 Blob 擁有仍然使用中的還原租用時，您才會看見此訊息。**  
  
     **\<Blob 的 URL> 的租用不是還原租用。正在中斷 \<Blob 的 URL> 的租用。**  
  
```  
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs()   
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties   
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
    {   
        Write-Host " There are no blobs with locked lease status"  
    }  
if($lockedBlobs.Count -gt 0)  
{  
    write-host "Breaking leases"  
    foreach($blob in $lockedBlobs )   
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 備份至 URL 的最佳作法和疑難排解](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  