---
title: managed_backup. sp_backup_config_basic （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3b3c547453c41dff6d32d1cafcd62746a2f194f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72305258"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定特定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]資料庫或實例的基本設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  您可以自行呼叫此程式，以建立基本的受管理備份設定。 不過，如果您打算加入「高級功能」或「自訂排程」，請先使用 managed_backup 來設定這些設定[sp_backup_config_advanced &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)和 managed_backup。在使用此程式啟用受管理備份之前，請先[sp_backup_config_schedule &#40;transact-sql&#41;。](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
 @enable_backup  
 啟用或停用指定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @enable_backup為**位**。 設定的第一個[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]實例時，所需[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的參數。 如果您要變更現有[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的設定，此參數是選擇性的。 在此情況下，任何未指定的設定值都會保留其現有的值。  
  
 @database_name  
 在特定資料庫上啟用受管理備份的資料庫名稱。  
  
 @container_url  
 指出備份位置的 URL。 當@credential_name為 Null 時，此 URL 是 Azure 儲存體中 blob 容器的共用存取簽章（SAS） url，而備份則使用新的備份來封鎖 blob 功能。 如需詳細資訊，請參閱[瞭解 SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。 當@credential_name指定時，這會是儲存體帳戶 URL，而備份會使用已被取代的備份來分頁 blob 功能。  
  
> [!NOTE]  
>  此參數目前僅支援 SAS URL。  
  
 @retention_days  
 備份檔案的保留期限，以天數為單位。 @storage_url為 INT。 當您第一次在實例[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]上設定時，這是必要的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參數。 變更設定時[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，這個參數是選擇性的。 如果未指定，則會保留現有的組態值。  
  
 @credential_name  
 用來向 Azure 儲存體帳戶進行驗證的 SQL 認證名稱。 @credentail_name為**SYSNAME**。 當指定時，備份會儲存至分頁 blob。 如果此參數為 Null，備份將會儲存為區塊 blob。 備份至分頁 blob 已淘汰，因此最好使用新的區塊 blob 備份功能。 用來變更[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態時為選擇性參數。 如果未指定，則會保留現有的設定值。  
  
> [!WARNING]
>  目前不支援** \@credential_name**參數。 僅支援備份至區塊 blob，這需要此參數為 Null。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="examples"></a>範例  
 您可以使用最新的 Azure PowerShell 命令來建立儲存體帳戶容器和 SAS URL。 下列範例會在 mystorageaccount 儲存體帳戶中建立新的容器 mycontainer，然後取得具有完整許可權的 SAS URL。  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 下列範例會針對[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]在其上執行的 SQL Server 實例啟用，並將保留原則設為30天，並將目的地設定為名為 ' mystorageaccount ' 的儲存體帳戶中名為 ' mycontainer ' 的容器。  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 下列範例停用執行所在之 SQL Server 執行個體的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup。 sp_backup_config_advanced &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
