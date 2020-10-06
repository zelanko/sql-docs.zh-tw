---
description: managed_backup.sp_backup_config_basic (Transact-SQL)
title: managed_backup managed_backup.sp_backup_config_basic (transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 428dff3f22b5a924f7a208a988334c14ece752a3
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753727"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]設定特定資料庫或實例的基本設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!NOTE]  
>  您可以自行呼叫此程式，以建立基本的 managed backup 設定。 但是，如果您打算新增 advanced 功能或自訂排程，請先使用 [managed_backup. sp_backup_config_advanced &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) 和 [managed_backup. sp_backup_config_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) 進行這些設定，再使用此程式啟用受控備份。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引數  
 @enable_backup  
 啟用或停用指定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @enable_backup是**BIT**。 設定第一個實例時的必要參數 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您要變更現有的設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，此參數是選擇性的。 在此情況下，任何未指定的設定值都會保留其現有的值。  
  
 @database_name  
 在特定資料庫上啟用 managed 備份的資料庫名稱。  
  
 @container_url  
 指出備份位置的 URL。 當 @credential_name 為 Null 時，此 URL 是共用存取簽章 (SAS) URL 指向 Azure 儲存體中的 blob 容器，而備份則使用新的備份來封鎖 blob 功能。 如需詳細資訊，請參閱 [瞭解 SAS](/azure/storage/common/storage-sas-overview)。 當 @credential_name 指定時，這會是儲存體帳戶 URL，而備份會使用已淘汰的備份來分頁 blob 功能。  
  
> [!NOTE]  
>  此參數目前只支援 SAS URL。  
  
 @retention_days  
 備份檔案的保留期限，以天數為單位。 @storage_url是 INT。 當您 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 第一次在實例上設定時，這是必要的參數 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 變更設定時 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，這個參數是選擇性的。 如果未指定，則會保留現有的組態值。  
  
 @credential_name  
 用來向 Azure 儲存體帳戶驗證之 SQL 認證的名稱。 @credentail_name 為 **SYSNAME**。 當指定時，備份會儲存至分頁 blob。 如果此參數為 Null，則備份會儲存為區塊 blob。 備份至分頁 blob 已被取代，因此最好使用新的區塊 blob 備份功能。 用來變更[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態時為選擇性參數。 如果未指定，則會保留現有的設定值。  
  
> [!WARNING]
>  目前不支援** \@ credential_name**參數。 只支援備份至區塊 blob，這需要將此參數設為 Null。  
  
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
  
 下列範例 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會針對執行它的 SQL Server 實例啟用、將保留原則設定為30天、將目的地設定為名為 ' mystorageaccount ' 之儲存體帳戶中名為 ' mycontainer ' 的容器。  
  
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
 [managed_backup managed_backup.sp_backup_config_advanced &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
