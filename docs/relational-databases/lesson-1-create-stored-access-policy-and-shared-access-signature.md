---
title: "第 1 課︰建立預存存取原則和共用存取簽章 | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe7163f6ff8d2f79a4eb3297c831e82d59b70c48
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="lesson-1-create-stored-access-policy-and-shared-access-signature"></a>第 1 課︰建立預存存取原則和共用存取簽章
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您將使用 [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) 指令碼，在 Azure Blob 容器上建立使用預存存取原則的共用存取簽章。  
  
> [!NOTE]  
> 此指令碼是使用 Azure PowerShell 5.0.10586 所撰寫。  
  
共用存取簽章是一個 URI，會將有限的存取權限授與容器、Blob、佇列或資料表。 預存存取原則可對伺服器端的共用存取簽章提供一層額外的控制，包括撤銷、逾期或延伸存取權。 使用這項新的增強功能時，您需要在容器上建立具有最低讀取、寫入和列出權限的原則。  
  
您可以使用 Azure PowerShell、Azure 儲存體 SDK、Azure REST API 或協力廠商公用程式，建立預存存取原則和共用存取簽章。 本教學課程示範如何使用 Azure PowerShell 指令碼來完成這項工作。 此指令碼會使用資源管理員部署模型，並建立下列新的資源  
  
-   資源群組  
  
-   儲存體帳戶  
  
-   Azure Blob 容器  
  
-   SAS 原則  
  
此指令碼一開始會宣告一些變數，來指定上述資源的名稱，以及下列必要輸入值的名稱：  
  
-   用來命名其他資源物件的前置名稱  
  
-   訂閱名稱  
  
-   資料中心位置  
  
> [!NOTE]  
> 此指令碼是以可讓您使用現有的 ARM 或傳統部署模型資源的方式所撰寫。  
  
此指令碼最後會產生適當的 CREATE CREDENTIAL 陳述式，您將在 [第 2 課︰使用共用存取簽章建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)中使用此陳述式。 系統會為您將此陳述式複製到剪貼簿，並輸出到主控台以供檢視。  
  
若要在容器上建立原則並產生共用存取簽章 (SAS) 金鑰，請依照下列步驟執行：  
  
1.  開啟 Window PowerShell 或 Windows PowerShell ISE (請參閱上述的版本需求)。  
  
2.  編輯並執行下列指令碼。  
  
    ```  
    \<#   
    This script uses the Azure Resource model and creates a new ARM storage account.  
    Modify this script to use an existing ARM or classic storage account   
    using the instructions in comments within this script  
    #>  
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionName='<your subscription name>'   # the name  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy  
  
    \<#   
    Using Azure Resource Manager deployment model  
    Comment out this entire section and use the classic storage account name to use an existing classic storage account  
    #>  
  
    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # adds an authenticated Azure account for use in the session   
    Login-AzureRmAccount    
  
    # set the tenant, subscription and environment for use in the rest of   
    Set-AzureRmContext -SubscriptionName $subscriptionName   
  
    # create a new resource group - comment out this line to use an existing resource group  
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new ARM storage account - comment out this line to use an existing ARM storage account  
    New-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the ARM storage account  
    $accountKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an ARM storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value 
  
    \<#  
    Using the Classic deployment model  
    Use the following four lines to use an existing classic storage account  
    #>  
    #Classic storage account name  
    #Add-AzureAccount  
    #Select-AzureSubscription -SubscriptionName $subscriptionName #provide an existing classic storage account  
    #$accountKeys = Get-AzureStorageKey -StorageAccountName $storageAccountName  
    #$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys.Primary  
  
    # The remainder of this script works with either the ARM or classic sections of code above  
  
    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzureStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzureStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql  
  
    ```  
  
3.  指令碼完成之後，會將 CREATE CREDENTIAL 陳述式放在剪貼簿中以供下一課使用。  
  
**下一課：**  
  
[第 2 課︰使用共用存取簽章建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="see-also"></a>另請參閱  
[共用存取簽章，第 1 部分：了解 SAS 模型](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[Create Container (建立容器)](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[Set Container ACL (設定容器 ACL)](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[Get Container ACL (取得容器 ACL)](https://msdn.microsoft.com/library/azure/dd179469.aspx)  
  
  
  

